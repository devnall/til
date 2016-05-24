# Send a JSON blob to a webserver as a POST via curl

`curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' URL`

For example:

`curl -X POST -H "Content-Type: application/json" -d '{"name": "bob", "id": "100"}' https://www.domain.com`
