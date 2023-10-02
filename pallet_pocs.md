# Proof of Contract Stake (Pallet)

- **Team Name:** Auguth Tech
- **Payment Address:** Fiat (DD.MM.YY, HH.MM)
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):**  2

### Overview

<b> One Sentence Summary </b><br>
<i>Forging Secure Public Networks through Staking Smart Contracts</i>

<b>Brief Description</b><br>
Blockchain technology, with the introduction of Ethereum chain, significantly impacted the ecosystem by introducing the concept of smart contracts. These self-executing contracts have significantly enhanced the functionality and versatility of blockchain networks, opening up a wide array of decentralized applications and use cases. However, despite this pivotal development, there has been a notable absence of a consensus mechanism that places smart contracts at its core. Recognizing this critical gap, we present Proof of Contract Stake (PoCS) – The First Developer Centric Concensus. 

PoCS is an innovative staking system that leverages contract gas history to select block producers. PoCS marks a significant advancement by seamlessly integrating elements of both proof-of-work and proof-of-stake. We have introduced a novel concept of 'code-mining' that incentivizes developers to actively participate in securing the network. By aligning the interests of developers with the network's security, PoCS introduces a dynamic where smart contract creators play a vital role in consensus. In addition, PoCS implements a robust system of 'stake scoring', taking into account factors such as contract age, reputation, and gas utilization. This design not only fortifies the network against collusion attacks but also ensures a fair and secure environment for all participants. It also addresses a longstanding concern in blockchain consensus models – the 'nothing at stake' attacks . By introducing a non-fungible, non-transferable unit of scarcity for staking, PoCS effectively mitigates this vulnerability, providing a solid foundation for a secure and reliable network. In addition, the stake accumulation attack in PoCS is time constraint and patterned which can be easily detected. This escalates costs over time and cannot be expedited with any external resources.

<b> Substrate Integration</b><br>
We have chosen Substrate as the foundation for our project's development due to a multitude of compelling reasons. Substrate provides a modular framework for blockchain development platform. By leveraging Substrate's extensive capabilities, we could design our innovative consensus mechanism effectively as it aligns perfectly with our goal of creating a dynamic and adaptable blockchain network. Additionally, our project envisions a future where cross-chain interoperability is a key component. This vision closely resonates with the Polkadot ecosystem, which provides of parachains ecosystem. The parachain ecosystem would help us design a robust implementation and test its interoperability. While this part is still under active research, we foresee our consensus mechanism being well-suited for integration into the broader Polkadot network. Besides, one of the most noteworthy features of Substrate is its native support for WebAssembly (Wasm) built contracts. Considering the research and future extensions, we wanted to develop the consensus on Wasm built contracts. 


<b> Team Interest</b><br>
Our interest in this project was sparked by a genuine enthusiasm for blockchain technology. Initially, we began as web3 developers, participating in hackathons and exploring dapp development. However, during one of these hackathons, we encountered notable limitations with the Ethereum Virtual Machine (EVM). Recognizing the need for a more robust solution, our research head, Joby Reuben, who has been researching blockchain for over 2 years, began to delve into various consensus mechanisms. Proof of Contract Stake (PoCS) stemmed out from his previous research and emerged as a promising avenue, and we've been dedicated to refining this concept for the past eight months.As we conducted our research, we identified the need for a WebAssembly (Wasm) environment to effectively implement this mechanism. This led us to the Polkadot ecosystem, which provided a suitable environment for our vision. 

In this landscape of ever-evolving blockchain technology we are poised to reshape the way we approach smart contracts and network security. The grants will help us validate our research and make it more robust with the para chain ecosystem. Thus, through this support, we aim to bring our vision to delivering a practical tool to the community and contributing to the ongoing evolution of blockchain technology. 
### Project Details
<b>Prior work - Research </b><br>
Our PoCS research is documented here <i>INSERT LINK</i>. We have done some simulations to show how PoCS would like if Ethereum used PoCS from genesis block using BigQuery. Check it out here <i>INSERT LINK</i>.

<b> Substrate implementation Design</b><br>
To implement PoCS on substrate we will be modifying `pallet-contracts` and  `pallet-staking` under APACHE 2.0 lisence. We decided to proceed with this approach since both of these pallets provide the primary required functionalities. In addition to this substrate also provides a elaborate user interface for integrating contracts which will ease out our implementation. Since we will be implementing it as staking mechanism, we will be using `pallet-staking` with BABE + GRANDPA protocols to modify proof of stake. 

<b> Core functionality</b><br>
Every newly deployed contract will have three extra storage fields: 
* scarcity (mapping field) - This field will be used to calculate the PoCS stake score. It will be updated anytime a transaction executes which corresponds to that contract. To calculate this we will use 
    * weight_history (Weight) - Total weight of a transaction executed. 
    * reputation (u64) - a parameter we assign to calculate the reputation of contract which depends on number of times it is called by a user or any other contract  
    * recent_blockheight (BlockNumberFor) - This is introduced to prevent vulnerabilities like DDoS attack
* delegateTo (AccountId) - Set by the deployer and for the consensus to know who is the deployer.  Only deployer can change this field
* delegateAt (Blocknumber) - The field is the current block height when the delegateTo field is updated

<b> Use-Case Diagram </b> <br>
<i>INSERT LINK</i>

