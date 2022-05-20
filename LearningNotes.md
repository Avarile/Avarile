#### Nestjs

1. Backend basic logic:
  - Request / Response  <=>  Validate data contained in the request(PIPE) => Make sure the user is authenticated(Guard) => route a request to a particular function(Controller) => Run some business logic(Service) => Access a data base(Repository).
  - Parts of Nestjs:
    - Controller -> handles the incoming request.
    - Services -> handles the data access and business logic.
    - Modules -> Groups together codes.
    - Pipes -> Validate incoming data.
    - Filters -> handles errors that happens during requests handling.
    - Guards -> Handles authentication.
    - Interceptors -> Add extra logic to incoming requests or outgoing response.
    - Repositories -> Handles data stored in a DB.

2. Detail of an api module (use UserModule for instance):
  - ApiModule
    - UserEntity: Lists the different properties that a User has.
    - Methods to find, update, delete and create a user.
