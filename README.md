# Rails example: Todo Tasks API

### Run the code locally by Docker commands
```
docker-compose up -d
# create and migrate database
docker-compose run --rm web rake db:create db:migrate
```

## CURL Calls
### Login & Signup at the one request
If user is not existed, auto signup and signin
```
curl --request POST \
  --url http://localhost:3000/api/users/sign_in \
  --header 'Content-Type: application/json' \
  --data '{
	"user": {
		"email": "test@example.com",
		"password": "password"
	}
}'

# Sample response. Copy the token value to make an authorization for each request
{
	"user": {
		"id": 2,
		"email": "test@example.com",
		"token": "eyJhbGciOiJIUzI1NiJ9.eyJpZCI6MiwiZXhwIjoxNjQ1MDAxNDYxfQ.r_CH4BvjKhdxM1UQscUJ17T7x5_rs1nPGgjD42-eK8g"
	}
}
```

### Create task
```
curl --request POST \
  --url http://localhost:3000/api/tasks \
  --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJpZCI6MiwiZXhwIjoxNjQ1MDAxNDYxfQ.r_CH4BvjKhdxM1UQscUJ17T7x5_rs1nPGgjD42-eK8g' \
  --header 'Content-Type: application/json' \
  --data '{
	"task": {
		"title":"Test task title",
		"description":"Test task description"
	}
}'
```
### Run the test
#### Unit test
```
docker-compose run web bundle exec rspec test spec/models/
```
#### Integration test
```
docker-compose run web bundle exec rspec test spec/requests/
```