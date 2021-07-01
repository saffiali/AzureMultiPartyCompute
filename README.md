# Authors

This article was authored and reviewed by:

- [Saffi Ali](https://www.linkedin.com/in/saffieldin/): Cloud Solution Architect – Customer Success at Microsoft
- [Venu Vedam](https://www.linkedin.com/in/vedam): Cloud Solution Architect – Partner Success at Microsoft

# Abstract

Multiparty Compute (MPC), or Privacy-Preserving Computation, is a concept that gives different parties in a business relationship the ability to share data, perform computations on it, and arrive at a mutually desired result without divulging private data of the individual parties.

This is an evolving field and there are several services on Azure that can help you build a secure MPC solution across the cloud and the edge. It is easy to get lost in the details. The purpose of this article is to de-mystify the MPC paradigm; the relevant offerings available on Azure; and when to choose a particular service over another. At the end of the article, we will give you an easy-to-use flowchart to help you decide on the best service to use for your multiparty compute system.

# Multiparty Computing and Blockchains

## What is Multiparty Computing?

Before we look at what multiparty compute options are available on Azure, let us define the term &quot;Multiparty Computing&quot; as it applies to our context. As the phrase suggests, it is a computing process that has multiple parties or enterprises participating. Take any business process, where your organisation needs to interact with other companies or entities. It is a multiparty business workflow. As part of your digital transformation journey, you are designing a software system to handle this workflow. Since this system needs to be accessible by all the companies taking part in the workflow, it needs to be robust, secure, and most importantly, trustworthy.

Such a system is called a multiparty computing system. It invariably has several independent groups accessing the system, feeding data to it, getting insights from the data, and in some cases, participating in the governance of the entire system.

That precisely is the definition of multiparty computing. It is a system where organizations that do not necessarily trust one another come together to participate in a business process enabled by a trustworthy data and compute backbone that is accessible by all these entities.

Let us take an example. An obvious choice for a multiparty workflow is the supply chain network of any company. In the Retail context, raw materials flow from the point of origin to the manufacturing unit. Finished goods from the manufacturer go through a set of shipping partners to a distribution hub from where they are sent to all the retail supermarkets.

![](/MPC-Images/Picture1.png)

_Figure 1: A typical Retail Supply chain_

This process has many companies working together – The raw materials supplier, the manufacturer, transport or shipping firms, warehouse operators, and the retail outlets not to mention the end consumer. The &quot;asset&quot; or the &quot;product&quot; changes hands many times as it traverses through the supply chain. It is important to track who has ownership of the asset at any given instant.

Similarly, a cross border payment system is another example of a multiparty workflow with banks from either side of the border participating in the funds transfer.

Any multiparty scenario has the following attributes:

1. There is always more than one organization in the mix.
2. They are independent.
3. They do not trust one another.
4. They all need access to a common computing and data storage platform.
5. Some of the processes handled by this system should be private within a subsect of the companies involved.

## Multiparty Compute Technologies

Multiparty Computing is an umbrella term that we use to denote a variety of technologies that enable you and me to transact securely over a network – whether it is a private LAN, WAN, or the internet.

Most famous in this group of technologies is what is arguably taking the world by storm – The &quot;Blockchain&quot;. Introduced in a 2008 whitepaper by Satoshi Nakamoto, whose real identity remains a mystery to date, Bitcoin was the very first use case of a blockchain. Some people still use the two terms interchangeably but blockchain is much more than just a cryptocurrency. It is a data ledger that can be shared between two (or more) independent parties and still have both (or all) parties trust the data on the ledger.

Blockchains are a form of distributed ledgers, where the transactions are bunched together in blocks with each block linking to the previous block in a Merkle Tree formation. However, there are other distributed ledgers that do not use blocks at all – where each transaction is linked to the previous transaction on the ledger. Corda from R3 is an example of a distributed ledger that is not a blockchain. Ethereum, on the other hand, is a blockchain. These days, the terms &quot;Blockchain&quot; and &quot;Distributed Ledgers&quot; are used interchangeably though.

However, blockchain is not the only multiparty computing option out there. Thanks to the recent advances made in the processor space, we now have access to hardware protected memory regions on the CPU itself. These regions, also called &quot;Secure Enclaves&quot; are cryptographically protected. You can place your data and run your process completely within the confines of the secure enclave where they are in the clear. For the outside world, though, it is all encrypted even while the process is running.

This means that even if you are a privileged administrator having full access to the server, you still cannot look at the process or the data inside those secure enclaves. If you are familiar with the term &quot;Trusted Computing Base&quot;, which is the bare minimum set of actors and systems that you must implicitly trust to keep your system secure, the secure enclave removes the privileged administrator, the super user, the system administrator, and the cloud service provider such as Microsoft, from the TCB of your system.

The narrower your system&#39;s TCB, the more secure your system.

This is the backbone of &quot;Azure Confidential Computing&quot; – where you have access to these secure enclaves. Since these enclaves have the capability to remotely attest themselves to other enclaves, you can design a multi organization network where the complete system runs from the enclaves – also called the Trusted Execution Environments.

Azure provides a service called Azure Confidential Ledger (ACL) that lets you run an Ethereum based ledger on the secure enclaves. (More details on it in the following sections.)

Finally, there is a need for a more centralised system of record, which has a few of the redeeming qualities of blockchain, namely immutability and trustworthiness. Azure SQL Database ledger is such an offering, which blends the power of a relational database that can operate at OLTP performance levels with the trust features that you can expect from multiparty systems. As Gartner predicted back in 2019 (Citation required), at least 20 percent of current blockchain/DLT implementations are better architected using centralised ledger technologies such as Azure SQL Database ledger. In these situations, you do not need any de-centralised consensus but just the immutability aspect of the ledger.

That brings us to the important decision matrix of when blockchains make sense and when you should shy away from them in favour of these other multiparty scenarios.

## Blockchain/DLT Decision Matrix

When we walk into an architecture and design workshop, where the main idea is to figure out how blockchains can help, we lead with the following set of questions.

![](/MPC-Images/Picture2.png)

_Figure 2: Blockchain Decision Matrix_

If the answers to the questions above are all yes, the business process is a good candidate for a blockchain based transformation. We can then look at the technology choices and how the system can be architected on Azure.

Blockchain may still make sense even if a few of the answers are not yes. However, in those cases, we normally look closely at the other multiparty compute options as well before deciding.

## Blockchain Network Models

We often use &quot;blockchain networks&quot; as a term to denote all implementations that have a significant presence of a blockchain ledger. This does not mean that blockchain networks are a single homogenous pattern. Depending on how you decide to dissect it, there are multiple patterns that can solve your business problems.

One important distinguishing factor is if there is a gating criteria for anyone interested in participating in the network. If it is open for all, it is called a public blockchain network. There are no rules or KYC forms. You just download the client on your server and join the network. Most cryptocurrencies follow this model including Bitcoin and Ethereum.

The other model is where you need permission from the existing members of the network to join the party. This is called, unimaginatively, a permissioned blockchain network or a private/consortium blockchain network. This model is generally favoured by enterprises that deal with a finite number of known other organizations. For instance, a superstore may want to have a closed and permissioned blockchain network for its supply chain participants. A few banks and corporates can have such a network for handling trade finance among themselves.

Both models are prevalent today. It all comes down to whether you are proposing blockchain as an end data store for your data or just as a middleware layer to bake trust into your system.

While there are other ways in which you can differentiate blockchain networks, we will save them for another blog post!

# Tamper-evidence vs distributed multiparty workflow.

The key decisive factor for choosing blockchain/DLT based solutions are the following:

1. The disruptive nature of the business-process **AND**
2. System and data integrity can be hindered if it is being controlled by single entity.

If your business process can run centrally or all parties taking part in that business process can trust one another, blockchain/DLT is not the best solution.

On the other hand, a lot of scenarios just want to bake trust in the data they are sharing. They need to Tamper-evidence or Tamper-proof the data. This can be achieved with non-blockchain based solutions.

In the next section, we will discuss the various multiparty compute options available on Azure.

# Azure Multiparty Compute options

Within Azure you have several options when it comes to multiparty solutions. They are not mutually exclusive, and in some cases, they are being used in-conjunction with each other.

## Blockchain based multiparty options:

As we mentioned in the introduction, blockchain makes sense for certain type of multiparty scenarios. Going back to the Architecture and Design workshop, once we decide that blockchain is the way to go for a given business process transformation, the next step is to design the technology stack. There are several types of blockchains in the market today such as Bitcoin, Ethereum, Hyperledger Fabric, Corda, Hedera Hashgraph etc. We tend to call them &quot;protocols&quot;. It is a just a convenient way of grouping them together.

The protocols space is still evolving. There is no interoperability worth speaking of now. Depending on the protocol chosen, you have access to a set of features. Hence the first step is to list down what we want from our blockchain based system. Then we can zero in on the protocol of choice.

Once the protocol is decided, the next step is to figure out how to deploy this network on the cloud. There are several deployment options available as shown in the picture below.

![](/MPC-Images/Picture3.png)

_Figure 3: Blockchain Ledgers - Deployment on Azure_

### Infrastructure as a service (IaaS)

You can run any ledger protocol on Azure using the infrastructure layer. You can spin up a few Virtual Machines (VMs), install the protocol on those VMs, and stitch them together for a blockchain network. It is easier said than done though. Since most blockchain implementations have multiple organizations and hence multiple cloud accounts, the networking puzzle to make these individual nodes talk to one another is a complex problem to solve.

Also, VMs are a maintenance nightmare for any organisation. Since most blockchain ledgers support deploying into Docker containers, most production deployments use Kubernetes engine to manage the containers instead of using VMs. Azure has a managed Kubernetes orchestrator called Azure Kubernetes Service (AKS) that you can use to deploy and configure your blockchain nodes.

While you can build the network from scratch, there are deployment templates available on Azure for most blockchain ledgers using which you can spin up a network in a matter of minutes either on AKS or on virtual machines.


### Blockchain/DLT as a service (BaaS)

infrastructure deployments are great from a customization point of view. But they are a management overhead for your IT team as you must take care of OS updates, patch updates, keeping the system up and running, high availability, and business continuity aspects. AKS based implementations come with some sort of a managed service for the VMs that power the AKS cluster. However, you still are responsible for managing the various AKS clusters in your cloud account along with any networking or storage options in your architecture.


### Azure Confidential Ledger

We know encryption at rest and in transit, but what about data in use for computation. Confidential Computing allow encrypting data while it is being used in RAM.

![](/MPC-Images/Picture4.png)

_Figure 4: Data protection lifecycle_

It lets you process data from multiple sources without exposing the input data to other parties. This type of secure computation enables many multiparty compute scenarios such as: anti-money laundering, fraud-detection, and secure analysis of healthcare data where data protection is mandatory in every step.

![](/MPC-Images/Picture5.png)

_Figure 5: Azure Confidential Computing_

It enables you to store unstructured, sensitive data records with integrity and confidentiality guarantees – all with high-availability and high-performance. Specifically, stored data is not only immutable and tamper-proof in the append-only ledger but is also independently verifiable. ACL harnesses the power of Confidential Computing&#39;s secure enclaves when setting up a decentralized blockchain network and requiring a minimalistic trusted computing base.

#### **Azure Confidential Ledger vs Azure Immutable Blob Storage**

[Immutable storage for Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-immutable-storage) enables users to store business-critical data objects in a WORM (Write Once, Read Many) state. This state makes the data non-erasable and non-modifiable for a user-specified interval. For the duration of the retention interval, blobs can be created and read, but cannot be modified or deleted. This means if someone with admin rights, they can alter the append-only interval to modify the data.

Unlike Immutable Storage, ACL harnesses the power of Confidential Computing&#39;s hardware-encrypted secure enclaves when setting up the decentralized blockchain network, limiting Microsoft&#39;s access to operating the nodes in the ledger.

| Factor | ACL | Immutable Blob Storage |
| --- | --- | --- |
| Confidential Hardware Enclaves | Yes | No |
| Append Only Data Integrity | Yes | Yes, limited to intervals |
| In-use Data Encryption | Yes | No |
| Blockchain ledger proof | Yes | No |

# Non-blockchain based multiparty options:

## Azure SQL Database ledger

Many organizations are turning to blockchains, where trust is low between parties that participate on the network. However, many of these networks are fundamentally centralized solutions where trust is important, but a fully decentralized infrastructure is a heavy-weight solution.

Ledger provides a solution for these networks where participants can verify the data integrity of the centrally housed data, rather than having the complexity and performance implications that network consensus introduces in a blockchain network.

Since it is a feature of Azure SQL Database, there is no complex figuration needed and it can be enabled in any existing Azure SQL Database.

It provides tamper-evidence capabilities in your database, enabling the ability to cryptographically attest to other parties, such as auditors or other business parties, that your data hasn&#39;t been tampered with.

![](/MPC-Images/Picture6.png)

_Figure 6: Azure SQL DB Ledger_

Ledger helps protect data from any attacker or high-privileged user, including Database Administrators (DBAs), and system and cloud administrators. Just like a traditional ledger, historical data is preserved such that if a row is updated in the database, its previous value is maintained and protected in a history table. The ledger provides a chronicle of all changes made to the database over time. The ledger and the historical data are managed transparently, offering protection without any application changes. Historical data is maintained in a relational form to support SQL queries for auditing, forensics, and other purposes. Ledger provides cryptographic data integrity guarantees while maintaining the power, flexibility, and performance of Azure SQL Database.

## Azure SQL Database Ledger vs. Azure Confidential Ledger

![](/MPC-Images/Picture7.png)

# Azure Multiparty compute decision tree.

![](/MPC-Images/Picture8.png)

# Summary

Trust is foundational in any business process that spans organizational boundaries. Azure goes beyond traditional blockchains. Microsoft Azure provides different options depending on the trust sensitivity and disrupted nature of the process.

Deciding which technology is best for your needs ultimately depends on the level of trust between parties transacting with the data, and the type of data being protected.

Azure empowers customers to apply the power of blockchain to sensitive data, simplifying solution development, reducing cost, and providing a new level of digital trust to transactions.
