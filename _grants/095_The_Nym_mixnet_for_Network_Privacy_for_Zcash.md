---
title: "The Nym mixnet for Network Privacy for Zcash"
status: "Accepted"
amount: "150000.0"
submitter: "[REDACTED] [REDACTED]"
email: "[REDACTED]"
date: "2023-10-18 14:58:39"
project_name: "The Nym mixnet for Network Privacy for Zcash"
summary: "The Nym mixnet for Network Privacy for Zcash"
total_grant_value: "150000.0"
submitter_last_name: "[REDACTED]"
original_title: "The Nym mixnet for Network Privacy for Zcash"
labels:
  - APPROVED
---

## Terms and Conditions

- [X] I agree
- [ ] Link to this issue on forum - _do after application has been submitted_

### Application Metadata

- **Submitter First Name:**
  [REDACTED]
- **Submitter Last Name:**
  [REDACTED]
- **Submitter Email:**
  [REDACTED]
- **Status:**
  Accepted
- **How did you learn about Zcash Community Grants:**
  Via Zcash Community Forums
- **Original Title:**
  The Nym mixnet for Network Privacy for Zcash

- **Labels:**
  - APPROVED

### Project Overview

- **Project Name:**
  The Nym mixnet for Network Privacy for Zcash
- **Last Updated:**
  2024-02-13 16:59:57
- **Sponsorship Request:**
  No
- **Project Image (Public Gallery):**
  nym-logo-black.png
- **Project Summary:**
  The Nym mixnet for Network Privacy for Zcash

### Project Description

- **Overview:**
  We will provide Zcash users with state-of-the-art network-level privacy, without compromising the reliability or usability of the Zcash network, by using the Nym Mixnet. Although shielded Zcash is state-of-the-art for defending user privacy against attackers with access to a copy of the blockchain, shielded Zcash is not enough to defend against attacks at the network level, i.e. the stream of TCP/IP packets used to submit transactions (for full-nodes) and read the Zcash blockchain (for light wallets). These attacks are not unrealistic: ISPs can easily snoop on network traffic to passively record Zcash activity, and adversaries such as Chainalysis have the ability to do both passive surveillance of the large portion of p2p traffic in a network (as it was revealed it had done to the much larger Bitcoin p2p network) and active attacks. The importance of network-level privacy is explicitly called out even in the original Zerocash paper (Section 6.4). Therefore, in order to have holistic privacy for their usage of shielded Zcash, Zcash needs to support network-level privacy. We present a quick summary of the network-level privacy topics below: Without network-level privacy protection, the node to which a wallet transaction is submitted would know the time and the IP address of the wallet user. This in itself is undesirable, opening the user to targeted attacks. Similarly, network-level adversaries such as system administrators, ISPs, and other entities with access to intermediate parts of the infrastructure can obtain network-level information about the Zcash user. If the timing data from the full node is combined with the blockchain data, statistical disclosure attacks [Danezis03] may compromise a frequent Zcash user (i.e. link the user’s IP address to the transactions. What are the options that Zcash has to offer network-level privacy to users? Encourage users to use a VPN. The benefits of this are clear: while the user’s IP address is hidden from the blockchain node, this option a) requires full trust of the VPN proxy and b) does very little against network-level adversaries. The Tor network is widely deployed and has been functioning for a number of years (the first research prototype was built as far back as 1996!); it has a large user base, and is highly suitable for web-browsing use cases. Although a user submitting a Zcash transaction using Tor (or a VPN for that matter), would prevent their IP address from being disclosed to the blockchain node, it offers weak protection against network-level adversaries which can mount a correlation attack. More specifically, the fact that Tor’s design is circuit-based, enables end-to-end correlation based on circuit start/end timings and any traffic patterns in the flow. A network adversary can exploit these features to correlate the two ends of a circuit, defeating the anonymity provided by the re-routing of data. An adversary can likely distinguish a “Zcash circuit” from a “website browsing circuit” based on traffic fingerprint features). Stolon, a proposed variant of Dandelion that relays new transactions over Tor connections, inherits the weaker threat model of Tor and does not defend against an adversary that is watching both nodes involved in the “steam” phase of Dandelion. In p2p networks like Zcash this is a realistic threat. Nym is per-packet and is hence optimized for provisioning maximum network-level privacy for applications like cryptocurrency transactions. Furthermore, the cover traffic introduced by a nym client not only disguises the timing of the transaction but also mixes it with the traffic on the nym network generated by other applications, hence providing a significant amount of protection, even against statistical disclosure attacks for frequent Zcash users. In May 2022 a new major release of Zcash has introduced the auto-shielding feature https://electriccoin.co/blog/halo-arc-for-zcash-proposed-for-release-later-this-year/ . Unless this is accompanied by a strong network-level privacy layer, it would permit adversaries to fingerprint Zcash users. That is, an adversary would obtain the user’s t-address (or extract it from the unified address), send a transaction to it, and observe the user’s wallet broadcasting the t2z auto-shielding transaction. Note that the adversary can easily repeat this process and thus obtain finer granularity IP measurements and track those over time. The usage of Nym should not compromise the reliability of the Zcash network or degrade user experience. To address such issues, the Nym network incentivizes the network participants (i.e. those running mix nodes, gateways, etc.) to behave reliably and efficiently handle traffic. This is a unique feature of Nym, allowing the network to scale with demand. Similarly, usage of the Nym network should be affordable and sustainable for Zcash users, hence Nym will be able to provide bandwidth to Zcash customers until 2024 for free [Nym is flexible on this point]; afterward we envisage a per-transaction fee model where a flat fee (i.e. independent of the value of the transaction) is paid to the Nym network for providing network-level privacy or bulk provisioning of ZCash traffic once we understand in 2024 how much traffic ZCash needs.
