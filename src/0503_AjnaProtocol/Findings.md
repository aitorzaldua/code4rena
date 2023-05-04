## [GAS‑1] abi.encode() is less efficient than abi.encodepacked()

abi.encodePacked() encodes its parameters using the minimal space required by the type.
If you do not need to pad to 32 bytes or if you are not making calls to a contract,
you need to use abi.encodePacked().

### Lines of code:

Contract: https://github.com/code-423n4/2023-05-ajna/blob/main/ajna-grants/src/grants/base/Funding.sol

`158: proposalId_ = uint256(keccak256(abi.encode(targets_, values_, calldatas_, descriptionHash_)));`

Contract: https://github.com/code-423n4/2023-05-ajna/blob/main/ajna-grants/src/grants/base/ExtraordinaryFunding.sol

`62: proposalId_ = _hashProposal(targets_, values_, calldatas_, keccak256(abi.encode(DESCRIPTION_PREFIX_HASH_EXTRAORDINARY, descriptionHash_)));`

`92: proposalId_ = _hashProposal(targets_, values_, calldatas_, keccak256(abi.encode(DESCRIPTION_PREFIX_HASH_EXTRAORDINARY, keccak256(bytes(description_)))));`

Contract: https://github.com/code-423n4/2023-05-ajna/blob/main/ajna-grants/src/grants/base/StandardFunding.sol

`314: bytes32 newSlateHash     = keccak256(abi.encode(proposalIds_));`

`349: proposalId_ = _hashProposal(targets_, values_, calldatas_, keccak256(abi.encode(DESCRIPTION_PREFIX_HASH_STANDARD, descriptionHash_)));`

`372: proposalId_ = _hashProposal(targets_, values_, calldatas_, keccak256(abi.encode(DESCRIPTION_PREFIX_HASH_STANDARD, keccak256(bytes(description_)))));`

`983: return keccak256(abi.encode(proposalIds_));`

## [GAS-2] Avoid emitting constants.

The constants are unnecessary to emit since the value will never change. Each element of an event/emit has a cost of 375 gas.
Reference: https://solodit.xyz/issues/8898

### Lines of code:

Contract: https://github.com/code-423n4/2023-05-ajna/blob/main/ajna-grants/src/grants/base/StandardFunding.sol

`746 to 752: emit VoteCast(account_, proposalId, 1, votes_,"");`

## [HIGH-1] transferFrom/safeTransferFrom : The `_from` parameter should be `msg.sender`

Always check each `transferFrom` call in smart contracts and verify that the `_from` parameter is `msg.sender`

Contract: https://github.com/code-423n4/2023-05-ajna/blob/main/ajna-grants/src/grants/GrantFund.sol

`67: token.safeTransferFrom(msg.sender, address(this), fundingAmount_);`
