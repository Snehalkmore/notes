## Transactional Management

### Transactional propogation type
```
class EmployeeService{
@Transactional(PropogationType="")
p.v.saveEmp(){

addressService.saveAddr(args);

}


class AddressService{
@Transactional(PropogationType="...") ..............propogation type provided
p.v. saveAddr(args){

}
```
1. PropogationType_REQUIRED_NEW
          it requires its own new transaction. If propogation type is required_new, then all other transaction would get suspended. It instructs spring container to create new transaction 
2. 
