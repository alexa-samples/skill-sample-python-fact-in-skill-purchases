# Build An Alexa Skill with In-Skill Purchases using ASK Python SDK

<img src="https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/fact/header._TTH_.png" />

## Setup the ASK CLI
There are several aspects of developing an Alexa skill with in-skill purchases that require the use of the Alexa Skills Kit Command Line Interface (ASK CLI), so this entire walkthrough will require you to have installed and configured the ASK CLI.  If you haven't done this before, here are the resources you need to get the ASK CLI installed on your machine:

* [Quick Start Guide for Installing the ASK CLI](https://developer.amazon.com/docs/smapi/quick-start-alexa-skills-kit-command-line-interface.html)
* [ASK CLI Command Reference](https://developer.amazon.com/docs/smapi/ask-cli-command-reference.html)

If you have used the ASK CLI previously, you will also need to **make sure** that you have the **most recent version** of the ASK CLI.  You can make sure you have the latest version by running the command:

```bash
$ npm update -g ask-cli
```

## Setup the ASK SDK for Python

We have provided the code for this skill on [here](../lambda/py). To properly upload this code to Lambda, you'll need to perform the following:
    
1. This skill uses the [ASK SDK for Python](https://github.com/alexa-labs/alexa-skills-kit-sdk-for-python) for development. The skill code is provided in the [lambda_function.py](../lambda/py/lambda_function.py), and the dependencies are mentioned in [requirements.txt](../lambda/py/requirements.txt). Download the contents of the [lambda/py](../lambda/py) folder. 
2. On your system, navigate to the lambda folder and install the dependencies in a new folder called “skill_env” using the following command:

    ```
    pip install -r py/requirements.txt -t skill_env
    ```
    
3. Copy the contents of the `lambda/py` folder into the `skill_env` folder. 

    ```
    cp -r py/* skill_env/
    ```

4. Zip the contents of the `skill_env` folder. Remember to zip the **contents** of the folder and **NOT** the folder itself.
5. On the AWS Lambda console, change the **code entry type** drop-down to **Upload a .ZIP file**, upload the zip created in the previous step and click on **Save**.

    *(Optional)* Follow the ASK Python SDK [Getting Started](https://alexa-skills-kit-python-sdk.readthedocs.io/en/latest/GETTING_STARTED.html#adding-the-ask-sdk-for-python-to-your-project) documentation, to check alternative ways of installing the sdk and deploying to AWS Lambda console.

6. On the **Triggers** section, add **Alexa Skills Kit** as a trigger and click on **Save**.

### Create Skill on Developer Console

1. Create a new skill by following these steps:

     * Log in to the Alexa Skills Kit Developer Console.
     * Click the Create Skill button in the upper right.
     * Enter `Premium Facts Sample` as your skill name and click Next.
     * For the model, select Custom and click Create skill.

2. Next, define the interaction model for the skill from the JSON Editor. Select JSON Editor from the sidebar and **replace** the contents with the contents provided in [this JSON file](models/en-US.json), and save it.

3. Build the skill model.

4. Navigate to the skill endpoints and add the previously created AWS Lambda Function ARN as the Default Region endpoint. Save the endpoints.

### Local installation for ASK CLI and Skill

1. Create a new directory for CLI work and navigate to the directory.

2. **Clone** the `Premium_Facts_Sample` skill created above using the CLI. This would get you the skill metadata and lambda code cloned at a single place, for working with ISP.

     ```bash
     $ ask clone
     ```

3. **Navigate** to your project folder.

     ```bash
     $ cd Premium_Facts_Sample
     ```

4. **Explore** the project structure.  You should see folders for lambda and models, and skill.json file.

     ```bash
     $ ls
     lambda         models         skill.json
     ```

### Creating In-Skill Products

There are ASK CLI commands for creating your in-skill purchases.  This guide will walk you through creating three different one-time purchases (entitlements), as well as a subscription.  Our sample code is expecting these to be created as described, so make sure to follow along carefully.

1. **Create** your first in-skill product.  You should be in the project's root directory.

     ```bash
     $ ask add isp
     ```

3. **Choose** Entitlement.

     ```bash
     ? List of in-skill product types you can choose (Use arrow keys)
     ❯ Entitlement
     Subscription
     ```

4. **Choose** Entitlement_Template as your template.

     ```bash
     ? List of in-skill product templates you can choose (Use arrow keys)
     ❯ Entitlement_Template
     ```

5. **Name** your in-skill product *science_pack*.

     ```bash
     ? Please type in your new in-skill product name:
     (Entitlement_Template) science_pack
     ```

6. **Repeat** steps #2 - #5 to create two more entitlements: *history_pack* and *space_pack*.

     ```bash
     ? Please type in your new in-skill product name:
     (Entitlement_Template) history_pack
     ...
     ? Please type in your new in-skill product name:
     (Entitlement_Template) space_pack
     ```

7. **Create** a subscription product named *all_access* using a similar process.

     ```bash
     $ ask add isp

     ? List of in-skill product types you can choose (Use arrow keys)
       Entitlement
     ❯ Subscription

     ? List of in-skill product templates you can choose (Use arrow keys)
     ❯ Subscription_Template

     ? Please type in your new in-skill product name:
     (Subscription_Template) all_access

8. **Navigate** to the new ISPs directory, and note the two folders, *entitlement* and *subscription*.  This is where the JSON files for each of your in-skill products reside.

     ```bash
     $ cd isps
     $ ls
     ```

9. **Navigate** to the *entitlement* folder.  You should see three files in this directory, one for each of the entitlements you created in our previous steps.

     ```bash
     $ cd entitlement
     $ ls
     ```

10. **Open** history_pack.json

     This JSON file contains all of the necessary fields for your in-skill product, but you'll need to add the details to get them ready to sell. Because we used the Entitlement_Template template, we have provided a small explanation for each field, make sure you replace all of them. Take a look at [the sample in our docs](https://developer.amazon.com/docs/smapi/isp-schemas.html#entitlement-schema) for an additional reference.  For this sample, at a minimum, you will need to update the name (not referenceName!), smallIconUri, largeIconUri, summary, description, purchasePromptDescription, boughtCardDescription, releaseDate and privacyPolicyUrl.  Alternatively you can copy and paste the contents of the files found here: [ISP Entitlements](isps.samples/entitlement).

     After updating *history.pack.json*, Fill out the details for the *science_pack.json* and *space_pack.json* files.  You will need to update with content about your science and space products including icons for each.

     > **IMPORTANT: Don't change the *referenceName* in your files, as our codebase is relying on those to be consistent.**

     Once you are happy with your pricing, descriptions, and the other metadata for your three entitlements, you should update the same fields plus the subscriptionPaymentFrequency for your subscription.  Alternatively you can copy and paste the contents of [All Access ISP subscription sample](isps.samples/subscription/all_access.json) into your *all_access.json* file.

11. **Review and edit** the subscription file.

     ```bash
     $ cd ../subscription
     $ open all_access.json
     ```

     Now that you have customized your in-skill products, you can deploy your skill using the ASK CLI, and start testing it.

     > _Note: Be sure to review the output to confirm there were no errors._

### Deployment

1. **Navigate** to the project's root directory. You should see a file named 'skill.json' there.

     ```bash
     $ cd ../..
     ```

2. **Deploy** the skill and the Lambda function in one step by running the following command:

     ```bash
     $ ask deploy
     ```
     Assuming that you followed all of the setup instructions for the ASK CLI, your entire skill and Lambda function should be created on their respective portals.


### Testing

1. To test, login to [Alexa Developer Console](https://developer.amazon.com/alexa/console/ask), click on the **Premium Facts Sample** entry in your skill list, and click on the "Test" tab.  The "Test" switch on your skill should have been automatically enabled.  If it was not, enable it now.

2. Your skill can now be tested on devices associated with your developer account, as well as the Test tab in the Developer Portal. To start using your skill, just type or say:

     ```text
     Alexa, open premium facts sample
     ```

**Note: The developer account associated with the skill is never charged for in-skill products.**  For more details about testing skills with in-skill products, please refer to the [In-Skill Purchase Testing Guide](https://developer.amazon.com/docs/in-skill-purchase/isp-test-guide.html)

Additional Resources
--------------------

### Community

-  [Amazon Developer Forums](https://forums.developer.amazon.com/spaces/165/index.html) : Join the conversation!
-  [Hackster.io](https://www.hackster.io/amazon-alexa) - See what others are building with Alexa.

### Tutorials & Guides

-  [Voice Design Guide](https://developer.amazon.com/designing-for-voice/) -
   A great resource for learning conversational and voice user interface design.

### Documentation

-  [Official Alexa Skills Kit Python SDK](https://pypi.org/project/ask-sdk/)
-  [Official Alexa Skills Kit Python SDK Docs](https://alexa-skills-kit-python-sdk.readthedocs.io/en/latest/)
-  [Official Alexa Skills Kit Docs](https://developer.amazon.com/docs/ask-overviews/build-skills-with-the-alexa-skills-kit.html)
