
# RestAPI with WebFlux and Security
## Using
* Spring Boot 3
* Spring Security (JWT)
* spring webflux
* Spring Data R2DBC
* Map Structure
* PostgreSQL
* flyway
# Local application launch
* Install PostgreSQL
# Create database
```
CREATE DATABASE "proselyte_webflux_security";
```
# Set correct values in application.yaml
```
spring:r2dbc:username
```
```
spring:r2dbc:password
```
# CURL requests:
### 1. User registration
```
curl --location 'http://localhost:8083/api/v1/auth/register' \
--header 'Content-Type: application/json' \
--data '{
     "username": "proselyte",
     "password": "test",
     "first_name": "Eugene",
     "last_name": "Suleimanov"
}'
```
### Answer example:
```
{
   "id": 1,
   "username": "proselyte",
   "role": "USER",
   "first_name": "Eugene",
   "last_name": "Suleimanov",
   "enabled": true
   "created_at": "2023-05-13T14:53:32.36094",
   "updated_at": "2023-05-13T14:53:32.360954"
}
```
### 2. User authentication
```
curl --location 'http://localhost:8083/api/v1/auth/login' \
--header 'Content-Type: application/json' \
--data '{
     "username": "proselyte",
     "password": "test"
   }'
   ```
### Response Example
```
{
  "user_id": 1,
  "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiI0Iiwicm9sZSI6IlVTRVIiLCJpc3MiOiJwcm9zZWx5dGUiLCJleHAiOjE2ODM5ODI0MzYsImlhdCI6MTY4Mzk3ODgzNiwianRpIjoiZjlmZDliMjYtN2UyOC00Y2QzLWIzY2MtOWM3MjdmNTdkNTliIiwidXNlcm5hbWUiOiJwcm9zZWx5dGUifQ.8gdTqi18le0h4GTAd_JnxTDybnDFQS03biRnMbRRpQQ",
  "issued_at": "2023-05-13T11:53:56.390+00:00",
  "expires_at": "2023-05-13T12:53:56.390+00:00"
}
```
### 3. Getting user data using the token received in the previous request
```
curl --location 'http://localhost:8083/api/v1/auth/info' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiI0Iiwicm9sZSI6IlVTRVIiLCJpc3MiOiJwcm9zZWx5dGUiLCJleHAiOjE2ODM5ODI0MzYsImlhdCI6MTY4Mzk3ODgzNiwianRpIjoiZj lmZDliMjYtN2UyOC00Y2QzLWIzY2MtOWM3MjdmNTdkNTliIiwidXNlcm5hbWUiOiJwcm9zZWx5dGUifQ.8gdTqi18le0h4GTAd_JnxTDybnDFQS03biRnMbRRpQQ'
```
### Response Example
```
{
   "id": 1,
   "username": "proselyte",
   "role": "USER",
   "first_name": "Eugene",
   "last_name": "Suleimanov",
   "enabled": true
   "created_at": "2023-05-13T14:02:37.248466",
   "updated_at": "2023-05-13T14:02:37.248482"
}
```
