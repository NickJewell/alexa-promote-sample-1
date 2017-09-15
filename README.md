
README

This is a simple repository that contains all the code components needed by the Alexa skill in order to call a 'HelloWorld' example against the Alteryx Promote API. 

HOW TO DEPLOY

Download this repository (including the multiple subfolders) and the alexa-promote.py file. Feel free to edit the contents of alexa-promote.py to meet your needs, and to include the relevant Alexa Skill ID, Promote Server URL, username and API key details. 

Zip these files locally so that you can import them into your AWS Lambda function as a single package (or host them in a dedicated S3 bucket). 

Create your AWS Lambda function by signing up at: https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions

Create your Alexa Skill by signing up at: 
https://developer.amazon.com/alexa-skills-kit

Test your skill using: 
http://echosim.io/

CONFIGURATION NOTES:
--------------------

LAMBDA FUNCTION Configuration: 

 - Be sure to use a blank python function template
 - Use Python 2.7
 - Set your handler to alexa-promote.lambda_handler (referencing the python code in the repo)
 - You'll need to create a basic lambda execution role. Instructions here: http://docs.aws.amazon.com/lambda/latest/dg/with-s3-example-create-iam-role.html
 - In Advanced Settings, use a timeout of 30s (as I've found the default 3s to be a little unforgiving!)
 - Once created, take a note of the ARN (Amazon Resource ID) as you'll need to link this into your Alexa Skill.

ALEXA SKILL Configuration: 

 - Add a new skill via the developer console at: https://developer.amazon.com/edw/home.html#/skills
 - Once created, make sure you note the skill ID (you then need to add this to your lambda function) 
 - Give the skill a name. For example 'Alteryx-Promote-Demo-1'
 - Give the skill an invocation, for example 'Promote'. This means you'll call the skill by saying 'Alexa, open Promote'
 - Define an Interaction Model. For this example, it's trivial. Use something like the code below:
 
> {
  "intents": [
    {
      "intent": "SayHi"
    },
    {
      "intent": "AMAZON.HelpIntent"
    }
  ]
}

 - Set up Sample Utterances so that the skill knows how to run. In our Python code we're expecting an Intent called SayHi, so add a sample such as:
> SayHi Run Demo

 - So when the user says 'Alexa, ask Promote to Run Demo', the correct python function will trigger. 
 - Go to the configuration tab, and make sure that the ARN for the Lambda code is entered here. 
 - Now go to the test tab, and start trying the skill out! If you get errors, go back to your AWS console and examine the Cloudwatch logs: you'll get all the python log details there. Also, check your Promote server's logs in case the model itself is having issues. 

