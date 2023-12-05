# Transactional Management

## Transactional propogation type

### 1. PropogationType_REQUIRED_NEW
1.1 it requires its own new transaction.
1.2 If propogation type is required_new, then all other transaction would get suspended.
1.3 It instructs spring container to create new transaction. Even if out transaction boundry exists, it creates new database connection.

```
class EmployeeService{
@Transactional(propogation="propogation.---")
p.v.saveEmp(){

addressService.saveAddr(args);

}


class AddressService{
@Transactional(propogation="propogation.---") ..............propogation type provided
p.v. saveAddr(args){

}
```
   
### 2. Nested
 2.1 Nested act like Required transaction, except it has "savepoints" between nested invocation.
2.2 Spring checks if transaction exists, it creates savepoint,
2.3 in case of business logic throws exception, transaction get rolled back with the savepoint.
   
```
class EmployeeService{
@Transactional(propogation="propogation.---")
p.v.saveEmp(employee e){
emprepo.save(e); .................................transaction wont get affected since exception occured in addressService
addressService.saveAddr(args); .....................savepoint

}


class AddressService{
@Transactional(propogation="propogation.NESTED") ..............propogation type provided
p.v. saveAddr(args){

}
```
### 3. MANDATORY
It wont open up new transaction itself, but throws exeption if no active transaction is present.
If inner logical transaction get rolled back, then outer transaction also get rolled back.

```
class EmployeeService{
//@Transactional(propogation="propogation.---").......commented annotation
p.v.saveEmp(employee e){
emprepo.save(e); 
addressService.saveAddr(args); 

}


class AddressService{
@Transactional(propogation="propogation.MANDATORY") ..............propogation type provided
p.v. saveAddr(args){

}
```    
     
