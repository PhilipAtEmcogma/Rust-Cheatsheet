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