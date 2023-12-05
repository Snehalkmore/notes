# Transactional Management

## Transactional propogation type


### 1. REQUIRED_NEW
1. it requires its own new transaction.
2. If propogation type is required_new, then all other transaction would get suspended.
3. It instructs spring container to create new transaction. Even if out transaction boundry exists, it creates new database connection.

```
class EmployeeService{
@Transactional(propogation="Propogation.---")
p.v.saveEmp(){

addressService.saveAddr(args);

}


class AddressService{
@Transactional(propogation="Propogation.---") ..............propogation type provided
p.v. saveAddr(args){

}
```
   
### 2. Nested
1. Nested act like Required transaction, except it has "savepoints" between nested invocation.
2. Spring checks if transaction exists, it creates savepoint,
3. in case of business logic throws exception, transaction get rolled back with the savepoint.
   
```
class EmployeeService{
@Transactional(propogation="Propogation.---")
p.v.saveEmp(employee e){
emprepo.save(e); .................................transaction wont get affected since exception occured in addressService
addressService.saveAddr(args); .....................savepoint

}


class AddressService{
@Transactional(propogation="Propogation.NESTED") ..............propogation type provided
p.v. saveAddr(args){

}
```
### 3. MANDATORY
1. It wont open up new transaction itself, but throws exeption if no active transaction is present.
2. If inner logical transaction get rolled back, then outer transaction also get rolled back.

```
class EmployeeService{
//@Transactional(propogation="Propogation.---").......commented annotation
p.v.saveEmp(employee e){
emprepo.save(e); 
addressService.saveAddr(args);  .......throws exception due to no transaction found

}


class AddressService{
@Transactional(propogation="Propogation.MANDATORY") ..............propogation type provided
p.v. saveAddr(args){

}
```

### 4. NEVER
1. It throws exception, if any some other transaction get started


### 5. NOT_SUPPORTED
1. If current transaction exists, it get suspended and business logic executed with transaction. 
2. The transaction will atuomicatically get resumed at the end.
3. After transaction resumed, either it can be rolled back or committed.
4. if RuntimeException thrown by  child() method, and it get propogated to parent() method and this logical transaction get rolled back.

```
class EmployeeService{
//@Transactional(propogation="Propogation.---").......commented annotation
p.v.saveEmp(employee e){
emprepo.save(e); 
addressService.saveAddr(args);  .......throws exception due to no transaction found

}


class AddressService{
@Transactional(propogation="Propogation.NOT_SUPPORTED") ..............propogation type provided
p.v. saveAddr(args){

}
```

### 6. SUPPORTS
It uses existing transaction, but does not open new transaction. 

### 7. REQUIRED (Default type . JPA have by default propogation type)
     
