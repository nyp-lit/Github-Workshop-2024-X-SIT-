# Challenge 2: Automation 🤖

![Pull request checks](https://github.githubassets.com/images/modules/site/actions/pr-checks-final.webp)
<sup>Example of Automated Checks Using GitHub Actions.</sup>
[<sup>Source</sup>](https://github.com/features/actions)

Throughout the Software Development Life Cycle (SDLC), we should be testing our applications frequently to identify and fix any bugs encountered. Additionally, we need to ensure that any libraries added are compatible and do not introduce security vulnerabilities.

While it is possible to manually test an application for bugs and vulnerabilities, the process is often time consuming, repetitive and tedious. **Automation** can help to reduce these burdens by automatically performing repetitive tests on your behalf, so that you can focus your precious time on development.

In this challenge, we will be learning about using GitHub Actions to automate common tests and Dependabot for automated dependency updates and alerts. We also encourage you to look through the codebase of the simple Node.js web app we have provided for these challenges.

Leveraging on these tools allows Developers to detect and prevent defects in their codebase earlier in the SDLC more frequently. This is known as "Shift-Left Testing" in DevOps, and it fully embodies the "Test early and often" mantra typically seen in Agile organizations practicing iterative development.

## Build and Unit Testing

Every time we make changes to the web app's codebase, we should perform tests to ensure that:

1. All dependencies (ie. libraries) we use in the project are compatible with the Node.js versions we plan to use
2. Any new code does not cause the web app to fail to build or execute
3. Any new code does not introduce bugs that break the functionality of either new or existing features

For points 1 and 2, we can test this by ensuring that the application builds and runs successfully after each change.

For point 3, we can test this using [unit testing](https://en.wikipedia.org/wiki/Unit_testing). Unit testing is outside the scope of this workshop, so we have provided an example within the `test/` folder for use in the challenge.

The above tests can be automated with the help of **GitHub Actions**. GitHub Actions is a feature that allows users to define and automate software workflows, such as building, testing and deploying. This is commonly known as Continuous Integration and Continuous Delivery (CI/CD).

_Events_ like pushing new changes to your repository triggers a workflow to be run, whereby _actions_ like tests are performed on your application code.

In the event that a GitHub Actions workflow (ie. pipeline) fails, alerts will be sent to notify developers of the failed pipeline. Additionally, if Pull Requests are used, failed pipelines can blocked changes from being merged into the `main` branch, proactively preventing bugs from introduced into your codebase.

To learn more about GitHub Actions, you may visit the [GitHub Actions documentation](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions).

### Challenge 2.1: Automate Testing using GitHub Actions

**Using GitHub Actions, perform build tests for Node.js versions 14.x, 16.x and 18.x and unit tests in the `test/` folder.**

You can run `npm test` for the unit tests.

Expected output: The web app should be compatible with all listed versions and unit tests pass.

![Example of build tests passing](https://user-images.githubusercontent.com/11332803/172466237-4f4c7551-9430-4e0b-a443-2fa94cbf7a4e.png)  
<sup>Example of build tests passing.</sup>

![Example of unit tests passing](https://user-images.githubusercontent.com/11332803/172466295-aa885460-56b9-434d-905f-7ecb64ad21ea.png)  
<sup>Example of unit tests passing.</sup>

### Challenge 2.1 Hints

<details>
  <summary>Spoiler warning</summary>
  <br/>

1. Create a file in `.github/workflows` folder (create folders if they do not exist) with `.yml` file extension, eg. `challenge2.yml`.
2. You may follow [this documentation](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs) for an example of a Node.js workflow.

</details>

## Code Linting

**Code linters** are static code analysis tools commonly used to improve the quality of code.

Linters help to flag out:

1. Formatting and styling inconsistencies
2. Non-adherence to coding standards and conventions
3. Common logical bugs / errors

Typically, different programming languages will have their own specialized linters specific to the syntax of the language. Modern linters will also allow developers to add custom rules.

In some code editing tools such as **JetBrains** IDEs and Visual Studio Code, there may be built-in functionality or downloadable extensions to lint code as you write it. However, we should still include automated code linting as a GitHub Action to enforce code quality, since not all repository collaborators may be use linting tools locally.

### Challenge 2.2: Lint the Codebase using GitHub Actions

**Using GitHub Actions, perform code linting.**

Expected outcome: The code linter should report linting issues in the codebase and fail the pipeline.

![Example of linting errors](https://user-images.githubusercontent.com/11332803/172466191-d6afcefa-8ed3-4a8b-8809-1ed8b4703265.png)  
<sup>Example of linting errors.</sup>

(Optional) Fix the issues identified by the code linter.

### Challenge 2.2 Hints

<details>
  <summary>Spoiler warning</summary>
  <br/>

1. You can reuse the `.yml` file you created in Challenge 2.1 and just add on the linting action.
2. You can consider using the [Super-Linter GitHub Action](https://github.com/github/super-linter), which natively supports linting all languages in the codebase.

</details>

## Automated Dependency Updates and Alerts

In almost all projects small or large, you will likely depend on external libraries to develop your applications. You may take a look at the dependencies required by the web app in the `package.json` file.

Even the most widely used dependencies may contain vulnerabilities. Vulnerabilities in dependencies may expose your application to potential exploitation and affects its security posture. It is important to keep all dependencies up-to-date so that these security risks are mitigated.

However, it is tedious to perform these checks manually, especially for larger projects that utilize many external libraries. It is also difficult to be thorough, since the libraries may also depend on other libraries that could contain vulnerabilities.

This process of checking for vulnerable dependencies can be fully-automated with the help of automated dependency updating tools. They can be used to:

1. Automatically check the codebase for vulnerable dependencies periodically
2. Send alerts when vulnerable dependencies are found
3. Suggest appropriate remediation actions via Pull Requests by upgrading outdated dependencies automatically

GitHub has a native feature for automated dependency updates: **Dependabot**. To learn more about Dependabot, you may visit [this article on Dependabot](https://github.blog/2020-06-01-keep-all-your-packages-up-to-date-with-dependabot/) and the [Dependabot documentation](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/about-dependabot-security-updates).

### Challenge 2.3: Configure Automated Dependency Updates

**Add automated dependency updating to your repository using Dependabot.**

You should configure Dependabot to do the following:

1. Check for vulnerable Node.js dependencies and create Pull Requests
2. Send alerts when vulnerable Node.js dependencies are found
3. Check for outdated Node.js dependencies and create Pull Requests
4. Daily scheduled version checks

Expected output: Dependabot detects vulnerable dependencies and creates Pull Requests to update affected dependencies.

![Example of warnings](https://user-images.githubusercontent.com/11332803/172466307-1e659395-a25d-4b02-9306-01f068043724.png)
<sup>Example of warnings.</sup>

(Optional) Update all vulnerable dependencies.

### Challenge 2.3 Hints

<details>
  <summary>Spoiler warning</summary>
  <br/>

1. You may follow [this documentation](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/configuring-dependabot-security-updates) for a guide to enabling security updates.
2. You may follow [this documentation](https://docs.github.com/en/code-security/dependabot/dependabot-alerts/configuring-dependabot-alerts#managing-dependabot-alerts-for-your-repository) for a guide to enabling security alerts.
3. You may follow [this documentation](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuring-dependabot-version-updates#example-dependabotyml-file) for a guide to enabling version updates and scheduled checks.

</details>

---

[< Back to Challenge 1](./challenge1.md) | [Go to Challenge 3 >](./challenge3.md)
