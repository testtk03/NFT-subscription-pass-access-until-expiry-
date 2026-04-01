# NFT-subscription-pass-access-until-expiry-
NFT subscription pass (access until expiry)
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract SubPass is ERC721 {
    uint256 public nextId;
    mapping(uint256 => uint256) public expiry;

    constructor() ERC721("SubPass", "SPASS") {}

    function mint(uint256 duration) public payable {
        require(msg.value == 0.01 ether, "Fee");
        uint256 id = nextId++;
        _mint(msg.sender, id);
        expiry[id] = block.timestamp + duration;
    }

    function isActive(uint256 id) public view returns (bool) {
        return block.timestamp < expiry[id];
    }
}