- **Proposed solution:**
  The Nym integration should allow any ZCash-enabled application to use the network, including pure point-to-point usage (i.e. p2p ZCash clients that each run full nodes) as it will allow Nym to be used with a full node running zebrad/zcashd. This will require direct integration via an HTTP proxy to zebrad (with zcashd as a backup via C bindings). This can then be expanded by Nym address integration with universal addresses, which would happen after both the initial integration with lightwalletd and zebrad/zcashd integration is complete.
- **Solution Format:**
  Improved Network Privacy Threat Model and Design Document for Zcash. This will be delivered by the Nym Research team; furthermore, we will use our network of privacy experts, including the Zcash Foundation, for a review. This document will be iterated as the integration continues. Create HTTPS Connect Proxy for Nym to allow Nym to work with gRPC Create a Service Provider component (transactions submission service) that would run between the mixnet and Zcash nodes. Integration via lighwalletd for sending, and possibly receiving, transactions.
- **Dependencies:**
  There is a dependency on Zcash Foundation due to the proposed plans for zebrad support and on ECC for lightclientd and possibly Zashi support.
- **Technical approach:**
  The Nym mixnet is a real-world deployed mixnet that offers stronger privacy protection for message-based transactions (such as cryptocurrency) than Tor, Dandelion, or I2P. In particular, Nym defends against both a global passive adversary that can observe the entire network, as well as provide increased privacy against fingerprinting of Zcash usage by local adversaries. Nym distinguishes itself by considering a strong, and in our mind, very realistic, threat model: it aims to protect users who have repeated interactions (sending z2z transactions to or receiving z2z payments from) with an active adversary with network-level visibility. This threat model, for example, covers the Fleshlight attack (Ian Miers 2018, https://www.youtube.com/watch?v=9s3EbSKDA3o ) which seeks to deanonymize merchants who accept electronic payments. In essence, mixnets de-link senders (as well as receivers) from the transaction (just like, say, the zk-SNARK Spend proofs unlink the sender’s identity) via 1) multiple hops, 2) mixing traffic on a per-packet basis, and 3) adding dummy traffic. Both Tor and Nym use three hops. Unlike Tor circuits that focus on effectively obfuscating an IP address, mix-nets are packet-based and so have much higher entropy and privacy than Tor as Nym also obscures the timing and volume of network traffic flow. Unlike Tor where all packets are delivered in a FIFO order, mix-nets “mix” packets (like shuffling a deck of cards) for an amount of time and so packet order is obfuscated. Even if there are fewer users than Tor, mixnets can provide higher privacy in terms of entropy against global passive adversaries via mixing dummy traffic. Note that, unlike other mixnets, Nym allows the optimization of dummy traffic based on existing traffic flows to prevent statistical disclosure attacks. We believe dummy traffic and the use of the Sphinx packet format by Nym also allow packets to be more resistant to ISP fingerprinting than Tor. Lastly, Nym is source-routed and so the amount of mixing and delays can be set by the client software to optimize the latency vs. privacy tradeoff on a per-application basis. Like Tor, Nym supports a wide variety of applications via “plug and play” proxies like SOCKS5, and so can already be used by Bitcoin wallets (e.g. Electrum and Blockstream Green). Latency delays can be set for milliseconds, seconds, or even minutes, and hence even relatively small numbers of users with infrequent usage can still obtain reasonable entropy (based on our simulations). We also note that mixnet privacy has a guarantee -- a single point of success -- similar to Zcash’s setup ceremony guarantee: it is sufficient for at least one mixnet node to provide strong uncorrelated entropy for the output to be statistically indistinguishable. Currently, alternatives like Tor and I2P cannot make guarantees of network-level anonymity in terms of entropy. Although some Tor co-founders have argued that entropy is not the best measurement and resistance to only local (and possibly mobile) adversaries is the current more realistic threat model, ( https://mail.freehaven.net/anonbib/cache/entropist.pdf ), we think that protection against the global passive adversary gives additional comfort. There are a number of possible integration points, but the most critical is lightwalletd as defending the metadata of light clients from full nodes provides the greatest possible protection for the greatest number of users. This would at least include sending transactions. Receiving transactions via downloading all transactions via a Nym-enabled lightwalletd will have to be investigated for performance, but some functions such as balance lookup should work through Nym. Note that integration with lightwalletd would require Go bindings to be created for Nym and Nym to support HTTP requests. However, the Nym integration is not limited to lightwalletd. The Nym integration should allow any ZCash-enabled application to use the network, including pure point-to-point usage (i.e. p2p ZCash clients that each run full nodes) as it will allow Nym to be used with a full node running zebrad/zcashd. This will require direct integration via an HTTP proxy to zebrad (with zcashd as a backup via C bindings). This can then be expanded by Nym address integration with universal addresses, which would happen after both the initial integration with lightwalletd integration is complete and zera. The Nym network is fully operational. All the features to ensure the privacy guarantees required by Zcash are already live. Further efficiency and security improvements are in active development. Other integrations with applications such as Keybase and Electrum already exist, and there are discussions with multiple other cryptocurrencies and browsers such as Brave. Our research team is also planning to study the real-world effects of mixing by measuring the aggregate input and output traffic for different kinds of traffic, although this is outside of the scope of the grant.

### Requested Grant Amount

- **Amount:**
  150000.0

### Budget Breakdown

- **Hardware/Software budget:**
  0.0
- **Hardware/Software justification:**
  N/A
- **Services budget:**
  0.0
- **Services justification:**
  N/A
- **Compensation budget:**
  150000.0
- **Compensation justification:**
  We consider Zcash integration as one of the core use cases for network privacy and hence would like to run this project on a standalone basis, separately from the rest of the Nym roadmap (module management oversight). This would ensure that business prioritization of Nym (including integration demands from other projects) has no impact on the Zcash integration project. We are able to do this because the Nym mixnet is already mature enough to a) provide the necessary privacy properties and b) handle the volume of traffic, so the risks to the project are low. We see the project as being made up of the following stages: POC. We anticipate that building a proof of concept component with the aim of submitting test transactions would be relatively straightforward to build. The initial PoC would focus on defending the network privacy of light clients via lightclientd from full nodes. Around 1 month of setup, integration, development, and testing should be sufficient. Cost order of 20k USD. 3-6 are development phases; We plan to allocate 1 developer for 6m; cost of approx 75k USD for Nym. Research, Testing and user acceptance: This necessitates both technical testing and attention from the project management team as well as the research team to determine the details of the threat model for users given constraints discovered in the development process; 2 people: 30k USD for Nym. Beta testing + Releases + any contingency/slippage costs. We plan to limit the costs to 25k; any additional costs would be taken by the Nym team. If the project is fully on schedule and contingency costs are lower, the remaining amount will be added to the next item. Total: 150k USD. Note that a pre-purchase of NYM for automated payment, actual wallet integration work, as well as user-evaluations as outlined in the original proposal, can be done in follow-up work.
