# Plutonication

> This document will be part of the terms and conditions of your agreement and therefore needs to contain all the required information about the project. Don't remove any of the mandatory parts presented in bold letters or as headlines (except for the title)! Lines starting with a `>` (such as this one) should be removed. Please use markdown instead of HTML (e.g. `![](image.png)` instead of `<img>`). 
>
> See the [Grants Program Process](https://github.com/w3f/Grants-Program/#pencil-process) on how to submit a proposal.
- **Team Name:** Plutonication
- **Payment Address:** 1WmPE1X9Ykpb7QcVamPtUSRjEZy2GMDeTm5N72DyXYiqMCo (USDT)
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2

> :exclamation: *The combination of your GitHub account submitting the application and the payment address above will be your unique identifier during the program. Please keep them safe.*
## Project Overview :page_facing_up:

### Overview

Please provide the following:

- If the name of your project is not descriptive, a tag line (one sentence summary).

Communications protocol that enables seamless interactions between dApps and wallets across all platforms.

- A brief description of your project.

Plutonication allows users to connect PlutoWallet to other dApps seamlessly on any platforms, accross multiple codebases.
DApp just generates a QR code and once it is scanned in the wallet, they will pair and the wallet will be able to receive transaction requests from the dApp. It works on the same principle as WalletConnect protocol.

You can see a short (90 sec) demo here: https://youtu.be/hw2B8-sBc9A?si=O8MiWa0Wq1jxfZdr

- An indication of how your project relates to / integrates into Substrate / Polkadot / Kusama.

Currently, the only way to connect your mobile wallet to other dApps is to use Wallet connect protocol, or a very clunky Polkadot Vault (Parity signer).

We think, we will be good competitors to WalletConnect and that we will do will better than them!

Our Plutonication Extension already works with most of the web dApps as supposed to WalletConnect, which is implemented into only a handful of dApps.

WalletConnect is also only available in javascript and we would like to expand it further to other programming languages.

C# is a very popular programming language for games and there have not been much focus on it in the Polkadot Ecosystem appart from Ajuna Network and their excellent Substrate.NetApi. We are dirrectly communicating with Ajuna developers to help better coordinate the Substrate.NetApi development and Plutonication, so that their are dirrectly compatible with each other.

- An indication of why your team is interested in creating this project.

We have been very pationate about Plutonication since the beginning. We have noticed the lack of WalletConnect protocol before it was available.

We have been working on Plutonication in our free time to prove the concepts are possible.

We have also landed a second place at Polkadot Global Series: Europe edition 2023 hackathon in Web3 and Tooling category.

### Project Details

We expect the teams to already have a solid idea about your project's expected final state. Therefore, we ask the teams to submit (where relevant):

- Data models / API specifications of the core functionality

Native Plutonication:

```mermaid
flowchart LR

subgraph Cloud
S[Plutonication Websocket Server]
end

subgraph Any device
D[dApp using Plutonication]
end

subgraph Phone
W["Mobile wallet
    Private key always stays here"]
end

S -- Receive signed payload --> D
D -- Send extrinsic payload --> S

S -- Receive extrinsic payload --> W
W -- Send signed payload --> S

D -. Scan QR code for establishing connection .-> W;
```

Plutonication on existing polkadot.js apps: 
```mermaid
flowchart LR

subgraph Cloud
S[Plutonication Websocket Server]
end

subgraph Web
D[dApp using Polkadot.js] ~~~ E[Plutonication Extension]
E -. Connection via Polkadot.js extension .- D
end

subgraph Phone
W["Mobile wallet
    Private key always stays here"]
end

S -- Receive signed payload --> E
E -- Send extrinsic payload --> S

S -- Receive extrinsic payload --> W
W -- Send signed payload --> S

E -. Scan QR code for establishing connection .-> W;
```

- An overview of the technology stack to be used

1) Plutonication server (Python): Flask, Flask-SocketIO
2) Mobile Wallet: https://github.com/rostislavLitovkin/plutowallet
3) Plutonication Native (C#): SocketIOClient, Substrate.NetApi
4) Plutonication Native (TS): socket.io-client, Polkadot.js
5) Plutonication Extension: socket.io-client, Polkadot.js extension

