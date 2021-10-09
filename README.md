# blockchain-developer-bootcamp-final-project
Final Project for Xenofon Kontouris for Consensys Blockchain Academy (Fall 2021) - Deployment of claims tokens (ERC-22222) for a shared pool of resources.

EXPLAINATION OF THE PROJECT:
The problem that this project is trying to solve is the fair and public distribution of funds to an ever changing pool of assets and users through ERC-2222 claims tokens. 

The problem is simple; assume an initial fund of X which is deployed across the Decentralized Finance space and has yielded returns. How do you measure the claim to future returns of users which are ever changing, and of funds which are as volatile as the basic crypto asset? This becomes mathematically  extremely burdensome, and highly complex to account for. 

EXAMPLE OF THE PROBLEMS SOLVED BY ERC-2222:
To explain this further, consider the below hyper simplified example; a situation where the initial 10 participants of a fund agree to provide 10USD in capital each. The total of the fund is now 100USD, and each participant owns 10 claims tokens, valued at 1USD each. All initial participants have a clear and fair claim to these assets - owning 10% of all claims tokens provides the token holder with a claim of 10% of all capital within the fund. 

A time period passes, ay one month, and the funds have been deployed in an LP which has yielded 10% returns to the original fund. Now the fund is worth 110USD, and each claim tokes is worth 1.1USD each. Each participant still owns 10 tokens each. Pretty simple this far. However this becomes more complex when additional capital is added by new participants on an asynchronous basis. 

Continuing, two additional participants decide to join in the fund at that new time period, providing 20USD each. Now the total of the fund is 150USD, where 12 participants have an uneven share of the claim to these funds and the new participants own (20/1.1 = 18.181818..) 18.182 tokens each. That means that the total amount of claims tokens deployed equals ((10 x 10) + (18.182 x 2) => 100 + 36.364 = 136.364) 136.364 times the token value of 1.1USD each (136.364 x 1.1USD = 150.0004USD) ~150USD in total 

//* please note that the 0.0004 extra cents here are due to mathematical simplification. This simplification will provide us a number of misalignments in the math following the example - another problem that will be solved by the implementation of ERC-2222.

Another time period passes, again one month, and yet again a 10% return to the capital collected is paid out. The total of the fund has increased to (150 x 1.1 = 165USD) 165USD. The total tokens are still 136.364, making each token valued at 1.21USD each. Now, instead of new additions to the fund, two of the original members decide to remove half of their capital; 5 out of their 10 tokens. That means that 10 tokens are burned, removing 10 * 1.21 = 12.1 USD from the fund's total, making it (165 - 12.1 = 152.9USD) 152.9 USP and each token still worth the same 1.21USD each. 

At this state, there are 2 fund participants that own 5 claims tokens each, 2 other fund participants that own 18.182 claims tokens each, and 8 participants that own 10 claims tokens each. 

As you understand, the above calculations are hyper simplified compared to realistic usecase. In the above example, we have set some steady parameters, like a standard interest period and a standard return for each time period. We have also started the fund with simple asset distribution, and we've not accounted for either a drop in total funds due to a misinvestment and market volatility, nor have we accounted for complex additions to the total fund in truly asynchronous time periods. 

In the real cryptoasset marketplace, the usage of ERC-2222 can help us account for more complex withdraws in non-fixed time periods, highly complex token distribution schemes, dynamic minting and removing of claims tokens and fund tokens when requested by the user, and the accounting of all of the above through the simple implementation of this one smart contract. This is a fantastic usecase that indicates the value of using smart contracts in everyday financial transactions. 

In addition to the above, a number of parameters and mechanics can be placed within the claim token mechanics. An example of this can be implementation of strict time commitments to the investment of capital within this share fund (lock-up period), and the "taxing" of premature withdraws (or even standard withdraws) of user funds. These mechanics can be used to achieve a number of goals. An example of this can be the buying and burning of another asset any time that there is a taxing event of withdraws of funds. 

WALKTHROUGH OF HOW THIS PROJECT WILL LOOK LIKE FOR THE USER: 
1- Visit website and connect to MetaMask; ideally on a sidechain, like xDai
1- KYC yourself and gain an ID NFT **(Might Skip)**
 -- Upload documents and hash them through a widget
 -- Receive NFT of the widget to your wallet
2- Place funds into a shared pool of resources
 -- See listed options and agree with T&C  
3- Control when to remove the funds (Options to remove prematurely and how that would cost)
 -- Showcase clear performance and withdraw penalty
  -- Allow for option to withdraw now or as soon as penalty is withdrawn (These requests should be monitors by the chain)
 -- Automatically restake assets if not withdrawn by user

PSEUDOCODE & FLOWCHART:
-- TBD

ISSUES TO SOLVE:
Although this Token Standard has a lot of existing documentation and an active team of developers that can help clarify things and simplify the implementation of this project, the token standard in not yet on OpenZeppelin and the development of the code is ongoing, therefore it has not been fully tested and security issues might emerge. 
The question of gas requirements is also not clear - will this token be ultra expensive to mint and use? I don't yet know. 
Lastly, the front end requirements of the final project are ones that I have not reviewed at all and might emerge as a legitimate roadblock. 

FRONTEND DESIGN SPECS: 
A very simple interface. As soon as user lands on the page, the site should ask him to connect his MetaMask (or other) wallet. If the user is in the incorrect network, then the site should provide him a link to a guide on how to add sidechains to his MetaMask (both in writing and on video). 

KYC needs come first - Before clicking on the "deposit to fund" button, a pop-up will emerge asking the user to make sure he uses a fresh wallet address and then ask for the upload of certain documents needed for KYC. These docs are: 
-- First and Last Name
-- Address
-- Passport Photocopy
-- Bill with address (in any language) 
-- IP address (automatically collected)
-- System and Browser information (automatically collected) 

All the above documents will be hashed on the spot, and an NFT of the hash, plus the list of documents used (and their file titles) will be made into two KYC NFT that will be sent to the wallet address of the user and the wallet address of the Dapp. The list of documents and data provided will be in the hidden section of the ID NFT that only NFT owners can view. The user will cover the transaction cost of these transactions. 

As soon as he is connected and KYC'd, the site should indicate a visual representation of the fund. My vision is to use a water tank. As soon as he inputs capital into this fund, the water tank will indicate the potion (percentage) of the fund that owned by the MetaMask wallet address by changing the color of the percentage of the fund that the address owns. 

Next to the water tank, a list of his fund contributed, plus the lifetime return of his funds will be listed. Alonside this, the number of claims tokens in the wallet of the user will be visible, and the next penalty-free withdraw period will be listed. If the user aims to withdraw his funds before the penalty-free destribution time period, a clear list of additional fees will be sent out to him as a warning. The pop-up will offer three options: 
-- Cancel Withdraw
-- Claim withdraw in the next penalty-free destribution period
-- Proceed with Withdraw now

Whichever button the user clicks will be the command that the Dapp will send to his wallet. 

ADDITIONAL RESOURCES AND LINKS: 
1. ERC-2222 GitHub Page: https://github.com/ethereum/EIPs/issues/2222![Consensys Academy - Xenofon Kontouris (Final Project Diagrams)](
2. Written Guide on MetaMask Network Additions (xDai): https://www.xdaichain.com/for-users/wallets/metamask/metamask-setup
3. Video Guide on MetaMask Network Additions: https://www.youtube.com/watch?v=R3aMKqSsX1Y
4. Draw.io of the Front End Process (Attached: https://user-images.githubusercontent.com/11343228/136669400-6728c1e2-56a6-4895-b1af-a999a2fd20a3.png)) 
