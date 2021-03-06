# Tournament Reward Claiming

In order to allow tournament recipients to claim an ERC20 token reward, an instance of the `RewardClaimHandler` may must deployed, and that information must be relayed to the frontend.

## Deploying `RewardClaimHandler` using MyEtherWallet

To do so, you will need an account with actual Ether. We will use [MyEtherWallet](https://www.myetherwallet.com/#contracts). For the purpose of this guide, we will issue rewards on the Kovan network, though you will almost certainly wish to use the public main network.

First we must deploy the contract `RewardClaimHandler` contract with MEW. You can find the bytecode in the `@gnosis.pm/pm-apollo-contracts` project in the build artifact `build/contracts/RewardClaimHandler.json` under the `bytecode` key, but this is reproduced for your convenience below:

```
0x6060604052341561000f57600080fd5b604051602080610c1b83398101604052808051906020019091905050806000806101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555033600160006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555050610b5f806100bc6000396000f30060606040526004361061008e576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806319ec3ded14610093578063553eb4db146100e0578063570ca735146101835780638c9845b0146101d8578063a2fb117514610201578063b88a802f14610264578063e110342214610279578063f7c618c11461028e575b600080fd5b341561009e57600080fd5b6100ca600480803573ffffffffffffffffffffffffffffffffffffffff169060200190919050506102e3565b6040518082815260200191505060405180910390f35b34156100eb57600080fd5b610181600480803590602001908201803590602001908080602002602001604051908101604052809392919081815260200183836020028082843782019150505050505091908035906020019082018035906020019080806020026020016040519081016040528093929190818152602001838360200280828437820191505050505050919080359060200190919050506102fb565b005b341561018e57600080fd5b610196610572565b604051808273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200191505060405180910390f35b34156101e357600080fd5b6101eb610598565b6040518082815260200191505060405180910390f35b341561020c57600080fd5b610222600480803590602001909190505061059e565b604051808273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200191505060405180910390f35b341561026f57600080fd5b6102776105dd565b005b341561028457600080fd5b61028c610759565b005b341561029957600080fd5b6102a16109f0565b604051808273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200191505060405180910390f35b60036020528060005260406000206000915090505481565b6000806000600280549050148015610314575060008551115b8015610321575083518551145b801561037a5750600160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16145b151561038557600080fd5b60009150600090505b84518110156104325783818151811015156103a557fe5b906020019060200201518201915083818151811015156103c157fe5b906020019060200201516003600087848151811015156103dd57fe5b9060200190602002015173ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550808060010191505061038e565b6000809054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff166323b872dd3330856040518463ffffffff167c0100000000000000000000000000000000000000000000000000000000028152600401808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020018373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020018281526020019350505050602060405180830381600087803b151561052957600080fd5b5af1151561053657600080fd5b50505060405180519050151561054b57600080fd5b8460029080519060200190610561929190610a15565b508242016004819055505050505050565b600160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1681565b60045481565b6002818154811015156105ad57fe5b90600052602060002090016000915054906101000a900473ffffffffffffffffffffffffffffffffffffffff1681565b600060028054905011801561070757506000809054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1663a9059cbb33600360003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546040518363ffffffff167c0100000000000000000000000000000000000000000000000000000000028152600401808373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200182815260200192505050602060405180830381600087803b15156106ef57600080fd5b5af115156106fc57600080fd5b505050604051805190505b151561071257600080fd5b6000600360003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550565b60008060006002805490501180156107be5750600160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16145b80156107cc57506004544210155b15156107d757600080fd5b60009150600090505b6002805490508110156108f7576003600060028381548110151561080057fe5b906000526020600020900160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020548201915060006003600060028481548110151561088057fe5b906000526020600020900160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000208190555080806001019150506107e0565b6000809054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1663a9059cbb33846040518363ffffffff167c0100000000000000000000000000000000000000000000000000000000028152600401808373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200182815260200192505050602060405180830381600087803b15156109ba57600080fd5b5af115156109c757600080fd5b5050506040518051905015156109dc57600080fd5b60006002816109eb9190610a9f565b505050565b6000809054906101000a900473ffffffffffffffffffffffffffffffffffffffff1681565b828054828255906000526020600020908101928215610a8e579160200282015b82811115610a8d5782518260006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555091602001919060010190610a35565b5b509050610a9b9190610acb565b5090565b815481835581811511610ac657818360005260206000209182019101610ac59190610b0e565b5b505050565b610b0b91905b80821115610b0757600081816101000a81549073ffffffffffffffffffffffffffffffffffffffff021916905550600101610ad1565b5090565b90565b610b3091905b80821115610b2c576000816000905550600101610b14565b5090565b905600a165627a7a723058200652f29a057236c9369c2c944946437d8769c29d3fdc0ea79bae1a4cd504018f0029
```

Then add the reward token address at the end, padded left to 64 hex characters (32 bytes/256 bits/one EVM word). For example, if your reward token address existed on the network at `0x3552D381b89Dcb92c59d7a0F8fe93b1e3BBE1886`, then we would append this to the bytecode:

```
0000000000000000000000003552D381b89Dcb92c59d7a0F8fe93b1e3BBE1886
```

Then deploy the contract. Once your contract is deployed, you should have an address. Let's say that address is `0x9720939c16665529dEaBE608bC3cA72509297F79`

## Deploying `RewardClaimHandler` using Truffle and pm-apollo-contracts

First, clone the [pm-apollo-contracts repo](https://github.com/gnosis/pm-apollo-contracts):
```
git clone https://github.com/gnosis/pm-trading-ui.git
```

Install the dependencies:
```
npm i
```

Make sure you have truffle installed globally, you can run `truffle version` in your terminal to check, if it says "command not found" or similar, install truffle by executing this command:
```
npm i -g truffle
```

Configuring the project for deployment is covered in this [guide](https://gnosis.github.io/lil-box/deployment-guide.html), in this part we'll cover the configuration very briefly as we expect that you already have it already prepared when you were going through previous parts of this guide.

Let's assume that our `RewardClaimHandler` will be deployed to the Rinkeby Test Network. In the real life example the contract should be probably deployed to the Mainnet, the idea is the same except you'd have to replace node url and change network name/id

Create `truffle-local.js` file inside the root directory, and copy paste the content:


### If you want to use a private key

```js
const Provider = require('truffle-privatekey-provider')

const accountCredential = 'Your private key'

const config = {
  networks: {
    rinkeby: {
      provider: new Provider(accountCredential, 'https://rinkeby.infura.io'),
      network_id: '4',
    },
  },
}

module.exports = config
```

__Important!__ For using private key as an account credential, we'll need a package called `truffle-privatekey-provider`, you can install it by running this command in your terminal:

```
npm i truffle-privatekey-provider
```

### Or if you want to use a mnemonic phrase

```js
const Provider = require('truffle-hdwallet-provider')

const accountCredential = 'Your mnemonic phrase'

const config = {
  networks: {
    rinkeby: {
      provider: new Provider(accountCredential, 'https://rinkeby.infura.io'),
      network_id: '4',
    },
  },
}

module.exports = config
```

Replace `accountCredential` variable with a credential of your choice. So either a private key or a mnemonic phrase. Don't forget that network's name and id has to be changed too if you want to deploy a contract to a different network.

Now, when you are done with the configuration, you need to run the following command:
```
npx truffle exec scripts/deploy_reward_contract.js --token=<token-address> --network=<your-network>
```

__Important!__ Don't forget to replace <token-address> with the address of a token you are going to use to reward your winners and <your-network> with your desired network's name. Token Contract and RewardClaimHandler have to be on the same network.

After running the command, you should get the following output (an example):
```
> npx truffle exec scripts/deploy_reward_contract.js --token=0x1a5f9352af8af974bfc03399e3767df6370d82e4 --network=rinkeby
Using network 'rinkeby'.

RewardClaimHandler: 0x79f32a252bb4b370e5a4a37f34e6ff0e1acc52bf
Transaction hash: 0xa2694e3924137116e59501cf54d5fa24e2432ae052e11d40cbfe93b689861870
```

Save the RewardClaimHandler address you got, you'll need it in the next section.


## Filling the contracts with winners and prize amounts

For this section, we're assuming that you already have correct configuration for `pm-scripts`. If you haven't used it, please first go to [pm-scripts](/pm-scripts) section of this documentation.

So, inside pm-scripts root directory, go to `conf/config.json` file. Now, you need to add `rewardClaimHandler` key to the json and configure it. You can use this example as a reference:
```json
  "rewardClaimHandler": {
    "blockchain": {
      "protocol": "https",
      "host": "node.rinkeby.gnosisdev.com",
      "port": "443"
    },
    "address": "0x42331cbc7D15C876a38C1D3503fBAD0964a8D72b",
    "duration": 86400,
    "decimals": 18,
    "levels": [
      { "value": 5, "minRank": 1, "maxRank": 1 },
      { "value": 4, "minRank": 2, "maxRank": 2 },
      { "value": 3, "minRank": 3, "maxRank": 3 },
      { "value": 2, "minRank": 4, "maxRank": 4 },
      { "value": 1, "minRank": 5, "maxRank": 5 },
      { "value": 0.9, "minRank": 6, "maxRank": 7 },
      { "value": 0.8, "minRank": 8, "maxRank": 9 },
      { "value": 0.7, "minRank": 10, "maxRank": 11 },
      { "value": 0.6, "minRank": 12, "maxRank": 13 },
      { "value": 0.5, "minRank": 14, "maxRank": 15 },
      { "value": 0.4, "minRank": 16, "maxRank": 17 },
      { "value": 0.3, "minRank": 18, "maxRank": 19 },
      { "value": 0.2, "minRank": 19, "maxRank": 34 },
      { "value": 0.1, "minRank": 34, "maxRank": 100 }
    ]
  }
```

Let's go through configurations options.

- __blockchain__ - an Ethereum node URL for RewardClaimHandler contract
- __address__ - RewardClaimHandler's contract address. You should've saved it in previous section
- __duration__ - duration of reward claiming period in seconds, starting from the time you put data to the contract. Immutable after registering the rewards
- __decimals__ - Number of decimals token reward contract uses
- __levels__ - Array which represents ranks and reward values. You can check the format in example configuration above. You can just copy-paste it from your interface configuration

After you're done with the configuration, just run this in your terminal:
```
node lib/main.js claimrewards
```

After the execution of this command you're done with smart contracts work, now let's configure the interface.

## Configuring the interface

Here are an example config of rewards section in the interface config:

```js
{
  "rewardClaiming": {
    "enabled": false,
    "claimReward": {
      "enabled": false,
      "claimStart": "2018-06-01T12:00:00",
      "claimUntil": "2018-07-01T12:00:00",
      "contractAddress": "0xe89f27dafb9ba68c864e47a0bf1e430664e419af",
      "networkId": 42
    }
  },
  "rewards": {
    "enabled": true,
    "rewardToken": {
      "symbol": "RWD",
      "contractAddress": "0x3552D381b89Dcb92c59d7a0F8fe93b1e3BBE1886",
      "networkId": 42
    },
    "levels": [
      { "value": 5, "minRank": 1, "maxRank": 1 },
      { "value": 4, "minRank": 2, "maxRank": 2 },
      { "value": 3, "minRank": 3, "maxRank": 3 },
      { "value": 2, "minRank": 4, "maxRank": 4 },
      { "value": 1, "minRank": 5, "maxRank": 5 },
      { "value": 0.9, "minRank": 6, "maxRank": 7 },
      { "value": 0.8, "minRank": 8, "maxRank": 9 },
      { "value": 0.7, "minRank": 10, "maxRank": 11 },
      { "value": 0.6, "minRank": 12, "maxRank": 13 },
      { "value": 0.5, "minRank": 14, "maxRank": 15 },
      { "value": 0.4, "minRank": 16, "maxRank": 17 },
      { "value": 0.3, "minRank": 18, "maxRank": 19 },
      { "value": 0.2, "minRank": 19, "maxRank": 34 },
      { "value": 0.1, "minRank": 34, "maxRank": 100 }
    ]
  },
  ...
}
```

Let's go through options here:

* __rewardClaiming__
  * __enabled__ - If enabled, then the interface will show a reward claiming box on scoreboard page
  * __claimReward__
    * __enabled__ - If enabled, then the interface will check if the current date is between `claimStart` and `claimUntil` and if it is, then the reward claiming process will be active. It was done because in some cases you'd want to sent the rewards manually instead of a contract.
    * __claimStart__ - Start date of reward claiming
    * __claimUntil__ - End date of reward claiming
    * __contractAddress__ - Address of previously deployed RewardClaimHandler
    * __networkId__ - RewardClaimHandler's network id
* __rewards__
  * __enabled__ - If enabled, interface will show reward amount and an address the user will get the rewards to on scoreboard page
  * __rewardToken__
    * __symbol__ - Reward token symbol
    * __contractAddress__ - Address of a reward token you want to use
    * __networkId__ = Reward token's network id
  * __levels__  - Array of objects which represents ranks and reward values, each object should contain three properties:
    * __value__ - Reward amount value in ETH. So if a token contract uses X decimals, the amount of tokens a user will get is __value__ * 10^X
    * __minRank__ - Minimum suitable rank for the reward
    * __maxRank__ - Maximum suitable rank for the reward, inclusive

Be aware that the `levels` key will show up on the scoreboard and signal to the players what their anticipated reward should be. Be sure that you have enough of the reward to offer!    

The best way to handle the reward claiming is to configure everything at the tournament start except `rewardClaiming.claimReward`, just keep it disabled. Then, when reward claiming start itself, deploy and fill the contract, enable claimReward via runtime config or change the config and deploy a new version of the interface.


