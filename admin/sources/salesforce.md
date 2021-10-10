# Salesforce Integration

The Savannah CRM Integration for Salesforce provides a two-way communication and data sharing between the two systems. Because of that, adding a Source of this type is more involved than other sources, and requires three separate steps: Installing a package in your Salesforce org, connecting your Savannah Source to Salesforce, and finally connecting your Salesforce org to Savannah.

![source_instructions.png](/images/sources/sfdc/source_instructions.png)

## Install Savannah CRM App in Salesforce

By clicking the "Install" button in Step 1 of the instructions, you will be redirected to a Salesforce page where you will be prompted to approve the installation of the Savannah CRM Integration package. **You must be a Salesforce Admin in your organization to do this part.**

![sfdc_approve.png](/images/sources/sfdc/sfdc_approve.png)

> Don't worry about the message saying the app is not authorized. As explained in the FAQs below, this is due to Salesforce's partner policies and not any deficiency in the Savannah CRM Integration package.

Be sure to select `Intall for All Users` to make it available to your staff.

I takes a few minutes to isntall, but you will be promoted when it is done.

![sfdc_installed.png](/images/sources/sfdc/sfdc_installed.png)

## Connect Savannah CRM to Salesforce

The next step looks a lot like adding other sources. After Clicking the "Connect" button in Step 2 f the instructions you will be asked by Salesforce to approve giving Savannah CRM access. This enables Savannah CRM to retrieve data from Salesforce.

![sfdc_auth.png](/images/sources/sfdc/sfdc_auth.png)

![savannah_added.png](/images/sources/sfdc/savannah_added.png)

## Connect Salesforce to Savannah CRM

The last step is to give Salesforce access to retrieve data from Savannah CRM. Salesforce does this through Named Credential, which provide a connection from your Salesforce pages back to Savannah.

After you completed Step 2 above you will be given an API key for your new Salesforce Source.

![savannah_apikey.png](/images/sources/sfdc/savannah_apikey.png)

Click on the (?) link next to the API key to be redirected to your Salesforce Named Credential page. From there open the `Savannah CRM API` credential and save your API key as the password, leaving everything else the same.

![sfdc_namedcredential.png](/images/sources/sfdc/sfdc_namedcredential.png)

![sfdc_namedcredential_form.png](/images/sources/sfdc/sfdc_namedcredential_form.png)

## Add Savannah CRM data to Salesforce pages

You have now connected Savannah with Salesforce! But in order for you to see community data, you first have to add the Savannah CRM Integration components to your pages. The integration package provides two components: `savannahMemberInfo` and `savannahCompanyInfo`, which you will need to add to your Contact and Account pages respectively.

To add these components, navigate to the page for a Contact or Account in Salesfore, and click the "Edit Page" from the gear menu.

![sfdc_page_edit.png](/images/sources/sfdc/sfdc_page_edit.png)

From the edit page, drag and drop the appropriate component onto where you want it to appear on your page.

![sfdc_company_component_add.gif](/images/sources/sfdc/sfdc_company_component_add.gif)


> You may be asked to activate the page, and whether or not to make it the org default. It's recommended that you make it the org default.

![sfdc_page_edit_default.png](/images/sources/sfdc/sfdc_page_edit_default.png)

## Data available in Salesforce

You will now start to see Savannah Company information show up on your Account pages

![sfdc_comany_overview.png](/images/sources/sfdc/sfdc_comany_overview.png)
![sfdc_company_members.png](/images/sources/sfdc/sfdc_company_members.png)
![sfdc_company_notes.png](/images/sources/sfdc/sfdc_company_notes.png)

And Savannah Member information show up on your Contact pages

![sfdc_member_profile.png](/images/sources/sfdc/sfdc_member_profile.png)
![sfdc_member_identities.png](/images/sources/sfdc/sfdc_member_identities.png)
![sfdc_member_connectiions.png](/images/sources/sfdc/sfdc_member_connectiions.png)
![sfdc_member_notes.png](/images/sources/sfdc/sfdc_member_notes.png)

## Data available in Savannah CRM

Additionally, you will see when a connection exists to a Salesforce record on your Savannah Member and Company pages.

![savannah_member_identities.png](/images/sources/sfdc/savannah_member_identities.png)
![savannah_company_profile.png](/images/sources/sfdc/savannah_company_profile.png)

## Frequently asked questions

1. **Why do I have to install your app in Salesforce?**
   
   Salesforce allows for the distribution of custom components to enhance your Salesforce experience through application packages.
   The Savannah CRM Integration package provides components for displaying data collected from your community directly in the Salesforce interface.

2. **Why isn't your app authorized by Salesforce?**
   
   In order for an application package to be authorized by Salesforce the developing company must sign up to be a Salesforce partner and pay a significant amount of money for a review of their application. As Savannah Software is still a small startup company, this is not an option for us as this time. But Savannah's source code is all open source and can be reviewed by anybody.

3. **I don't want sales people getting contact information for all my community members (and vice-versa)!**
   
   The Savannah CRM Integration is designed to balance the needs of community managers and sales professionals alike. Because of that, it will **ONLY** share information about a person if there is already a record for that person in both systems. That means a Salesforce Contact record must have already been created through some other means before it will be enhanced with information from Savannah CRM (and vice-versa).

4. **What information from Salesforce is shared with Savannah?**
   
   If a Savannah CRM Member record matches a Salesforce Contact record, Savannah will import a link to that Contact and the Account record (if any) associated with it.

5. **What information from Savannah is shared with Salesforce?**
   
   If a Salesforce Contact record matches a Savannah CRM Member record, Salesforce will display the date range of their activity (but not the content of the activity), any Tags assigned to them, their Engagement Level in various projects, their account name on other sources, their top and recent contacts, and any notes assigned to that Member.

   Additionally, if a Salesforce Account record matches a Savannah CRM Company record, Salesforce will display the date range of member activity (but not the content of the activity), the top Tags from member conversations, a list of Member names and their Engagement Level in the community, and any notes assigned to members of the Company.
   