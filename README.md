 <h1>Smart UI Testing With StoryBook</h1>

<img height="400" src="https://user-images.githubusercontent.com/126776938/232535120-b4856bdd-c869-4bcd-bcdb-29a83e30505c.png">


<p align="center">
  <a href="https://www.lambdatest.com/blog/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample" target="_bank">Blog</a>
  &nbsp; &#8901; &nbsp;
  <a href="https://www.lambdatest.com/support/docs/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample" target="_bank">Docs</a>
  &nbsp; &#8901; &nbsp;
  <a href="https://www.lambdatest.com/learning-hub/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample" target="_bank">Learning Hub</a>
  &nbsp; &#8901; &nbsp;
  <a href="https://www.lambdatest.com/newsletter/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample" target="_bank">Newsletter</a>
  &nbsp; &#8901; &nbsp;
  <a href="https://www.lambdatest.com/certifications/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample" target="_bank">Certifications</a>
  &nbsp; &#8901; &nbsp;
  <a href="https://www.youtube.com/c/LambdaTest" target="_bank">YouTube</a>
</p>
&emsp;
&emsp;
&emsp;

*Using the LambdaTest platform, you can perform regression testing in just one click and find Visual UI Regression bugs easily with the help of Smart Testing. The @lambdatest/smartui package is LambdaTest's command-line interface (CLI) aimed to help you run your SmartUI tests on LambdaTest platform.*

*Learn the how to get started with Smart UI testing with StoryBook on the LambdaTest platform.*

