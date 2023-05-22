# spring-boot-jwtAuth
In this project I used spring boot with some libraries managed by maven to create an authentication system that implements the Json Web Token architecture. The database that stores the users info is PostgreSQL and it's dropped each time the server reboots. Users password are also encrypted with SHA256
The system is pretty basic but it covers the main point that is having a functional authentication for users, as I didn't develop the front-end I tested it with Postman (warning: when writing the body on the post requests be sure to use the JSON format).
In order to do that we have I created 3 endpoints, 2 does not require a bearer token and one does:
1. `api/v1/auth/register`. This endpoint is on the whitelist and it's used to register a user to the database, once it's registered a JWT is returned. It requires a POST request with a body in this format:
```JSON
{
    "firstname": "Guillermo",
    "lastname": "JWT",
    "email": "guillermocasey@gmail.com",
    "password": "1234"
}
```
2. `api/v1/auth/authenticate`. This endpoint is also in the whitelist and it's used to login as a user, if the login runs successfully, a JWT is returned. It requires a POST request with a body in this format:
```JSON
{
    "email": "guillermocasey@gmail.com",
    "password": "1234"
}
```
3. `api/v1/demo-controller`. This endpoint is named demo as it can be some private part of the application. It requires a GET request with an authorization of type Bearer Token with the JWT that the user received in the register or login endpoint. If the token is null or expired, a 403 forbbiden response is returned.

I validated some things just by returning a 403 forbbiden response. For example, if the password is incorrect for that user's email.

## Technologies
* Spring Boot 3.0
* Spring Security
* JSON Web Tokens (JWT)
* BCrypt
* Maven

## Build

To build this project, you will need the following:

* JDK 17+
* Maven 3+


To build and run the project, follow these steps:

* Clone the repository: `https://github.com/guille-k6/spring-boot-jwtAuth`
* Navigate to the project directory: cd spring-boot-security-jwt
* Add database "jwt_security" to postgres 
* Build the project: mvn clean install
* Run the project: mvn spring-boot:run 

-> The application will be available at http://localhost:8080.

