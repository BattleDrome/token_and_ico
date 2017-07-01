# ICO Instructions & Tutorial:
## Contribution
### To Contribute from any “Full” wallet address:
*This includes any wallet not using a smart-contract to store your balance. So far we've tested this with Geth, Solidity, and MyEtherWallet. For any other wallet type, please either verify if it's using a smart-contract to handle your transactions/balance, OR to play it sade, use the "Execute a function" instructions below, and execute the "contribute" function to participate.*

**(do NOT use this method to send from a multi-sig contract, or any other contract based wallet. It will fail to work because of gas stipend limits.)**

1. Send Ether to the ICO contract address in the amount you would like to contribute.
ICO Contract Address: `0xeaAf270436a0ed397ED23BBF64DF7b1DCAfF142F`
2. You will be awarded balance based on your contribution, and can continue to send additional transactions in the future.
3. At any time you can check your balance, using the steps below
4. At ICO completion, you execute the “payMe” function on the contract, which will either return your ETH to you in full, in the event the ICO was unsuccessful, or send your new FAME tokens to the same address you used to send in your contribution.

*If you are using a contract, or a multi-sig wallet, or any other contract based wallet, you must instead execute the “contribute” function on the contract, sending along with it the amount of ETH you wish to contribute. Otherwise all of the above steps still apply.*

## To Execute a Function on the ICO Contract:
**Note** *If you are executing any function which returns a value of "Tokens" it will return the "raw" number of FAME tokens, which must be divided by 1,000,000,000,000 in order to get the "Actual" number of FAME tokens.*
eg: `43,750,000,000,000 = 43.75 FAME`
### For Parity Users:
1. Access the Parity Web UI
2. If you don't have a "Contracts" tab, go to the "Settings" tab, and check the box to enable it.
3. Go to the Contracts Tab
4. Click the +Watch Button
5. Choose “Custom Contract” and click Next
6. Paste the following address into the “network address” field:
`0xeaAf270436a0ed397ED23BBF64DF7b1DCAfF142F`
7. Type in “BattleDromeICO” In the “contract name” field
8. Type a description such as "BattleDrome ICO Contract" in the description field
9. Paste the ABI code from the section below into the ABI field. (note you can select it easily in chrome by tripleclicking in the text field with the ABI below)
10. Click the "add contract" button
11. Now the contract will appear in your list of saved contracts. You can click on it to view all of the functions which can be read or queried without requiring a transaction, such as the "isStarted", "isComplete", "isSuccessful", or "checkTokBalance" or "checkEthBalance" functions.
12. If you wish to execute a function requiring a transaction such as "contribute" or "payMe" you will need to click on the "Execute" button near the top of the page.
13. Then click the address you wish to execute the function from
14. And choose the function you wish to execute from the dropdown list

