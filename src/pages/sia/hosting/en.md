# Hosting?
Hosts are the backbone of the Sia network, they are a critical part of the Sia ecosystem. Hosts sell their storage space and bandwidth in exchange for Siacoin. Without hosts, renters would not be able to store data and Skynet would not be able to function.

Hosting requires a basic level of technical knowledge. Hosts need to be familiar with basic port forwarding, firewall rules, disk management, along with some concepts unique to Sia’s decentralized storage model.

## Uptime
Hosting is a commitment. Ideally hosts would be available 24/7, but some downtime is expected. Over 85% uptime is acceptable for most renters. It is important that hosts are available as much as possible to give renters access to their data and earn revenue. Failing to fulfill storage commitments can cause the host to lose Siacoin.

## Hardware Requirements
Sia is able to run on a variety of different devices, architectures, and operating systems. Sia has official releases for Windows, Mac, and Linux. There are hosts running on low power devices like Raspberry Pi’s all the way up to high power rack mount servers.

requirements             | cores | memory   | SSD      | Disk Space|OS
-------------------------|-------|----------|----------|-----------|-----
Minimum Requirements     |2 cores|4GB Memory|60GB SSD  |4TB HDD    |Whatever
Recommended Requirements |4 cores|8GB memory|256GB SSD |4TB HDD    |Linux

It is highly recommended to store Sia’s blockchain (20GB+) and metadata on an SSD for better speeds. Renter data can be stored on normal consumer HDD to maximize space and minimize costs. Sia is optimized to run on Linux, other operating systems will work but come with trade-offs or increased risk.

## Wallet Balance
Hosts need to keep their wallet’s topped up with Siacoin in order to submit storage proofs and form new contracts. Due to how contract payouts work, mosts hosts are locking more collateral than they have incoming, it can take up to a year before the host has enough expiring contracts to self-sustain off only their earned revenue.

>Usually around $10 USD in SC is enough for new hosts to get up and running, but it largely depends on the host’s pricing and collateral.

## Earning Revenue
Hosts earn revenue by providing storage and bandwidth to renters. Renters pay for this usage in Siacoin. At the end of the contract earned revenue is automatically sent to the host’s wallet. If a contract is formed for 3 months the host will be payed only after the contract has expired.

>There are currently two bugs which make tracking revenue very difficult: host revenue does not show up in Sia’s transaction list and Sia’s built in revenue totals are inaccurate. Combined, this makes tracking earned revenue extremely difficult since host’s often lock up more collateral than they earn in revenue.

## Risking Collateral
To incentivize hosts to remain online long term, hosts are expected to risk collateral for the data they are storing. If a host cannot prove they have stored the data they have agreed to their collateral and payment is burned. This keeps hosts accountable and incentivized.

Most hosts have found that between 1 and 2 times storage price is a good balance of collateral for earning the most revenue.

## Storage Proofs
At the end of a contract the host has the option to submit a storage proof. This is proof that the host stored the data they were expected to for the contract’s duration. After the expiration of a contract, the host has 24 hours (144 blocks) to submit a storage proof during the `proof window`. If the host does not submit a storage proof the host’s risked collateral and the renter’s spent allowance is burned.

>In most instances it is in the host’s best interest to submit a storage proof, but there are some cases where submitting a proof would not make sense. If the cost of submitting a storage proof is greater than the host’s potential loss the host will not submit a proof.

## Contracts
Contracts create an instant payment channel between a host and renter that allows the renter to quickly pay for storage and bandwidth usage. Contracts are blockchain enforced agreements between a host and renter that automatically resolve at the end of the contracting period. This keeps the entire ecosystem working transparently and honestly.

The host and renter both lock Siacoin into a contract for the entire duration. When a contract is created the renter and host agree on how much allowance the renter should lock in, how much collateral the host should lock in, and how long the contract is for. Revenue, unspent allowance, and collateral is automatically returned to its owner at the end of the contracting period.