- Documentation of core components, protocols, architecture, etc. to be deployed

### Plutonication Server
- Used for reliable establishing of connection.
- Passes payloads between Wallets and dApps.

### Mobile Wallet
- Has access to the private key
- signs the payloads and sends them back to the dApp.
- Never exposes the private key

### dApp
- needs to have access to either: Plutonication Native / Plutonication Extension

### Plutonication Native
- A simple package that allows the dApp get connected with the Mobile Wallet.
- Connects the dApp with the Plutonication server.
- Helps to generate a QR code for the Wallet to establish the connection.

### Plutonication Extension
- a polkadot.js extension that works with any existing dApp that supports polkadot.js extension.
- Connects the dApp with the Plutonication server.
- Generate a QR code for the Wallet to establish the connection.

- PoC/MVP or other relevant prior work or research on the topic
    - Second place at Polkadot Global Series: Europe edition 2023 hackathon in Web3 and Tooling category.
    - https://github.com/cisar2218/Plutonication
    - Plutonication is integrated to: https://github.com/rostislavLitovkin/plutowallet
    - https://github.com/rostislavLitovkin/plutonicationextension

- What your project is _not_ or will _not_ provide or implement

Any improvements to PlutoWallet appart from the things needed for Plutonication to work in the PlutoWallet.

Although it is planned support Kotlin and Swift programming languages as well, it is not part of this grant proposal.

We are certainly willing to make PRs to other popular dApps to utilise Plutonication, it is also not part of this grant proposal. We would be willing to do a follow-up grant or get a treasury funding to make the PRs.

### Ecosystem Fit

Help us locate your project in the Polkadot/Substrate/Kusama landscape and what problems it tries to solve by answering each of these questions:

- Where and how does your project fit into the ecosystem?

Our project is comparable to WalletConnect, which was also our inspiration.
When we started making our first prototypes in February, WalletConnect was not available in the Polkadot Ecosystem yet.
Even thought they have taken a lot of time and had a lot more experience then us, they were unable to make quick and elegant deliveries.
WalletConnect still is not supported by most of the dApps. We think we can do better. Actually, we already did.

We made a Plutonication Extension, which already allows you to interact with existing dApps, even though they have not implemented the Plutonication standard directly. This can be a perfect middle ground during the transition of popularizing the Plutonication. Even if the user wanted to use a new niche dApp, they can do so with Plutonication.

Wallet connect is also only supported in javascript. We want to make Plutonication available in more languages, including a very popular C# language, which is mostly used for game development. We will make web3 gaming possible on game consoles, thanks to the Plutonication.

