# Serverless — Building a crypto wallet balance API to use with google spreadsheets (part 2)

In this part of the series we’ll be building a serverless API endpoint to serve our google spreadsheet to track crypto wallets! You can find the repo [HERE](https://github.com/kvaggelakos/serverless-crypto-balance)

In case you missed it the other posts of my Serverless series:
**Part 1**: [Beyond the over simplistic todo apps and into the world of reality](https://hackernoon.com/serverless-part-1-e75b4a5e59e6) (building a Serverless function to run FFMPEG when a file is uploaded to a bucket)
**Part 2:** This article

![](https://i.imgur.com/zfkqeTu.png)

**What we want to do:**
 Whenever we open our google spreadsheet, we want it to check our wallets in real time to see our balance.

The result will look something like this:

![](https://i.imgur.com/i2cZHgE.png)

**Why serverless:**
 We could use serverless in this case to quickly deploy a scalable API to run an arbitrary amount of lookups for various wallets. Also, we’d only call the endpoint when we’re browsing our spreadsheet, so it’s nice to not have to pay for those days the spreadsheet is closed.

Luckily this isn’t as advanced as part 1. I know I promised beyond simplistic todo apps, but I think this is a valid use case for serverless, something simple, small, yet very powerful.

This is a pretty straightforward Serverless configuration, we have one handler, it’ll be the one serving back the balance. As you can see in the http path, we’re taking in a parameter `id`, which will be the wallet address.

One thing to notice (as we saw in part 1), is the plugin used to allow us to run things locally before we deploy. Another thing we introduce here is the concept of an **authorizer for this lambda**. We wouldn’t want anyone to just abuse our system! We also define username and password env variables to check against once we deploy.

Sidenote: Type `request` for the serverless framework allows us to just check against normal `basic auth`  . You can read more about [different authorizer types here](https://serverless.com/framework/docs/providers/aws/events/apigateway/#http-endpoints-with-custom-authorizers).

``` yml
service: serverless-crypto-balance

plugins:
  - serverless-offline

provider:
  name: aws
  runtime: nodejs6.10
  timeout: 10
  memorySize: 512
  environment:
    USERNAME: test
    PASSWORD: test

functions:
  authorizer:
    handler: authorizer.auth

  balance:
    handler: handler.balance
    events:
      - http:
          path: /api/v1/balance/{id}
          method: get
          authorizer:
            name: authorizer
            type: request
```

In my serious attempt to not re-invent the wheel I found [crypto-balances](https://github.com/litvintech/crypto-balances) a node module to query various crypto backends/nodes to figure out a balance that an address holds! Great!

For those interested in how it works, check out the source. [One piece of the code](https://github.com/litvintech/crypto-balances/blob/master/src/address-checker.coffee) that really intrigued me was how we could pass in any address and that it figures out which service/node to query for a balance. Now I quickly realized this module hasn’t been updated in 2 years and since we’ve had forks etc, which kinda screws with this auto detection! (Always room for improvement).

You will also notice we never really add anything in this code for checking auth, this decision is made by the API Gateway to check it for you, which is a really nice separation.

As you can see below we’re simply wrapping the result of the `crypto-balances` call into a response that serverless likes and off we go 🚀

``` js
var balance = require('crypto-balances')


module.exports.balance = (event, context, callback) => {
  balance(event.pathParameters.id, function(error, result) {

    if (result.length === 0) {
      return callback(null, {
        statusCode: 404
      })
    }

    if (error) {
      return callback(null, {
        statusCode: 500,
        error: error
      })
    }

    callback(null, {
      statusCode: 200,
      body: JSON.stringify(result)
    });
  });
};

```

Running it locally should look something like this:

![](https://i.imgur.com/kUGh0Mv.png)

[This article](https://news.bitcoin.com/500-million-mistakenly-sent-ethereums-genesis-address/) from news.bitcoin.com claims the ETH genesis address (0x00…0) has over 7k ETH. Let’s see if we can verify that!

![](https://i.imgur.com/GzWvwkm.png)

Our api works! Also, we’ve confirmed the claim. The genesis address does indeed have over 7k ETH :) One thing to note is that in this instance, our dependency chose to use [http://api.etherscan.io](http://api.etherscan.io/) to lookup the balance, it will vary by wallet address we’re trying to lookup.

Alright, so we have a fancy api now. Cool, but what if we want to protect it? Perhaps we don’t want others to spam our poor little lambda!

If you checked the screenshot above carefully you’d have seen a `--user test:test` parameter to curl in order to pass auth. This is how it’d look if we passed the wrong info:

![](https://i.imgur.com/plOUpB0.png)

We get a nice 401 back! So how can we achieve this? Let’s dig into the authorizing code!

We had previous defined an authorizer in the `serverless.yml` this makes our API gateway run our authorizer before letting anyone through to our lambda.

On line 9 we construct our Basic auth string based on environment variables (which again were defined in the `serverless.yml)`

On line 11 we then match `authString` with whatever is passed in the header by the caller. If it’s a match we return a *carefully* crafted policy document, which includes the action (invoking the lambda) and the effect “allow”.

If it doesn’t match, we throw back a 401.

``` js
module.exports.auth = (event, context, callback) => {
  try {

    // Grab the header
    const authorizationHeader = event.headers.Authorization || event.headers.authorization
    const authUser = process.env.USERNAME // Get creds from env
    const authPass = process.env.PASSWORD
    // Let's build the auth string
    const authString = 'Basic ' + new Buffer(authUser + ':' + authPass).toString('base64')

    if (authString === authorizationHeader) {
      return callback(null, {
        principalId: authUser,
        policyDocument: {
          Version: '2012-10-17',
          Statement: [
            {
              Action: 'execute-api:Invoke',
              Effect: 'Allow', // Allow!
              Resource: event.methodArn,
            },
          ],
        },
        context: {}
      })
    } else {
      return context.fail("Unauthorized") // Booh!
    }
  } catch (error) {
    console.error(error)
    return {
      statusCode: 500,
      body: JSON.stringify({
        statusCode: 500,
        message: 'Something went wrong trying to authorize',
        requestId: context.awsRequestId
      })
    }
  }
};

```

Let’s deploy this before we continue so we can use it with our google spreadsheet script.

Using the serverless framework all we need to do is run: `sls deploy -v`
 Making sure it works:

![](https://i.imgur.com/GzWvwkm.png)

Once we have our serverless deployed it’s time to make it easy to query it from our sheet.

Below is the complete spreadsheet code we need to paste into our google spreadsheet script editor.

``` js
function WALLETBALANCE(address) {
  var serverlessEndpoint = 'https://abc123.execute-api.us-east-1.amazonaws.com/dev/api/v1/balance/';
  var username = 'test';
  var password = 'test';
  
  var headers = {
    "Authorization" : "Basic " + Utilities.base64Encode(username + ':' + password)
  };
  
  var response = UrlFetchApp.fetch(serverlessEndpoint + address, { headers: headers });
  var result = JSON.parse(response.getContentText());
  return result[0].quantity + " " + result[0].asset;
}
```

To add the script, open up the script editor like the screenshot below:

![](https://i.imgur.com/i33qjhs.png)

Then paste it in and save!

![](https://i.imgur.com/EmE3Hvg.png)

I hope you enjoyed **part 2** of this series going in to serverless a bit beyond the surface!

**A couple of real life problems encountered in this part:**

1. We learned how to utilize an **authorizer in serverless**. We passed in a basic auth header and matched it against the computed string by processing environment variables.
2. We also looked at how to connect a spreadsheet with our serverless function to actually use it for something interesting.
Thanks for reading! Please spread the ❤ with some claps and stars!

![](https://i.imgur.com/te2eQ2E.png)

[Serverless — Building a crypto wallet balance API to use with google spreadsheets (part 2)](https://hackernoon.com/serverless-part-2-61ad3986371f)