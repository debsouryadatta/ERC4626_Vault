### Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a Hardhat Ignition module that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.js
```


### Steps of Dev:
1. Intro of ERC4626 -> how it works, walk through the important functions
2. In Remix IDE, Creating a basic OceanToken contract and deploying it, Creating a basic Vault contract and deploying it
3. Deploying, the OceanToken contract (With account 1)
4. Deploying the Vault contract with the address of the OceanToken contract as the constructor argument (With account 1)
5. Inside the OceanToken contract, calling the `approve` function to approve the Vault contract to spend the OceanToken contract's tokens of account 2
6. Inside the OceanToken contract, calling the `allowance` function to check the allowance of the Vault contract to spend the OceanToken contract's tokens of account 2
7. Inside the Vault contract, calling the `deposit` function to deposit some OceanToken contract's tokens of account 2 and get back some shares

8. Now the totalAssets & the totalSupply of the Vault contract should be the amount that was deposited
9. Now the account 2(depositor) should have same number of shares as it deposited tokens i.e. 100 shares. Vault address is the share token address
10. Inside the Vault contract, calling the `redeem` function to redeem some shares of account 2 and get back some OceanToken contract's tokens. After redeeming all the 100 shares, the account 2 should have 0 shares and the totalAssets & the totalSupply of the Vault contract should be 0
11. Setting the owner & the entryFeeBasisPoints of the Vault contract in the constructor
12. Overriding the `_entryFeeBasisPoints` & `_entryFeeRecipient` functions in the Vault contract
13. Redeploying the contracts(now _basisPoints is required for deploying the vault contract) and repeating the steps, starting from fresh
14. Now, we can see that when the account 2 deposits 100 OceanToken contract's tokens, it gets back 99 shares and the totalAssets & the totalSupply of the Vault contract should be 99, since 1% entry fee is deducted
15. We can also see that the account 1(_entryFeeRecipient), is getting the entry fee.
16. `convertToAssets` & `convertToShares` functions in the Vault contract gives the same amount of assets/shares as the input amount

17. Will sort of mock a strategy in the Vault contract, and will hardcode a 10% return on any deposit and we will see how the vault reacts to that and see how it works
18. Using some functions of solmate library to perform the hooks before and after the deposit and redeem functions(This part not coded), checkout this github repo for more info: https://github.com/jspruance/erc4626-vault-tutorial/blob/main/contracts/Vault.sol


- Approve func(OceanToken contract):
    - vault address(spender add), xxx eth(amount)

- Allowance func(OceanToken contract):
    - account 2(owner add), vault address(spender add)

- Deposit func(Vault contract):
    - xxx eth(amount), account 2(shares receiver add)

- Redeeem func(Vault contract):
    - xxx shares(amount), account 2(token receiver add), account 2(owner add)

- Strategies by which the vault can invest the assets:
    - Lending, Staking, Yield farming, Liquidity providing, etc.
