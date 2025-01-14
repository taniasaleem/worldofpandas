# World of Panda Smart Contract

## Overview

The **WorldOfPanda** smart contract is an ERC-721-based NFT contract designed to create and manage a unique collection of Panda-themed NFTs. It incorporates functionality for minting, transferring, royalty management, and pre-sale mechanisms. The contract also introduces special features such as legendary Panda NFTs and whitelist privileges.

## Features

### 1. **ERC-721 Standard Compliance**

The contract is fully compliant with the ERC-721 standard and includes extensions such as:

- **ERC721URIStorage**: Allows for storage of unique token URIs.
- **ERC721Burnable**: Supports token burning.
- **ERC721Royalty**: Implements royalty payments.

### 2. **Minting**

The contract allows for the minting of NFTs with the following features:

- Mint price: Adjustable for both whitelist and regular users.
- Unique token URIs enforced by a hash-based uniqueness check.
- Batch minting of up to 10 NFTs per transaction.
- Special legendary Panda NFT minted for users minting 6,000 or more NFTs.

### 3. **Whitelist Mechanism**

- Whitelisted addresses enjoy reduced minting prices and early access during the pre-sale phase.
- Whitelisted users are limited to two batch mint calls during the pre-sale period.

### 4. **Royalty Management**

- Default royalty is set during contract deployment and can be queried by the admin.
- Royalties are automatically sent to the admin address upon minting.

### 5. **Pre-sale and Public Sale**

- Configurable pre-sale and public sale start times.
- Restrictions for non-whitelisted users during the pre-sale phase.

### 6. **Legendary Panda NFT**

- A special legendary Panda NFT is minted for the first user to mint 6,000 or more NFTs.
- Legendary Panda NFTs have a unique URI.

## Deployment Parameters

- **_contractName**: Name of the NFT collection.
- **_contractSymbol**: Symbol for the NFT collection.
- **_nftMintPrice**: Initial minting price for regular users.
- **_whiteListPrice**: Initial minting price for whitelisted users.
- **_royality**: Default royalty percentage (in basis points).

## Key Functions

### Minting Functions

- `batchMint(string[] memory tokenUriList)`: Allows users to mint multiple NFTs in one transaction.
- `safeMint(address to, string memory tokenUri)`: Internal function to mint a single NFT.
- `legendaryMint(address _sender)`: Internal function to mint the legendary Panda NFT.

### Admin Functions

- `setPresaleTime(uint256 time)`: Sets the pre-sale start time.
- `setActualSaleTime(uint256 time)`: Sets the public sale start time.
- `setNFTshow(uint256 time)`: Sets the time after which token URIs are visible.
- `setAdmin(address _admin)`: Updates the admin address.
- `addWhiteList(address id)`: Adds an address to the whitelist.
- `removeWhiteList(address id)`: Removes an address from the whitelist.
- `sendContractBalance(address _to)`: Transfers the contract's balance to the specified address.

### Query Functions

- `getMintedList()`: Returns a list of all minted NFT IDs.
- `getContractBalance()`: Returns the current contract balance.
- `getAdmin()`: Returns the current admin address.
- `getRoyaltyValue()`: Returns the royalty percentage.

### Token Management

- `tokenURI(uint256 tokenId)`: Returns the token URI if the current time is greater than `NFTshowtime`. Otherwise, returns a placeholder URI.
- `UniqueSVG_by_Hash(bytes memory _tokenURI)`: Checks if a token URI is unique.

## Events

- `TokenMinted(uint256 indexed tokenId, address owner)`: Triggered when a new token is minted.
- `priceSetEvent(uint ID, bool price_is_set)`: Triggered when a price is set for a token.
- `payment_Sent(bool payment_Sent)`: Triggered when a payment is successfully sent.

## Security

- **Admin Control**: Only the admin can update critical configurations like sale times and whitelist status.
- **Access Control**: Critical functions are protected by `onlyAdmin` or `onlyOwner` modifiers.
- **Uniqueness Enforcement**: Ensures that all minted NFTs have unique URIs.
- **Pre-sale Restrictions**: Prevents non-whitelisted users from minting during the pre-sale period.

## Deployment

To deploy the contract, use the constructor with the following parameters:

```
constructor(
    string memory _contractName,
    string memory _contractSymbol,
    uint256 _nftMintPrice,
    uint256 _whiteListPrice,
    uint96 _royality
)
```

## Example Deployment

```
WorldOfPanda pandaContract = new WorldOfPanda(
    "WorldOfPanda",
    "WOP",
    0.05 ether,
    0.03 ether,
    500 // 5% royalty
);
```

## License

This project is licensed under the MIT License.
