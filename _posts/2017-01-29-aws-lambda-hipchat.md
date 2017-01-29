---
published: true
comments: true
layout: post
title: How to post to HipChat from AWS Lambda
---
At first, I investigated using a bot to post to HipChat ([GitHub's Hubot](https://hubot.github.com/)) but it seemed a little overkill. It had many features that I didn't need, and had to be run on a server 24/7. I did run it using [Heroku](https://www.heroku.com/) so it didn't cost anything, but it was a bit too clunky.

So instead, I started looking for other ways to achieve this, [Amazon Web Services' Lambda](https://aws.amazon.com/lambda/) looked like the best option. The tagline Amazon use for the service is:

> Run code without thinking about servers.

and that's exactly what I wanted! Lambda lets you run Python code, and the best part is, the first million requests you make each month are free.

So, how do you setup Lambda to post to HipChat?

Firstly, login to [hipchat.com](hipchat.com), select the _Rooms_ tab, and find the room you would like to post in. Now, make a note of the _API ID_ as you will need this later. Then click on _Tokens_ in the left menu.

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.08.37.png)

Now, enter a name for your Token, make sure you have selected _Send Notifications_ and click _Create_.

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.13.06.png)

You will now see your API token, this will allow you to post to the room. Make a note of it.

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.15.55.png)

Next, login to AWS (Create an account [here](https://aws.amazon.com/free/) if you don't already have one). Navigate to the Lambda service. Click _Create a Lambda function_ and choose the _Blank Function_ blueprint.

You now have the option to choose a Trigger for the function. I wanted to post to HipChat once, per day at 9AM for example, so I selected _CloudWatch Events - Schedule_.

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.24.27.png)

Enter a name, desciption and a schedule expression. You can find the syntax for scheduling [here](http://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html).

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.28.23.png)

Make sure to tick the _Enable_ box and click next.

Now we need to configure the function. Enter a name, description and choose _Python 2.7_ as the runtime.

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.34.04.png)

Next, copy and paste the code from below into the code section.

{% gist c6cb00b76db38b5de9e7a84b650e23e1 %}

Change _enter_token_here_ and _enter_room_id_here_ to the values you saved earlier. Note: you can also change _'color': 'purple'_ and _'from': 'Lambda'_ to change how your message will appear in HipChat.

_message = "Write your message here"_ - Enter the message you would like to post inside the speech marks.

Now, set the Handler to the functionName.post so in my case, HipChat-Post.post

Select _Choose an existing role_ then select the role called _lambda_basic_execution_.

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.42.01.png)

Leave all other options as default, and click _Next_ at the bottom of the page. Then scroll down and click _Create function_.

Congratulations, you have created your first Lambda function! 

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.46.27.png)

Select _Test_ at the top of the page, it will ask you for input, but we don't need any, so leave the options as default and click _Save and Test_.

You should now see 'Success' output to the execution results, and your message in HipChat!

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.59.39.png)

![]({{site.baseurl}}/images/Screen%20Shot%202017-01-29%20at%2016.57.38.png)