- **Startup funding required:**
  No
- **Total proposed grant value:**
  150000.0

### Team Members

- **Project Lead:**
  Nym Technologies
- **Background:**
  Nym Technologies is a company based in Neuchatel in Switzerland specializing in developing Privacy Technologies. The company was founded in 2018 and has raised multiple rounds of capital, most recently 30m of public funding in February 2022. The company has 40+ employees across the globe and has launched its mixnet infrastructure in Summer 2022. The Nym team includes a number of expert researchers in the domain of privacy-enhancing technologies and network-level privacy, including Claudia Diaz and Ania Piotrowska. Claudia Diaz has done seminal work on network-level privacy from mixnets to fingerprinting attacks. Ania Piotrowska designed Loopix, the most advanced mixnet design to date, which Nym is based on. Harry Halpin worked with both of them to start Nym after meeting in PANORAMIX, the five-year European Commission project to build a mixnet that would be able to withstand attacks by a global passive adversary after the Snowden revelations showed that such an adversary was realistic, and it is outside Tor’s threat model. The Nym development team is formed from expert programmers such as Mark Sinclair, who leads a team of core Rust and Go cryptographic engineers along with front-end developers and integration developers. Members of the Nym team have been active in the Zcash community forums, attended events such as Zcon, have worked with members of Bootstrap (Electric Coin Company) to run nodes, done the first extensive user study of Zcash wallet usage, and discussed this proposal extensively with members of Zcash founding team such as Madars Virza, Zooko Wilcox and Eran Tomer. Furthermore, we can already demonstrate successful integration with Bitcoin and the Liquid side-chain via Blockstream Green Wallet, and have a working generic SOCKS5 proxy useful for a variety of applications, including Telegram and Keybase. Although Zcash’s underlying codebase does not support SOCKS5 and thus development effort is needed for Zcash integration, this is work that the Nym team is very comfortable with.

