# Setting Up Shopify Development Workflow with GitHub Integration
#
***

## Overview
This document provides a step-by-step guide to set up a structured development workflow for your Shopify store using Shopify UI, GitHub, VS Code, and GitHub Actions for deployment. The workflow includes a development environment, a staging environment with password access, and the production environment (live website).

### Prerequisites
- Shopify account with admin access
- GitHub account
- VS Code or another code editor with Git support
- Basic knowledge of Git and GitHub

### Create a GitHub Repository
- Go to GitHub and create a new repository.
- Name the repository appropriately (e.g., `facemira-shopify`).
- Initialize it with a README for documentation purposes.
#
***

## Step 1: Connecting Shopify to GitHub

*Next, connect your Shopify store to the GitHub repository to sync your theme.*

### Connect to GitHub
- In your Shopify Admin, go to **Online Store > Themes**.
- Click **Add theme > Connect from GitHub**.
- Authorize Shopify to access your GitHub account and select your repository.
- Connect to the `main` branch.
#
***

## Step 2: Set Up GitHub Repository
1. Clone the repository to your local machine using VS Code or Git commands.
    ```bash
    git clone https://github.com/yourusername/your-repo.git
    ```

### Setting Up Branches for Different Environments

*We will create branches in GitHub to represent different environments.*

**Create Branches in GitHub:**
- Create three branches in your GitHub repository: `dev`, `uat`, and `main`.
  - `dev` is for daily development work.
  - `uat` is for UAT and will be deployed to a staging theme in Shopify.
  - `main` represents your live environment.
#
***

## Step 3: Set Up Shopify CLI and Theme Development
*Use VS Code and Shopify CLI for local development.*

### Prerequisites: Install Ruby
*Before installing the Shopify CLI, ensure that Ruby is installed on your machine.*

- **Check if Ruby is installed:**
    - Open a terminal or command prompt.
    - Type `ruby -v` and press Enter.
    - If Ruby is installed, you should see the version number. If not, proceed with the installation steps below.
