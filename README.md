# Note: This cheatsheet is last updated on July 2023 for building Smart Contract using Rust on Solana network.  Until July 2023, Solana only works on Linux and iOS, and not on Windows. 
#       I will aperiodically update it whenever I found something new and interesting in coding Smart Contract for the Solana network.
# ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#  
# The following, are guided steps for installing and setup Rust and getting it to interact with Solana blockchain on a Windows machine.
# NOTE: the steps involve installing Linux subsystem.
## 1. Open powershell as administrator
## 2. Install ubuntu using the following command:
###     wsl --install
## 3. Upon finishing install, setup (username and password) and restart the machine, update and upgrade the the libraries using the following command:
###     sudo apt update && sudo apt upgrade
## 4. Install windows subsystem for linux using the following command:
###     curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
###    Note: when performing the above command, if encounter an error "curl: (6) could not resolve host: sh.rustup.rs", try the following command to restart wsl and see if it resolves the problem (worked on win 11):
####    wsl --shutdown
####    wsl
#
## 5. After installing the subsystem, need to restart wsl for the subsystem and updates to take into effects, use the following command:
###     exit  or wsl --shutdown
###     wsl
#
## 6. Next install Solana CLI in the window machine, two useful official link on how to install it can be found in the following:
### a: https://solana.com/developers
### b: https://solana.com/developers/guides/setup-local-development
##  Starting the linux vm (e.g. ubuntu) using the following command:
### wsl
## Install the Solana CLI tool suite using the folllowing command:
### sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
#
#
# When testing dapp and/or smart contracts on local machine we need to have a local test validator setup on a separate command line window, and leave it running for the entire duration, official documentation on how to set it up can be found at the following:
## https://solana.com/developers/guides/setup-local-development#windows-users-only
# command to use to setup / run test validator:
## solana-test-validator
# NOTE: TO START THE TEST VALIDATOR, WSL MUST BE IN THE ROOT FOLDER! USE THE FOLLOWING TO GET TO ROOT:
## cd ~
# after running the test validator, configure Solana CLI to use localhose validator for all future terminal commands, using the following command:
## solana config set --url localhost
# Solana CLI configuration settings can be review using:
## solana config get
#
# In addition to run develop and test dapp correct, we need to setup a Solana wallet and have some testnet SOL for interaction, official setup for Solana wallet can be read using the following link:
## https://solana.com/developers/guides/setup-local-development#windows-users-only
# However, this README uses a chrome based Solana wallet called Phantom Wallet (https://phantom.app), here's the steps to set up the Phantom wallet:
## 1. Go to phantom.app and install the wallet, for this README we uses chrome plugin version
## 2. After installing the Chrome plugin, create a new wallet.  Make sure to save the seed phrase at a safe location.
#
# To get some Solana testnet token to your wallet do the following, after setting up a wallet:
## 1. Switch the wallet to connect it to the Solana Devnet
## 2. Use the following command in Solana CLI to request Devnet airdrops of 2SOL to our wallet address:
### solana airdrop 2 <RECIPIENT_ACCOUNT_ADDRESS> --url https://api.devnet.solana.com
#
## Alternatively we could set a simple file system wallet, set it as default wallet and sent the devnet Sol there by the following the steps in the link below:
###  https://solana.com/developers/guides/setup-local-development#windows-users-only
#
# --------------------------------------------------------------------------------------
#
# To get publickey of a wallet use the following command in wsl:
## solana-keygen pubkey
# To check the balance of wallet use the following command (note change name of network, for different network):
## solana balance --url devent
#
# --------------------------------------------------------------------------------------
#
# To create a token do the following steps:
## when creating the token on the mainnet, change devnet to the url of the mainnet
# 1. To install token cli, run the following command:
##  cargo install spl-token-cli
# 2. Then to create the token, run the following:
##  spl-token creaate-token --url devnet
# 3. Create an account to hold the tokens before minting, use the following:
## spl-token create-account <TOKEN_ADDRESS> --url devnet
### note: TOKEN_ADDRESS is the address of the created token in step 2 above, and the returned id is the token account address
# 4. Minting the token, use the following code:
## spl-token mint <TOKEN_ADDRESS> <NUMBER> --url devnet
### note: TOKEN_ADDRESS is the address of the created token in step 2, NUMBER is how many token we want to mint.
## After minting the token we can check the balance using the following:
## spl-token balance <TOKEN_ADDRESS> --url devnet
## To Check the circulating supply of the token, after minting use the following:
## spl-token supply <TOKEN_ADDRESS> --url devnet
# 5. To put a cap of circulating supply, thus preveting misuses such as creating a infinite supply (i.e. over dialuting the supply). Renounce and disable the ability to mint tokens using the folllowing:
## spl-token authorize <TOKEN_ADDRESS> mint --disable --url devent
#
# Tokens can be burnt (only our own tokens can be burned), by using the following:
## spl-token burn <ACCOUNT_ADDRESS> <NUMBER> --url devnet
### Note: ACCOUNT_ADDRESS is the address created in step 3 to hold the tokens, NUMBER is the amount we want to burn
#
# --------------------------------------------------------------------------------------
#
# To transfer the newly minted token from developer account to another wallet can use the following code:
## spl-token transfer <SOURCE_TOKEN_ADDRESS> <AMOUNT> <TARGET_TOKEN_ADDRESS> --url devnet --fund-recipient
### Note: SOURCE_TOKEN_ADDRESS is the token address, TARGET_TOKEN_ADDRESS is the wallet address we want to sent the token to, AMOUNT is the amount of token we want to sent, --fund-recipient is use incase the recipient wallet don't have enough sol to cover for the gas fee, thus the sender pays for it.
#
# --------------------------------------------------------------------------------------
# Deploying a Solana Smart Contract, by deploying an example project
# 
# Solana hello-world example github:
## https://github.com/solana-labs/example-helloworld
#
# On top of installing WSL  (for windows), Node.js is also required to develop smart contract in Solana.  The offical guid can be found below:
## https://learn.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl
# To do so, follow the following steps
# 1. Start Ubuntu command line by using the following:
##  wsl
# 2. Install cURL by using the wolling:
##  sudo apt-get install curl
# 3. Install NVM, by using the following:
##  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
# 4. Verify NVM by using the following (correct respond should be 'NVM'):
## command -v nvm
### NOTE: if the above command does not respond even install is successful, try restarting wsl and try again.
# 5. Install node and lts by using the following:
## nvm install node
## nvm install --lts
# 6. Install Rust (official webpapge: https://rustup.rs/), fun the following:
##  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
### default installation (option 1) should be fine for many cases.
# 7. Configure the CLI, by using the following (for Windows):
##  solana config set --url localhost
# 8. Generate a new key pair using:
##  solana-keygen new
### NOTE: use 'solana-keygen new --force' if a keypair had been created previously
# 9. Start local Solana cluster by using the following:
##  solana-test-validator
### NOTE: if the following error occurs
#### Unable to connect to validator: Client error: test-ledger/admin.rpc does not exist 
### that means we need to change the ubuntu director to root and then reinitialise, thus simply do (pay attention there a space between cd and ~):
#### cd ~
# 10. Leave the validator running on the background, and open a new wsl to build the on-chain program.
# 11. Clone the Solana github example repo from and using the following in a new wsl:
##  https://github.com/solana-labs/example-helloworld/
##  git clone https://github.com/solana-labs/example-helloworld.git
# 12. Go to the helloworld repo and install everything, using the following:
## cd example-helloworld/
## npm install
# 13. Build the on-chain program by using:
## npm run build:program-rust
### NOTE: incase there's a 'cc linker' error when building, which can be solve by installing the build essential and run the build program command again.  Essential toolchain can be install by following (for ubuntu):
####    sudo apt install build-essential
# 14. Deploy the program to the validator using the following:
##  solana program deploy dist/program/helloworld.so
# 15. Run the program by using the following:
## npm start
#
# ------------------------------------------------------------------------------------------------------------------
#
# To display Logs, implement in the program
# 1. Start a new wsl terminal
# 2. Start the progam in the terminal that didn't host the logger, but using the following:
##  npm start
#
# -------------------------------------------------------------------------------------------------------------------
#
# Reminder to whenever a code is change, we need to re-build and re-dploy the smart contracts.
# Use the following code to do so:
## npm run <DIRECTORY_OF_PROJECT>
### e.g. 'npm run build:program-rust', where this command build the program-rust file under the src folder (where changes are made)
## solana program deploy <DIRECTORY_OF_THE_SMART_CONTRACT>
### e.g. 'solana program deploy dist/program/helloworld.so' , where we want to redeploy the helloworld smart contrct, and it is located at the directory dist/program/helloworld.so
# After rebuilding and redeploying the smart contract we can use 'npm start' to test the functinoality
#
# -------------------------------------------------------------------------------------
#
#   When writing the test cases its not a good practice to just write and run it at the end.  Because throughout stages of the project, we will have different expectation and expected outcome and data structures at different stages.
# It is better to have a TEST-DRIVEN DEVELOPMENT, that is:
# First write the test cases and specify the data structure we need to use in the test case (rather than first defing the data structure use in the implementation itself)
# Because if we dive straight into the implementation fist instead of having a Test-Driven Development, it's likely to have incorproated some form of biases and shortcuts into the implementation.
# These biases and shortcuts might work while development is in process or when testing a particular function(s), but it might have bugs and faults in it, which only manifest and affect when the whole implementation is in process.
# Therefore best implementation for Test-Driven Development and to remove biases, are:
# if working solo or small team, write the test case first and test the implementation line-by-line on the go.
# if working in a team, have someone else write the test case
