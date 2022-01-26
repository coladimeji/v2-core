# Steps to ReCreate Uniswap V2

Forking A devi project in ths case Uniswsap V2
Copy paste or clone original code
customize code
Deploy smart contracts + frontend
Boosstap Liquidity

Fork Uniswap smart contract

 The first smart contract I we need is factory. This is used to create market for different pairs such as Dai Ether, and so on. This smart contract is located in the uniswap v2 core repo in the organization of uniswap on github.
 Open Terminal and create a project with mkdir example uniswap1
 cd to the folder
insert EXAMPLR: git clone https://github.com/Uniswap/uniswap-v2-core
click enter
NOTE: when you have the code downloaded locally you can start your customization.
You can cd to the folderto see what was downloaded by writing
cd uniswap-v2-core then cd contracts/ ls -1
NOTE: List of all dependables such as uniswapV2factory.sol, uniswapV2Pair.sol test, interface-etc. will show.
NOTE: If you want you can change the name of the project but for me am keeping it simple.
 go back to github page and open another dependencies called periphery. It allow you to use the dependencies more easily
another important file we need is router, it allows you to navigate the uniswap ecosystem easily
 cd .. cd .. back to the  rootfolder and 
 copy the url and paste on the terminal :git clone https://github.com/Uniswap/uniswap-v2-periphery
 click enter
 cd uniswap-v2-periphery
then ls contracts/
NOTE: all contract directories such as UniswapRouter.sol,UniswapV2Migrator.sol etc will show.
 now cd .. 
to go back to the folder
NEXT
DEPLOY SMART CONTRACTS TO THE BLOCKCHAIN

 for the deployment I will be using Truffle suite.
NOTE: Truflle uses node.js so I need to install that first then,
 npm install -g truffle
 click enter
 after download, create a new file called core
cd to core
 inside core/ we initailize new truffle project
truffle init
 click enter
ls -1
NOTE:Now you will see we have files such as contracts migrate test truffle-config.js in the folder
NOTE: copy paste core repo of uniswap
 cp -r ../uniswap-v2-core/contracts/* contracts
 click enter
 ls -1 contracts/
 click enter
NOTE: now all directories such as Migration.sol, UniswapV2ERC20.sol, interface etc will show.
Now we need to create an immigration file to tell truffle how to deploy the core contract of uniswap
touch migrations/2_deploy_contracts.js
Then open th js folder
 vim migrations/2_deploy_contracts.js
open th template
insert code inside deploy.js
 add code to UniswapFactory

Go back to Terminal and create smart contracts 
 navigate back to cd uniswap/core
click enter
At the root of the project, initialize npm init -y
click enter
now we install @openzeppelin library of solidity 
npm install @openzeppelin/contracts@2.5.1
NOTE: we need to be specific in the version of solidity in order to be compatable.
click enter
 create 2 contracts
touch contracts/Token1.sol
touch contracts/Token2.sol
vim contracts/Token1.sol
click enter
 add code to token1 copy and paste in token2.. change code to token 2
 navigate to Truffle folder scroll down the page, change the correct version of solidity example, 0.5.16
 Now we are deploying to the local environment using ganache
 npm install -g ganache-cli
 click enter
 ganache-cli
NOTE: Ganache cli has started
 open second Terminal
``truflle migrate --reset
 check the result to make surue you see the sddrees of uniswap factcory
NOTE: next we going to deploy router smart contracts
 insert cd ..
 mkdir periphery
NOTE: create a folder called periphery exactly as we did for core
from uniswap/core 
 cd ..
 mkdir periphery/
 cd periphery
.inside the periphry folder we need to install 
NOTE:I need to seperate core and periphery contracts becuasethey use diffrent version of solidity thier is no way to deal with this easily in a single truffle project hence we create a folder and install another version of truffle.
 truffle init
NOTE: you will see: init succesful sweet

Next, Lets copy over the contracts
 cp -r ../uniswap-v2-periphery/contracts/* contracts
 click enter
ls -l contracts/
NOTE: you will see Migrations.sol UniswapsMigrator.sol etc.
The istall need some npm packages so we install npm but first we init the project
npm init -y
 we need to:  npm install @uniswap/lib @uniswap/v2-core
 press enter
 on the new truffle we need to change the version of the solidity to correspond with the new brough forward folders.
 vim truffle-config.js
 change to 0.6.6
NOTE:in uniswap when you create a uniswap market uniswap uses weth ether so we need to create weth ether wrap ether is a S20token of ethereum
to deploy factory or pair contract you don't need but for router contract you need, so I will create weth eth.

CREATE WRAPPED CONTRACT
 touch contracts/WETH.sol
 vim contracts/WETH.sol
 click enter
NOTE Blank page WETH.sol opens
 for the code we go to etherscan.io
NOTE: on etherscan we search for wrapped ether, also you need to verified the account of any wrapped ether you copy the code to be sure its correct.
 click on contract/ copy the code
 paste on WETH.sol
 change the version of solidity 0.6.6 
 Now we open WETH.sol adjust the code by adding emit key word on line 40,46,55,77
NOTE:
deposit withdrawal approval transfer
 line 35 -also change the to receive( external payable {
Also change the contract name to name of your chioice

run truffle compile

Create mmgration module on deploy_contracts.js
touch migrations/2_deploy_contracts.js
click enter
 vim migrations/2_deploy_contracts.js
 click enter
 copy and paste from migration code created befor change to  const Router =artifacts("UniswapsV2Router02.sol)

 copy the contract address when we deploy the factory erlier on ganache '0xB590378E2025Cd8398a86305C3490943F701ecE5'
 copy the address where we copied the contract from and paste in 
weth = await WETH.at('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2');
} else {
await deployer.deploy(WETH);
} await deployer.deploy(Router ,FACTORY_ADDRESS,  weth.address);
 naviagate to Truffle-config.js and assign to development network
 Go to pherophery folder and run truffle migrate -- reset
NOTE: It is going to connect to the ganache we started before  eventhough we started from another folder. what ateers is the port 8545
 I do have a error The UniswapV2Router02.sol is too big. I have to comment out some of the contract/ swap supporting fee-on transfer token will be comment out from line 210 - 404 library function

Navigate to interface and comment out function from line 35 - 45
 now I will run truflle compile again
NOTE: one of the diffculty in deploying smart contract is the different code that are combined, different version of solidity to deal with and there is no code to deploy smart contract, you have to configure and manage it on your own.






