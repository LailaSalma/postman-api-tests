# Postman API Tests: DummyJSON Products

Postman collection that tests the products endpoints of the public [DummyJSON](https://dummyjson.com) API. It runs from the command line with Newman, so it can later be used in a CI pipeline.

The collection checks the status code, the response schema (required fields and their types) and runs the same requests with several product IDs from a CSV file, including an ID that does not exist and must return 404.

## Repository contents

- `postman/Phase2CollectionOrganization.postman_collection.json`: the collection, with the requests grouped in a `Products` folder and the test scripts
- `postman/DummyJSON.postman_environment.json`: the environment, with the `baseUrl` variable (`https://dummyjson.com`)
- `postman/datadriven.csv`: the test data, one product ID and the expected status code per row

## Prerequisites

- Node.js (LTS version)
- Newman:

```bash
npm install -g newman
```

## How to run

From the repository root:

```bash
newman run postman/Phase2CollectionOrganization.postman_collection.json \
  -e postman/DummyJSON.postman_environment.json \
  -d postman/datadriven.csv
```

## Expected result

Newman runs 3 iterations, one per CSV row. A clean run finishes with 0 failed assertions, including the row that expects a 404 for a product that does not exist.
