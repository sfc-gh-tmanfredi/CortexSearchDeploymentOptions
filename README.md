# Cortex Search App - Deployment Options

This repo provides the tools for demonstrating deployment options for a UI that will allow a user to ask questions of documents.  These are depicted in the attached Powerpoint but can be summarized as: 

**Option1a**: Provider account develops a Streamlit app as a Native App.  The App is published as a listing on Snowflake Marketplace or via Private Share. The Provider also owns the document content and hosts a Cortex Search service that is also published to Marketplace or Private Share as a Cortex Knowledge Extension.  A Consumer account discovers and installs the Native App and the CKE.  Upon executing the App, the consumer can ask questions of the documents on residing on the provider account.  

**Option1b**: Like Option1a, but instead of a Native App,  the Consumer configures an Agent that is used by Snowflake Intelligence as the UI to achieve the same effect as Option1a. 

**Option2a**: Like Option1a, but the Consumer account is the owner of the document content. Consumer sets up the Cortex Search service which runs locally so there is no need for the CKE. 

**Option2b**: Like Option 1b, but instead of a Native App,  the Consumer configures an Agent that is used by Snowflake Intelligence as the UI to achieve the same effect as Option1b. 

**Prerequisites**:  You need 2 Snowflake accounts (enterprise edition or higher) to execute this demo effectively

Steps

# On the PROVIDER account (If Option 1), on CONSUMER account (if option 2)#
*** Execute each statement individually.  You will execute different GRANTs at the bottom depending on whether this is a provider or consumer accoutn
-	Execute the setup script FinDocSearch_SETUP

# Create Native App on Provider (Option 1a/2a) #
-	Project->App Packages
-	Click +App Packages
-	Name the package FinDocSearchNA_package
-	Select “Distribute to accounts in your organization”
-	Select Add
-	Click “Add First Version”
-	Select
    -	Version Name: V1
    -	Release Channels: Default
    -	Database with application files: 
      -	DB: FINDOCSEARCHDB
      -	Schema: STAGED_CONTENT
      -	Select Path: /
  -	Click Add
-	Click Done when the message “V1 Patch 0” appears

# On the provider account, create a listing and publish #
-	Click Data Products->Provider Studio
-	Click “Listings”
  - Select +Create Listing
  - Select “Specified Consumers”
  - Name the listing DocSearchNA_listing. Click “Save”
-	Click “Add Data Product”.  Select “FINDOCSEARCH_PACKAGE”
-	Click “Access Type”. Select Free
-	Under “Who can access”, select Add consumer accounts
-	  Add the consumer account in the form <organization>.<account name>. Click Save
-	Under Description, select “Describe your data product”
-	Under Legal Terms select “Add legal Terms”. Select “Terms of service will be provider offline” 
-	Click publish.  Listing should now be Live

# Install app on the consumer account #
- Click Data Products->Private Sharing OR Data Sharing->Private Sharing (depending on UI version)
- Locate listing “DocSearchNA_listing” and click “Get”
- Under Options, name the database FindDocSearchApp
- Application will install

# Run native app #
-	When install is complete, go to Data Products->Apps or Catalog-> apps (depending on UI version) 
-	Click DocSearchNA_listing
-	Here you can select a specific model (under advanced options) 
-	Now type in a question about your documents. You can make the prompt as simple or complex as you like

# Clean up #
- On Consumer Account
  - Data->Databases OR Catalog->Database Explorer, locate **FINDOCSEARCHAPP**
  - Click … Select Uninstall
  - Catalog->Database Explorer, locate **FINDOCSEARCHDB**
  - Click… Select Drop

- On Provider Account
  - Data->Databases OR Catalog->Database Explorer, locate **FINDOCSEARCHDB**
  - Click… Select Drop




