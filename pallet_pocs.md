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

1. Fields to be added to Pallet-contracts <br>
Every newly deployed contract will have three extra storage fields: 
* scarcity (mapping field) - This field will be used to calculate the PoCS stake score. It will be updated anytime a transaction executes which corresponds to that contract. To calculate this we will use 
    * weight_history (Weight) - Total weight of a transaction executed. 
    * reputation (u64) - a parameter we assign to calculate the reputation of contract which depends on number of times it is called by a user or any other contract  
    * recent_blockheight (BlockNumberFor) - This is introduced to prevent vulnerabilities like DDoS attack
* delegateTo (AccountId) - Set by the deployer and for the consensus to know who is the deployer.  Only deployer can change this field
* delegateAt (Blocknumber) - The field is the current block height when the delegateTo field is updated

2. Staking mechanism: <br>
In the context of Substrate, the integration of Babe and Grandpa protocols, alongside the Staking Pallet, complements the PoCS mechanism 
*  Babe's deterministic block production process aligns with PoCS's commitment to security. Validators with higher reputation and weight history, as determined by the scarcity mapping, are incentivized to actively participate in proposing and validating blocks
* Grandpa Protocol : Just like proof of stake Grandpa, with its finality gadget based on GHOST protocol, adds an extra layer of security. Once blocks are finalized, they become irreversible, providing an additional level of confidence in the integrity of the blockchain. 
* Staking Pallet (Validator Selection): The Staking Pallet integrates with PoCS as validators selected based on their scarcity scores, are entrusted with the responsibility of proposing and validating blocks. This delegation ensures that validators with a proven track record of actively participating in the network are granted the authority to contribute to the consensus process.

<b> Use-Case Diagram </b> <br>
<i>INSERT LINK</i>

<b>What your project is not or will not provide or implement</b><br>
We have structured our implementation into 3 milestones. In this grant our focus is to develop a first version which would implement pallet-contract to calculate the  staking score in simplistic yet efficient way with above mentioned fields. It would handle 
* Stake score update when deployer deploys contract 
* Stake score update when a user calls contract function or other contracts call the contract function
* Integration with proof of stake in substrate.

We will continue to research as we implement, not all vulnerabilities might be handled in the very first version with above functionalities. But we will extend it to our future plans or extend the grants after accomplishing the milestones and scope in this proposal.


### Ecosystem Fit
Our project integrates with the Substrate framework, providing a modular and adaptable foundation for our innovative consensus mechanism. This positions us for potential integration into the broader Polkadot ecosystem, aligning with the vision of cross-chain interoperability through parachains.


<b> Target Audience </b><br>
Our primary target audience includes developers within the blockchain space, particularly those focused on Polkadot ecosystem contract and dapp developers. Additionally, our project aims to serve the broader community of blockchain enthusiasts seeking to engage with a dynamic and secure consensus mechanism.

<b> What need(s) does your project meet? </b><br>
Our project addresses the critical need for a consensus mechanism that is developer-centric and tailored to the nuances of smart contract interactions. By incentivizing developers through our innovative Proof of Contract Stake (PoCS) model, we empower them to actively participate in securing the network. This not only enhances network security but also fosters a more collaborative and inclusive blockchain ecosystem. Furthermore, our integration with Substrate and potential linkage to the Polkadot network addresses the need for cross-chain interoperability, opening up a realm of possibilities for decentralized applications and services.

<b> Similar Projects (How it is different) </b><br>
There are no similar projects in polkadot as well as other blockchains as of now since its proposing a new consensus. 

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

- **Total Estimated Duration:** 16 weeks
- **Full-Time Equivalent (FTE):**  3
- **Total Costs:** 30,000 USD

Upfront ask - We have a minimal upfront ask of 2k USD for our resource utilization in research phase. 

### Milestone 1 - Simple Contract Staking with Aura Compatibility

- **Estimated duration:** 4 weeks
- **FTE:**  3
- **Costs:** 6,500 USD

| Number |        Deliverable        |                                                                                                             Specification                                                                                                             |
|--------|:-------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 0a.    | License                   | Apache 2.0  Unlicense                                                                                                                                                                                                  |
| 0b.    | Documentation             | We will provide both inline documentation of the code and a basic tutorial that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c.    | Testing | Core functions will be fully covered by primary unit tests to ensure functionality                                |                                                                                                                      |
| 1.     | Modified Substrate pallet-contract:      | We will create customized version of Substrate `pallet-contracts` that will include the fields required to calculate the staking score. This will be updated whenever a deployer deploys a new contract. showcase the demo on polkadot frontend with new added fields and their values.                                              |

### Milestone 2 — External Calls Monetization Model

- **Estimated duration:** 5 weeks
- **FTE:**  3
- **Costs:** 9,500 USD

| Number |        Deliverable        |                                                                                                             Specification                                                                                                             |
|--------|:-------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 0a.    | License                   | Apache          |
| 0b.    | Documentation             | We will provide both inline documentation of the code and a basic tutorial that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c.    | Testing and Testing Guide | Core functions will be fully covered by comprehensive unit tests to ensure functionality tests.  |
| 1.     | Cont. Modify Substrate pallet-contract or other relevant pallets    | We will handle external calls in this milestone and implement subsequent updates on scarcity mapping. This method should also be compatible for our next milestone of integrating with staking, so we will be overviewing proof of staking implementation in polkadot |

### Milestone 3 — Integrate with BABE+GRANDPA to add proof of stake

- **Estimated duration:** 7 weeks
- **FTE:**  3
- **Costs:** 12,000 USD

| Number |        Deliverable        |                                                                                                             Specification                                                                                                             |
|--------|:-------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 0a.    | License                   | Apache   |
| 0b.    | Documentation             | We will provide both inline documentation of the code and a basic tutorial that explains how a user can use the consensus |
| 0c.    | Testing and Testing Guide |Unit tests for the consensus to check its robustness  |
| 0d.    | Launch pallet                    | We will launch our genesis block with the new consensus. This can be sister chain to Polkadot chain |
| 0e.    | Publish yellow paper                   | We will publish our research as yellow paper  |
| 1.     | Integrate staking       |   Integrate BABE+GRANDPA to select validators based on our scarcity mapping. Polkadot frontend to show subsequent updates  |
            
## Future Plans

- Once completed with this grant milestones, we would be working on further research and moving towards testnet launch as a sister chain to Polkadot. Since it is first of its kind we will be actively discussing our future plans and research directions with the community. 

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
