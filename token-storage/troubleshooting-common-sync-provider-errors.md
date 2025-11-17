# Troubleshooting - Common Sync Provider Errors

### What can I do if I’m having issues syncing with Github, Gitlab or Azure Devops

<details>

<summary>Error syncing with Provider, check details:</summary>

It’s likely that your existing provider's PAT's status has expired and, if necessary, generate a new one to connect the plugin to your repo.

#### 1. Verify Your Current PAT Status

You need to check the status of the PAT you provided to the Tokens Studio plugin.

* **Step 1:** Navigate to GitHub PAT Settings.
  * Go to your GitHub Profile
  * Settings
  * Developer Settings
  * Personal access tokens
  * Tokens (classic).
* **Step 2:** Check Expiration Date.
  * Find the token you created for the Tokens Studio plugin.
  * Check its Expiration date or Status. If it has expired or been revoked due to inactivity, it is no longer usable.

#### 2. Generate a New Personal Access Token (PAT)

If your token is expired or invalid, you must generate a new one.

* **Step 1:** Create New Token.
  * On the GitHub PAT page, click "Generate new token" $\rightarrow$ "Generate new token (classic)."
* **Step 2:** Set Expiration.
  * Give the new token a descriptive name (e.g., "Tokens Studio Figma Plugin").
  * Set a new Expiration Date. For security, it's best practice to use a shorter lifespan, but ensure it's long enough for your workflow (e.g., 90 days or 1 year).
* **Step 3:** Define Scopes (Permissions).
  * You must select the correct permissions. For full sync functionality (read/write), select the repo scope.
* **Step 4:** Copy the Token.
  * After creation, GitHub will display the new token string only once. Copy it immediately and save it in a secure location.

#### 3. Update the Plugin Credentials

The final step is to replace the old, expired token with the new one in the plugin.

* **Step 1:** Open Plugin Sync Settings.
  * In the Tokens Studio plugin, go to the "Sync" tab and select the GitHub provider.
* **Step 2:** Enter the New PAT.
  * Paste the newly generated PAT into the "Personal Access Token" field.
* **Step 3:** Connect.
  * Click "Connect" or "Save Credentials."

The plugin should now connect successfully, and you can resume pushing/pulling changes.\


</details>

<details>

<summary>Invalid File Path/Token Storage Location</summary>

If you are receiving an error when trying to push updates, especially when your settings worked previously, it might be due to an unexpected character or path format in the Token Storage Location field.

#### 1. Identify the File Path Issue

The error in the conversation was caused by an unnecessary leading forward slash (/) in the file path field.

* **Step 1:** Check Your File Path.
  * Navigate to the settings tab in the Tokens Studio plugin.
  * Review the Token Storage Location field (sometimes labeled "File Path").

#### 2. Correct the File Path Formatting

The path must be relative to the root of your repository and should not begin with a forward slash (/).

* **Incorrect Path (Causes Error):** /Themes
* **Correct Path:** Themes (if the file is in a top-level folder named 'Themes')
* **Correct Path (for file in root):** tokens.json (if the file is directly in the root)
* **Correct Path (for nested file):** tokens/core/colors.json

After making the correction, try pushing your changes again.

* **Step 1:** Remove Leading Slash.
  * If your path starts with a /, remove the leading slash from the Token Storage Location field.
* **Step 2:** Save Credentials.
  * Save your updated sync credentials.
* **Step 3:** Push Changes.
  * Attempt to Push your updates to your repository again.

</details>

<details>

<summary>Buttons Grayed Out (Read-Only Mode)</summary>

If some of the buttons/functions in the plugin are disabled, it indicates that the plugin believes it only has read access to the token file or the repository. This is usually a permission issue imposed by the repository owner/admin.

#### 1. Verify Your User Permissions on the Repository

Even if you are a Pro user and your PAT is correctly configured, your user account itself must have explicit write permissions set by the repository administrator.

* **Step 1:** Check Your Role.
  * Contact the administrator of the repository (GitHub, GitLab, or Azure DevOps) where your tokens are stored.
  * Confirm that your user account has a role that grants Write access to the repository (e.g., Collaborator, Developer, or Maintainer).
