
---

## Documentation

### Authentication & Signature

All endpoints require signature validation. The following headers are mandatory:

- `X-API-KEY`: Your API key
- `X-TIMESTAMP`: Unix timestamp in milliseconds
- `X-SIGNATURE`: Signature generated according to the rules below

---

### ✍️ Signature Generation Formats

| Endpoint                    | Signature Builder Used         | Message Format                                                   |
|----------------------------|-------------------------------|-----------------------------------------------------------------|
| `/api/v2/deposit`          | `DepositSignatureBuilder`      | `X-API-KEY + X-TIMESTAMP + URI + amount + currency`             |
| `/api/v2/withdraw`         | `WithdrawSignatureBuilder`     | `X-API-KEY + X-TIMESTAMP + URI + amount + currency`             |
| `/api/v2/available-banks`  | `DefaultSignatureBuilder`      | `X-API-KEY + X-TIMESTAMP + URI`                                 |

---

### 📥 POST `/api/v2/deposit`

Initiates a deposit transaction from the user.

#### Headers

```http
X-API-KEY: your-api-key
X-TIMESTAMP: 2024-06-18T12:00:00Z
X-SIGNATURE: your-signature
Content-Type: application/json
```


#### Request Body
```json
{
  "bankAccountId": "string",
  "amount": "string",
  "userId": "string",
  "userName": "string",
  "name": "string",
  "processId": "string",
  "iban": "string"
}
```


---

### 📤 POST `/api/v2/withdraw`

Initiates a withdrawal transaction from the user.

#### Headers

```http
X-API-KEY: your-api-key
X-TIMESTAMP: 2025-06-18T12:00:00Z
X-SIGNATURE: your-generated-signature
Content-Type: application/json
```


#### Request Body

```json
{
  "bankAccountId": "string",
  "amount": "string",
  "userId": "string",
  "userName": "string",
  "name": "string",
  "processId": "string",
  "iban": "string"
}
```


---

### 🏦 GET `/api/v2/available-banks`

Lists active banks available for the user to select.

#### Headers

```http
X-API-KEY: your-api-key
X-TIMESTAMP: 2025-06-18T12:00:00Z
X-SIGNATURE: your-generated-signature
```
---

### ✅ Response Format (Common)

```json
{
  "transactionId": "string",
  "bankId": "string",
  "amount": 100.00,
  "userId": "string",
  "userName": "string",
  "name": "string",
  "processId": "string",
  "type": "deposit | withdraw",
  "convertedName": "string",
  "status": "string",
  "bank": "string",
  "bankAccountName": "string",
  "bankAccountIban": "string",
  "exAmount": 105.50,
  "exName": 1.05
}
```


---

### 🛡️ Notes

- Even if the `currency` field is missing in the JSON, it is included as an empty string during signature generation.
- All date and numeric values should be sent in UTC and ISO 8601 format if applicable.
- If signature validation fails, the server responds with `401 Unauthorized`.

---