### For myEtherWallet 
1. Access your myEtherWallet account (note if you don't have a wallet, follow this tutorial to create a wallet: https://myetherwallet.groovehq.com/knowledge_base/topics/how-do-i-create-a-new-wallet )
2. Once you have accessed your wallet, you can navigate to the "Contracts" tab
3. Paste the ICO Contract address `0xeaAf270436a0ed397ED23BBF64DF7b1DCAfF142F` into the "Contract Address" field
4. Paste the ABI JSON into the ABI/JSON Interface Field (copy from below, you can easily select the whole ABI by triple-clicking inside the field in chrome)
5. Click the "Access" button. This will then pop up below a "Read/Write Contract" section, with a "Select a Function" dropdown.
6. You can now select the function you wish to access using the dropdown, and it will either show you the value of the query (for example if you check isStarted, it will return "True" or "False") or it will present you with a "Write" button.
7. Click the "Write" button, and it will prompt you any variables to provide, and an amount of ether to send. So for example if you are calling "Contribute" you can send in Ether this way to contribute to the ICO. 
8. If you wish to check the balance of a contributor, choose checkEthBalance function, and provide the address you want to check.

*Note: For myEtherWallet we are working on having the token and ICO contract added as standard "default" contracts. This will greatly simplify the process, hopefully very soon. These instructions will be updated once this is confirmed.*


### For Geth Users:
Coming Soon!

## ICO Contract Function Description:
Variable/Function | Purpose
--- | ---
`ratio` | The number of FAME tokens issued per ETH
`minimumPurchase` | Minimum number of ETH accepted in a contribution transaction
`startBlock` | The Block Number at which the ICO officially begins accepting contributions
`duration` | The number of Blocks that the ICO will run for
`fundingGoal` | The minimum number of Ether that the ICO must receive in contributions in order to be considered "Successful"
`fundingMax` | The absolute maximum number of Ether that the ICO contract will accept, if this number if reached, the ICO will end immediately and be declared a success.
`devRatio` | The ratio of Purchased Tokens to one Dev Token. In other words, if devRatio = 20, then for each 20 Tokens Sold, 1 Dev Token will be issued (or 5% extra)
`tokenAddress` | The Address of the ERC20 FAME Token Contract
`escrow` | The Address of our Escrow Provider. This is the hard-coded address that all final Ether will be sent to upon Successful completion of the ICO
`creator` | This is the Address of the Developer Account. This is where the Developer Tokens will be sent when minted, OR in the event the ICO is not a success, this is where ALL minted FAME will be sent back.
`savedBalance` | The final Ether Balance of the Contract. This is saved so that once withdrawls happen, we can look back and determine what the balance was easily.
`contribute()` | send in contribution (send ETH along with execution)
`isStarted` | Boolean (True or False) is the ICO started?
`isComplete` | Boolean (True or False) Is the ICO Complete?
`isSuccessful` | Boolean (True or False) Is the ICO past it's minimum goal?
`checkEthBalance(address)` | Returns the number of Ether Balance held for `account`
`checkTokBalance(address)` | Returns the number of Token Balance held for `account`
`checkTokSold` | The total number of Tokens Sold via contributions
`checkTokDev` | The total number of Tokens being issued to Developers (based on dev Ratio)
`checkTokTotal` | The Overall Total number of Tokens being minted (sold + dev). *Note if successful, any tokens beyond this number are burned!*
`percentOfGoal` | The Percentage of the Minimum Goal we have achieved.
`payMe` | Each Contributor must call this function after ICO completion to either get their tokens sent if the ICO was successful, or get a full refund of all of their Ether if the ICO was not successful.
`payCreator` | This function is called to pay out the Creator (if ICO was a success, Ether is sent to escrow, if ICO was not a success, all Tokens sent to creator address).

## Contract ABI
```
[{"constant":true,"inputs":[],"name":"creator","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"duration","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"devRatio","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"fundingMax","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_contributor","type":"address"}],"name":"checkTokBalance","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"startBlock","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_contributor","type":"address"}],"name":"checkSavedEthBalance","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"isStarted","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"checkTokDev","outputs":[{"name":"total","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"ratio","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"savedBalance","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"fundingGoal","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"checkTokSold","outputs":[{"name":"total","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"checkTokTotal","outputs":[{"name":"total","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_contributor","type":"address"}],"name":"checkEthBalance","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"tokenAddress","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"tokenBalance","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"creatorPaid","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"minimumPurchase","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"isComplete","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"Token","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"contribute","outputs":[],"payable":true,"type":"function"},{"constant":false,"inputs":[],"name":"payMe","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"payCreator","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"escrow","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"percentOfGoal","outputs":[{"name":"goalPercent","type":"uint16"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"isSuccessful","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"inputs":[],"payable":false,"type":"constructor"},{"payable":true,"type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_contributor","type":"address"},{"indexed":true,"name":"_value","type":"uint256"},{"indexed":true,"name":"_timestamp","type":"uint256"}],"name":"Contribution","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_receiver","type":"address"},{"indexed":true,"name":"_value","type":"uint256"},{"indexed":true,"name":"_timestamp","type":"uint256"}],"name":"PayTokens","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_receiver","type":"address"},{"indexed":true,"name":"_value","type":"uint256"},{"indexed":true,"name":"_timestamp","type":"uint256"}],"name":"PayEther","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_value","type":"uint256"},{"indexed":true,"name":"_timestamp","type":"uint256"}],"name":"BurnTokens","type":"event"}]
```