<b>What your project is not or will not provide or implement</b><br>
We have structured our implementation into 3 milestones. In this grant our focus is to develop a first version which would implement pallet-contract to calculate the  staking score in simplistic yet efficient way with above mentioned fields. It would handle 
* Stake score update when deployer deploys contract 
* Stake score update when a user calls contract function or other contracts call the contract function
* Integration with proof of stake in substrate.

We will continue to research as we implement, not all vulnerabilities might be handled in the very first version with above functionalities. But we will extend it to our future plans or extend the grants after accomplishing the milestones and scope in this proposal.


### Ecosystem Fit

#### For Polkadot & General

#### Target Audience

#### Meeting needs

#### Similar Projects (How it is different)

## Team :busts_in_silhouette:

### Team members

- Team Leader: Purva Chaudhari
- Team Members : Ajay Joshua (Development) , Joby Reuben (Research)

### Contact

- **Contact Name:** Purva Chaudhari
- **Contact Email:** purva@auguth.com
- **Website:** [pocs-consensus.xyz](https://pocs-consensus.xyz)

### Legal Structure

- **Registered Address:** Tamil Nadu, India - 624619
- **Registered Legal Entity:** Auguth Tech Pvt Ltd (CIN : U72900TZ2019PTC033024)

### Team's experience

- **Purva Chaudhari**:
- **Ajay Joshua**:
- **Joby Reuben**:

### Team Code Repos

- https://github.com/Purva-Chaudhari
- https://github.com/I-Corinthian

### Team LinkedIn Profiles

- https://www.linkedin.com/in/purva-chaudhari-02b12b178/
- https://www.linkedin.com/in/ajay-joshua-a8a250176/
- https://www.linkedin.com/in/jobyreuben
  
## Development Status :open_book:

#### [PoCS Github Repo](https://github.com/auguth/pallet_pocs)

#### [Research & Documentation](https://pocs-consensus.xyz)

## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:** 15 weeks
- **Full-Time Equivalent (FTE):**  3
- **Total Costs:** 30,000 USD

### Milestone 1 - Simple Contract Staking with BABE & Aura Compatibility

- **Estimated duration:** 5 weeks
- **FTE:**  3
- **Costs:** 12,000 USD

| Number |        Deliverable        |                                                                                                             Specification                                                                                                             |
|--------|:-------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 0a.    | License                   | Apache 2.0 / GPLv3 / MIT / Unlicense                                                                                                                                                                                                  |
| 0b.    | Documentation             | We will provide both inline documentation of the code and a basic tutorial that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c.    | Testing and Testing Guide | Core functions will be fully covered by comprehensive unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests.                                                                       |
| 0d.    | Docker                    | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone.                                                                                                                         |
| 0e.    | Article                   | We will publish an article/workshop that explains [...] (what was done/achieved as part of the grant). (Content, language and medium should reflect your target audience described above.)                                            |
| 1.     | Substrate module: X       | We will create a Substrate module that will... (Please list the functionality that will be implemented for the first milestone. You can refer to details provided in previous sections.)                                              |

### Milestone 2 — External Calls Monetization Model

- **Estimated duration:** 6 weeks
- **FTE:**  3
- **Costs:** 12,000 USD

| Number |        Deliverable        |                                                                                                             Specification                                                                                                             |
|--------|:-------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 0a.    | License                   | Apache 2.0 / GPLv3 / MIT / Unlicense                                                                                                                                                                                                  |
| 0b.    | Documentation             | We will provide both inline documentation of the code and a basic tutorial that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c.    | Testing and Testing Guide | Core functions will be fully covered by comprehensive unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests.                                                                       |
| 0d.    | Docker                    | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone.                                                                                                                         |
| 0e.    | Article                   | We will publish an article/workshop that explains [...] (what was done/achieved as part of the grant). (Content, language and medium should reflect your target audience described above.)                                            |
| 1.     | Substrate module: X       | We will create a Substrate module that will... (Please list the functionality that will be implemented for the first milestone. You can refer to details provided in previous sections.)                                              |

### Milestone 3 — Substrate PoCS Node Template

- **Estimated duration:** 4 weeks
- **FTE:**  3
- **Costs:** 6,000 USD

| Number |        Deliverable        |                                                                                                             Specification                                                                                                             |
|--------|:-------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 0a.    | License                   | Apache 2.0 / GPLv3 / MIT / Unlicense                                                                                                                                                                                                  |
| 0b.    | Documentation             | We will provide both inline documentation of the code and a basic tutorial that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c.    | Testing and Testing Guide | Core functions will be fully covered by comprehensive unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests.                                                                       |
| 0d.    | Docker                    | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone.                                                                                                                         |
| 0e.    | Article                   | We will publish an article/workshop that explains [...] (what was done/achieved as part of the grant). (Content, language and medium should reflect your target audience described above.)                                            |
| 1.     | Substrate module: X       | We will create a Substrate module that will... (Please list the functionality that will be implemented for the first milestone. You can refer to details provided in previous sections.)                                              |
            
## Future Plans

**Short Term**
- Sample 1
- Sample 2

**Long Term**
- Sample 1
- Sample 2

## Referral Program :moneybag: 

- **Referrer:** [Name](https://github.com/<account>)
- **Payment Address:** 

## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** 

Through recommendation from [Builders Tribe](https://buidlerstribe.com/) to apply for W3F grants

**If there are any other teams who have already contributed (financially) to the project.**

No, Self Funded

**Previous grants you may have applied for**

No
