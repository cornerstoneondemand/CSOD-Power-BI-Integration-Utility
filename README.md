# CSOD-Power-BI-Integration-Utility
This utility helps you formulate your Query String to paste into the Power BI Desktop formula bar.

**Microsoft Power BI** helps you stay up to date with the information that matters to you.  With Power BI, **_dashboards_** help you keep a finger on the pulse of your business. Your dashboards display **_tiles_** that you can click to explore further with **_reports_**. Connect to multiple **_datasets_** to bring all of the relevant data together in one place.

_Need help understanding the building blocks that make up Power BI?  See [Power BI - Basic Concepts](http://support.powerbi.com/knowledgebase/articles/487029-power-bi-preview-basic-concepts)._

### How to integrate Power BI with the Edge API

This tutorial will show you how to connect Power BI to your Cornerstone portal as a data source using Edge APIs and **Basic 2-Factor Authentication**.

**Note:** This integration currently only supports Basic 2-Factor Authentication.  Signature based authentication cannot be used at this time.

**Prerequisite:** _Power BI Desktop_ application and familiarity using it.

#### Create your API key

1. Login to the portal that you want to integrate with Microsoft Power BI Desktop using the same user credentials that you plan to use for API authentication.  

2. Navigate to the **Edge API** navigation tab.  

3. Click on **ApiManagement**.  

4. Click on the **Create Api** button.  

5. Enter a name for your API.  Leave the **Signature Needed** and **Enforce TTL **_unchecked_. Click **Save**.  

6. You should be back at the _Api List_.  Find the API that you just created. Click on the down arrow in the top-right corner for the API you just created and select **View Sessions**.  

7. Click on **Create Session**.  

8. Enter a name for your session.  Click **Save**.  

9. You should now see the Session Token you just created it.  Make note of the token, you will need it in a future step.  

#### Construct your Query String

1. Formulate your OData URL for the data you wish to pull from your Cornerstone portal, you will need this in the next step.  The URL consists of a concatenation of: 
    - **Service Root URL** (ex.- '_http://&lt;your-portal&gt;/services/_') 
    - **Resource Path** (ex.- '_dwdata/User?_') 
    - **Query Options** (ex.- '_$select=UserEmail,UserDivision,UserFirstName,UserLastName,UserLastAccess,UserID,UserPosition,UserManagerID_')  

2. Open the **Cornerstone Edge - Power BI Utility** HTML page in your web browser.  

3. Fill out the four required fields: _Username_, _Password_, _Session Token_, and _OData URL_, and click **Generate**.  

    - Enter the Cornerstone **username** and **password** for the same user that you created the session token with in earlier steps.
    - Enter the session token that you created in earlier steps.
    - Enter the OData URL that you formulated in earlier steps.  

4. Select the output _Query String_ in the **Result** text box and copy it to your clipboard.  

#### Setup Query in Power BI Desktop

1. Open _Microsoft Power BI Desktop_.  

2. Navigate to **Get Data** &gt; **Blank Query** which will open the _Query Editor_.  

3. Paste the _Query String_ into the Power BI **Formula Bar**.  

4. Enter a **Name** for your query.  

5. After entering a query name, you should see a warning message asking you to "_Please specify how to connect._". Click on **Edit Credentials**.  

6. On the _Access an OData feed_ popup, select **Anonymous**, select the **first radio button** with the root of your URL, and click **Connect**.  

7. Power BI will then connect to your data source and retrieve the desired data.  
  
8. Click **Close & Apply**.  

9. _Power BI Desktop_ is now setup to retrieve data from your Cornerstone portal. 

#### Setup Query in Power Query (Optional)

Instead of _Power BI Desktop_, you also have the option to use _Power Query for Excel_.  Follow the steps below to setup your query string in Power Query, assuming you already have it installed.

1. Open _Excel_.

2. Navigate to **Power Query** &gt; **From Other Sources** &gt; **Blank Query** which will open the _Query Editor_.

3. Paste the _Query String_ into the Power Query **Formula Bar**.

4. Enter a **Name** for your query.

5. After entering a query name, you should see a warning message asking you to "_Please specify how to connect._". Click on **Edit Credentials**.

6. On the _Access an OData feed_ popup, select **Anonymous**, select the **first radio button** with the root of your URL, and click **Connect**.

7. Power Query will then connect to your data source and retrieve the desired data.

8. Click **Close & Load**.

9. _Power Query for Excel_ is now setup to retrieve data from your Cornerstone portal.

#### Troubleshooting Tips

1. **sessionToken** in the URL is case sensitive.

2. Make sure the API and sessionToken are active and enabled via the Edge API page.

3. If you get the error: "_Expression.Error: The 'Authorization' header is only supported when connecting anonymously. These headers can be used with all authentication types: Accept, Accept-Charset, Accept-Language, Cache-Control, If-Modified-Since, Referer_" this means the OData authentication type is not set to _Anonymous_. To modify the setting, navigate to File &gt; Options and settings &gt; Data source settings. Find your data source URL from the list, click **Edit**, edit the credential type to be _Anonymous_, and click **Done**.  Try again.
