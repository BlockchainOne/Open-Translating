# Serverless — Beyond the over simplistic todo apps into the world of reality (part 1)

Besides the shitty todo apps that are so conveniently demonstrated for all new technologies I wondered what the **world of** **serverless** would **really** be like.

This is **part 1** **of 3** of building a real world example using the [serverless framework](https://serverless.com/) and how you can monetize your new infinitely scalable solutions.

In this part I talk about how to use serverless (the framework) to build an ffmpeg wrapper based on bucket events. The code for my [open sourced serverless-ffmpeg can be found here](https://github.com/kvaggelakos/serverless-ffmpeg).

**What we want to do:**  
Whenever a media file is uploaded to an s3 bucket, we want to post-process that into various formats using ffmpeg.

![](https://i.imgur.com/HufeoV6.png)

**Why serverless:**
 Serverless allows us to trigger a function once a file has been added/delete to a bucket, perfect for our post-processing action. Also we pay for the time we process, no more, no less. Last but not least, we can batch process and not worry about how many files are uploaded at once.

This is THE file where it all is tied together and if you’ve ever built anything bigger than a todo app, you know this will be a bottleneck — and it is. However! there are some fancy stuff you can do to make it a bit better, such as reference another file (see notes below) or use [javascript to generate parts of the yml](https://serverless.com/framework/docs/providers/aws/guide/variables/#reference-variables-in-javascript-files).

A couple of notes:

1. As you can see I’m using things like: `${file(./config.yml):source_bucket}` to grab values out of another yaml file. This is one way to abstract away the complexity of the serverless.yml and focus on a few parameters that may be important for deployment.
2. Line 29, we define the parameters that will be passed to the ffmpeg binary. They’re passed as env variables in the lambda function! (as you’ll see in the coming sections)
3. Line 30–60 is for having access to the buckets that we need for the app.
4. Line 67 defines the event handler, funny enough it also creates the bucket

serverless.yml for serverless-ffmpeg

We need webpack to bundle our javascript nicely, as well as use es6/7 features to write some modern day JS (rather than being bound to node 6.10 that lambda allows us). Let’s take a look at the webpack config + babelrc files to make that happen.

1. On line 8, we’re using the `slsw.lib.entries` in order to auto generate entries based on our functions in serverless. Thanks to the smarts of the serverless-webpack lib.
2. On line 23–24 we’re copying the binaries that will be used in our app. The reason we’re doing that here, is because we need the binaries to have executable permissions (+x).

This is where serverless starts! As we specified in our `serverless.yml` we want a function called `main` to run from our `handler.js` file, whenever there is an object created event in our source bucket.

1. Line 7 calls a function to extract the newly uploaded file’s location in the source bucket.
2. Thanks to our fancy webpack config, we can now use await/async which is what we do while we download the recently uploaded file from the source bucket into the lambda process.
3. Line 14 we run the ffmpeg function, which calls the binary in turn (see next section).
4. Line 15 we upload the results into the destination bucket.
5. Line 23 showcases how we use the predefined parameters as environment variables.

Let’s take a look at some of the interesting parts of the app code to see how this is all tied together.

1. Line 4 Make sure our lambda root is in the PATH env variable, this way we can call binaries with `spawn` directly located in our project root!
2. Line 21 we’re merging the arguments that we pass to the ffmpeg process.
3. Line 29 we call spawn with our arguments and hook up some event handlers
4. Line 34–35 we make sure to capture stdout and stderr, without this we literally have no idea what’s going on, if anything goes wrong.

As part of any real world application unit testing is important. But how can we test serverless functions? We can unit test parts of them! But how do we unit test calling a binary to do things? We set up our testing infrastructure to support this!

In order for us to achieve this we’ll need [ava](https://github.com/avajs/ava) (ava is great!), it allows us to quickly get started with a minimalistic configuration (see this [package.json](https://github.com/kvaggelakos/serverless-ffmpeg/blob/master/package.json#L43) for how to configure it properly).

1. Import ava and some helpers to deal with files.
2. Line 8 Run our ffprobe function which returns a json result ( [see it’s code to see how](https://github.com/kvaggelakos/serverless-ffmpeg/blob/master/src/ffmpeg.js#L9) )
3. Line 16 Run ffmpeg on a test file and expect a file to exist at the end of the test
4. Line 26 clean up after testing

One of the great things about serverless is how easy it is to deploy and tear down. Since serverless framework does it all in a cloudformation templates it’s fast and easy. No more “what command did I run where”.

To deploy the whole stack, we run: `sls deploy -v`. This will show the output of the cloudformation status so that we can make sure all resources are created as they should.

That’s it!

You can view this little video to see how it all works in the end.

I hope you enjoyed this quick deep dive into serverless and a real world example! In the next parts we’ll be looking at more fun real world scenarios and how to monetize them, so stick around!

**A couple of real life problems we encountered in this part:**

1. We want to add webpack to make this worth our time
2. We need to use a plugin with webpack and keep permissions for this binary to actually work (together with serverless framework)
3. A bucket is created if we attach events to it! Seems random, I know. But I don’t make the rules.
In the next parts I’ll reveal more life scenarios and problems solved.

If you have any questions or comments please post them here and I’ll do my best to help.

One thing that wasn’t obvious to me when I started out was how important plugins were for the serverless framework. The two plugins we’ll be using in this part are (more plugins in part 2 and 3):

[serverless-webpack](https://github.com/serverless-heaven/serverless-webpack)  
 Because as of today aws lambda supports node 6.10, which does not fully support es6. We want that fancy es6/7 and some other nice packaging features.

[serverless-s3-remover](https://github.com/sinofseven/serverless-s3-remover)  
 You’ll quickly realize you’re deploying and tearing down your stack with the serverless framework many times as you’re testing things. If you’re working with buckets, this simply helps us remove the buckets and the content in them when we destroy our stack. ( **WARNING: You will loose content with this** )

[Serverless — Beyond the over simplistic todo apps into the world of reality (part 1)](https://hackernoon.com/serverless-part-1-e75b4a5e59e6)