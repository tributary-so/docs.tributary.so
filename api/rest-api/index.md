# REST API

The Tributary API server exposes a REST interface for querying subscriptions, payment events, managing webhooks, and issuing JWT tokens. The full endpoint reference below is generated at build time from our live OpenAPI 3.0 spec.

**Base URL**: `https://api.tributary.so`

______________________________________________________________________

## Endpoint Reference

The reference is generated from the API server's JSDoc annotations and served live at `https://api.tributary.so/openapi.yaml`. If the spec is unreachable the section below will be empty — the API server may be starting up or the domain is not yet deployed.

# Tributary API 1.9.0

Modular Express API for subscription and payment services on Solana. Provides health checks, subscription status lookups, on-chain event queries, webhook management, JWT issuance, JWKS publishing, and admin key rotation.

______________________________________________________________________

**License:** MIT

## Servers

| Description       | URL                        |
| ----------------- | -------------------------- |
| Production        | <https://api.tributary.so> |
| Local development | <http://localhost:3002>    |

## Webhooks

______________________________________________________________________

### POST /v1/webhooks

Register a webhook

Description

Creates a new webhook subscription for a gateway.

**Request body**

```json
{
    "gateway_pubkey": "string",
    "endpoint_url": "string",
    "active": true
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the request body

```json
{
    "type": "object",
    "required": [
        "gateway_pubkey",
        "endpoint_url"
    ],
    "properties": {
        "gateway_pubkey": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Gateway authority public key."
        },
        "endpoint_url": {
            "type": "string",
            "format": "uri",
            "description": "HTTPS (or HTTP) URL Tributary will POST events to."
        },
        "active": {
            "type": "boolean",
            "default": true,
            "description": "Whether the webhook is active immediately."
        }
    }
}
```

**Responses**

```json
{
    "id": 1,
    "gateway_pubkey": "string",
    "endpoint_url": "string",
    "active": true,
    "created_at": "2022-04-13T15:42:05.901Z",
    "updated_at": "2022-04-13T15:42:05.901Z"
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "id",
        "gateway_pubkey",
        "endpoint_url",
        "active"
    ],
    "properties": {
        "id": {
            "type": "integer",
            "example": 1
        },
        "gateway_pubkey": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Gateway authority public key."
        },
        "endpoint_url": {
            "type": "string",
            "format": "uri",
            "description": "Webhook target URL."
        },
        "active": {
            "type": "boolean",
            "example": true
        },
        "created_at": {
            "type": "string",
            "format": "date-time"
        },
        "updated_at": {
            "type": "string",
            "format": "date-time"
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### GET /v1/webhooks

List webhooks

Description

Returns all webhooks, optionally filtered to active only and paginated.

**Input parameters**

| Parameter     | In    | Type    | Default | Nullable | Description                               |
| ------------- | ----- | ------- | ------- | -------- | ----------------------------------------- |
| `active_only` | query | boolean | False   | No       | When `true`, return only active webhooks. |
| `limit`       | query | integer |         | No       |                                           |
| `offset`      | query | integer |         | No       |                                           |

**Responses**

```json
[
    {
        "id": 1,
        "gateway_pubkey": "string",
        "endpoint_url": "string",
        "active": true,
        "created_at": "2022-04-13T15:42:05.901Z",
        "updated_at": "2022-04-13T15:42:05.901Z"
    }
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "$ref": "#/components/schemas/Webhook"
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### GET /v1/webhooks/gateway/{gatewayPubkey}

List webhooks for a gateway

Description

Returns all webhooks registered for the given gateway.

**Input parameters**

| Parameter       | In    | Type    | Default | Nullable | Description |
| --------------- | ----- | ------- | ------- | -------- | ----------- |
| `active_only`   | query | boolean | False   | No       |             |
| `gatewayPubkey` | path  | string  |         | No       |             |

**Responses**

```json
[
    {
        "id": 1,
        "gateway_pubkey": "string",
        "endpoint_url": "string",
        "active": true,
        "created_at": "2022-04-13T15:42:05.901Z",
        "updated_at": "2022-04-13T15:42:05.901Z"
    }
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "$ref": "#/components/schemas/Webhook"
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### DELETE /v1/webhooks/gateway/{gatewayPubkey}

Delete all webhooks for a gateway

**Input parameters**

| Parameter       | In   | Type   | Default | Nullable | Description |
| --------------- | ---- | ------ | ------- | -------- | ----------- |
| `gatewayPubkey` | path | string |         | No       |             |

**Responses**

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### GET /v1/webhooks/{id}

Get a webhook by ID

**Input parameters**

| Parameter | In   | Type    | Default | Nullable | Description |
| --------- | ---- | ------- | ------- | -------- | ----------- |
| `id`      | path | integer |         | No       |             |

**Responses**

```json
{
    "id": 1,
    "gateway_pubkey": "string",
    "endpoint_url": "string",
    "active": true,
    "created_at": "2022-04-13T15:42:05.901Z",
    "updated_at": "2022-04-13T15:42:05.901Z"
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "id",
        "gateway_pubkey",
        "endpoint_url",
        "active"
    ],
    "properties": {
        "id": {
            "type": "integer",
            "example": 1
        },
        "gateway_pubkey": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Gateway authority public key."
        },
        "endpoint_url": {
            "type": "string",
            "format": "uri",
            "description": "Webhook target URL."
        },
        "active": {
            "type": "boolean",
            "example": true
        },
        "created_at": {
            "type": "string",
            "format": "date-time"
        },
        "updated_at": {
            "type": "string",
            "format": "date-time"
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### PUT /v1/webhooks/{id}

Toggle a webhook's active flag

**Input parameters**

| Parameter | In   | Type    | Default | Nullable | Description |
| --------- | ---- | ------- | ------- | -------- | ----------- |
| `id`      | path | integer |         | No       |             |

**Request body**

```json
{
    "active": true
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the request body

```json
{
    "type": "object",
    "required": [
        "active"
    ],
    "properties": {
        "active": {
            "type": "boolean"
        }
    }
}
```

**Responses**

```json
{
    "id": 1,
    "gateway_pubkey": "string",
    "endpoint_url": "string",
    "active": true,
    "created_at": "2022-04-13T15:42:05.901Z",
    "updated_at": "2022-04-13T15:42:05.901Z"
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "id",
        "gateway_pubkey",
        "endpoint_url",
        "active"
    ],
    "properties": {
        "id": {
            "type": "integer",
            "example": 1
        },
        "gateway_pubkey": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Gateway authority public key."
        },
        "endpoint_url": {
            "type": "string",
            "format": "uri",
            "description": "Webhook target URL."
        },
        "active": {
            "type": "boolean",
            "example": true
        },
        "created_at": {
            "type": "string",
            "format": "date-time"
        },
        "updated_at": {
            "type": "string",
            "format": "date-time"
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### DELETE /v1/webhooks/{id}

Delete a webhook

**Input parameters**

| Parameter | In   | Type    | Default | Nullable | Description |
| --------- | ---- | ------- | ------- | -------- | ----------- |
| `id`      | path | integer |         | No       |             |

**Responses**

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

## Tokens

______________________________________________________________________

### POST /v1/tokens/issue

Issue a short-lived JWT

Description

Validates that the caller has an active subscription policy (or a recent payment transaction signature) and issues a JWT bound to the subscription. Rate-limited to 200 requests per minute per wallet.

**Request body**

```json
{
    "walletPublicKey": "string",
    "tokenMint": "string",
    "policyAddress": "string",
    "recipient": "string",
    "transactionSignature": "string",
    "trackingId": "string"
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the request body

```json
{
    "type": "object",
    "properties": {
        "walletPublicKey": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Caller wallet public key (required unless `transactionSignature` is supplied)."
        },
        "tokenMint": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "SPL token mint of the subscription."
        },
        "policyAddress": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Specific payment policy address."
        },
        "recipient": {
            "type": "string",
            "minLength": 32,
            "maxLength": 44,
            "description": "Recipient wallet public key."
        },
        "transactionSignature": {
            "type": "string",
            "pattern": "^[1-9A-HJ-NP-Za-km-z]{87,88}$",
            "description": "Base58 transaction signature of a recent payment."
        },
        "trackingId": {
            "type": "string",
            "description": "Checkout tracking ID."
        }
    }
}
```

**Responses**

Schema of the response body

```json
{
    "type": "object",
    "description": "Token bundle (shape defined by the token issuer service)."
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

## Subscriptions

______________________________________________________________________

### GET /v1/subscriptions

Look up subscription details

Description

Returns matching subscription policy records. Provide at least one filter (up to three combined). If `walletPublicKey` is given, `tokenMint` is also required.

**Input parameters**

| Parameter          | In    | Type   | Default | Nullable | Description                                    |
| ------------------ | ----- | ------ | ------- | -------- | ---------------------------------------------- |
| `gatewayPublicKey` | query | string |         | No       | Gateway authority public key.                  |
| `recipient`        | query | string |         | No       | Recipient wallet public key.                   |
| `tokenMint`        | query | string |         | No       | SPL token mint. Defaults to USDC when omitted. |
| `trackingId`       | query | string |         | No       | Tracking ID assigned at checkout.              |
| `userPublicKey`    | query | string |         | No       | User (owner) wallet public key.                |
| `walletPublicKey`  | query | string |         | No       | User wallet public key (requires `tokenMint`). |

**Responses**

```json
{
    "success": true,
    "data": [
        {}
    ],
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "success",
        "data",
        "timestamp"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": true
        },
        "data": {
            "type": "array",
            "items": {
                "type": "object",
                "description": "Subscription policy record (gateway, recipient, schedule, status)."
            }
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch ms."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

## Skill

______________________________________________________________________

### GET /v1/skill/{encoded}

Generate Lando skill markdown

Description

Decodes a base64-encoded checkout session, fetches mint decimals on-chain, converts the human-readable amount to its integer representation, and renders a `text/markdown` skill document the Lando agent uses to drive the subscription checkout.

**Input parameters**

| Parameter | In   | Type   | Default | Nullable | Description                                                                  |
| --------- | ---- | ------ | ------- | -------- | ---------------------------------------------------------------------------- |
| `encoded` | path | string |         | No       | Base64-encoded subscription parameters produced by `CheckoutSessionManager`. |

**Responses**

```json
"string"
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "string"
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

## OneTime

______________________________________________________________________

### GET /v1/onetime/{trackingId}

Look up one-time payment

Description

Returns one-time payment records for a tracking ID. Optionally filter by recipient and paginate with `limit` / `offset`.

**Input parameters**

| Parameter    | In    | Type    | Default | Nullable | Description                            |
| ------------ | ----- | ------- | ------- | -------- | -------------------------------------- |
| `limit`      | query | integer | 100     | No       | Maximum records to return.             |
| `offset`     | query | integer | 0       | No       | Number of records to skip.             |
| `recipient`  | query | string  |         | No       | Filter by recipient wallet public key. |
| `trackingId` | path  | string  |         | No       | Tracking ID assigned at checkout.      |

**Responses**

```json
{
    "success": true,
    "data": null,
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "success",
        "data",
        "timestamp"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": true
        },
        "data": {
            "oneOf": [
                {
                    "type": "object",
                    "description": "Single record (when exactly one matches)."
                },
                {
                    "type": "array",
                    "items": {
                        "type": "object"
                    },
                    "description": "Multiple records."
                }
            ]
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch ms."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

## JWKS

______________________________________________________________________

### GET /v1/jwks

JWKS (mounted under /.well-known too)

Description

Returns the JSON Web Key Set used to verify JWTs issued by `/v1/tokens/issue`. Cached publicly for 1 hour. Also served at `/.well-known/jwks.json` for OIDC-style discovery.

**Responses**

```json
{
    "keys": [
        {}
    ]
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "keys"
    ],
    "properties": {
        "keys": {
            "type": "array",
            "items": {
                "type": "object",
                "description": "JWK (RFC 7517) — kid, kty, alg, use, crv, x, y."
            }
        }
    }
}
```

**Response headers**

| Name            | Description | Schema |
| --------------- | ----------- | ------ |
| `Cache-Control` |             | string |

## Health

______________________________________________________________________

### GET /v1/health

Health check

Description

Returns service liveness, name, and version.

**Responses**

```json
{
    "success": true,
    "data": {
        "status": "ok",
        "service": "tributary-api",
        "version": "1.9.0"
    },
    "timestamp": 1719300000000
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "success",
        "data",
        "timestamp"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": true
        },
        "data": {
            "type": "object",
            "required": [
                "status",
                "service",
                "version"
            ],
            "properties": {
                "status": {
                    "type": "string",
                    "example": "ok"
                },
                "service": {
                    "type": "string",
                    "example": "tributary-api"
                },
                "version": {
                    "type": "string",
                    "example": "1.9.0"
                }
            }
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds.",
            "example": 1719300000000
        }
    }
}
```

## Events

______________________________________________________________________

### GET /v1/events

Query on-chain events

Description

Polymorphic event lookup. Exactly one filter mode is applied per request, evaluated in this priority order: `signature` → `slot` → `trackingId` → `eventName` → `startTime`/`endTime`. If none match, a generic `searchEvents` is run.

**Input parameters**

| Parameter    | In    | Type    | Default | Nullable | Description                                                   |
| ------------ | ----- | ------- | ------- | -------- | ------------------------------------------------------------- |
| `endTime`    | query | string  |         | No       |                                                               |
| `eventName`  | query | string  |         | No       | Event name filter.                                            |
| `limit`      | query | integer | 100     | No       |                                                               |
| `maxSlot`    | query | integer |         | No       |                                                               |
| `minSlot`    | query | integer |         | No       |                                                               |
| `offset`     | query | integer | 0       | No       |                                                               |
| `signature`  | query | string  |         | No       | Transaction signature (returns a single event or 404).        |
| `slot`       | query | integer |         | No       | Solana slot number.                                           |
| `startTime`  | query | string  |         | No       |                                                               |
| `trackingId` | query | string  |         | No       | Encoded memo tracking ID (matched via 64-byte memo encoding). |

**Responses**

Schema of the response body

```json
{
    "oneOf": [
        {
            "type": "object",
            "description": "Single event (when `signature` is supplied)."
        },
        {
            "type": "array",
            "items": {
                "type": "object"
            },
            "description": "Event list."
        }
    ]
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

### GET /v1/events/count

Count events

Description

Returns a count of events optionally filtered by name and/or time range.

**Input parameters**

| Parameter   | In    | Type   | Default | Nullable | Description |
| ----------- | ----- | ------ | ------- | -------- | ----------- |
| `endTime`   | query | string |         | No       |             |
| `eventName` | query | string |         | No       |             |
| `startTime` | query | string |         | No       |             |

**Responses**

```json
{
    "count": 42
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "count"
    ],
    "properties": {
        "count": {
            "type": "integer",
            "example": 42
        }
    }
}
```

______________________________________________________________________

### GET /v1/events/names

All known event names

Description

Returns the distinct set of event names indexed in the database.

**Responses**

```json
[
    "string"
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "string"
    }
}
```

______________________________________________________________________

### GET /v1/events/names/tributary

Tributary event names

Description

Returns the canonical set of event names emitted by the Tributary program.

**Responses**

```json
[
    "string"
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "string"
    }
}
```

______________________________________________________________________

### GET /v1/events/payments

Payment records

Description

Returns `PaymentRecord` events optionally filtered by gateway and/or policy.

**Input parameters**

| Parameter       | In    | Type    | Default | Nullable | Description |
| --------------- | ----- | ------- | ------- | -------- | ----------- |
| `gateway`       | query | string  |         | No       |             |
| `limit`         | query | integer | 100     | No       |             |
| `offset`        | query | integer | 0       | No       |             |
| `paymentPolicy` | query | string  |         | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/payments/stats

Payment statistics

Description

Aggregated payment statistics (count, volume) optionally filtered by gateway and/or time range.

**Input parameters**

| Parameter   | In    | Type   | Default | Nullable | Description |
| ----------- | ----- | ------ | ------- | -------- | ----------- |
| `endTime`   | query | string |         | No       |             |
| `gateway`   | query | string |         | No       |             |
| `startTime` | query | string |         | No       |             |

**Responses**

Schema of the response body

```json
{
    "type": "object"
}
```

______________________________________________________________________

### GET /v1/events/policies/created

PolicyCreated events

Description

Returns `PaymentPolicyCreated` events.

**Input parameters**

| Parameter     | In    | Type    | Default | Nullable | Description |
| ------------- | ----- | ------- | ------- | -------- | ----------- |
| `gateway`     | query | string  |         | No       |             |
| `limit`       | query | integer | 100     | No       |             |
| `offset`      | query | integer | 0       | No       |             |
| `recipient`   | query | string  |         | No       |             |
| `userPayment` | query | string  |         | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/policies/deleted

PolicyDeleted events

**Input parameters**

| Parameter       | In    | Type    | Default | Nullable | Description |
| --------------- | ----- | ------- | ------- | -------- | ----------- |
| `limit`         | query | integer | 100     | No       |             |
| `offset`        | query | integer | 0       | No       |             |
| `owner`         | query | string  |         | No       |             |
| `paymentPolicy` | query | string  |         | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/policies/status-changed

PolicyStatusChanged events

**Input parameters**

| Parameter       | In    | Type    | Default | Nullable | Description |
| --------------- | ----- | ------- | ------- | -------- | ----------- |
| `limit`         | query | integer | 100     | No       |             |
| `offset`        | query | integer | 0       | No       |             |
| `paymentPolicy` | query | string  |         | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/gateways/created

GatewayCreated events

**Input parameters**

| Parameter   | In    | Type    | Default | Nullable | Description |
| ----------- | ----- | ------- | ------- | -------- | ----------- |
| `authority` | query | string  |         | No       |             |
| `limit`     | query | integer | 100     | No       |             |
| `offset`    | query | integer | 0       | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/gateways/deleted

GatewayDeleted events

**Input parameters**

| Parameter   | In    | Type    | Default | Nullable | Description |
| ----------- | ----- | ------- | ------- | -------- | ----------- |
| `authority` | query | string  |         | No       |             |
| `gateway`   | query | string  |         | No       |             |
| `limit`     | query | integer | 100     | No       |             |
| `offset`    | query | integer | 0       | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/gateways/fee-bps-changed

GatewayFeeBpsChanged events

**Input parameters**

| Parameter | In    | Type    | Default | Nullable | Description |
| --------- | ----- | ------- | ------- | -------- | ----------- |
| `gateway` | query | string  |         | No       |             |
| `limit`   | query | integer | 100     | No       |             |
| `offset`  | query | integer | 0       | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/gateways/fee-recipient-changed

GatewayFeeRecipientChanged events

**Input parameters**

| Parameter | In    | Type    | Default | Nullable | Description |
| --------- | ----- | ------- | ------- | -------- | ----------- |
| `gateway` | query | string  |         | No       |             |
| `limit`   | query | integer | 100     | No       |             |
| `offset`  | query | integer | 0       | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/gateways/signer-changed

GatewaySignerChanged events

**Input parameters**

| Parameter | In    | Type    | Default | Nullable | Description |
| --------- | ----- | ------- | ------- | -------- | ----------- |
| `gateway` | query | string  |         | No       |             |
| `limit`   | query | integer | 100     | No       |             |
| `offset`  | query | integer | 0       | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/referrals/rewards

ReferralRewardDistributed events

**Input parameters**

| Parameter       | In    | Type    | Default | Nullable | Description |
| --------------- | ----- | ------- | ------- | -------- | ----------- |
| `gateway`       | query | string  |         | No       |             |
| `limit`         | query | integer | 100     | No       |             |
| `offset`        | query | integer | 0       | No       |             |
| `paymentPolicy` | query | string  |         | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/user-payments/created

UserPaymentCreated events

**Input parameters**

| Parameter   | In    | Type    | Default | Nullable | Description |
| ----------- | ----- | ------- | ------- | -------- | ----------- |
| `limit`     | query | integer | 100     | No       |             |
| `offset`    | query | integer | 0       | No       |             |
| `owner`     | query | string  |         | No       |             |
| `tokenMint` | query | string  |         | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/program/config-created

ProgramConfigCreated events

**Input parameters**

| Parameter | In    | Type    | Default | Nullable | Description |
| --------- | ----- | ------- | ------- | -------- | ----------- |
| `admin`   | query | string  |         | No       |             |
| `limit`   | query | integer | 100     | No       |             |
| `offset`  | query | integer | 0       | No       |             |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

______________________________________________________________________

### GET /v1/events/typed/{eventName}

Typed event lookup

Description

Returns strongly-typed events for the given Tributary event name.

**Input parameters**

| Parameter   | In    | Type    | Default | Nullable | Description                                              |
| ----------- | ----- | ------- | ------- | -------- | -------------------------------------------------------- |
| `eventName` | path  | string  |         | No       | Tributary event name (see `/v1/events/names/tributary`). |
| `limit`     | query | integer | 100     | No       |                                                          |
| `offset`    | query | integer | 0       | No       |                                                          |

**Responses**

```json
[
    {}
]
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "array",
    "items": {
        "type": "object"
    }
}
```

## Admin

______________________________________________________________________

### POST /v1/admin/keys/rotate

Rotate the JWT signing key

Description

Generates a new signing key, promotes it as active, and keeps the previous key in the JWKS for a grace period so in-flight tokens continue to validate. Requires the `x-admin-key` header.

**Input parameters**

| Parameter     | In     | Type   | Default | Nullable | Description                                          |
| ------------- | ------ | ------ | ------- | -------- | ---------------------------------------------------- |
| `AdminApiKey` | header | string | N/A     | No       | Admin API key (ADMIN_API_KEY env var on the server). |

**Responses**

```json
{
    "message": "Key rotated successfully",
    "newKid": "string",
    "oldKid": "string",
    "gracePeriodEndsAt": "2022-04-13T15:42:05.901Z"
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "message",
        "newKid",
        "oldKid",
        "gracePeriodEndsAt"
    ],
    "properties": {
        "message": {
            "type": "string",
            "example": "Key rotated successfully"
        },
        "newKid": {
            "type": "string",
            "description": "New active key ID."
        },
        "oldKid": {
            "type": "string",
            "description": "Previous key ID (still in JWKS during grace)."
        },
        "gracePeriodEndsAt": {
            "type": "string",
            "format": "date-time",
            "description": "ISO 8601 timestamp after which the old key is retired."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

```json
{
    "success": false,
    "error": "string",
    "timestamp": 0
}
```

⚠️ *This example has been generated automatically from the schema and it is not accurate. Refer to the schema for more information.*

Schema of the response body

```json
{
    "type": "object",
    "required": [
        "error"
    ],
    "properties": {
        "success": {
            "type": "boolean",
            "example": false
        },
        "error": {
            "type": "string"
        },
        "timestamp": {
            "type": "integer",
            "description": "Unix epoch milliseconds."
        }
    }
}
```

______________________________________________________________________

## Schemas

### Error

| Name        | Type    | Description              |
| ----------- | ------- | ------------------------ |
| `error`     | string  |                          |
| `success`   | boolean |                          |
| `timestamp` | integer | Unix epoch milliseconds. |

### Webhook

| Name             | Type              | Description                   |
| ---------------- | ----------------- | ----------------------------- |
| `active`         | boolean           |                               |
| `created_at`     | string(date-time) |                               |
| `endpoint_url`   | string(uri)       | Webhook target URL.           |
| `gateway_pubkey` | string            | Gateway authority public key. |
| `id`             | integer           |                               |
| `updated_at`     | string(date-time) |                               |

## Security schemes

| Name        | Type   | Scheme | Description                                          |
| ----------- | ------ | ------ | ---------------------------------------------------- |
| AdminApiKey | apiKey |        | Admin API key (ADMIN_API_KEY env var on the server). |

## Tags

| Name          | Description                           |
| ------------- | ------------------------------------- |
| Health        | Service health probes                 |
| Skill         | Lando skill markdown generation       |
| Subscriptions | Recurring subscription lookups        |
| OneTime       | One-time payment lookups              |
| Events        | On-chain event queries                |
| Webhooks      | Webhook endpoint management           |
| Tokens        | JWT issuance for active subscriptions |
| JWKS          | JWT key set publishing                |
| Admin         | Administrative key rotation           |

______________________________________________________________________

## Authentication

The API exposes a mix of public read endpoints and gateway-scoped write endpoints:

- **Public reads** (e.g. `GET /subscriptions`, `GET /events/*`) require no authentication.
- **Gateway writes** (e.g. webhook management) are authorized via the gateway signer key.
- **JWT tokens** for checkout sessions are issued via the `/tokens` family — see the SDK's `jwt-auth` docs for client-side use.

______________________________________________________________________

## Asset Catalog (`/v1/assets/*`)

A public, IP-rate-limited (120/min) proxy to the tokens.xyz asset catalog. The upstream `x-api-key` is injected server-side — never shipped to the browser. Used by the type-ahead token picker in both `apps/app` and `apps/showcase-payment-policies` (ADR-0028). Responses are wrapped in the standard `ApiResponse<T>` envelope.

### `GET /v1/assets/search?q=<query>&limit=<n>`

Search the catalog for assets (stablecoins, LSTs, tokenized equities, …). Server filters out any result whose primary variant is missing or whose mint isn't a valid Solana base58 mint.

| Param   | Required | Default | Notes                      |
| ------- | -------- | ------- | -------------------------- |
| `q`     | yes      | —       | Symbol, name, or asset id. |
| `limit` | no       | `20`    | Clamped to `[1, 50]`.      |

**Failure stance:** on upstream error, returns `200` with `results: []` (empty state, not error state). Redis-cached per query for 60s.

```bash
curl 'https://api.tributary.so/v1/assets/search?q=usdc&limit=5'
```

```json
{
  "success": true,
  "data": {
    "query": "usdc",
    "results": [
      {
        "assetId": "usd",
        "symbol": "USDC",
        "name": "USD Coin",
        "category": "stablecoin",
        "imageUrl": null,
        "primaryVariant": {
          "mint": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
          "decimals": 6,
          "kind": "native",
          "trustTier": "tier1"
        }
      }
    ]
  },
  "timestamp": 1783070812696
}
```

### `GET /v1/assets/resolve?mint=<base58>`

Resolve a single Solana mint to its asset metadata.

| Param  | Required | Notes                            |
| ------ | -------- | -------------------------------- |
| `mint` | yes      | Solana base58 mint, 32-44 chars. |

**Failure stance:** on upstream error, falls back to the baked-in `MINT_OVERRIDES` map (USDC, SOL, USDT, mSOL, devnet USDC) so account balances never render as truncated mints. Returns `404` only when the mint is unknown to upstream **and** absent from the fallback map. Redis-cached per mint for 10min.

```bash
curl 'https://api.tributary.so/v1/assets/resolve?mint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v'
```

```json
{
  "success": true,
  "data": {
    "mint": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
    "assetId": "usd",
    "symbol": "USDC",
    "name": "USD Coin",
    "decimals": 6,
    "imageUrl": null,
    "category": "stablecoin"
  },
  "timestamp": 1783070812696
}
```

### Client package

Browser consumers should use the shared `@tributary-so/tokens-client` package (pure fetch client + react-query hooks) rather than hand-rolling the envelope handling. See ADR-0028 for the design and `packages/tokens-client/src/` for the API.

______________________________________________________________________

## SDK Integration

For programmatic access, use the `@tributary-so/sdk` or `@tributary-so/payments` packages instead of raw HTTP calls where possible. See:

- [TypeScript SDK](https://docs.tributary.so/integration-guide/pull-payments/sdk/index.md)
- [Checkout Links](https://docs.tributary.so/integration-guide/pull-payments/checkout/index.md)
- [JWT Auth](https://docs.tributary.so/integration-guide/pull-payments/jwt-auth/index.md)
