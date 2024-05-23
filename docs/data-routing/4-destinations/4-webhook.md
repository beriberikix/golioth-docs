---
title: webhook
---

|   |   |
|---|:---:|
|__Latest Version__| `v1.0.0` |
|__Input Content Type__| Any |

The `webhook` destination sends data via a `POST` request to the provided URL,
with the supplied headers.

### Parameters

|Parameter|Type|Description|Required|
|---|---|---|:---:|
|`url`|`string`| The connection string for a MongoDB instance. |✅|
|`headers`| Map (`string`: `string`)| Headers to be included in requests. ||

### Example Secrets

`API_KEY`
```
sup3rs3cr3t
```

### Example Usage

```yaml
    destination:
      type: webhook
      version: v1
      parameters:
        url: https://my-webhook.example.com
        headers:
         x-api-key: $API_KEY
```

### Example Input

```json
{
  "temp": 32
}
```

### Example Output

The following headers will be present on all requests, in addition to any
defined in the parameters.

- `Ce-Source`: ID of device
- `Ce-Subject`: ID of project
- `Ce-Type`: Prefixed path (if path is `/sensor`, the value will be
  `io.golioth.data.v1/.s/sensor`)
- `Content-Type`: the content type of the data message payload

```json
{
  "temp": 32
}
```