### Funding History

- **Previous funding:**
  No
- **Other funding sources:**
  No

### Risks and Evaluation

- **Execution risks:**
  The primary risk the Nym team runs is the lack of acceptance of pull requests by the Zcash wallet developers of ECC (lightwalletd) and ZCash Foundation’s work on zebrad. We view this risk as low, and it would be mitigated by agreeing on the design of the Nym integration jointly with the Zcash core developers. Our general belief is that users should be given options for network-level privacy, although it would also be attractive to make these as invisible as possible and to enable “privacy by default.” However, for the scope of this grant we would want it to be an opt-in/opt-out feature (up to app developers) with an easy “off-on” switch users can toggle. If zebras is yet ready, we can focus on zcashd and we could integrate with z_sendmany RPC call to send transactions over the Nym mixnet when suitably configured. As zebrad matures, we could focus on integration against zebrad, and zebras’s modular design should make this easier. As Nym’s software is in Rust, integration should be straightforward and easier with zebrad rather than zcashd. A secondary risk would be the maturity of the Nym network itself. As detailed in the blog post by the Zcash Foundation, https://www.zfnd.org/blog/mixnet-production-readiness/ 1 , there have been concerns that the Nym network itself would not be able to support shielded Zcash usage. However, Nym has several hundred mix nodes (likely around the same number as Zcash full nodes) and can actively handle 1000s of tx per second, therefore we can easily handle current and future amounts of the shielded Zcash transactions. A third risk is that there is a fundamental underlying incompatibility between our approach and Zcash’s design or implementation that prevents network-level privacy, such as issues in terms of wallet communication or the inability of Nym to work with core third-party libraries that Zcash relies on (such as gRPC for light wallet clients). However, we believe all these issues are solvable.
- **Unintended Consequences:**
  Note as Nym would be an optional feature (although we would envisage it to be on by default), the negative effects would be very limited, i.e. in the worst case scenario, Zcash wallet / full node users could simply turn it off (and indeed, in an event some kind of failure is detected, this would be done automatically). Nevertheless, with the Nym network fully operational, we would see users experiencing higher bandwidth usage (due to cover traffic) and a very small amount of added complexity in the UI. Although the grant would cover the costs of the Nym infrastructure for the foreseeable future, later the users would be exposed to small transaction fees to Nym (or this could again be covered by Zcash). However, the benefits of a) Strong network level privacy b) Education of Zcash users about network privacy, and c) Decreased reliance on existing solutions such as Tor in our view far outweigh the potential downsides.