- Who is your target audience (parachain/dapp/wallet/UI developers, designers, your own user base, some dapp's userbase, yourself)?

dApps developers - To integrate the Plutonication in their dApps. We will ensure that the developers will receive a good documentation.

Wallet developers - We are welcoming other wallets to use the Plutonication. We would like to help them make this possible.

Users - In the end, it will be mainly used by mobile focused users. They will be able to interact with web3 apps on unusual platforms, like game consoles, smartwatches ...

- What need(s) does your project meet?

You are unable securely interact with dApps on gaming consoles, smartwatches and other unusual platforms. Without Plutonication, you would have to expose your private key, which is very unsafe.

You can also interact with existing web dApps with your mobile wallet. Again, you do not need to expose your private key to multiple places (in this case browser extension wallet), which would be very unsafe.

- Are there any other projects similar to yours in the Substrate / Polkadot / Kusama ecosystem?

    Yes, WalletConnect

  - If so, how is your project different?

    We support more programming languages. We also have a browser extension that enables Plutonication on existing dApps.

    WalletConnect also mainly focuses on Ethereum ecosystem. We are focusing only on Polkadot.
    
    

## Team :busts_in_silhouette:

### Team members

- Name of team leader: 

Dušan Jánsky

- Names of team members:

Rostislav Litovkin

### Contact

- **Contact Name:** Dušan Jánsky
- **Contact Email:** cisar2218@gmail.com
- **Website:** https://github.com/cisar2218/Plutonication

### Legal Structure

- **Registered Address:** None
- **Registered Legal Entity:** None

### Team's experience

Please describe the team's relevant experience. If your project involves development work, we would appreciate it if you singled out a few interesting projects or contributions made by team members in the past. 

#### Dušan Jánsky
- Alumnus at Polkadot Blockchain Academy 2023 in Berkeley
- Student at Faculty of Electrical Engineering Czech Technical University in Prague - Opens Informatics (specialization in computer games and computer graphics)
- Fullstack developer at [Universal Scientific Technologies](https://www.ust.cz/)
- Polkadot Global Series 2023 (Europe) - second place

#### [Rostislav Litovkin](http://rostislavlitovkin.pythonanywhere.com/aboutme)
- Alumnus at Polkadot Blockchain Academy 2023 in Berkeley
- Experienced .net MAUI developer, e.g.:
   - [Galaxy Logic Game](https://github.com/RostislavLitovkin/galaxylogicgamemaui) (successful game for watches and mobiles, 50k+ downloads)
- Frontend developer at [Calamar explorer](https://calamar.app/)
- Successful student at Polkadot DevCamp #2
- Successful student at [Solana Summer School](https://ackeeblockchain.com/school-of-solana)
- Polkadot Global Series 2023 (Europe) - second place
- Audience choice prize at EthPrague 2023

If anyone on your team has applied for a grant at the Web3 Foundation previously, please list the name of the project and legal entity here.

Rostislav Litovkin helped with **Calamar.app - TopMonks s.r.o**

### Team Code Repos

- https://github.com/ThunderFly-aerospace/thumby
- https://github.com/topmonks/calamar
- https://github.com/RostislavLitovkin/GalaxyLogicGameMAUI
- https://github.com/RostislavLitovkin/Uniquery.Net

Please also provide the GitHub accounts of all team members. If they contain no activity, references to projects hosted elsewhere or live are also fine.

- https://github.com/cisar2218
- https://github.com/rostislavlitovkin

### Team LinkedIn Profiles (if available)

- https://www.linkedin.com/in/dusan-jansky-6aab69239/
- btw Rosta hates LinkedIn :D

## Development Status :open_book:

If you've already started implementing your project or it is part of a larger repository, please provide a link and a description of the code here. In any case, please provide some documentation on the research and other work you have conducted before applying. This could be:

The idea was already tested by WalletConnect. Now, we are expanding it further in the Polkadot ecosystem.

We have already made working MVPs which can be found here:

https://github.com/cisar2218/Plutonication

https://github.com/rostislavLitovkin/plutowallet

https://github.com/rostislavLitovkin/plutonicationextension

## Development Roadmap :nut_and_bolt:

This section should break the development roadmap down into milestones and deliverables. To assist you in defining it, we have created a document with examples for some grant categories [here](../docs/Support%20Docs/grant_guidelines_per_category.md). Since these will be part of the agreement, it helps to describe _the functionality we should expect in as much detail as possible_, plus how we can verify and test that functionality. Whenever milestones are delivered, we refer to this document to ensure that everything has been delivered as expected.

Below we provide an **example roadmap**. In the descriptions, it should be clear how your project is related to Substrate, Kusama or Polkadot. We _recommend_ that teams structure their roadmap as 1 milestone ≈ 1 month.

> :exclamation: If any of your deliverables is based on somebody else's work, make sure you work and publish _under the terms of the license_ of the respective project and that you **highlight this fact in your milestone documentation** and in the source code if applicable! **Projects that submit other people's work without proper attribution will be immediately terminated.**

### Overview

- **Total Estimated Duration:** Duration of the whole project (e.g. 2 months)
- **Full-Time Equivalent (FTE):**  Average number of full-time employees working on the project throughout its duration (see [Wikipedia](https://en.wikipedia.org/wiki/Full-time_equivalent), e.g. 2 FTE)
- **Total Costs:** Requested amount in USD for the whole project (e.g. 12,000 USD). Note that the acceptance criteria and additional benefits vary depending on the [level](../README.md#level_slider-levels) of funding requested. This and the costs for each milestone need to be provided in USD; if the grant is paid out in Bitcoin, the amount will be calculated according to the exchange rate at the time of payment.

### Milestone 1 Plutonication Server (Python: Flask)

- **Estimated Duration:** 1 month
- **FTE:**  0.33
- **Costs:** 5,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | MIT |
| **0b.** | Documentation | We will provide both **in code documentation for individual methods**. We will also provide a tutorial on how to run the Plutonication Server locally and in cloud. |
| **0c.** | Testing and Testing Guide | All of the functions will be end-to-end tested with a sample dApp written in typescript (with Plutonication and Polkadot.js api) and a sample Wallet (PlutoWallet) |
| **0d.** | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone and for running the server in production. |
| 1. | PlutonicationServerFlask | A Python server with Flask and Flask-SocketIO used for establishing a stable websocket connection between the dApp and Wallet. |
| 1a. | create_room | dApp creates room |
| 1b. | pubkey  | Sends an account address (SS58 encoded) from wallet to dApp |
| 1c. | sign_payload | dApp requests an extrinsic payload signature |
| 1d. | sign_raw | dApp requests a raw message signature |
| 1e. | payload_signature | wallet provides an extrinsic payload signature |
| 1f. | raw_signature | wallet provides a raw message signature |

### Milestone 2 Plutonication C# version

- **Estimated duration:** 1 month
- **FTE:**  0.5
- **Costs:** 7500 USD

> :exclamation: **The default deliverables 0a-0d below are mandatory for all milestones**, and deliverable 0e at least for the last one. 

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | MIT |
| **0b.** | Documentation | We will provide both **in code documentation for individual methods** and a **tutorial** explaining how to integrate Plutonication into a c# dApp. |
| **0c.** | Testing and Testing Guide | All of the functions will be end-to-end tested with a sample dApp written in c# (with Plutonication and Substrate.NetApi) and a sample Wallet (PlutoWallet) |
| **0d.** | Docker | We will provide a Dockerfile for a sample dApp that can be used to test all the functionality delivered with this milestone. |
| 1. | PlutonicationDAppClient | This would be a series of methods tailored for use with dApps. We will make sure that it is compatible with Substrate.NetApi |
| 1a. | Initialize(..) | Method used for initializing the PlutonicationDAppClient |
| 1b. | ReceiveAddress(..) | Handles the receiving of SS58 encoded address |
| 1c. | SendPayloadAsync(..) | Method used for requesting an extrinsic payload sign |
| 1d. | SendRawAsync(..) | Method used for requesting a raw message sign |
| 2. | PlutonicationWalletClient | This would be a series of methods tailored for use with wallets. |
| 2a. | SendAddress(..) | Sends the SS58 encoded address of the account in the wallet |
| 2b. | SendSignedPayloadAsync(..) | Method used for sending a signed extrinsic payload back to the dApp. The signed extrinsic payload will then be added to the extrinsic and submitted to chain. |
| 2c. | SendSignedRawAsync(..) | Method used for sending a signed raw message back to the dApp. |
| 3. | NuGet package | We will provide a NuGet package, which is commonly used it c# development. It is comparable to NPM packages in Javascript world. |
| 4. | Sample dApp | We will make a sample C# console dApp (with Plutonication and Substrate.NetApi) published to a public github repo. |

### Milestone 3 Plutonication Typescript version

- **Estimated Duration:** 1 month
- **FTE:**  0.5
- **Costs:** 7500 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | MIT |
| **0b.** | Documentation | We will provide both **in code documentation for individual methods** and a **tutorial** explaining how to integrate Plutonication into a javascript/typescript dApp. |
| **0c.** | Testing and Testing Guide | All of the functions will be end-to-end tested with a sample dApp written in typescript (with Plutonication and Polkadot.js api) and a sample Wallet (PlutoWallet) |
| **0d.** | Docker | We will provide a Dockerfile for a sample dApp that can be used to test all the functionality delivered with this milestone. |
| 1. | PlutonicationDAppClient | This would be a series of methods tailored for use with dApps. We will make sure that it is compatible with polkadot.js api |
| 1a. | Initialize(..) | Method used for initializing the PlutonicationDAppClient |
| 1b. | ReceiveAddress(..) | Handles the receiving of SS58 encoded address |
| 1c. | SendPayloadAsync(..) | Method used for requesting an extrinsic payload sign |
| 1d. | SendRawAsync(..) | Method used for requesting a raw message sign |
| 2. | PlutonicationWalletClient | This would be a series of methods tailored for use with wallets. |
| 2a. | SendAddress(..) | Sends the SS58 encoded address of the account in the wallet |
| 2b. | SendSignedPayloadAsync(..) | Method used for sending a signed extrinsic payload back to the dApp. The signed extrinsic payload will then be added to the extrinsic and submitted to chain. |
| 2c. | SendSignedRawAsync(..) | Method used for sending a signed raw message back to the dApp. |
| 3. | QR code pop-up | We will provide a function that would embed an HTML qr code popup into a dApp. The QR code is used for establishing a connection. |
| 4. | NPM package | We will provide an NPM package, which is commonly used it javascript/typescript development. |
| 5. | Sample dApp | We will make a sample typescript console dApp (with Plutonication and Polkadot.js api) published to a public github repo. |

### Milestone 4 Plutonication extension

- **Estimated Duration:** 1 month
- **FTE:**  0.33
- **Costs:** 5,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | MIT |
| **0b.** | Documentation | We will provide **inline documentation of the code**. |
| **0c.** | Testing and Testing Guide | All of the functions will be end-to-end tested with a sample dApp (https://polkadot.js.org/apps/) and a sample Wallet (PlutoWallet) |
| **0d.** | Docker | We will not provide a docker file |
| **0e.** | Article | We will publish an article that explains what was done as part of the grant. We will mention how Plutonication is ground-breaking and can be used by anyone. |  
| 1. | Plutonication Extension | This is a __polkadot.js extension__ compatible browser extension for Plutonication. |
| 1a. | Inject(..) | Injects the browser extension into the polkadot.js dApp. |
| 1b. | ReceiveAddress(..) | Handles the receiving of SS58 encoded address |
| 1c. | SendPayloadAsync(..) | Method used for requesting an extrinsic payload sign |
| 1d. | ReceiveSignedPayloadAsync(..) | Method used for receiving a signed extrinsic payload data. This signed extrinsic payload will then be added to the extrinsic and submitted to chain. (Done automatically by polkadot.js) |
| 1e. | SendRawAsync(..) | Method used for requesting a raw message sign |
| 1f. | ReceiveSignedRawAsync(..) | Method used for receiving a signed raw message. |
| 2. | Chrome browser extension | We will provide an NPM package, which is commonly used it javascript/typescript development. |

## Future Plans

Please include here

- how you intend to use, enhance, promote and support your project in the short term, and
- the team's long-term plans and intentions in relation to it.

Once all of these 4 milestones are completed, we will have a solid ground to start integrating Plutonication to other dApps.

Our goal would be to create multiple PRs to already popular dApps to utilise Plutonication. At that point, other wallet companies will have a solid motivation to start integrating Plutonication into their wallets too.

Further plans are to combine Plutonication with PlutoWallet custom layouts (find more in PlutoWallet readme: https://github.com/RostislavLitovkin/PlutoWallet) and make onboarding of new users easier.

The endgoal would be to become a defaultly used solution for wallet injection.

## Referral Program (optional) :moneybag: 

You can find more information about the program [here](../README.md#moneybag-referral-program).
- **Referrer:** Name of the Polkadot Ambassador or GitHub account of the Web3 Foundation grantee
- **Payment Address:** BTC, Ethereum (USDC/DAI) or Polkadot/Kusama (USDT) payment address. Please also specify the currency. (e.g. 0x8920... (DAI))

## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** Web3 Foundation Website / Medium / Twitter / Element / Announcement by another team / personal recommendation / etc.

Here you can also add any additional information that you think is relevant to this application but isn't part of it already, such as:

- Work you have already done.

https://github.com/cisar2218/Plutonication

https://github.com/rostislavLitovkin/plutonicationextension

https://github.com/rostislavLitovkin/plutowallet

- If there are any other teams who have already contributed (financially) to the project.

Nobody has financially supported the project.

- Previous grants you may have applied for.

None yet.
