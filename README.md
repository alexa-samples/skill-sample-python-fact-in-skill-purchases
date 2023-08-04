# Build An Alexa Skill with In-Skill Purchases using Developer Console

<img src="https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/fact/header._TTH_.png" />

Create Skill on Developer Console by importing from GitHub
--------------------

1.  Go to the **[Alexa Developer Console](https://developer.amazon.com/alexa/console/ask)**. Enter your account credentials and click the **Sign In** button.
(If you don't already have an account, you will be able to create a new one for free.)

2.  Once you have signed in, select the **Create Skill** button near the top-right of the list of your Alexa Skills.

3. Give your new skill a **Name**, for example, 'Premium Facts Sample'.

4. Select the Default Language. This tutorial will presume you have selected 'English (US)'. Click the **Next** button at the top right.

5. Select **Other** under the *'Choose a type of experience'* section.

6. Select the **Custom** model under the *'Choose a model'* section.

7. Select **Alexa-hosted (Python)** under the *'Hosting services'* section. Click the **Next** button at the top right.

8. Choose **Start from scratch** from the *Templates* section and click the **Import skill** button at the top right.

9. Paste the following link in the dialog box and click **Import**.
	```
	https://github.com/alexa-samples/skill-sample-python-fact-in-skill-purchases
	```

Once the skill is created, you will have an Alexa-hosted skill with the interaction model based on the content provided in this [JSON file](models/en-US.json), and the code as per this [lambda function](lambda/py/lambda_function.py).

Creating In-Skill Products
--------------------

1. To create an In-Skill product, on the **Build** page, under Skill builder checklist, click **Monetize Your Skill**. Or, in the left pane, click **TOOLS**, and then select **Monetize Your Skill**.

2. Follow all the steps in the documentation for **[Add a product and link it with the skill](https://developer.amazon.com/en-US/docs/alexa/in-skill-purchase/create-isp-dev-console.html#create-and-edit-in-skill-products)**

Testing
--------------------

1. To test, login to [Alexa Developer Console](https://developer.amazon.com/alexa/console/as), click on the **Premium Facts Sample** entry in your skill list, and click on the "Test" tab.  The "Test" switch on your skill should have been automatically enabled.  If it was not, enable it now.

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

### Documentation

-  [Create and Manage In-Skill Products](https://developer.amazon.com/en-US/docs/alexa/in-skill-purchase/create-isp-dev-console.html)
-  [Test In-Skill Purchasing Skills](https://developer.amazon.com/en-US/docs/alexa/in-skill-purchase/isp-test-guide.html#test-products)

