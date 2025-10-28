---
description: >-
  Starting September 9th, 2025, Bitbucket will disable the use of app passwords
  for authentication.
---

# Migration from App Passwords to API Tokens

This change is part of Atlassian’s ongoing effort to strengthen account security by phasing out weaker authentication methods and moving to **API tokens**, which offer finer-grained access controls and better security practices.\
\
**Important:** No changes are taking effect immediately, and existing integrations using app passwords will continue to function without interruption. However, this change is time-sensitive, with a 12-month transition period. Integrations with app passwords will stop working entirely on June 9, 2026.

## **Impact on Existing sync Providers**

If you already have a Bitbucket sync provider connected with an app password, it will continue to work after September 9th.\
However, users will be unable to add new Bitbucket sync providers using App passwords. We highly recommend migrating from app passwords to API tokens.\
Read more [here](https://support.atlassian.com/bitbucket-cloud/docs/api-token-permissions/) for scopes on API tokens.

## Migration steps

* Open the sync provider settings, go to your list of configured sync providers
* Find the bitbucket sync provider using App passwords(we will highlight that in red for your view, along with the warning, _'App Password migration required'_)

<figure><img src="../../../.gitbook/assets/Screenshot 2025-09-04 at 2.06.21 PM.png" alt="" width="375"><figcaption></figcaption></figure>

* Click on Migrate to API Tokens
* Your form will open with all existing details, except app passwords

<figure><img src="../../../.gitbook/assets/Screenshot 2025-09-04 at 2.07.02 PM.png" alt="" width="375"><figcaption></figcaption></figure>

* Add an API Token generated from Atlassian
* Replace user name with user email
* Click on save to complete the migration of your existing sync from App passwords to API tokens
* Repeat the above steps for any other existing Bitbucket syncs with App passwords\
  \
