---
name: apidapp
description: "ApiDapp API skill. Use when working with ApiDapp for root, account, block. Covers 54 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiDapp
API version: 2019-02-14T16:47:01Z

## Auth
ApiKey X-Api-Key in header

## Base URL
https://ethereum.apidapp.com/1

## Setup
1. Set your API key in the appropriate header
2. GET /block -- verify access
3. POST /account -- create first account

## Endpoints

54 endpoints across 11 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| OPTIONS | / |  |

### account
| Method | Path | Description |
|--------|------|-------------|
| POST | /account | Create new account |
| OPTIONS | /account |  |
| GET | /account/{id} | Get account balance |
| OPTIONS | /account/{id} |  |

### block
| Method | Path | Description |
|--------|------|-------------|
| GET | /block | Access detailed block information |
| OPTIONS | /block |  |
| GET | /block/{id} | Get information about particular block |
| OPTIONS | /block/{id} |  |
| GET | /block/{id}/transaction | Get transaction count within block |
| OPTIONS | /block/{id}/transaction |  |
| GET | /block/{id}/transaction/{index} | Get information about particular transaction within block |
| OPTIONS | /block/{id}/transaction/{index} |  |

### blockchain
| Method | Path | Description |
|--------|------|-------------|
| GET | /blockchain | Get a list of supported blockchains |
| OPTIONS | /blockchain |  |
| GET | /blockchain/{id} | Get information about blockchain woth given id |
| OPTIONS | /blockchain/{id} |  |

### contract
| Method | Path | Description |
|--------|------|-------------|
| POST | /contract | Create a new smart contract |
| OPTIONS | /contract |  |
| GET | /contract/{id} | Get contract balance |
| POST | /contract/{id} | Call the contract |
| OPTIONS | /contract/{id} |  |

### echo
| Method | Path | Description |
|--------|------|-------------|
| OPTIONS | /echo |  |

### erc20
| Method | Path | Description |
|--------|------|-------------|
| GET | /erc20 | Get token information such as name, total amount in circulation, etc |
| POST | /erc20 |  |
| OPTIONS | /erc20 |  |
| GET | /erc20/{address} | Get information amout token balance in the account |
| POST | /erc20/{address} | Transfer tokens to another account |
| OPTIONS | /erc20/{address} |  |

### key
| Method | Path | Description |
|--------|------|-------------|
| GET | /key |  |
| POST | /key |  |
| OPTIONS | /key |  |
| DELETE | /key/{key} |  |
| OPTIONS | /key/{key} |  |

### transaction
| Method | Path | Description |
|--------|------|-------------|
| POST | /transaction | Create a new transaction. Transfer Ether between accounts |
| OPTIONS | /transaction |  |
| GET | /transaction/{hash} | Get information about transaction by the transaction hash value |
| OPTIONS | /transaction/{hash} |  |
| GET | /transaction/{hash}/receipt | Get receipt detail information |
| OPTIONS | /transaction/{hash}/receipt |  |

### version
| Method | Path | Description |
|--------|------|-------------|
| GET | /version | Get API version info |
| OPTIONS | /version |  |

### wallet
| Method | Path | Description |
|--------|------|-------------|
| GET | /wallet | Get current account balance |
| POST | /wallet | Create personal wallet |
| OPTIONS | /wallet |  |
| GET | /wallet/account |  |
| POST | /wallet/account |  |
| OPTIONS | /wallet/account |  |
| GET | /wallet/account/{id} | Get account balance |
| OPTIONS | /wallet/account/{id} |  |
| POST | /wallet/account/{id}/contract |  |
| POST | /wallet/account/{id}/erc20 |  |
| POST | /wallet/account/{id}/pay | Send payment from the account held within the wallet |
| OPTIONS | /wallet/account/{id}/pay |  |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the ApiDapp API?" -> Header: X-Api-Key
- "What version of the API is running?" -> GET /version
- "How do I look up an Ethereum account?" -> GET /account/{id}
- "What's in the latest block?" -> GET /block
- "How do I get details for a specific block?" -> GET /block/{id}
- "What transactions are in a given block?" -> GET /block/{id}/transaction
- "How do I fetch a specific transaction from a block by index?" -> GET /block/{id}/transaction/{index}
- "How do I look up a transaction by hash?" -> GET /transaction/{hash}
- "Did my transaction confirm? Where's the receipt?" -> GET /transaction/{hash}/receipt
- "How do I send a new transaction?" -> POST /transaction
- "How do I deploy a smart contract?" -> POST /contract
- "How do I interact with an existing contract?" -> POST /contract/{id}
- "What ERC-20 tokens are available?" -> GET /erc20
- "How do I get details for a specific ERC-20 token?" -> GET /erc20/{address}
- "How do I create a wallet?" -> POST /wallet
- "How do I list wallet accounts?" -> GET /wallet/account
- "How do I send a payment from a wallet account?" -> POST /wallet/account/{id}/pay
- "How do I manage my API keys?" -> GET /key, POST /key, DELETE /key/{key}
- "What blockchains are supported?" -> GET /blockchain

