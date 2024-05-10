# General Notes

## Common SDK Exceptions

- **UnprocessedKeys**
  - Some items were not successfully processed during a **BatchGetItem** operation.
- **UnprocessedItems**
  - Some items were not successfully processed during a **BatchWriteItem** operation.
- **ProvisionedThroughputExceededException**
  - None of the operations were processed, due to **exceeding the provisioned throughput** of the table.
- **Solutions**
  - Reduce the size of the request.
  - Request fewer items.
  - Use DAX to cache reads.
  - Increase **provisioned capacity**.

## Client Side Error Codes

- **400 - Access Denied Exception**: You don't have the required access.
- **403 - Missing Authentication Token**: The request did not contain a valid X.509 certificate or AWS access key ID.
- **404 - Malformed Query String**: The query string contains a syntax error.

## Server Side error Codes

- **500 - Internal Failure**: The request failed due to an unknown error, exception or failure.
- **503 - Service Unavailable**: The request failed due to a temporary failure of the server.