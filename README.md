# ontology-rosetta
Ontology node which follows Rosetta Blockchain Standard
## Build docker image

```sh
make
docker build -t ontology-rosetta:0.1 .
```

## Running docker image

```sh
docker run --env NETWORK_ID=1 --name rosettatest -d -v /opt/data/Chain:/data/Chain -v /opt/data/rosetta-config.json:/data/rosetta-config.json -p 9090:8080 ontology-rosetta:0.1
```
## How to use

### configuration

the default configuration file is rosetta-config.json

```
{
  "rosetta":{
    "version": "1.3.1",
    "port": 8080
  },

  "monitorOEP4ScriptHash": ["c27b58e3743062689fdcf1eae3ef5dc55b5ae68a",
  "e5a49d7fd57e7178e189d3965d1ee64368a1036d",
  "a0fcb515a1d42b4aaf9734aabf40411fa93f6849",
  "6df81bc4b30189b0987b54f1d02b62f732cfd8a1",
  "073e70265590c8e9c3617d115b1e4a36b26dd455",
  "ecc3ba5b1a2afcfcafa1a3f3b3a6e61d3018ac94",
  "b71fc841b203bcf08e81311131671885db689faf",
  "bdc9c45c6d706b54cf5772c48d43661fa7db25cd",
  "6bbc07bae862db0d7867e4e5b1a13c663e2b4bc8",
  "f916e8ebccbf27049b8444073032c27aa5c5c392",
  "78b98deed62aa708eaf6de85843734ecdfb14c1b",
  "24b3a4a8736a2ef70344bbdb4a9de82f0147caab",
  "b52b63902ed5d6455cd7929a13613fc1b88a056f",
  "59287ef2517ba65fb70fba8f0118d7fb4ed25fbc",
  "6c80f3a5c183edee7693a038ca8c476fb0d6ac91"]

}
```

rosetta 

​	version : rosetta sdk verison

​	port: rosetta restful api port

monitorOEP4ScriptHash:

OEP4 token codehash to monitor, you can find them on <https://explorer.ont.io/token/list/oep4/10/1>



## Restful API