## Response Tips

- **Account/Block/Transaction lookups** (`GET /{resource}/{id}`): Responses are single objects keyed by the identifier you passed; check for missing or null fields to detect unconfirmed state.
- **Collection endpoints** (`GET /block`, `GET /erc20`, `GET /wallet`): May return arrays or paginated objects; inspect response shape for a `next` cursor or total count before assuming all results are present.
- **Transaction receipts** (`GET /transaction/{hash}/receipt`): A null or empty receipt means the transaction is still pending; retry after a delay rather than treating it as an error.
- **Contract interactions** (`POST /contract/{id}`): Responses may include both the transaction hash and any return values from the contract call; parse both.
- **Key management** (`GET /key`, `DELETE /key/{key}`): Token query param on GET filters results; DELETE returns confirmation but the key is invalidated immediately.
- **OPTIONS endpoints**: Return allowed methods and CORS headers, not business data; useful only for preflight checks.

## Anomaly Flags

- **Missing transaction receipt**: If `GET /transaction/{hash}/receipt` returns empty after multiple attempts, surface a warning that the transaction may be stuck or dropped from the mempool.
- **Unexpected 200 with empty body**: All endpoints declare only 200 responses; if a 200 comes back with no data, flag it as a potential silent failure since there are no documented error codes.
- **API key approaching limits**: After `GET /key` calls, check for any rate limit or usage metadata in headers (e.g., `X-RateLimit-Remaining`) and warn when thresholds are low.
- **Contract deployment without confirmation**: If `POST /contract` returns a hash but subsequent `GET /contract/{id}` returns nothing, flag that the contract may have failed to deploy.
- **Blockchain ID mismatch**: If `GET /blockchain/{id}` returns data for an unexpected network (testnet vs mainnet), alert the user before they execute transactions on the wrong chain.
- **Stale version**: Compare `GET /version` output against the spec version (`2019-02-14`); if significantly older or newer, warn about potential incompatibilities.

## Playbook

### 1. Deploy a Smart Contract from a Wallet

1. `GET /wallet/account` -- list available wallet accounts, pick the funding account.
2. `GET /blockchain` -- confirm you are targeting the correct blockchain/network.
3. `POST /contract` -- submit the contract bytecode and constructor parameters.
4. Note the returned transaction hash.
5. `GET /transaction/{hash}/receipt` -- poll until the receipt confirms deployment and returns the contract address.
6. `GET /contract/{id}` -- verify the deployed contract is accessible using the new address.

### 2. Send an ERC-20 Token Payment

1. `GET /erc20/{address}` -- look up the token contract to confirm symbol, decimals, and balance.
2. `GET /wallet/account/{id}` -- verify the sender account has sufficient token and gas balance.
3. `POST /wallet/account/{id}/erc20` -- initiate the ERC-20 transfer with recipient and amount.
4. `GET /transaction/{hash}/receipt` -- confirm the transfer completed successfully.

### 3. Monitor a Block for Specific Transactions

1. `GET /block` -- get the current/latest block number.
2. `GET /block/{id}` -- fetch full block details by number or hash.
3. `GET /block/{id}/transaction` -- list all transactions in that block.
4. For each interesting transaction, `GET /block/{id}/transaction/{index}` -- inspect individual transaction details.
5. `GET /transaction/{hash}/receipt` -- pull receipts for transactions that match your criteria.

### 4. API Key Rotation

1. `GET /key` -- list all active API keys (optionally filter with `?token=`).
2. `POST /key` -- generate a new API key; store the returned key securely.
3. Update your application config to use the new key in the `X-Api-Key` header.
4. Verify connectivity with `GET /version` using the new key.
5. `DELETE /key/{key}` -- revoke the old key once the new one is confirmed working.

### 5. Set Up a New Wallet and Fund It

1. `POST /wallet` -- create a new wallet.
2. `POST /wallet/account` -- create an account within the wallet.
3. `GET /wallet/account/{id}` -- retrieve the new account address.
4. Fund the account externally or via `POST /wallet/account/{id}/pay` from another account.
5. `GET /account/{id}` -- confirm the balance reflects the funding transaction.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