[<img height="58" width="200" src="https://user-images.githubusercontent.com/70570645/171866795-52c11b49-0728-4229-b073-4b704209ddde.png">](https://accounts.lambdatest.com/register?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample)


## Table of Contents:

* [Pre-requisites](#pre-requisites)
* [Steps To Create A SmartUI Project](#steps-to-create-a-smartui-project)
* [Running Your First StoryBook SmartUI Test](#running-your-first-storybook-smartui-test)
* [Setting Up GitHub App Integration With SmartUI](#setting-up-github-app-integration-with-smartui)


## Pre-requisites

1. Basic understanding of [StoryBook](https://storybook.js.org/docs/react/get-started/introduction) is required.
2. Node version installed should be higher than `14.15.0.` Click [here](https://nodejs.org/en/download/releases/) to know more.
3. StoryBook version installed should be higher than `6.4.0.` Click [here](https://github.com/storybookjs/storybook/releases) to know more.
4. Login to [LambdaTest SmartUI](https://smartui.lambdatest.com/) with your credentials.

## Steps To Create A SmartUI Project

The first step is to create a project with the application in which we will combine all your builds run on the project. To create a SmartUI Project, follow these steps:

1. Go to the [Projects page](https://smartui.lambdatest.com/).
2. Click on the `new project` button.
3. Select the platform as **Web** for executing your `StoryBook` tests.
4. Add name of the project, approvers for the changes found, tags for any filter or easy navigation.
5. Click on the **Submit**.

## Running Your First StoryBook SmartUI Test

### Step 1: Install the Dependencies

Install required NPM modules for `LambdaTest Smart UI StoryBook CLI` in your Frontend project.

```
npm install @lambdatest/smartui-storybook -g
```

### Step 2: Setup with StoryBook

Add the following to your `.storybook/main.js`. You can read more about this here Storybook [Feature flags](https://storybook.js.org/docs/react/configure/overview#feature-flags).

```
module.exports = {
  features: {
    buildStoriesJson: true,
  },
};
```

### Step 3: Configure your Project Token

Setup your project token show in the **SmartUI** app after, creating your project.

 <b>For Linux/macOS:</b>
 
  ```
 export PROJECT_TOKEN="123456#1234abcd-****-****-****-************"
  ```

   <b>For Windows:</b>

  ```
  set PROJECT_TOKEN="123456#1234abcd-****-****-****-************"
  ```

## Step 4: Create and Configure SmartUI Config

You can now configure your project settings on using various available options to run your tests with the SmartUI integration. To generate the configuration file, please execute the following command:

```bash
smartui config create .smartui.json
```

Once, the configuration file will be created, you will be seeing the default configuration pre-filled in the configuration file. Here is our [StoryBook Sample](https://github.com/LambdaTest/smartui-storybook-sample/tree/master).

```bash
{
  "storybook": {
    "browsers": [
      "chrome",
      "firefox",
      "safari"
      // Add more browser configuration here
    ],
    "resolutions": [
      [1920, 1080]    // Add more view ports to capture here
    ],
    "include": [],    // (Optional) Only compare limited stories
    "exclude": []     // (Optional) Don't compare the stories
  }
}
```

### Step 5: Execute the Tests on SmartUI Cloud using CLI

You can now execute your `StoryBook` components for `Visual Regression Testing` using the following options:. Run the following command to run Visual Regression tests on your Storybook components.

**For Locally Hosted Server:**

```bash
smartui storybook http://localhost:6006 --config .smartui.json
```

**For Static Build:**

```bash
npm run build-storybook
smartui storybook ./storybook-static --config .smartui.json 
```

**For Public Hosted URL:**

```bash
smartui storybook https://<your_public_hosted_url> --config .smartui.json
```

You can also provide path to the storybook-static directory instead of the local Storybook URL. Use `--help` for more information on usage.

## Setting Up Github App Integration with SmartUI

### Steps 1: Integrate the your Lambdatest Account with GitHub App. 

You can integrate your LambdaTest account with the GiHub application in the following ways:

- Using OAuth

![github-app-landing-92ef6e152a7302cb9ab88f5034b9ec0c](https://user-images.githubusercontent.com/126776938/232715867-f375b4df-1bc9-4e88-8340-44e986be2e9a.png)


### Step 2: Select your GitHub repository 

Go to your GitHub repository where you want to configure your SmartUI project. Check out our GitHub sample [here](https://github.com/LambdaTest/smartui-node-sample).


### Step 3: Setting up your CI configuration

Setting up your CI workflow to execute on GitHub. Here is an example setup with `GitHub Actions`:

Go to `.github/workflows/<your_ci_file>.yml`.

```bash
    name: Storybook PR Checks
on:
  pull_request:
    branches:
      - master

env:
  PROJECT_TOKEN: ${{ secrets.PROJECT_TOKEN }}

jobs:
  smartui-gihub-action:
    name: Execute Storybook build
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1

    - name: Find Last CommitId
      run: |
        API_HOST=https://api.github.com
        # Check out the PR branch
        git checkout $GITHUB_HEAD_REF
        # Get the commit ID of the last commit
        COMMIT_ID=$(git rev-parse HEAD)
        echo "Last commit ID of PR: $COMMIT_ID"
        GITHUB_URL=$API_HOST/repos/$GITHUB_REPOSITORY/statuses/$COMMIT_ID
        echo "GITHUB_URL: $GITHUB_URL"
        echo "GITHUB_URL=$GITHUB_URL" >> $GITHUB_ENV
   
    - name: Install Dependencies
      run: |
        npm install
        npm install @lambdatest/smartui-storybook -g
    - name: Create storybook static build
      run: npm run build-storybook

    - name: Execute storybook build
      run: |
        smartui --version
        smartui config create .smartui.json
        smartui storybook ./storybook-static --config .smartui.json
```

### Step 4: Execute your test suite with CI

After the setup is completed, you can now execute your test suite with the Continuos Integration (CI) pipeline with any tool of your choice.

### Step 5: Commit you changes over git on a branch and raise the PR to main branch.

### Step 6: Now you will see the `lambdatest-smartui-app` in the PR.

## Documentation & Resources :books:
      
Visit the following links to learn more about LambdaTest's features, setup and tutorials around test automation, mobile app testing, responsive testing, and manual testing.

* [LambdaTest Documentation](https://www.lambdatest.com/support/docs/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample)
* [LambdaTest Blog](https://www.lambdatest.com/blog/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample)
* [LambdaTest Learning Hub](https://www.lambdatest.com/learning-hub/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample)    

## LambdaTest Community :busts_in_silhouette:

The [LambdaTest Community](https://community.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample) allows people to interact with tech enthusiasts. Connect, ask questions, and learn from tech-savvy people. Discuss best practises in web development, testing, and DevOps with professionals from across the globe 🌎

## What's New At LambdaTest ❓

To stay updated with the latest features and product add-ons, visit [Changelog](https://changelog.lambdatest.com/) 
      
## About LambdaTest

[LambdaTest](https://www.lambdatest.com?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample) is an intelligent unified digital experience testing cloud that helps businesses drastically reduce time to market through faster test execution, ensuring quality releases and accelerated digital transformation. The platforms allows you to perform both real time and automation testing across 3000+ environments and real mobile devices, making it a top choice among other cloud testing platforms. Over 10,000+ enterprise customers and 2+ million users across 130+ countries rely on LambdaTest for their testing needs. 

### Features

* Run Selenium, Cypress, Puppeteer, Playwright, and Appium automation tests across 3000+ real desktop and mobile environments.
* Real-time cross browser testing on 3000+ environments.
* Test on Real device cloud
* Blazing fast test automation with HyperExecute
* Accelerate testing, shorten job times and get faster feedback on code changes with Test At Scale.
* Smart Visual Regression Testing on cloud
* 120+ third-party integrations with your favorite tool for CI/CD, Project Management, Codeless Automation, and more.
* Automated Screenshot testing across multiple browsers in a single click.
* Local testing of web and mobile apps.
* Online Accessibility Testing across 3000+ desktop and mobile browsers, browser versions, and operating systems.
* Geolocation testing of web and mobile apps across 53+ countries.
* LT Browser - for responsive testing across 50+ pre-installed mobile, tablets, desktop, and laptop viewports
    
[<img height="58" width="200" src="https://user-images.githubusercontent.com/70570645/171866795-52c11b49-0728-4229-b073-4b704209ddde.png">](https://accounts.lambdatest.com/register?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample)
      
## We are here to help you :headphones:

* Got a query? we are available 24x7 to help. [Contact Us](mailto:support@lambdatest.com)
* For more info, visit - [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=playwright-sample)
