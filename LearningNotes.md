#### Nestjs

1. Backend basic logic:
  - Request / Response  <=>  Validate data contained in the request(PIPE) => Make sure the user is authenticated(Guard) => route a request to a particular function(Controller) => Run some business logic(Service) => Access a data base(Repository).
  - Parts of Nestjs:
    - Entity -> Data Format for DB.
    - Controller -> handles the incoming request.
    - Services -> handles the data access and business logic.
    - Modules -> Groups together codes.
    - Pipes -> Validate incoming data. Request.payload normally utilizing Pipes
    - DTO -> To validate incoming request bodies, this is the Data Format to frontend. Response normally using DTO.
    - Filters -> handles errors that happens during requests handling. It's normally is an implementation of the Interceptors.
    - Guards -> Handles authentication. It's 
    - Interceptors -> Add extra logic to incoming requests or outgoing response.
    - Repositories -> Handles data stored in a DB.
    - Logger -> Nest already have it.


2. Detail of an api module (use UserModule for instance):
  - ApiModule
    - UserEntity: Lists the different properties that a User has.
    - Methods to find, update, delete and create a user.

3. Repositories of typeOrm:
  - create()
  - save()
  - insert()
  - update()
  - find(): run query
  - findOne(): run query return the first one
  - remove()
  - delete()
  
4. Definition of DTOs:
  - To validate incoming date in the body, so we gonna need class-validator and class-transformer
  - everything else is similar to the yup/zod, sort of.
  
5. Definition of Service:
  - Service is to call Repo's methods, in order to complete certain task --- create, update, delete, put......
  - the import should includes: Repository from typeorm
  - the import should includes: InjectRepository from @nestjs/typeorm  (you have a Repo then you need to inject it, pretty neat hah)
  - also the Entity themselves needs to be imported aswell.

6. Backend Flow:
  - Request => 
  - Validation Pipe(utilizing DTO to do the validation) => 
  - Controller(routing, retrive specific data from incoming request, filter harmful data if nessisary) => 
  - Service(utilizing the Entity), doing all the business logic
    - create / update / find / findOne / remove an entityInstance
    - all other business logics
    - save the entityInstance into the database 
    - => 
  - Repository(utilizing the Entity), Repo is generated by the typeorm and doing all the CRUD => 
  - DataBase well, just the data source

7. there are serveral hooks in the typeorm like @AfterUpdate @After

8. the reason why we dont use insert / update / delete is because they directly manipulate the data base, and won't trigger the hook. this may cause problems and we wont know why problems occurs.

9. IMPORTANT: the excepiton should be throw by the Service but not Controller

10. Filtered Response (for example: we dont actually return the password of a user when we get users)
  - below is How the request and response works:
  - Request [Get/users/2]                                                                                => UsersController[findUser()] => UserService[findOne()]
  - [Class Serializer Interceptor: Turns an instance of UserEntity into a plain object on some rule]     <=                [UserEntity] <=
  - so we can add @Exclude in any Column in Entity, to mark it that "this prop will not be returned"
  - and we also need to implement the  UseInterceptors(ClassSerializerInterceptor) to the Controllers we need to filter
  - on a second thought, what if a admin want to inspect all the users, and he should have all the infos --- including the password, so we need to make some change, here we need to create an custom interceptor.

11. Custom Decorator: Optional cuz this only make the codes more readerable. --- its actully just a function.



12. The entire authentication process: ![Authentication Process](https://github.com/Avarile/Avarile/blob/main/image0.png)