* **Step 2:** Check Branch Protection Rules (If Applicable).
  * If you can write to other branches but not main, the admin may have set up Branch Protection Rules that restrict who can push to that specific branch. The resolution for this is to use a[ feature branch workflow](https://www.google.com/search?q=%233-resolve-by-using-a-feature-branch-recommended-workflow-for-branch-protection-rules), which requires a PR/Merge Request to update main.

#### 2. Double-Check Your Personal Access Token (PAT) Scopes

While less likely if you recently set up the PAT, it's worth a quick check to ensure the token didn't lose its permissions.

* **Step 1:** Review Scopes.
  * Go to your Git provider's PAT settings (e.g., GitHub Personal Access Tokens).
  * Verify that the PAT you used for the plugin still has the required write permission scope selected (e.g., repo for GitHub, api for GitLab, or Code (Read & Write) for Azure DevOps).
* **Step 2:** Re-enter/Generate Token.
  * If the scopes are correct, try re-entering the existing PAT in the plugin's sync settings and reconnecting. If the issue persists, generate a new PAT with the correct scopes and update the plugin.

</details>

<details>

<summary>Contents Don't Pass Schema Validation</summary>

This error usually indicates that there's an issue with the structure or content of the JSON token file(s) stored in your Git repository. The plugin cannot load the tokens because the file does not adhere to the required JSON format and schema.

#### 1. Identify and Correct JSON Syntax Errors

The first step is always to fix any syntax errors in your token file(s).

* **Step 1:** Access the File.
  * Find the exact token file(s) (e.g., tokens.json, colors.json) that are failing validation.
  * Open the file directly in your Git provider's online editor or, preferably, in a dedicated code editor like VS Code.
* **Step 2:** Check for Basic Errors.
  * Look for common JSON mistakes: missing commas between key-value pairs, mismatched curly braces ({ }), or square brackets (\[ ]).
  * Ensure the file is not completely empty. At a minimum, it must contain an empty JSON object: JSON `{}`
  * Use the code editor's built-in syntax checker or an online JSON validator to pinpoint the error location.

#### 2. Validate the Tokens Studio Schema

If the file is valid JSON but still fails, its internal structure might not comply with the Tokens Studio schema.

* **Step 1:** Check Token Nesting.
  * All tokens must be placed inside a set or group object. For example, your tokens can't be at the root level of the file; they must be nested:\
    JSON

```
{
  "global": {
    "color": {
      "primary": {
        "value": "#007AFF",
        "type": "color"
      }
    }
  }
}
```

* Ensure the value and type keys are present and correctly formatted for each token.
* **Step 2:** Remove Invalid Content.
  * If you manually edited the file, ensure no comments or extraneous characters were accidentally added outside of the valid JSON structure.

#### 3. Save and Pull the Fixed File

Once the JSON is corrected, you must update your repository and pull the fix into the plugin.

* **Step 1:** Commit the Fix.
  * Commit and push the corrected token file(s) to your Git repository.
* **Step 2:** Pull in the Plugin.
  * In the Tokens Studio plugin, go to the "Sync" settings and perform a "Pull" action to load the valid file from your repository.

The plugin should now successfully load the tokens, allowing you to save and push changes without the schema validation error.

</details>

<details>

<summary>Pushing to a Protected Main Branch</summary>

### **Understand Why the Plugin is Pushing Changes**

When you export tokens as variables, the plugin updates the `$themes.json` file in your repository to include the necessary Figma Variable IDs. This step is crucial for the plugin to correctly fetch and apply the tokens alongside the variables later on. This update constitutes a required change that needs to be committed and pushed to your repo.

#### 1. Check PAT Permissions

* Ensure your Personal Access Token (PAT) has the Code scope with `Read & Write` permissions.

#### 2. Review Branch Protection Rules

If the PAT is correct, the push is likely being blocked by a repository policy:

* **Step 1:** In your repository settings, check the Branch Policies applied to your main (or default) branch.
* **Step 2:** If you have policies like "Require a minimum number of reviewers" or "Limit merge types" enabled, direct pushes to that branch are blocked—even for the plugin.

#### &#x20;3. Implement Feature Branch Workflow

The required action is to push the changes to a temporary branch and then merge it into main via a Pull Request (PR).

* **Step 1:** Switch Branch
  * In the Tokens Studio plugin's "Sync" settings, switch the current branch to a new branch off of main (e.g., feature/variable-export-update).
* **Step 2**: Export and Push
  * Export your tokens as variables to Figma.
  * Push the changes when prompted. The `$themes.json` update will be committed to the new branch.
* **Step 3:** Create Pull Request
  * Go to your provider.
  * Create a Pull Request (PR) to merge your new branch (feature/variable-export-update) into your main branch. This process satisfies the main branch protection rules.

</details>
