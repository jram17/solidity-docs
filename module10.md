# 10. Token Standards

 **Welcome to the Pokémon Token League!**
To evolve your training journey, you now need **PokéCoins (ERC-20)** to buy items, **unique Legendary Pokémon (ERC-721)** to build your team, and perhaps even **Pokémon packs (ERC-1155)** that hold multiple cards at once!

Solidity uses different **ERC token standards** to define how tokens behave. Each standard has unique properties for different use cases—from identical tokens to rare, one-of-a-kind digital collectibles.

**Unlock ERC-20 PokéCoins and mint legendary Pokémon (ERC-721).**

## ERC Standards: ERC-20, ERC-721, and ERC-1155

**ERC-20 – Fungible Tokens**

The **ERC-20** standard defines a set of functions and events for fungible tokens—where each token is identical and interchangeable (e.g., USDC, DAI).

**Key Functions:**

-   `balanceOf(address)`
-   `transfer(to, amount)`
-   `approve(spender, amount)`
-   `transferFrom(from, to, amount)`

ERC-20 tokens are widely used in DeFi and represent currencies, staking tokens, or governance assets.
``` jsx 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract PokeCoin is ERC20 {
    constructor() ERC20("PokeCoin", "PKC") {
        _mint(msg.sender, 1000 * 10 ** decimals());
    }
}
```
### **ERC-721 – Non-Fungible Tokens (NFTs)**

**ERC-721** defines the standard for **non-fungible tokens**—unique assets like digital art, collectibles, or in-game items.

**Key Functions:**

-   `ownerOf(tokenId)`
-   `safeTransferFrom(from, to, tokenId)`
-   `tokenURI(tokenId)` (metadata)

Each token has a unique ID and can point to metadata or artwork via IPFS or a centralized URL.

```jsx
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract LegendaryPokemon is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    constructor() ERC721("LegendaryPokemon", "LPM") {}

    function mintPokemon(address trainer) public returns (uint256) {
        _tokenIds.increment();
        uint256 newId = _tokenIds.current();
        _safeMint(trainer, newId);
        return newId;
    }
}

```

### **ERC-1155 – Multi-Token Standard**

**ERC-1155** supports both **fungible and non-fungible tokens** in a single contract, making it highly gas-efficient for games, marketplaces, and batch transfers.

**Key Features:**

-   Batch minting/transfers (`safeBatchTransferFrom`)
-   Shared metadata for similar token types
-   Lower gas usage than ERC-721 for multiple tokens

```jsx
// SPDX-License-Identifier: **MIT**
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract PokePack is ERC1155, Ownable {
    constructor() ERC1155("https://api.example.com/metadata/{id}.json") {}

    function mintCard(address to, uint256 id, uint256 amount) public onlyOwner {
        _mint(to, id, amount, "");
    }

    function mintPack(address to, uint256[] memory ids, uint256[] memory amounts) public onlyOwner {
        _mintBatch(to, ids, amounts, "");
    }
}

```

> 💡 **Use ERC-20** for fungible assets, **ERC-721** for one-of-a-kind items, and **ERC-1155** when dealing with large collections or hybrid assets.