- **Evaluation plan:**
  The project will be successful in the long-term if a) The Nym network integration is included in lightwalletd b) Nym integration works with zebrad (or zcashd) and eventually if wallets integrate, c) as many wallets as possible d) turned on by default e) is utilized by many users and f) the network continues to be reliable and supports a growing volume of traffic. 
   All of the above are easy to monitor. In terms of a) lightwalletd and b) full node integration, the code will either work or not and upstream patches are accepted. However, the goal should still be getting this into the hands of real-world users, not just being a proof-of-concept that no one uses. In this case, c) and d) are self-explanatory; to gauge e) we could simply add a transaction counter to the network requestor (releasing aggregated stats only over a significant time period, e.g. monthly/weekly) and f) comes from standard Nym network monitoring. 
   Note that we will not specifically be funding wallet integration work, but will first see how many wallets can integrate natively without being paid for the work from ZCash Community Grants. Therefore, c), d) e) and f) are to a large extent dependent on wallet integrations that are not funded and outside the scope of this current grant, but would be the focus of a future grant if they do not happen organically. 
   In terms of qualitative metrics, the primary result we will share with the community is the report on what Nym is, how it helps the threat model and solves privacy leaks in ZCash, and concretely how the code for Nym can be integrated into ZCash wallets. In terms of a quantitative evaluation, the first metric we will report is the increase in privacy as measured in network-level entropy is added by using the Nym mixnet. We will also quantitatively measure increased latencies for sending Zcash via various wallets with different degrees of mixing and can compare to base-lines such as no network-level privacy and the latency added by Tor/Arti. The last metric will be the number of wallets that are organically integrated into Nym that we are aware of. Assuming there is wallet integration, then we will ask the wallets to provide the percentage of transactions from the Nym-enabled wallet using the Nym network across and per wallets and whether it is an optional feature or not. If using Nym is not a default feature, we will ask why or why not people are using Nym in these interviews. This work itself will lay the groundwork for a full report, similar to those already done by Nym for wallets: [2105.02793] Holistic Privacy and Usability of a Cryptocurrency Wallet , to be shared with the Zcash community. The highlights will also be shared in blogpost form. Any qualitative metrics will be done with full compatibility with the General Data Protection Regulation. To summarize, focus on lighwalletd first, then zebrad, then universal addresses, with no explicit wallet integration or token support included. This has lowered the budget considerably, which we think is more in line with ZCG and community feedback. To be very concrete, we would consider this project a full success if the wallet as well as full node developers agree to turn the Nym integration on by default and hence we see >30% of the Zcash shielded wallet transactions on the wallet benefitting from Nym-grade network privacy if offered as an optional feature. If it was a default feature then we would prefer to see >80% shielded wallet transactions from the wallet using Nym mixnet. This would require major ZCash wallets using the Nym network.

### Project Timeline

- **Project timeline determination:**
  The timeline was developed based on our previous experience in integrating Nym against wallets and full nodes. In particular, we have tried to be realistic and so budgeted a large amount of time for the light wallet integration (6 months) as well as 2 months of slippage.

### Milestone 1

- **Amount:**
  20000.0
- **Expected Completion Date:**
  3/31/2024

  - **Deliverables:**
    - Ramp-up, resource allocation, and information gathering. Create the improved threat model and design document.

### Milestone 2

- **Amount:**
  75000.0
- **Expected Completion Date:**
  9/30/2024

  - **Deliverables:**
    - Working code: We anticipate that building a proof of concept component with the aim of submitting test transactions would be relatively straightforward to build. The initial PoC would focus on defending the network privacy of light clients via lightclientd from full nodes. For the PoC, we will add Nym Service Provider and test by submitting test transactions through the Mixnet. For full nodes –  we will try do tx submission over Nym using str4d’s code.  After the first month of exploring options using PoC code, the next 5 months  development, and testing should be sufficient to producig the binding and library code needed for ZCash and Nym integration.

### Milestone 3

- **Amount:**
  30000.0
- **Expected Completion Date:**
  11/30/2024

  - **Deliverables:**
    - Wallet integration: Testing and acceptance with the wallet developer community, re-visting work on threat model, and integration for receiving transactions as well as universal address support.

### Milestone 4

- **Amount:**
  25000.0
- **Expected Completion Date:**
  2/28/2025

  - **Deliverables:**
    - Beta testing + Releases + any contingency/slippage costs.  Finalize threat model and design document complete for implemented features. We plan to limit the costs to  25k; any additional costs would be taken by the Nym team. If the project is fully on schedule and contingency costs are lower, the remaining amount will be added to the next item.

### Additional Milestones

- **Additional Milestones:**
  Yes

### Submission Date

- **Submission Date:**
  2023-10-18 14:58:39

### File Attachments

- **nym-whitepaper.pdf**: [Additional documentation]

