# Note: this cheatsheet is created on July 2023 for a course I did learning to use Rust to build on Solana network.  Until July 2023, Solana only works on Linux and iOS, and not on Windows. 
#
# Thus, to install, setup and get Solana to on a Windows machine you need to do the followings:
## 1. open powershell as administrator
## 2. install ubuntu using the following command:
###     wsl --install
## 3. upon finishing install, setup (username and password) and restart the machine update the the library using the following command:
###     sudo apt update && sudo apt upgrade
## 4. install windows subsystem for linux using the following command:
###     curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
###    Note: when performing the above command, if encounter an error "curl: (6) could not resolve host: sh.rustup.rs", try the following command to restart wsl and see if it resolves the problem (worked on win 11):
####    wsl --shutdown
####    wsl
#
## 5. after installing the subsystem, need to restart wsl for the subsystem and updates to take into effects, use the following command:
###     exit  or wsl --shutdown
###     wsl
#
## 6. Next install Solana CLI in the window machine, two useful official link on how to install it can be found in the following:
### a: https://solana.com/developers
### b: https://solana.com/developers/guides/setup-local-development
##  Starting the linux vm (e.g. ubuntu) using the following command:
### wsl
## install the Solana CLI tool suite using the folllowing command:
### sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
#
#
# When testing dapp and/or smart contracts on local machine we need to have a local test validator setup on a separate command line window, and leave it running for the entire duration, official documentation on how to set it up can be found at the following:
## https://solana.com/developers/guides/setup-local-development#windows-users-only
# command to use to setup test validator:
## solana-test-validator
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