The host has some controls to block unfavorable contracts. Renters decide the duration of the contract and how much collateral the host should lock for the data they want to store, but the host can limit how much collateral they are willing to lock into a single contract and the maximum duration of the contract.

**Max Duration** is the maximum duration that a contract can be for. This is usually represented in months. The average duration is around 3 months. Hosts are payed only at the end of the contract duration. If a host commits to storing data for 6 months, but fails to submit a storage proof all revenue and collateral will be burned.

**Max Collateral** is the maximum amount of collateral a host is willing to lock into a single contract. Large contracts can cause performance issues on hosts and locking too much collateral into a single contract may limit the number of contracts a host can form with other renters.

**Collateral Budget** the total amount of Siacoin to use for forming contracts. This is currently bugged so the budget can fill up without actually having collateral locked. Setting this to a very high number regardless of wallet balance can help to reduce unnecessary restarts.

## Pricing
Hosts get to set their own prices, the storage marketplace is meant to be a free and open competition between hosts to provide the best value to renters. Historically, there has been much more supply than demand so profits are low. This isn’t to say that hosts can’t earn a small profit. Hosts with good reputations or better connections are often chosen even if the cost would be higher.

**Storage Price** is the cost to store data on the host, usually represented as SC per terabyte per month. Around ***$1 – $2 USD per TB*** is a good starting price

**Download Bandwidth Price** is the cost to download data from the host, otherwise known as `egress`, usually represented as SC per terabyte. Between ***$1 – $5 USD per TB*** is a good starting price. In a more competitive market it might make sense to charge more if you have a Gigabit connection with no data cap or are in a location with few hosts.

**Upload Bandwidth Price** is the cost to upload data to the host, otherwise known as `ingress`. Usually this is represented as SC per terabyte. Onboarding data is the most important part of hosting, it is generally recommended to set this low or even to 0 to onboard as much data as possible.

**Collateral** is the amount of collateral the host needs to risk per TB of data stored. Between **1 – 2 times** storage price is a good reference point.

**Contract Price** is the cost to form a contract with the host, this should not be more than **1 SC**. Contract price is meant to cover transaction fees for submitting a storage proof. The default **0.15 SC** is for the most part fine, most storage proofs cost less than **0.01 SC** to submit.

## Announcements
Hosts are required to announce either an IP address or DNS address where renters can connect to them. The announcement has four parts: the ip/domain, the port to connect on, the host’s public key, and a signature. This makes it easy for renters to discover and connect with new hosts and update existing hosts.

Announcing a DNS like `myhost.hosting.com:9982` instead of an IP address avoids having to announce multiple times if you do not have a static IP.

## Ranking
Most renters rank hosts based on criteria they find important. There is no centralized ranking system for hosts, each renter uniquely ranks hosts they can connect with based on different criteria. For the most part a host’s individual rank can be very different between two renters.

The original Sia renter ranks hosts based on age, pricing, collateral ratio, available storage, and estimated uptime. When picking new hosts to store data with the renter does not necessarily pick in order of rank. As such, **Sia rank** should not be considered an important metric for hosts. To break the top 50 a host would need to sacrifice most of their revenue potential. Custom scoring systems that take into account transfer speed, availability and latency over pricing are also being used.

## Useful Tools For Hosts
- [SiaStats](https://siastats.info) / hosts | monitors and benchmarks all hosts on the network.
- [Sia Central](https://troubleshoot.siacentral.com) | easily troubleshoot port forwarding, dns resolution, and connection issues.
- [Sia Host Manager](https://siacentral.com) | alternative to Sia-UI with better financial tracking and fiat price pinning.

## Where to go next?
If you want to start hosting, it is also good to know more about the renters. [Our guide]() will lead you through everything you should know before you start.

*Written by Nate (Updated by Nate: January 26, 2021)*

*Updated by Covalent (March 12, 2021)*