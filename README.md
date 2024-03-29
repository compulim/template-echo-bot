# template-echo-bot

This repo is for quickly set up an Azure bot with Node.js Web App. It will clone the [Bot Builder Samples](https://github.com/microsoft/BotBuilder-Samples/) and add GitHub Action to deploy your bot.

## Why this is needed?

[Bot Builder Samples](https://github.com/microsoft/BotBuilder-Samples/) repository contains great samples. But it is a mono-repository and need extra tweaks to deploy code using GitHub Actions.

Using GitHub Actions, you can easily modify your bot code and re-deploy automatically.

With this template repository, it will simplify deploying a bot from samples to your environment:

- No need to manual copying sample bot from its own folder to a new repository
- No need to write your own GitHub workflow for deploying to Azure Web App
- No need to patch the bot to support Azure Web App ZipDeploy
   - ZipDeploy is a super-fast deployment for Azure Web App, it only take 10 seconds to deploy a bot
   - No need to write your own `web.config` to support ZipDeploy

## Steps

1. Set up your Web App
   1. (Optional) Set the application settings `WEBSITE_RUN_FROM_PACKAGE=1` will speed up deployment significantly
   1. Download the publish profile
   1. Enable Web Socket by toggling Configruation > General settings > Web sockets
1. [Fork this repo via the "Use this template" button](https://github.com/compulim/template-echo-bot/generate)
1. [Add a new secret](../../settings/secrets/actions/new) named `PUBLISH_PROFILE`
   - Paste the content of the publish profile file you downloaded from step 1 into the value field
1. [Navigate to the scaffold workflow](../../actions/workflows/set-up-scaffold.yaml)
1. Click "Run workflow" to set up the scaffold
1. [Modify `bot.js` to trigger the first deployment](../../edit/main/bot.js)

## Application settings

In general, you should set the following environment variables in your Azure Web App > Configuration > Application Settings.

| Name | Value | Notes |
| - | - | - |
| `DIRECTLINE_EXTENSION_VERSION` | `latest` |
| `DirectLineExtensionKey` | | Azure Bot > Channels > Direct Line > App Service extension |
| `MicrosoftAppId` | | Azure Bot > Configuration > Microsoft App ID |
| `MicrosoftAppPassword` | | Azure Bot > Configuration > Microsoft App ID > Manage Password |
| `MicrosoftAppType` | `MultiTenant` | |
| `WEBSITE_NODE_DEFAULT_VERSION` | `~16` | TBD: Should bump to `~18` |
| `WEBSITE_RUN_FROM_PACKAGE` | `1` | Enable faster deployment |

### General

Please refer to [this article](https://learn.microsoft.com/en-us/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=multitenant%2Caadv2%2Cjavascript#bot-identity-information) on adding application settings to Azure Web App.

### Direct Line App Service Extension

Please refer to [this article](https://learn.microsoft.com/en-us/azure/bot-service/bot-service-channel-directline-extension-node-bot?view=azure-bot-service-4.0) on adding application settings to Azure Web App.

Also, add the following code, in additional to the code snippet in the article:

```ts
const { AuthenticationConstants } = require('botframework-connector');
```
