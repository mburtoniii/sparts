## Utilizing a Blockchain to Establish Trust in the Open Source Software Used Across the SupplyChain

### Introduction

The main focus of this project is to deliver a Blockchain ledger that ensures a certain level of integrity is maintained with respect to the use of open source software across the supply chain.  

The lion share of today’s software is constructed from open source software.  For instance, in the data center it is typical for more than 80% of the software to be open source due to wide adoption of solutions such as Linux, various Apache offerings, MySQL, PHP, Pyhton and Node.js, to name a few. Similarly, Embedded Software, which serves as the nervous system for many commercial products, is predominately comprised of Open Source (e.g., phones, watches, cameras, drones, self-driving automobiles …). 

Modern software solutions can be viewed as being comprised of many smaller reusable software sub-components, which intrinsically represents a new kind of intellectual “part”. A software part could simply consist of a few source files that compile to create a single program or library (atomic parts) or hundreds, if not thousands, of open source sub-parts that are combined to create much larger complex parts, such as a Linux runtime or an automobile braking sub-system (composite parts). Regardless of whether a software solution is simple or complex, it has become necessary that we conceptualize each deliverable as a discrete unit or part. 

As a consequence it important that software suppliers maintain an accurate and complete list of the open source parts in their products in order to: 1) identify, review and secure the distribution rights (licenses) for each part; 2) understand the impact of an open source security vulnerability on a product (e.g., heartbleed bug); 3) enable identification of cryptography technologies (e.g., export licensing); and 4) enable accurate reporting on all open source parts as a requirement to obtain functional safety certification for safety critical product (e.g, automobiles, aircraft, elevators and medical devices).

Establishing trust on who did what, when and how within the supply chain with respect to open source is critical. That is, which suppliers created which parts and included which open source compliance artifacts for a given product. This is particularly challenging because we need to maintain global supply chain state information. We solved this problem by using Linux Foundation’s Hyperledger platform in order to create a Blockchain ledger that tracks which suppliers delivered which software parts that used which open source for which products and who delivered (or did not deliver) which compliance artifacts. 

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