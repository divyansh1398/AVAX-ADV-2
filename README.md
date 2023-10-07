# Avax-Advance Assignment

We will utilize the subnet configuration we established within our local network using the HyperSDK.

## Description

We intend to utilize HyperSDK's initial repository to set up and initiate our custom subnet within our local network, where we will be actively working on it.

## Getting Started

### Note:

To facilitate checking, you should generate your own build since the build files exceed 25MB in size and lack file extensions, 
preventing me from uploading them. Similarly, for the test folder, you can retrieve it from the official repository.

## Initialize

1. To begin, please navigate to the 'const/const.go' file and assign a name and symbol to your subnet's native token. Make sure you have GO installed before proceeding.
2. Next, create a 'controller/registry.go' file and include the initializations for minting, creating, and transferring within it.
3. Now run this command.
   ``go mod tidy``
   it will download all the dependency.
4. After completing the above steps, execute the script to apply the configurations you've set, and the testing will be automated.
   ``./scripts/run.sh`` or ``bash ./scripts/run.sh``
5. Once the configurations and testing have been successfully completed, you can proceed to run the script to generate the build as mentioned earlier.
   ``./scripts/build.sh`` or ``bash ./scripts/build.sh``
   
_This command will put the compiled CLI in `./build/token-cli`._
   

### Executing program


_By default, this allocates all funds on the network to
`token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp`. The private
key for this address is
`0x323b1d8f4eed5f0da9da93071b034f2dce9d2d22692c172f3cb252a64ddfafd01b057de320297c29ad0c1f589ea216869cf1938d88c9fbd70d6748323dbf2fa7`.
For convenience, this key has is also stored at `demo.pk`._


Lastly, you'll need to add the chains you created and the default key to the
`token-cli`. You can use the following commands from this location to do so:
```bash
./build/token-cli key import demo.pk
./build/token-cli chain import-anr
```

_`chain import-anr` connects to the Avalanche Network Runner server running in
the background and pulls the URIs of all nodes tracking each chain you
created._

### Mint and Trade
#### Step 1: Create Your Asset
First up, let's create our own asset. You can do so by running the following
command from this location:
```bash
./build/token-cli action create-asset
```

When you are done, the output should look something like this:
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
metadata (can be changed later): cc
continue (y/n): y
✅ txID: u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
```

_`txID` is the `assetID` of your new asset._

The "loaded address" here is the address of the default private key (`demo.pk`). We
use this key to authenticate all interactions with the `tokenvm`.

#### Step 2: Mint Your Asset
Now that we've successfully created our own asset, we can proceed to mint a quantity of it. You can do so by
running the following command from this location:
```bash
./build/token-cli action mint-asset
```

Once you've completed the minting process, the output should resemble something similar to this, typically done by minting tokens to your own address for simplicity.
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
assetID: u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
metadata: cc supply: 0
recipient: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
amount: 1000000
continue (y/n): y
✅ txID: BdogHcRMcKcZmaVA5c7svJ7yR288TrXKPNnYqXjLjqxzVhdx5
```

#### Step 3: View Your Balance
Now, let's verify that the minting process was successful by confirming our balance. You can do
so by running the following command from this location:
```bash
./build/token-cli key balance
```

When you are done, the output should look like this:
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
assetID (use TKN for native token): u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
uri: http://127.0.0.1:15613/ext/bc/w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
metadata: cc supply: 1000000 warp: false
balance: 1000000 u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
```

#### Step 4: Create an Order
With some of our token (`cc`) in hand, the next step is to place an on-chain order that enables individuals to exchange the native token (`TKN`) for some of ours.
You can do so by running the following command from this location:
```bash
./build/token-cli action create-order
```

When you are done, the output should look like this:
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
in assetID (use TKN for native token): TKN
✔ in tick: 1
out assetID (use TKN for native token): u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
metadata: cc supply: 1000000 warp: false
balance: 1000000 u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
out tick: 100
supply (must be multiple of out tick): 100
continue (y/n): y
✅ txID: 2CB56oBf2b7Upi1Bk8nwztCugyR8b7uY3TUUTkvyzwpXxCwPzQ
```

_`txID` is the `orderID` of your new order._

The "in tick" represents the amount of the "in assetID" that an individual must trade to receive the "out tick" of the "out assetID." 
It's essential to note that any execution of this order must involve a trade in multiples of the "in tick" to ensure validity and prevent precision issues when calculating decimal rates on-chain.
#### Step 5: Fill Part of the Order
Now that we have an order on-chain, let's fill it! You can do so by running the
following command from this location:
```bash
./build/token-cli action fill-order
```

When you are done, the output should look something like this:
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
in assetID (use TKN for native token): TKN
balance: 999.999998638 TKN
out assetID (use TKN for native token): u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
metadata: cc supply: 1000000 warp: false
available orders: 1
0) Rate(in/out): 10000000.0000 InTick: 1.000000000 TKN OutTick: 100 u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP Remaining: 100 u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
select order: 0
value (must be multiple of in tick): 1
in: 1.000000000 TKN out: 100 u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
continue (y/n): y
✅ txID: ExHemDFkceKj8FmC23egmEyUFzEhoMF2CZHWHqLofP7UeYvFV
```

Note how all available orders for this pair are listed by the CLI (these come
from the in-memory order book maintained by the `tokenvm`).

#### Step 6: Close Order
If you've had a change of heart and no longer wish to permit others to execute your order, you can cancel it by running the following command from this location:
```bash
./build/token-cli action close-order
```

When you are done, the output should look like this:
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: w846RNV4z9DtSMJ1UDUZh8XmarZKxF9WNTRFwAfXv6eaYSN6U
orderID: 2CB56oBf2b7Upi1Bk8nwztCugyR8b7uY3TUUTkvyzwpXxCwPzQ
out assetID (use TKN for native token): u1d2LGZaDvVKgCne5HrGR6vMH2CupqjUTtCEFNZEa4Mno44gP
continue (y/n): y
✅ txID: 2fYGH9oXZb6oMs9h5zxNrTNQnSgvevr1A5B6az3YodGRT81PEy
```

Any funds that were previously locked up in the order will be refunded to the creator's account upon cancellation.
