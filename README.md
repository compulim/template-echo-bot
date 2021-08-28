# template-echo-bot

This repo is for quickly set up a Node.js Web App Bot. It will clone the [Bot Builder Samples](https://github.com/microsoft/BotBuilder-Samples/) and add GitHub Action to deploy your bot.

## Steps

1. Set up your Web App Bot
   1. (Optional) Set the application settings `WEBSITE_RUN_FROM_PACKAGE=1` will speed up deployment significantly
   1. Download the publish profile
1. [Fork this repo via the "Use this template" button](https://github.com/compulim/template-echo-bot/generate)
1. [Add a new secret](../../settings/secrets/actions/new) named `PUBLISH_PROFILE`
   - Copy and paste the content of the publish profile file you downloaded from step 1
1. [Navigate to the scaffold workflow](../../actions/workflows/set-up-scaffold.yaml)
1. Click "Run workflow" to set up the scaffold
