# [M01] - Use safeTransfer() instead of transfer()

## Summary

transfer() and transferFrom() functions return a boolean value indicating success. This parameter needs to be checked for success. Some tokens do not revert if the transfer failed but return false instead.

## Vulnerability Detail
USDT doesn't correctly implement EIP20 and their transfer/transferFrom function returns void instead of success boolean.

## Impact
Using _claimRedeem function if _asset.transfer() fails would lead to loss of funds for user.

## Code Snippet
https://github.com/sherlock-audit/2024-03-amphor/blob/main/asynchronous-vault/src/AsyncSynthVault.sol#L771

## Tool used
Manual Review

## Recommendation
Recommend using SafeERC20 library from OpenZeppelin
