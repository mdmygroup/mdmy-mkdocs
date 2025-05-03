# GitHub and Shopify

***
## What is GitHub?

GitHub is a platform for version control and collaboration. It allows you and your team to work on projects from anywhere, while managing changes to code or content. Essentially, it helps track revisions and contributions, ensuring that updates can be made smoothly and with a record of who made which changes.

***
## Why Do We Need GitHub for Shopify Stores?

For Shopify stores, GitHub offers a systematic way to manage changes to the store’s theme and other configurable elements. It:
- **Ensures Consistency:** Keeps the store’s backend organized and consistent across different versions and developers.
- **Facilitates Collaboration:** Multiple team members can work on different aspects of the store simultaneously without overlapping or conflicting changes.
- **Tracks Changes:** Provides a clear history of what changes were made, who made them, and when they were made, which is crucial for debugging and understanding past decisions.

***
## Why Do We Need DEV - UAT - PROD Environments?

- **DEV (Development):** This is where all new features, updates, and fixes are initially made. It’s a testing ground for new ideas that you don’t want to expose to real users yet.
- **UAT (User Acceptance Testing):** After changes are made in DEV, they move to UAT where they are tested to ensure they meet user expectations and don’t introduce any new issues. This is crucial for quality control.
- **PROD (Production):** This is your live Shopify store that customers interact with. Changes moved to PROD are final and should be fully tested and ready for public use.

***
## What is a Pull Request?

A pull request (PR) is a method of submitting contributions back to a project. It allows team members to review and discuss changes before they are merged into a more stable environment. This is especially important in a multi-environment setup like ours, where we have separate stages for development, testing, and production.


### When to Open a PR from DEV to UAT

- **Feature Completion:** Open a PR when a feature or a significant bug fix in the DEV environment is complete. Ensure that the feature is working as expected and that any major bugs have been addressed.
- **End of a Sprint:** If you're working in sprints, a PR might be opened at the end of a sprint to move all completed work to the UAT for more rigorous testing.
- **Pre-Testing Phase:** Before any new or updated feature can be exposed to a broader testing audience or before performing user acceptance tests, it needs to be moved from DEV to UAT.

### When to Open a PR from UAT to PROD

- **Successful UAT:** Once the changes in UAT have been thoroughly tested and approved by testers or stakeholders, a PR should be opened to move these changes to PROD.
- **Release Schedule:** If your team follows a release schedule, changes might be accumulated in UAT and moved to PROD as part of a planned release.
- **Critical Fixes:** If a critical fix was tested in UAT and needs to be made available urgently to all users, a PR should be opened to quickly transition this fix to PROD.

By adhering to these guidelines, your team can maintain a smooth and reliable workflow from development through to production, ensuring that each feature is properly vetted and stable before being released to end users.

***
## How Do I Open a Pull-Request on GitHub to Promote My Work? (Step by Step)

1. **Make Changes in the DEV theme on Shopify:**
- Work on the Shopify DEV theme from the Shopify UI itself.

2. **Open a Pull Request:**
- Go to the repository page on GitHub (the store you are currently working on).
- You’ll see a "Pull Request" button. Click it.
- You’ll see a "New Pull Request" button. Click it.
- Select the Compare Branch (Source: i.e. `DEV` or `UAT`)
- Select the Base Branch (Target: i.e. `UAT` or `PROD`)
- You’ll see a "Create Pull Request" button. Click it.
- Add a title and description for your changes. Explain why and what you have changed.

3. **Review and Collaborate:**
- Invite team members to review your changes. They can leave comments, request further modifications, or approve the changes.
- Make any necessary updates based on feedback.

4. **Merge the Pull Request:**
- Once the pull request is approved, you or an authorized person can merge it into the target branch.
- This will include your changes in the next update cycle to the environment (e.g., `UAT` or `PROD`).

5. **Close the Pull Request:**
- After merging, close the pull request to keep the project clean and organized.

***
## Using GitHub for Creating Custom Shopify Demos for Leads

### Introduction to Creating Branches for Leads on GitHub

When we identify potential clients interested in updating their websites (on Shopify), we use GitHub to manage and demonstrate customized changes. This process begins by creating a unique branch for each lead, which allows us to tailor our approach without affecting our main templates.

#### Why Create a Specific Branch for Each Lead?

Creating a branch named `demo/{name_of_lead}` from the main branch ensures that each demo remains organized and isolated from our core templates. This practice:
- **Prevents conflicts:** Keeps main templates clean and free from experimental changes.
- **Improves tracking:** Allows us to monitor changes specific to each lead, making it easier to revert or adjust without disrupting other work.
- **Enhances presentation:** Enables personalized demonstrations that are tailored to the specific needs and preferences of each lead.

#### How to Create a Branch on GitHub

1. **Navigate to the MDMY-Demo-Store Repository:** Go to your GitHub repository where the Shopify templates are stored [mdmygroup-template-shopify-store](https://github.com/mdmy-mlepicier/mdmygroup-template-shopify-store).
2. **Switch to the Main Branch:** Ensure you are on the main branch (often called `main` or `master`).
3. **Create a New Branch:**
   - Click on the branch selector menu at the top of the file list.
   - Type `demo/{name_of_lead}` in the textbox that appears.
   - Click “Create branch `demo/{name_of_lead}` from `main`” from the drop-down menu.
3. **Alternative: Create a New Branch:**
   - Click on the **"X branches"`** button [(here)](https://github.com/mdmy-mlepicier/mdmygroup-template-shopify-store/branches) right of the branch selector menu at the top of the file list.
   - Click the **"New Branch"** green button on the top right.
   - Type `demo/{name_of_lead}` in the textbox that appears.
   - Make sure the **Source** is selected to be `main`
   - Click the “Create new branch” green button.

### Integrating a GitHub Branch with Shopify

Once the branch is created, the next step is to connect this branch to our Shopify store to show real-time changes to our leads.

#### How to Connect a GitHub Branch to Shopify

1. **Log into Shopify Admin Panel:** Go to your Shopify store’s admin panel.
2. **Access Theme Management:** Navigate to ‘Online Store’ and then ‘Themes’.
3. **Connect to GitHub:**
   - On the theme editor page, click on the **"Add theme"** button
   - Look for an option or a button that says ‘Connect to GitHub’.
   - Select the repository `mdmygroup-template-shopify-store` 
   - Select the specific branch `demo/{name_of_lead}` you just created.
   - Click "Connect"
   - Within a couple of seconds you will see the theme corresponding to the template you want to modify for the lead.
   - Click ‘Customize’.

#### What Does This Integration Do?

Connecting a GitHub branch to Shopify allows you to:
- **Preview Changes:** See how modifications in the GitHub branch will look in a live Shopify environment, tailored specifically for the lead.
- **Isolate Changes:** Ensure that changes made in the `demo/{name_of_lead}` branch do not affect other branches or the main production environment.
- **Tailor Experiences:** Make adjustments based on the feedback directly in the branch, providing a customized experience that can significantly enhance client engagement and satisfaction.

### Conclusion

This setup allows us to make client-specific changes on Shopify using GitHub branches without affecting the overall project. Each lead receives a personalized demonstration that showcases exactly how their Shopify store could look and function, helping them make informed decisions about partnering with us for their website needs.

By following this process, we maintain high standards of organization and efficiency, ensuring that each demo is both impactful and aligned with the lead’s specific requirements.


***