Following  rosetta protocol(https://djr6hkgq2tjcs.cloudfront.net/docs/Reference.html) , ontology-rosetta providing following Restful APIs:

### Network

**/network/list**

*Get List of Available Networks*

Request:

```
{
    "metadata": {}
}
```

Response:

Sample

```
{
    "network_identifiers": [
        {
            "blockchain": "ont",
            "network": "mainnet"
        }
    ]
}
```

**/network/options**

*Get Network Options*

Request:

Use the available "network_identifier" from /network/list

```
{
    "network_identifier":  {
            "blockchain": "ont",
            "network": "mainnet"
        }
    
}
```

Response:

Sample

```
{
    "version": {
        "rosetta_version": "1.3.1",
        "node_version": "1.9.0"
    },
    "allow": {
        "operation_statuses": [
            {
                "status": "SUCCESS",
                "successful": true
            },
            {
                "status": "FAILED",
                "successful": false
            }
        ],
        "operation_types": [
            "transfer"
        ],
        "errors": [
            {
                "code": 400,
                "message": "network identifier is not supported",
                "retriable": false
            },
            {
                "code": 401,
                "message": "block identifier is empty",
                "retriable": false
            },
            {
                "code": 402,
                "message": "block index is invalid",
                "retriable": false
            },
            {
                "code": 403,
                "message": "get block failed",
                "retriable": true
            },
            {
                "code": 404,
                "message": "block hash is invalid",
                "retriable": false
            },
            {
                "code": 405,
                "message": "get transaction failed",
                "retriable": true
            },
            {
                "code": 406,
                "message": "transaction hash is invalid",
                "retriable": false
            },
            {
                "code": 407,
                "message": "commit transaction failed",
                "retriable": false
            },
            {
                "code": 408,
                "message": "tx hash is invalid",
                "retriable": false
            },
            {
                "code": 409,
                "message": "block is not exist",
                "retriable": false
            },
            {
                "code": 500,
                "message": "service not realize",
                "retriable": false
            },
            {
                "code": 501,
                "message": "addr is invalid",
                "retriable": true
            },
            {
                "code": 502,
                "message": "get balance error",
                "retriable": true
            },
            {
                "code": 503,
                "message": "parse int error",
                "retriable": true
            },
            {
                "code": 504,
                "message": "json marshal failed",
                "retriable": false
            },
            {
                "code": 505,
                "message": "parse tx payload failed",
                "retriable": false
            },
            {
                "code": 506,
                "message": "currency not config",
                "retriable": false
            },
            {
                "code": 507,
                "message": "params error",
                "retriable": true
            },
            {
                "code": 508,
                "message": "contract addr invalid",
                "retriable": true
            },
            {
                "code": 509,
                "message": "preExecute contract failed",
                "retriable": false
            },
            {
                "code": 510,
                "message": "query balance failed",
                "retriable": true
            }
        ]
    }
}
```



**/network/status**

*Get Network Status*

Request:

Use the available "network_identifier" from /network/list

```
{
    "network_identifier":  {
            "blockchain": "ont",
            "network": "mainnet"
        }
    
}
```

Response:

Sample

```
{
    "current_block_identifier": {
        "index": 4789126,
        "hash": "76fcf0fbd5e979721fe52e472ac79eb26f4bc502c371508574c0e03386be20e6"
    },
    "current_block_timestamp": 1560312815000,
    "genesis_block_identifier": {
        "index": 0,
        "hash": "1b8fa7f242d0eeb4395f89cbb59e4c29634047e33245c4914306e78a88e14ce5"
    },
    "peers": [
        {
            "peer_id": "4584491680478203539",
            "metadata": {
                "address": "3.21.156.220:20338",
                "height": 8325360,
                "state": 4
            }
        },
        {
            "peer_id": "15540261876814914032",
            "metadata": {
                "address": "23.99.134.190:20338",
                "height": 8325359,
                "state": 4
            }
        },
        {
            "peer_id": "18276482511736887962",
            "metadata": {
                "address": "18.220.195.232:20338",
                "height": 8325360,
                "state": 4
            }
        },
        {
            "peer_id": "16061082910762282354",
            "metadata": {
                "address": "139.219.138.225:20338",
                "height": 8325359,
                "state": 4
            }
        },
        {
            "peer_id": "6670297000549095677",
            "metadata": {
                "address": "52.231.153.200:20338",
                "height": 8325360,
                "state": 4
            }
        },
        {
            "peer_id": "407576854451017996",
            "metadata": {
                "address": "34.217.180.221:20338",
                "height": 8325360,
                "state": 4
            }
        }
    ]
}
```



### Account

**/account/balance**

*Get an Account Balance*

Request:

```json
{
    "network_identifier":  {
            "blockchain": "ont",
            "network": "mainnet"
        },
    "account_identifier": {
        "address": "AFmseVrdL9f9oyCzZefL9tG6UbviEH9ugK",
        "metadata": {}
    },
	"block_identifier": {
            "index": 310
        }
}
```

Response:

Sample:

```json
{
    "block_identifier": {
        "index": 310,
        "hash": "11405500403779cff364803bbd7fe4dc74ba9119015fd79473c188b727769c52"
    },
    "balances": [
        {
            "value": "14700000",
            "currency": {
                "symbol": "ONT",
                "decimals": 0,
                "metadata": {
                    "ContractAddress": "0100000000000000000000000000000000000000",
                    "TokenType": "Governance Token"
                }
            }
        },
        {
            "value": "1750000140000",
            "currency": {
                "symbol": "ONG",
                "decimals": 9,
                "metadata": {
                    "ContractAddress": "0200000000000000000000000000000000000000",
                    "TokenType": "Utility Token"
                }
            }
        }
    ]
}
```



## Block

**/block**

*Get a Block*

Request:

```json
{
    "network_identifier":  {
            "blockchain": "ont",
            "network": "mainnet"
        },
    "block_identifier": {
        "index":54
    }    
    
}
```

Response:

Sample:

```json
{
    "block": {
        "block_identifier": {
            "index": 54,
            "hash": "790ea8942e5722c75ba638312caa8c1380c41da4c145d6493ae510eb6017c5f3"
        },
        "parent_block_identifier": {
            "index": 53,
            "hash": "2b52c7fcdbdcd362211e1646fa6351c8f6fd4cbfa520fe7857133e59061ff348"
        },
        "timestamp": 1530389834000,
        "transactions": [
            {
                "transaction_identifier": {
                    "hash": "20247d9df50d830b8978a5c49313a6f8a118fd5bb9c2950e3c7f95f5ac6410f6"
                },
                "operations": [
                    {
                        "operation_identifier": {
                            "index": 0
                        },
                        "type": "transfer",
                        "status": "SUCCESS",
                        "account": {
                            "address": "AJMFNZL5jGjZJEhBrJfVLHJeJ3KwiczJ6B"
                        },
                        "amount": {
                            "value": "-1000000000",
                            "currency": {
                                "symbol": "ONT",
                                "decimals": 0,
                                "metadata": {
                                    "ContractAddress": "0100000000000000000000000000000000000000",
                                    "TokenType": "Governance Token"
                                }
                            }
                        }
                    },
                    {
                        "operation_identifier": {
                            "index": 1
                        },
                        "related_operations": [
                            {
                                "index": 0
                            }
                        ],
                        "type": "transfer",
                        "status": "SUCCESS",
                        "account": {
                            "address": "AWyEMxiLUVr5MeVJe3Fw5Xsij7iZUmfYyk"
                        },
                        "amount": {
                            "value": "1000000000",
                            "currency": {
                                "symbol": "ONT",
                                "decimals": 0,
                                "metadata": {
                                    "ContractAddress": "0100000000000000000000000000000000000000",
                                    "TokenType": "Governance Token"
                                }
                            }
                        }
                    }
                ]
            }
        ]
    }
}
```

**Note**

A transfer will record as  two operations (please refer to :<https://djr6hkgq2tjcs.cloudfront.net/docs/ApiDesign.html#single-party-linked-operations>)



**/block/transaction**

*Get a Block Transaction*

Request:

```json
{
    "network_identifier":  {
            "blockchain": "ont",
            "network": "mainnet"
        },
    "block_identifier": {
            "index": 54,
            "hash": "790ea8942e5722c75ba638312caa8c1380c41da4c145d6493ae510eb6017c5f3"
        },
    "transaction_identifier": {
        "hash": "20247d9df50d830b8978a5c49313a6f8a118fd5bb9c2950e3c7f95f5ac6410f6"
    }
    
}
```

Response:

Sample:

```
{
    "transaction": {
        "transaction_identifier": {
            "hash": "20247d9df50d830b8978a5c49313a6f8a118fd5bb9c2950e3c7f95f5ac6410f6"
        },
        "operations": [
            {
                "operation_identifier": {
                    "index": 0
                },
                "type": "transfer",
                "status": "SUCCESS",
                "account": {
                    "address": "AJMFNZL5jGjZJEhBrJfVLHJeJ3KwiczJ6B"
                },
                "amount": {
                    "value": "-1000000000",
                    "currency": {
                        "symbol": "ONT",
                        "decimals": 0,
                        "metadata": {
                            "ContractAddress": "0100000000000000000000000000000000000000",
                            "TokenType": "Governance Token"
                        }
                    }
                }
            },
            {
                "operation_identifier": {
                    "index": 1
                },
                "related_operations": [
                    {
                        "index": 0
                    }
                ],
                "type": "transfer",
                "status": "SUCCESS",
                "account": {
                    "address": "AWyEMxiLUVr5MeVJe3Fw5Xsij7iZUmfYyk"
                },
                "amount": {
                    "value": "1000000000",
                    "currency": {
                        "symbol": "ONT",
                        "decimals": 0,
                        "metadata": {
                            "ContractAddress": "0100000000000000000000000000000000000000",
                            "TokenType": "Governance Token"
                        }
                    }
                }
            }
        ]
    }
}
```

