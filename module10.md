# 10. Token Standards

> Welcome to the Pokémon Token League!

You're now ready to unlock the blockchain equivalent of the Pokémon world’s trading cards, currency, and item packs. This module explores how to bring PokéCoins, Legendary Pokémon, and booster packs to life using Ethereum's most powerful token standards:

- ERC-20: For fungible PokéCoins and in-game currency
- ERC-721: For one-of-a-kind Legendary Pokémon
- ERC-1155: For versatile PokéPacks that contain items, characters, or both!

## ERC Token Standards Overview

Ethereum Request for Comments (ERC) standards define how tokens behave. Solidity contracts follow these standards to ensure compatibility across wallets, marketplaces, and dApps.

| Standard | Type         | Use Case                         | Unique Feature                  |
| -------- | ------------ | -------------------------------- | ------------------------------- |
| ERC-20   | Fungible     | PokéCoins, currencies, XP points | Identical and divisible tokens  |
| ERC-721  | Non-fungible | Legendary Pokémon, unique items  | Unique IDs for each token       |
| ERC-1155 | Multi-token  | Booster packs, hybrid items      | Batch operations & shared logic |




## ERC-20 – PokéCoins: Your In-Game Currency

ERC-20 tokens are like PokéCoins in your wallet—every unit is equal and interchangeable.

**Key Functions:**

-   `totalSupply()` – Total coins available
-   `balanceOf(address)` – Trainer’s PokéCoin balance
-   `transfer(to, amount)` – Send PokéCoins
-   `approve() / transferFrom()` – Allow others to spend on your behalf


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

> ERC-20 tokens are widely used in DeFi and represent currencies, staking tokens, or governance assets.

## **ERC-721 – Non-Fungible Tokens (NFTs)**

>  Legendary Pokémon: Unique Collectibles

**ERC-721** tokens are perfect for Legendary Pokémon—each with a distinct identity and metadata.
**ERC-721** defines the standard for **non-fungible tokens**—unique assets like digital art, collectibles, or in-game items.

**Key Functions:**

-   `ownerOf(tokenId)` - Who owns the Pokémon
-   `safeTransferFrom(from, to, tokenId)` - Trade Pokémon safely
-   `tokenURI(tokenId)` (metadata)

Each token has a unique ID and can point to metadata or artwork via IPFS or a centralized URL.


### Example: Legendary Pokémon Contract

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

### **ERC-1155 – PokéPacks: Multiple Items, One Contract - Multi-Token Standard**

**ERC-1155** is ideal for booster packs that might contain a mix of items—PokéBalls, berries, even Pokémon!

**Key Features:**

-   Batch minting/transfers (`safeBatchTransferFrom`)
-   Shared metadata for similar token types
-   Lower gas usage than ERC-721 for multiple tokens

### Example: PokéPack Contract

```jsx
// SPDX-License-Identifier: MIT
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


## 🧭 What’s Next?

You've minted coins, captured legendaries, and packed your deck. But to become a true Solidity Champion, you’ll need to defend your contracts like a Master Trainer guards their team.

Next up:

Module 11 – Bonus Module: Advanced Solidity Concepts
 
Face off against gym-leader-level challenges like access control, reentrancy attacks, and upgradeable contracts.
You'll learn how to guard your assets, structure roles, and future-proof your code using security patterns and proxy architecture.
