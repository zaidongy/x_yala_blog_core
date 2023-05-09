# Description
This application is a "Base" or "Core" app to many [Blog](https://blog.yansalabs.com/) posts written by Yansa Labs.

# What's in it? 
It's a Artist, Album, Tracks and Playlist application, allowing data load from Spotify.com API.

- Table of Artists
- table of Albums
- Table of Tracks/Songs
- Table of Playlists
- M2M Table of Tracks <> Playlists

# How do I use it?
After you import this application into your ServiceNow instance (A Personal Developer Instance, is recommended). You will need to: 

- Signup for a Developer account on spotify.com (or if you have a normal spotify account, just login)
- Create an application in your developer.spotify.com account
- Setup an oAuth application registry in ServiceNow
- Create a Credential Record in ServiceNow for your oAuth application registry
- "Get an OAuth Token" from Spotify
- Initiate a data load.


## Install on your PDI from "Source Control"
The following steps will be a HIGH level guideline on how to install this application in your PDI via Source Control. 

[SN Doc on Import from Source Control](https://developer.servicenow.com/dev.do#!/learn/courses/tokyo/app_store_learnv2_devenvironment_tokyo_managing_the_development_environment/app_store_learnv2_devenvironment_tokyo_source_control/app_store_learnv2_devenvironment_tokyo_importing_an_application_from_source_control)

- it assumes you have basic understanding of "Git" and ServiceNow

1. In your PDI, open studio.
2. When prompted to select an application, choose "Import from Source Control"
3. Choose Http
4. Copy/Paste the HTTP Clone URL from GitLab
5. Credential: Leave empty
6. Branch: **It is imperative** you clear SN's default and use `master` branch
7. Import!

## Spotify Developer Account and Application

1. Go to [Spotify Developer Site](https://developer.spotify.com/)
2. Login Using your personal spotify account, or create a new one.
3. In the top right corner, click your name and select "Dashboard"
4. Select "Create App"
5. Enter fields as prompted (you can leave Website blank or just use your PDI URl for website)
  - **Note:** Your Redirect URL should be: https://YourInstanceName.service-now.com/oauth_redirect.do 
    - Be sure to replce the `YourInstanceName` with your actual PDI name
6. Click "Save"
7. This will take you to your app page
8. Click on "Settings" in the top right, we need to get your Client ID and Client Secret to enter in ServiceNow
9. On the setting page, take note of your client ID, and click the link to view your Client Secret. we will be copy/pasting these into ServiceNow shortly.

## Setup oAuth Application Registry in ServiceNow. 

1. Login to your PDI
2. Navigate to **System OAuth > Application Resgistry**
3. Click New
4. Select *Connect to a third party OAuth Provider*
5. Enter the following details:
  - **Name:** A name for you to remember it by
  - **Client ID:** The client ID from your spotify App Settings page
  - **Client Secret:** The Client Secret from your spotify app settings page
  - **Default Grant Type:** Authorization Code
  - **Authorization URL:** `https://accounts.spotify.com/authorize`
  - **Token URL:** `https://accounts.spotify.com/api/token`
6. Save the application Registry

## Create a Credential and get an oAuth token

1. Navigate to **Connection & Credentials > Credentials**
2. Click **New** 
3. Select `OAuth 2.0 Credentials`
4. Fill out:
  - **Name:** A name to remember it by
  - **OAuth Entity Profile:** Locat a profile that has the name of your App registry in it.
5. Save the record
6. Open the credential record you just created (if not still on the form)
7. In the related links you will see "Get OAuth Token", click this link.
8. It will pop-out a new window, and if setup correctly you will be asked to "Agree" or "Login" to your spotify account.
9. Login / Agree

## Initiate Data Load

1. In your PDI Navigate to **Yansa blog - CORE > Music Data Loaders > Create New**
2. Choose the type of data you wish to load, and click `Submit`
3. After a few moments, the state should automatically change to In Progress and albums will start loading (you can monitor on the Album Count)


## Toubleshooting

1. If the data load errors or has authentication errors, go to your Credential and "Get OAuth token" then come back and execute the data load again (It will resume where it left off more or less).


# Interacting with the app

- Review the application menu items, under the application menu: `Yansa Blog - CORE`
