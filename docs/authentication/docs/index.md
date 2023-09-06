## Authentication

We provide a REST API in a JSON format. The authentication API is a good start to test the connection.

Every request done to the API requires the api-key and account-id in the header (REST), as well as the correct content type for data transfers.

**GET**

```
https://dropday.io/api/v1
```

**Header example**

```json
{
  "Content-Type": "application/json",
  "Accept": "application/json",
  "api-key": "tdh7nNUp3DZAHsMtw3dQYhDsm3wf593hMGbyXP6Y5R8DTF2Rwy4QCvkWFYQb",
  "account-id": "101",
}
```