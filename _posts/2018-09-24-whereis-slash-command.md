---
published: true
comments: true
layout: post
title: WhereIs - A Slack command to help you locate people
---

<p align="center">
  <img src="https://raw.githubusercontent.com/LewisLebentz/lewislebentz.github.io/master/images/Screenshot%202018-09-23%20at%2021.12.42.png" alt="WhereIs - Slack Command"/> 
</p>

After it was announced that we would be moving away from HipChat to Slack at my company, I decided it would be a good time to learn how to create a [Slack](https://slack.com) 'slash command' and at the same time use the [Serverless Framework](https://serverless.com) to automate a lot of the setup.

So I created a command `/whereis` that uses the [Cisco Prime Infrastructure](https://www.cisco.com/c/en/us/products/cloud-systems-management/prime-infrastructure/index.html) API to grab the location of a user based on the username they authenticate to the network with, which in our case is the user's Active Directory username which is authenticated via 802.1x.

Once the API has been queried it returns a variety of fields, including the specific Access Point the user is connected to, but I didn't want to be that granular. So in my code I return the Floor of the AP and the time the user associated to it.

The code for this has been written in Python, and is deployed to [AWS Lambda](https://aws.amazon.com/lambda) and [API Gateway](https://aws.amazon.com/api-gateway) with Serverless. This automates most of the setup and allows you to put everything in version control.

I have open-sourced the code, and posted it to GitHub here:

[https://github.com/LewisLebentz/WhereIs](https://github.com/LewisLebentz/WhereIs)

Feel free to send a PR or add a comment to this post with any improvements. It would greatly appreciated as it's the first time I've ever created a 'proper' public project on GitHub.

Please find steps below to set this up for your own environment:

Setup
---

1. Clone the WhereIs repository and enter the directory.

       git clone https://github.com/LewisLebentz/WhereIs.git && cd WhereIs

2. If you haven't already, install the Serverless Framework.

       npm install serverless -g
 * You will need AWS credentials setup on your machine before being able to run Serverless commands. Follow the guide [here](https://serverless.com/framework/docs/providers/aws/guide/credentials).

3. Install the dependencies.

       npm install --save

       pip install pipenv

4. Update serverless.yml changing the region, securityGroupIds and subnetIds where applicable.

5. Update handler.py changing the url variable with your Cisco Prime IP/address.

6. Run the command to deploy.

       sls deploy

   <img src="https://raw.githubusercontent.com/LewisLebentz/lewislebentz.github.io/master/images/Screenshot%202018-09-23%20at%2022.51.59.png" width="700">

### Slack Setup ###

1. Login to Slack and navigate to the [Create a Slack App](https://api.slack.com/apps?new_app=1) page.

2. Give your app a name and choose the workspace you'd like to deploy it to.

   <img src="https://raw.githubusercontent.com/LewisLebentz/lewislebentz.github.io/master/images/Screenshot%202018-09-23%20at%2022.24.19.png" width="400">

3. Under 'Features' navigate to 'Slash Commands' and select 'Create New Command'. Call the command whatever you like, and for the Request URL enter the URL returned when the `sls deploy` command finished executing. Fill in the Description and Hint with something meaningful and save.

4. Now, under 'Settings' choose 'Install App' and install it to your workspace.

5. Finally, in Slack run `/whereis firstname.surname` and it should return the location from Prime!