- **Install Ruby:**
    - For Windows:
        - Download and install Ruby using RubyInstaller available at [RubyInstaller for Windows](https://rubyinstaller.org/).
        - Follow the installation prompts, and ensure you select the option to add Ruby to your PATH.
    - For macOS:
        - Ruby comes pre-installed on macOS. However, you might want to use a version manager like `rbenv` or `rvm` to manage different Ruby versions.
        - To install Ruby using `rbenv`, use the following commands in your terminal:
            ```
            brew install rbenv
            rbenv init
            rbenv install 2.7.0
            rbenv global 2.7.0
            ```
    - For Linux (Ubuntu/Debian):
        - Use the package manager to install Ruby. For example, in Ubuntu, you can install Ruby using the following commands:
            ```
            sudo apt update
            sudo apt install ruby-full
            ```
- **Verify Ruby Installation:**
    - Open a terminal or command prompt.
    - Run `ruby -v` to check the installed Ruby version. You should see the Ruby version number displayed.

*Now that Ruby is installed, you can proceed with installing the Shopify CLI as outlined in the next steps.*

### Prerequisites: Install Node.js
*Ensure Node.js is installed on your machine as prerequisites for Shopify CLI.*

1. **Install Node.js:**
   - Visit [Node.js official website](https://nodejs.org/) and download the latest stable version.
   - Run the downloaded file and follow the installation prompts to install Node.js and npm (Node package manager).
   - To verify the installation, open a terminal or command prompt and run:
     ```bash
     node -v
     npm -v
     ```
   - This will display the Node.js and npm version numbers, confirming they are correctly installed.

### Install Shopify CLI 3.x
*Use Node.js to install the latest version of Shopify CLI.*

1. **Install Shopify CLI using npm:**
    - With Node.js installed, open your terminal or command prompt.
    - Run the following command to install Shopify CLI 3.x:
      ```bash
      npm install -g @shopify/cli @shopify/theme
      ```
    - This command installs Shopify CLI globally on your machine using npm.
2. **Verify Shopify CLI Installation:**
    - Once the installation is complete, you can verify it by running:
      ```bash
      shopify version
      ```
    - This command should return the version number of Shopify CLI, indicating that it is successfully installed.
3. **Log in to your Shopify account:**
    - Run the following command to log in to your Shopify account and connect your local environment to your Shopify store:
      ```bash
      [OUTDATED] - shopify auth login
      ```
    - Follow the prompts in your web browser to complete the login process.
4. **Initialize a new theme or pull an existing one:**
    - To start working on a new Shopify theme, use:
      ```bash
      shopify theme init
      ```
    - To work on an existing theme from your Shopify store, use:
      ```bash
      shopify theme pull eac56e-c0.myshopify.com
      ```
    - Choose the theme you want to work on from the list provided in the terminal.

Now you have Node.js and Shopify CLI 3.x installed, and you're ready to start developing with Shopify.

#
***

## Step 4: Development Workflow
*Work on the `dev` branch and push changes to GitHub.*
1. Make changes to your Shopify theme files locally in VS Code.
3. Use Git to commit changes to your GitHub repository. Use descriptive commit messages.
   ```bash
   git add .
   git commit -m "Description of changes"
   git push origin main
    ```
4. Create separate branches for feature development or bug fixes as needed.
5. Push changes to the current `dev` branch on GitHub.

### Implement Branch Protection Rules

1. **Protect `UAT` and `main` branches on GitHub:**
   - Go to your GitHub repository.
   - Navigate to **Settings > Branches**.
   - Click on **Add rule** to create a new branch protection rule.
   - Enter `UAT` in the branch name pattern field to apply the rule to the UAT branch.
   - Repeat the process for the `main` branch.
   - Select the following options for both branches:
     - **Require pull request reviews before merging:** This ensures that changes can only be made via pull requests that are reviewed and approved.
     - **Require status checks to pass before merging:** (optional) This ensures that any configured tests or checks pass before changes can be merged.
     - **Include administrators:** This applies the same rules to administrators to ensure no direct pushes can be made.
2. **Enforce Pull Requests:**
   - With these protections in place, changes to the `UAT` and `main` branches can only be made through pull requests.
   - Developers will make changes in the `DEV` branch, then submit a pull request to merge into `UAT` for testing.
   - Once changes in `UAT` are approved, a pull request can then be made from `UAT` to `main` for final deployment.

### Using Git Hooks for Workflow Enforcement

Git hooks are scripts that run automatically before or after certain Git actions, such as commit, push, or receive. They can enforce rules and automate workflows. To prevent direct pushes to the `UAT` and `main` branches, you can use a `pre-push` hook.

**Setting Up a `pre-push` Git Hook:**

1. **Navigate to the Git Hooks Directory:**
   - Go to the `.git/hooks` directory in your local repository.
   - This directory contains sample scripts for various hooks, typically suffixed with `.sample`.
2. **Create the `pre-push` Hook:**
   - Create a new file named `pre-push` in the `.git/hooks` directory, without any extension.
   - Ensure the file is executable. On Unix-like systems, use `chmod +x pre-push`.
3. **Script the `pre-push` Hook:**
   - Edit the `pre-push` file to include a script that checks the current branch and rejects the push if it's `UAT` or `main`. Here’s a simple script for this purpose:
    ```bash
    #!/bin/sh

    # Get the current branch name
    current_branch=$(git branch --show-current)

    # Check if the current branch is either UAT or main
    if [ "$current_branch" = "UAT" ] || [ "$current_branch" = "main" ]; then
        echo "Direct pushes to $current_branch are not allowed. Please use pull requests."
        exit 1
    fi

    exit 0
    ```
4. **Test the Hook:**
   - Attempt to push changes directly to the `UAT` or `main` branch.
   - The hook should prevent the push and display a message instructing to use pull requests.

#### How It Works:

- The `pre-push` hook script runs before the push action is completed.
- It checks the current branch name; if it's `UAT` or `main`, the script exits with status 1, aborting the push.
- If the branch is neither `UAT` nor `main`, the script exits with status 0, allowing the push to proceed.

#### Limitations and Considerations:

- Git hooks are local to the repository and need to be set up by each developer in their local environment.
- They can be bypassed if a developer intentionally removes or modifies the script.
- For more robust enforcement, consider using server-side hooks or continuous integration checks, if supported by your platform.

Using a `pre-push` Git hook helps enforce the workflow policy of not pushing directly to `uat` and `main` branches, ensuring changes go through the proper review process via pull requests.

#
***

## Step 5: Local Development and Testing with Shopify CLI
*Develop and test your Shopify theme locally using Shopify CLI.*

1. **Start the local development server:**
    - After you've pulled your theme using Shopify CLI, navigate to your theme's directory in the terminal.
    - Run the following command to start a local development server:
      ```bash
      shopify theme dev
      ```
    - This command will build your theme and start a local server. You will be provided with a local URL (e.g., `http://127.0.0.1:9292`) and a preview URL which is a live link to your Shopify store with the changes you're making locally.
2. **View and test your theme locally:**
    - Open the local URL in your web browser to see your theme in action. This local environment allows you to see changes in real-time as you develop.
    - Use the preview URL to view how your theme looks on your actual Shopify store. This is particularly useful for testing how changes look and function in a live-like environment without affecting the actual live site.
3. **Make and test changes:**
    - As you modify your theme files in VS Code, save your changes and refresh the browser window where your local or preview URL is open to see the updates.
    - Test all changes thoroughly in both the local and preview environments to ensure functionality and responsiveness across different devices and browsers.
4. **Use Theme Check:**
    - Shopify CLI comes with Theme Check, a tool that helps you identify errors and enforce Shopify theme best practices.
    - Run `shopify theme check` in your terminal to analyze your theme code. It will provide feedback and suggestions for improvements.
    ```bash
    shopify theme check
    ```
5. **Push changes to GitHub:**
    - Once you're satisfied with the changes and they have been tested locally, commit your changes to your Git repository and push them to the corresponding branch (usually `dev` or `feature` branches) for further actions like pull requests and code reviews.

*Testing locally with Shopify CLI ensures that you can develop and refine your theme with immediate feedback and robust testing, leading to a more reliable and polished final product for your Shopify store.*

#
***

## Step 6: Publish UAT Branch to Staging Theme and Preview
*Deploy the UAT branch to a separate staging environment accessible via UAT's Theme Preview Link.*

1. **Create a Staging Theme in Shopify:**
    - Go to your Shopify Admin and navigate to **Online Store > Themes**.
    - Duplicate your live theme to create a staging theme or upload a theme that connects to your `uat` branch.
    - Rename this theme to something identifiable as staging, e.g., "[UAT] - Facemira".
2. **Connect the Staging Theme to the UAT Branch:**
    - In the Shopify Admin for the staging theme, use the GitHub integration to connect the `uat` branch.
    - This ensures that changes pushed to the `uat` branch are reflected in this staging theme.

### Use Shopify Theme Previews for UAT

1. **Maintain separate themes for DEV and UAT:**
   - In Shopify, have separate themes for DEV and UAT that are connected to their respective branches in GitHub.
   - Regularly update these themes by pulling the latest changes from their connected branches.
2. **Generate Preview Links:**
   - In the Shopify Admin, go to **Online Store > Themes**.
   - Next to the UAT theme, click on **Actions > Preview** to open the theme preview.
   - Share this preview link with your team for UAT testing. The link is accessible without affecting the live site.
3. **Protect Access:**
   - While Shopify doesn’t provide password protection for specific themes, ensure that access to the preview links is restricted to authorized personnel only.

*By following these steps, you will have a separate staging environment for your `uat` branch, allowing you to test and validate changes thoroughly before they are pushed to the live environment on `facemira.com`.*

#
***

## Step 7: Implementing GitHub Actions for CI/CD

*Set up GitHub Actions to automate the deployment process from staging to production.*

### GitHub Actions Setup
- Create a `.github/workflows` directory in your repository.
- Add a YAML file for your CI/CD pipeline (e.g., `shopify-deploy.yml`).

    ```yaml
    name: Deploy to Shopify
    
    on:
      push:
        branches:
          - staging
    
    jobs:
      build:
        runs-on: ubuntu-latest
    
        steps:
        - uses: actions/checkout@v2
    
        - name: Setup Node.js
          uses: actions/setup-node@v2
          with:
            node-version: '14'
    
        - name: Install Shopify CLI
          run: npm install -g shopify-cli
    
        - name: Deploy to Shopify Staging
          run: |
            shopify login --store your-staging-store.myshopify.com --password $secrets.SHOPIFY_PASSWORD
            shopify theme push --nodelete --unpublished
    ```
    
### Automated Testing

*Automated testing verifies that your code functions correctly before deployment. For Shopify theme development, this includes testing Liquid templates, JavaScript, CSS, and integrations.*

**Unit Testing**
*Unit tests assess individual parts of the code. For JavaScript testing, tools like Jest or Mocha are commonly used.*
- **Example of a Jest Test for JavaScript:**
    - Perform unit testing of JavaScript functions using Jest. Below is an example of how to write a simple test case.
    ```javascript
        // Function to test
    function add(a, b) {
        return a + b;
    }
    
    // Jest test case
    test('adds 1 + 2 to equal 3', () => {
        expect(add(1, 2)).toBe(3);
    });
    ```

### Visual Regression Testing

*Visual regression testing tools like Percy or BackstopJS help detect unintended visual changes by comparing screenshots over time.*

- **Setting Up BackstopJS:**
    - Follow the steps below to set up BackstopJS for visual regression testing in your project.
        ```bash
        # Install BackstopJS
        npm install -g backstopjs
        
        # Initialize BackstopJS in your project
        backstop init
        
        # Generate reference screenshots
        backstop reference
        
        # Run tests to compare against the reference
        backstop test
        ```

### Cross-Device and Cross-Browser Compatibility Testing

*Testing your website across multiple devices and browsers ensures compatibility and consistent user experience. Tools like BrowserStack or LambdaTest can automate this process.*

- **Integrating BrowserStack with GitHub Actions:**
    - Automate cross-browser and cross-device testing by integrating BrowserStack with GitHub Actions. See the example workflow configuration below.
        ```YAML
        name: BrowserStack Test

        on: push
        
        jobs:
          browserstack:
            runs-on: ubuntu-latest
        
            steps:
            - uses: actions/checkout@v2
        
            - name: Run BrowserStack Test
              run: |
                # Command to trigger BrowserStack test
                curl -u "YOUR_BROWSERSTACK_USERNAME:YOUR_BROWSERSTACK_ACCESS_KEY" \
                -X POST "https://api.browserstack.com/automate/builds.json" \
                -d '{"desiredCapabilities": {"browser": "Chrome", "browser_version": "latest", "os": "Windows", "os_version": "10"}}'
        ```

### Performance Testing

*Regular performance testing is crucial to ensure that your Shopify store is optimized for speed and user experience. Tools like Lighthouse or WebPageTest can automate performance testing and provide actionable insights.*

- **Setting Up Lighthouse for Performance Testing:**
    - Lighthouse is an open-source, automated tool for improving the quality of web pages. It can be run against any web page, public or requiring authentication, to audit performance, accessibility, and more.
        ```bash
        # Run Lighthouse performance audit from the command line
        lighthouse https://your-shopify-store-url.com --view
        
        # Run Lighthouse in headless mode and output the results to a file
        lighthouse https://your-shopify-store-url.com --output json --output-path ./your-report.json
        ```

### Security Scans

*Security scanning is essential to detect vulnerabilities and ensure that your Shopify store is safe for users. Tools like Snyk or OWASP ZAP can be integrated into your CI/CD pipeline to automatically check for security issues.*

- **Integrating Snyk for Security Scanning:**
    - Snyk is a tool that finds and fixes vulnerabilities in your dependencies. It can be integrated into your GitHub repository to automatically scan for security issues each time code is pushed.
        ```bash
        # Install Snyk CLI
        npm install -g snyk
        
        # Authenticate with your Snyk account
        snyk auth
        
        # Test your project for vulnerabilities
        snyk test
        ```
        
### Deployment Strategies

*Implementing reliable deployment strategies like blue-green deployment or canary releases can significantly reduce the risk of errors during updates and ensure smooth transitions between versions.*

- **Blue-Green Deployment**
    - In blue-green deployment, two identical environments are maintained: one is the live production environment (Blue), and the other is the staging or pre-production environment (Green). At any time, only one of these environments is live, with the other serving as a staging area for testing new releases.
- **Canary Releases**
    - Canary releases involve rolling out changes to a small subset of users before a full rollout. This strategy allows monitoring the impact of the new changes on system performance and user experience in a controlled way.
- **Implementing Canary Releases in Shopify:**
    - Shopify doesn't have built-in support for canary releases, but you can simulate this process to gradually introduce changes and assess their impact before a full rollout.
    - **Strategy 1: Segmenting Your Audience**
        - Use customer tags to segment your audience in Shopify. For example, you can tag a small percentage of users as 'Canary' and selectively roll out changes to them.
        - You can then customize the experience for these tagged users, perhaps by using alternate templates or special promotions that are only visible to them.
    - **Strategy 2: Using Feature Flags**
        - Implement feature flags in your Shopify theme code. Feature flags allow you to enable or disable features without deploying new code.
        - You can manage these flags through your theme settings or externally via a third-party service. This way, you can turn on new features for a controlled group of users.
            ```javascript
            if settings.enable_new_feature
              <!-- New feature code here -->
            else
              <!-- Existing feature code here -->
            endif
            ```
    - **Strategy 3: A/B Testing Tools**
        - Utilize A/B testing tools that integrate with Shopify, such as Google Optimize, to selectively roll out new features or changes to a portion of your traffic.
        - These tools allow you to show different versions of your store to different segments of visitors, effectively simulating a canary release.

### Monitoring and Feedback

Continuous monitoring of your Shopify store's performance, user interactions, and feedback is crucial for maintaining a high-quality user experience and facilitating ongoing improvements.

- **Setting Up Monitoring Tools**
    - Tools like Google Analytics, Hotjar, or Shopify's built-in analytics can provide comprehensive insights into user behavior, site performance, and overall user experience.
- **Implementing User Feedback Loops**
    - Establishing mechanisms for collecting user feedback directly on your site can be invaluable. Tools like UserVoice or Qualaroo help gather and analyze user feedback, enabling data-driven decision-making for future developments.
- **Example of Setting Up Google Analytics:**
    - Integrate Google Analytics with your Shopify store to track user behavior and e-commerce metrics.
        1. Create a Google Analytics account if you don't have one.
        2. In Shopify Admin, go to `Online Store` > `Preferences`.
        3. Enter your Google Analytics tracking code in the Google Analytics account field.


#
***

## Step 8: Managing Deployment to Production

*Finally, merge changes from `staging` to `main` for live deployment.*

#### Production Deployment
- After UAT, merge `uat` branch into `main` through a pull request on GitHub.

### Manually Updating the Live Theme in Shopify Admin

*To manually update the live theme in Shopify Admin by pulling changes from the `main` branch, follow these steps:*

1. **Merge Changes to Main Branch:**
   - Ensure that all changes in the `uat` branch are tested and approved.
   - Create a pull request from the `uat` branch to the `main` branch in GitHub.
   - Review the pull request, ensure everything is in order, and then merge it. Now, the `main` branch will have the latest approved changes.
2. **Pull Changes in Shopify Admin:**
   - Go to the Shopify Admin panel and navigate to **Online Store > Themes**.
   - Locate your live theme, which should be connected to the `main` branch of your GitHub repository.
   - You should see an option to **Update from GitHub** or similar (this option appears if there are new changes in the connected GitHub branch that have not been pulled into Shopify).
   - Click on this option to pull the latest changes from the `main` branch into your live Shopify theme.
3. **Review and Publish:**
   - Before the changes go live, Shopify usually allows you to preview them. Take this opportunity to do a final check to ensure everything looks and functions as expected.
   - Once satisfied with the preview, confirm the update to publish the changes on your live site.

### Important Notes

- **Backup First:** Always ensure you have a recent backup of your live theme before pulling and applying changes. This provides a fallback option in case anything goes wrong.
- **Monitor After Updates:** After updating the live theme, monitor the website closely for any issues. Check the functionality, loading times, and user experience to ensure that the update has not adversely affected the site performance.
- **Communicate with the Team:** Ensure that all team members are aware of the update schedule to avoid conflicts or simultaneous updates. Communication is key in a collaborative environment, especially when dealing with live environment updates.

#
***

## Step 9: Best Practices for Theme Customization and Deployment

1. **Designated Theme for Customizations:**
   - Only customize the theme named "[DEV] - Store". This is our development environment where all initial changes and testing should take place.
2. **Use of UAT for Previews:**
   - The UAT environment is strictly for previewing and testing the changes made in the DEV environment. Do not make direct changes in UAT.
3. **Code Promotion Through Pull Requests (PRs):**
   - Promote changes from DEV to UAT and from UAT to PROD only through pull requests, ensuring a controlled and reviewed process.
4. **Regular Review and Testing:**
   - Thoroughly review and test changes in the DEV environment before merging them to UAT. This ensures stability and quality in our deployments.
5. **Scheduled Updates to PROD:**
   - Communicate and schedule updates from UAT to PROD in advance, allowing all stakeholders to prepare and verify changes.
6. **Documentation and Change Logs:**
   - Keep detailed records of changes, including the rationale and approvals, to maintain transparency and accountability in the development process.
7. **Training and Compliance:**
   - Regularly train stakeholders on these processes and monitor adherence to ensure the integrity and stability of our online presence.

# 
#

***
#
***

