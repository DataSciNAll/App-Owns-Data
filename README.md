# App Owns Data samples

## Objective of this Project

The purpose of this repository is to showcase code on how to integrate Power BI Embed application with Azure 
Analysis Services.  CUSTOMDATA() is a function in AAS that controls Row Level Security.  The Power BI Embed
App needs to pass a parameter into CUSTOMDATA when generating the Power BI Embed token.  This example reuses the
App Owns Data project from Microsoft and adds the following;

1. CUSTOMDATA field in Embed Report UI to pass in a single parameter
2. Setup of Service Principal when using Effective Identity

Read this documentation to prepare your environment
https://docs.microsoft.com/en-us/power-bi/developer/embedding-content

## Choose Auth Method

In web.config:

- For authentication with master user credential choose MasterUser as AuthenticationType.

- For authentication with app secret choose ServicePrincipal as AuthenticationType (Preview).

More details here: https://docs.microsoft.com/en-us/power-bi/developer/embed-service-principal

To embed reports, dashboards and tiles, the following details must be specified within web.config:

| Detail            | Description                                                                                           |
|-------------------|-------------------------------------------------------------------------------------------------------|
| applicationId     | Id of the AAD application registered as a NATIVE app.                                                 |
| workspaceId       | The group or workspace Id in Power BI containing the reports, dashboards and tiles you want to embed. |
| pbiUsername       | A Power BI username (e.g. Email). The user must be an admin of the group above. (For Master User Only)|
| pbiPassword       | The password of the Power BI user above. (For Master User Only)                                       |
| applicationSecret | Seecret Key of the AAD application registered as a NATIVE app. (For Service Principal Only)           |
| tenant            | Tenant Id of the Apllication   . (For Service Principal Only)                                         |
| spobjectid        | Service Principal Object ID.  User ID to submit to Embed Token                                        |
| sprole            | Generic role to submit for effective Identity                                                         |

## Modifications to EmbedService.cs

Comment Line 105 or Line 106 to pass into Embed Token CUSTOMDATA.  Line 106 for Live Connections and Line 105 for everything else

Comment Line 121 & Line 122 or Line 124 to enable Service Principal. LIne 121 & Line 122 for CUSTOMDATA + SP and Line 124 for all else


## Important

For security reasons, in a real application, the user and password and app secret should not be saved in web.config. Instead, consider securing credentials with an application such as KeyVault.
