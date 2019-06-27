# AWS Sandbox

A simple Node.js web app to explore Amazon Web Services.

Based on Academind's tutorial video [Getting Started with AWS | Amazon Web Services BASICS](https://academind.com/learn/aws/the-basics/getting-started-with-aws/). Check out his Github repository [here](https://github.com/academind/aws-first-node-app).

## Demo

Access a demonstration of the working application at this custom [AWS link](http://awssandbox-env.jfv7jgtbmz.us-east-2.elasticbeanstalk.com/).

## Get started with AWS Sandbox App locally

Ensure you have Node.js installed, then install the required dependencies enumerated in the package.json to your project:

``` bash
npm install express body-parser cookie-parser debug jade morgan serve-favicon --save
```

Note: You can also achieve a fresh install with all package dependencies using the following commands:

``` bash
rm -rf node_modules
npm install
```

### Entry point

Our entry point is `bin/www`, which is pointed to in our `package.json` start script. We can run the app either using `node ./bin/www` or `npm start`.

## Tutorial

### Create a free AWS account

1. Create an AWS Account [here](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=header_signup&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start).
1. Set Account type to `Personal` if you're just playing around with their services to learn what they offer.
1. Fill in billing info and select the `Free` Support Plan.
1. Review their [tutorials](https://aws.amazon.com/getting-started/tutorials/launch-an-app/) page.

### Virtual Servers in the Cloud

1. Sign In to the Console [here](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fnc2%3Dh_ct%26src%3Dheader-signin%26state%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&forceMobileApp=0).
1. Search [`EC2`](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Home:) (or navigate `All services` > `Compute` > `EC2`)
1. Click `Launch Instance` and select an operating system for you Web Server to be run on. (Be sure it's tagged with `Free tier eligible`.)
1. Choose an Instance Type that's tagged with `Free tier eligible` (there should only be one).
1. Click `Review and Launch`, and confirm on the next page.
1. Create a new key pair on the dropdown menu, and name it "aws-sandbox." Be sure to `Download Key Pair`. (You will need the pem file when you connect to the instance.)
1. Launch Instances.
1. View your [instance](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:sort=instanceId) by navigating `Services` > `EC2` > `Instances`.
1. When you no longer wish to run your free server, choose `Actions` > `Instance State` > `Terminate`.

(Note: When you shut down the instance, the storage is lost. You get 8 GB free for 1 year on the Free Tier.)

### Deploy a web app

1. On the [homepage](https://us-east-2.console.aws.amazon.com/console/home?region=us-east-2) look under "Build a solution" and choose "Build a web app."
1. Name it `aws-sandbox`, choose `Node.js` as the Platform, and select `Upload your code`.

(Note: When you download a repository from Github, there will be a folder that contains the root of your project _inside the zip_. The zip file itself must contain the root, so unzip the project, select all the files and folders in root, and send it to zip.)

3. Choose your zipped Node.js project and click "Upload".
1. Click "Configure more options" and from there "Create App." (It will take a few minutes as it installs all our dependencies and gets the environment set up.)

### Opps, the app is Degraded!

When the app launches it should give a health status of "Degraded." This is because we selecting "Node.js" as our Platform, and our app is actually a Node.js Express app. To resolve the issue, continue with the following steps:

1. On your instance's [Dashboard](https://us-east-2.console.aws.amazon.com/elasticbeanstalk/home?region=us-east-2#/environment/dashboard?applicationName=aws-sandbox&environmentId=e-ptacw83iic) page (`Services` > `Elastic Beanstalk` > `aws-sandbox` > `AwsSandbox-env`) select the `Configuration` tab.
1. In the "Software" category, choose `Modify` and 

By default AWS tries to launch the app.js file (the standard entry point). In the `package.json` under `scripts`, look for `"start": "node ./bin/www"`. This means `www` is our entry point. We have to let AWS know where to find our entry point by giving it the Node command:

``` bash
npm start
```

This will execute the start script in our package.json and launch the app.

3. Input `npm start` in the "Node command" field and Apply the changes. (This will take a few minutes again.)
1. Visit the URL provided on your [Dashboard](https://us-east-2.console.aws.amazon.com/elasticbeanstalk/home?region=us-east-2#/environment/dashboard?applicationName=aws-sandbox&environmentId=e-ptacw83iic) page.