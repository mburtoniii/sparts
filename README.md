## Utilizing a Blockchain to Establish Trust in the Open Source Software Used Across the SupplyChain

### Introduction

The main focus of the project is to deliver a Blockchain ledger to track the open source components used across a supply chain. Tracking the open source used is necessary to understand which components are used in any manufactured product. It is important that software suppliers maintain an accurate and complete list of the open source parts in their offerings in order to: 1) identify, review and secure the distribution rights (licenses) for each part; 2) understand the impact of an open source security vulnerability on a product; 3) enable identification of cryptography technologies (e.g., export licensing); and 4) enable accurate reporting on all open source parts as a requirement to obtain functional safety certification for safety critical products (e.g, medical devices, aircraft, autonomous driving vehicles, elevators and so forth).

Ultimately a Blockchain ledger is used to established trust on who did what, when and how within the supply chain  That is, which suppliers created which parts and included which open source compliance artifacts for a given product. This is particularly challenging because a mechanism is required to maintain a global state across the supply chain ensure accountability. We solved this problem by using Linux Foundation’s Hyperledger project's Sawtooth platform to construct a Blockchain ledger that tracks which suppliers delivered which software parts that used which open source for which products and who delivered (or did not deliver) which compliance artifacts. We were required to define a new construct , the **Compliance Envelope**, which represents a standard method of collecting, indexing and bundling the compliance artifacts in such a way that the artifacts can be delivered as a single unit. We use the Ledger to associate a given compliance envelope to the respective software part and supplier. 

### Example Illustration

The biggest challenge to obtaining a complete and accurate Open Source Bill of Materials (OSS-BOM) for a product (along with the other compliance artifacts) arises because software parts are provided by multiple different suppliers. Consider the simple example illustrated below  where three different suppliers provide software parts for the manufacturing of a video camera V sold by manufacturer M. Supplier S1 delivers the microprocessor accompanied by the firmware and software drivers. Supplier S2 assembles and delivers the Linux runtime operating system and Supplier S3 delivers the applications that manage the camera display, menu and various functions. Ideally, when camera V ships, it should be accompanied by a single compliance envelope that contains, as a minimum, a list of all the open source parts incorporated by the various suppliers (OSS BOMs) and the mandatory source code and legal notices.

![video-camera-arch](C:\Users\mgisi\Documents\Users\mgisi\gospace\src\sparts\docs\images\video-camera-arch.png)

​	**Figure 2**: Video camera V, suppliers, parts, envelopes and open source artifacts 

Manufacturer M needs a way to trust that 1) each supplier has prepared the required compliance artifacts for their respective contribution; 2) in the event that an artifact was missing or not properly prepared (e.g., source), we can identify who is responsible for remedying the situation; and 3) no one supplier can sabotage (hack) the integrity of the compliance artifacts of another supplier. All in all, tracking the artifacts across the supply chain to establish trust that each supplier did the right thing presents a formidably challenge.

The SParts project developed a Blockchain Ledger to manage this complexity, while simultaneously establishing greater trust around the use of open source software. It serves as a global data store that tracks the state of suppliers, their list of software parts, the corresponding envelopes and envelope content. Typical transactions performed on the ledger include adding a part to a supplier’s parts list, assigning an envelope to a software part, and adding, updating and removing artifacts from an envelope.

<center><img src="./docs/images/blockchain-illustration.png" width="642" height="443" /><center>

Figure 3 illustrates ledger entries that represent the parts for video camera V presented in Figure 2. Transactions 101 through 104 represent software part 37 and transactions 105 through 110 represent part 101. Transaction 111 illustrates that an additional artifact was later added to the part 37 envelope and transaction 112 illustrates that the source code was updated for part 101’s envelope. In the first instances, Supplier S1 forgot to include a notice artifact but was able to remedy it after the fact. In the second instance, Supplier S2 was able to determine that some of the mandatory/required source code was missing and to efficiently remedy the issue by simply updating the ledger. By recording software part information in the ledger, customers of both suppliers S1 and S2 would automatically receive the updates. When manufacturer M ships the video camera, they could query the ledger to obtain the latest and most comprehensive collect compliance artifacts.

### Project Organization

To run a blockchain managed network we developed the following components: 

1. **Blockchain** **Ledger** (ledger/) - The ledger, built using the Hyperledger Project's Sawtooth platform,  tracks all the open source components and the meta data about the compliance artifacts of the open source parts to ensure the integrity of all the components used. The ledger is accessible via a RESTful API.
2. **Admin** - Two applications are provide that provide supply chain  network administrative services: 
   - **Conductor** (conductor/) - system service responsible for providing services, monitoring and managing the different supply chain components (ledger and applications).  This application is required to be up and running. 
   - **Ledger Dashboard** (admin/) - an application that enables one to monitor the Ledger content
3. **Applications**  (apps/) The apps directory contains demonstration applications that provide examples of applications to utilize the ledger:
   {0}. **SParts Software Parts Catalog** - A website application that provides a catalog of a collection of software parts  that connects to the supply chain network that are tracked in the ledger. 

In addition to the above core services the following important data objects are defined. These are the entities that are tracked within the ledger:

- **Suppliers** - each supplier needs to register with the ledger using the RESTFUL api. 
- **Parts** - The supplier needs to register the software parts they want tracked on the ledger. 
- **Compliance artifacts** - artifacts prepared to satisfy the license obligations for the different opens source components used. They typically include obligatory/mandatory/required source code, written offers for source, license notices and/or copies of licenses. The collection could also include information that, although not required by a license, provides important insight, such as OSS BOM, SPDX licensing data and cryptography information

- **Compliance Envelope** - a construct that represents a standard method of collecting, indexing and bundling the artifacts in such a way that they can be delivered as a single unit. Regardless of whether a software offering is a simple atomic part (e.g., software library), or a more complex one such as the software runtime that controls a consumer device, the envelope contains a rich collection of information that represents all the open source parts that the offering was comprised of. 


### Getting Started

See the Getting Start document in the project's documentation directory (/doc). 