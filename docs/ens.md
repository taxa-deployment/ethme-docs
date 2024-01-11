---
title: ENS-DNS Redirection
date: 2024-01-05
slug: ens

---
## How ETH.me Retrieves Data from ENS

ETH.me functions akin to a reverse proxy for the ENS and IPFS protocols, enabling access via HTTPS through client-side browsers.

When a user sends an HTTPS request to `name.eth.me`, our wildcard DNS record `*.eth.me` captures the request. The server then informs the client's browser of the corresponding ENS names. Subsequently, the browser's web3.js accesses the default ENS resolver contract on the Ethereum mainnet. The frontend JavaScript then redirects the browser to the appropriate URL, following the redirection rules outlined in the "Redirection Rules" section. The interaction between user-end browser, ETH.me and Ethereum blockchain can be described by the picture below:

![interactions](ens-1.png)

## Redirection Rules

ETH.me can redirect a DNS request such as `name.eth.me` to any link specified in the ENS domain records of `name.eth`. This includes links to platforms like Twitter, GitHub, LinkedIn, and IPFS.

To determine the redirection target, the ENS domain owner should set a subfield named **`index`**. When a user requests a URL at `name.eth`, ETH.me, by default, searches for the `index` record. The value of the `index` field indicates another field. For instance, if set to `twitter`, ETH.me will redirect to the URL specified in the `twitter` field. You should set 2 ENS records to setup the twitter link redirection:

| Name         | Value               |
|:----------------|:-------------------------|
| index        | *twitter* |
| *twitter*    | https://twitter.com/TaxaNetwork |

If the `index` field value is unset, ETH.me will redirect based on the exact sequence in the "ENS Subfields Reference" table provided in the section below.

## ENS Subfields Reference

The following table outlines the various subfields recognized by ETH.me for redirection purposes:

| Name         | Comment               |
|:----------------|:-------------------------|
| index        | The primary field for redirection |
| contentHash  | URL of an IPFS resource |
| twitter      | Link to a Twitter profile |
| url          | Any arbitrary HTTPS URL |
| gitHub       | Link to a GitHub profile |
| discord      | Discord server or user link |
| opensea      | Link to an OpenSea profile or collection |
| telegram     | Telegram group or channel link |
| reddit       | Reddit profile or subreddit link |
| etherscan    | Link to an Etherscan page |

## Setting up IPFS URLs
Setting up a decentralized web3 website involves utilizing protocols like IPFS and ENS. Firstly we will need a static website or webpage to upload it to IPFS. There are several methods to upload files to IPFS, some of which are listed below.

### Using Pinning Service
An easy way to upload & pin your files to IPFS is to use a pinning service. The benefit of using pinning services is they run lots of IPFS nodes so you don't have to run your own IPFS node to make sure that your website is accessible.. 

1. Go to [Pinata.cloud](https://pinata.cloud/) and sign up or log in.

2. Once you are logged in, on Dashboard select `Upload` and click `Browse`.

3. Navigate to your website folder and click `Open`.

4. After that, click `Upload`.

5. Once uploaded you can see your folder/file pinned & listed on dashboard. You can copy the CID from your listed file and use it in IPFS format, like this `ipfs://`**`CID`**, `ipfs://`**`QmUFrzU2YfTgwhQaQ2RAZ2Pi2fAd75KwWSz6tYJT7yMFqv`**

### Using Fleek
Fleek is a service similar to Netlify, but for Web3 applications. Once you've pushed your changes to git, Fleek builds, pins, and updates your site on IPFS. 

1. Upload your website to Github.

2. Go to Fleek and sign in using your Github account.

3. Once logged in, click `Add new site` and select `IPFS` as Hosting service.

4. Click `Deploy site`.

5. Once the site is deployed, copy the CID from `Deploy Log` and prepend `ipfs://`.

More details on Fleek deployment can be found [here](https://docs.ipfs.tech/how-to/websites-on-ipfs/introducing-fleek/), in IPFS docs.

### Deploying your Own Node
If you want to run your own IPFS node you can,

1. Download & install the IPFS desktop from [IPFS desktop downloads page](https://github.com/ipfs/ipfs-desktop/releases).

2. Open IPFS desktop and go to the Files page.

3. Click `add file` and select your webpage.

4. Once added click the three dot menu on your file, and copy `CID`.

5. In order to keep the content long term you need to pin the files. Click three dot menu on your file, and click `Pin`.

More details on hosting file on your own node can be found [here](https://docs.ipfs.tech/how-to/websites-on-ipfs/single-page-website/#install-ipfs-desktop), in IPFS docs.

## Link ENS and IPFS
Once you have uploaded your website on IPFS, you can link it to your ENS Name by setting the contenthash record. This can be done using the ENS Manager.

1. Go to [ENS Manager App](https://app.ens.domains/).

2. Select your ENS name you want to link your IPFS to.

3. Navigate to the `Records` tab and click `Edit Records`.

4. Then go to `Other` tab, and in the Content hash field enter your IPFS link (like this, `ipfs://`**`QmUFrzU2YfTgwhQaQ2RAZ2Pi2fAd75KwWSz6tYJT7yMFqv`**).

5. Click save and confirm transaction.

A detailed step by step guide on IPFS Uploading and Linking IPFS with ENS Name can be found [here](https://docs.ipfs.tech/how-to/websites-on-ipfs/single-page-website/#install-ipfs-desktop), in ENS Domains article.
