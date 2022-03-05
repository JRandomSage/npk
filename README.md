# NPK - Increase your cred yield!

NPK is a distributed hash-cracking platform built entirely of serverless components in AWS including Cognito, DynamoDB, and S3. It was designed for easy deployment and the intuitive UI brings high-power hash-cracking to everyone.

![Image](/readme-content/dashboard-active.png)

'NPK' is an initialism for the three primary atomic elements in fertilizer (Nitrogen, Phosphorus, and Potassium). Add it to your hashes to increase your cred yield!

## How it works

Let's face it - even the beastliest cracking rig spends a lot of time at idle. You sink a ton of money up front on hardware, then have the electricity bill to deal with. NPK lets you leverage extremely powerful hash cracking with the 'pay-as-you-go' benefits of AWS. For example, you can crank out as much as 1.2TH/s of NTLM for a mere $14.70/hr. NPK was also designed to fit easily within the free tier while you're not using it! Without the free tier, it'll still cost less than $2 per MONTH to have online!

## Features

### 1. Super easy install

Paste a one-liner into AWS CloudShell. Done.

![cloudshell](https://user-images.githubusercontent.com/143415/156900982-9430a21f-8b87-4aa5-bbf7-10aacc4c7c0c.png)

### 2. Intuitive campaign builder

Take the trial-and-error out of complex attack types with the intuitive campaign builder. With a couple clicks you can create advanced campaigns that even advanced Hashcat users would struggle to emulate.

![gpu_families](https://user-images.githubusercontent.com/143415/156901010-a6ae07e8-273b-496c-8916-b0d8955d840f.png)

### 3. Campaign price and coverage estimates

Take the guess-work out of your campaigns. See how far you'll get and how much it will cost *before* starting the campaign.

![coverage](https://user-images.githubusercontent.com/143415/156901016-a63b2ea1-fcf0-4a48-99c5-a1c6ab2e3221.png)

### 4. Max price enforcement and runaway instance protection

GPU instances are expensive. Runaway GPU instances are EXTREMELY expensive. NPK will enforce a maximum campaign price limit, and was designed to prevent runaway instances even with a complete failure of the management plane.

### 5. Multi-Tenancy & SAML-based single sign-on

NPK supports multiple users, with strict separation of data, campaigns, and results between each user. It can optionally integrate with SAML-based federated identity providers to enable large teams to use NPK with minimal effort.

![Image](/readme-content/userManagement.png)

### 6. Data lifecycle management

Configure how long data will stay in NPK with configurable lifecycle durations during installation. Hashfiles and results are automatically removed after this much time to keep things nicely cleaned up.

## Easy Install

**ProTip:** To keep things clean and distinct from other things you may have in AWS, it's STRONGLY recommended that you deploy NPK in a fresh account. You can create a new account easily from the 'Organizations' console in AWS. **By 'STRONGLY recommended', I mean 'seriously don't install this next to other stuff'.**

1. Log into the AWS Console for the account you want to deploy to.
2. Click the AWS CloudShell button in the top right corner.
![cloudshell_icon](https://user-images.githubusercontent.com/143415/156901055-5107d4b2-c5b4-4ca5-8454-57e7504e2316.png)

3. Paste in the one-liner: `curl https://npkproject.io/cloudshell_install.sh | bash`
4. Use the wizard to complete the configuration
5. (Optional) If you said 'no' at the end of the wizard, run `npm run deploy -- -ys`

## Advanced Install

If you want to add advanced features like Georestrictions, SAML auth, or custom data lifecycles, follow the simple install, then modify the settings file at `/home/cloudshell-user/npk/npk-settings.json`. It's recommended that you keep a copy of your settings file, but it's not a big deal if you lose it - just re-run the easy install.

* `campaign_data_ttl`: This is the number of seconds that uploaded files and cracked hashes will last before they are automatically deleted. **Defaults to `86400` or 7 days**.
* `campaign_max_price`: The maximum number of dollars allowed to be spent on a single campaign.**Defaults to `50`**.
* `georestrictions`: An array of https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 country codes that access should be ALLOWED. Traffic originating from other countries will not be permitted. Remove the entry entirely if you don't wish to use it. **Defaults to `[]`**.
* `sAMLMetadataFile` or `sAMLMetadataUrl`: Only one can be configured. Leave them out entirely if you're not using SAML.

See https://github.com/c6fc/npk/wiki/Detailed-NPK-Settings for more details about advanced configurations, or https://github.com/c6fc/npk/wiki/Configuring-SAML-SSO for help configuring SAML SSO.

## Modify Install

You can change the settings of an install without losing your existing campaigns. Edit `npk-settings.json` as necessary, then rerun `npm run deploy`. It's that easy!

```sh
~/npk$ vim npk-settings.json
~/npk$ npm run deploy
```

If it's been a while and your CloudShell has timed out (and you don't have an npk-settings.json file anymore), just run the installer again and provide the same answers. The deploy will re-attach to your existing environment easily.

## Uploading your own dictionaries and rule files

Once NPK has been deployed, administrative users can use the NPK console to upload wordlists and rule files using the 'Dictionary Management' link in the sidebar. NPK supports plain-text and gzipped dictionaries.

![upload_dictionaries](https://user-images.githubusercontent.com/143415/156901465-6e906177-e9fa-4189-8cda-0735813d02c0.png)

## Uninstall

You can completely turn down NPK and delete all of its data from AWS using the built-in Terraform binary:

```sh
~/npk$ cd render-npk
~/npk/render-npk$ npx terraform destroy
```

If you don't have a `render-npx` directory, run `npm run deploy -- -y` first to create it.

# Official Discord Channel

Have questions, need help, want to contribute or brag about a win? Come hang out on Discord!

[![Porchetta Industries](https://discordapp.com/api/guilds/736724457258745996/widget.png?style=banner3)](https://discord.gg/k5PQnqSNDF)