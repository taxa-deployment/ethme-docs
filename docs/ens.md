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

To determine the redirection target, the ENS domain owner must set a subfield named `index`. When a user requests a URL at `name.eth`, ETH.me, by default, searches for the `index` record. The value of the `index` field indicates another field. For instance, if set to `twitter`, ETH.me will redirect to the URL specified in the `twitter` field.

If the `index` field value is unset, ETH.me will redirect based on the sequence in the "ENS Subfields Reference" table provided below.

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
