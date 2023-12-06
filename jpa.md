# JPA notes

## Difference between JPA and CRUD repository
<img width="484" alt="image" src="https://github.com/Snehalkmore/notes/assets/14993594/ecb193af-c8ff-4f14-985e-fb83ecee91a4">


## JPA FIND Query
```
public interface StudentRepo implements JpaRepository<customCLass,int>{


 List<Student> findByName(String name);

 ....And is used similarly we can use or
 List<Student> findByNameAndAge(String name, int age);

 ....greaterThan operator
 List<Student> findByAgeGreaterThan(int age);

....contains operator
 List<Student> findByPincodeNameContains(int pincode);

....between operator
 List<Student> findByAgeBetween(int minAge,int maxAge);

....in operator
 List<Student> findByIdIn(List<Integer> ids);

...like operator
List<Student> findNameLike(String name); ..... pass input like %name%
   
}

```

## JPA Paging and Sorting

how to test?

```
Pageable pageable = new PageRequest(int pageIndex, int noOfRecordsOnPage);    ...... Pageable interface & PageRequest class
Page<Student> studentsPerPage = studentRepository.findAll(pageable);           .............Page<Studdent>
studentsPerPage.stream().forEach(e->sysout(e.getName));
***********************************************************************

Sort Desc order with multiple properties
------------------------------------------
List<Student> students = repositroy.findAll(new Sort(Direction.DESC,"name",age))      .... first sort by name then age in desc order

*************************************************************************************

Sort with diff order
----------------------------
List<Student> students = repositroy.findAll(
             new Sort(new Sort.Order(Direction.DESC,"name")
             ,new Sort(new Sort.Order(Direction.ASC,"age"))
```



## Native Query - simple sql query and named paramenter query exampl
```
public interface StudentRepo implements JpaRepository<customCLass,int>{

@Query(value = "select * from student", nativeQuery=true)        ............simple query
List<Student> findAllStudentNQ();


@Query(value = "select * from student where fnm =:firstName", nativeQuery=true)      ............named parameter query
List<Student> findAllStudentNQ(@Param("firstName")String firstName);

}

```


## JPQL

```
read queries
public interface StudentRepo implements JpaRepository<customCLass,int>{

@Query(value = "select st.fnm,st.age from student st")        .........partial data fetch
List<Student> findAllStudentPartialData();


@Query(value = "from student where name=:fmn")                   ............find by name
List<Student> findByFirstName(@Param("fmn") String fmn);

@Modifying
@Query(value = "delete from student where name=:fmn")                   ............delete by name use @Modifying
List<Student> deleteStudentByFirstName(@Param("fmn") String fmn);


}
```


Note : 
1. use @Modifying for delete update or insert queries
2. In Junit, if we annotate test method with @transactional, we cannot commit the changes to db since it get rolled back.
in case, if we want to persist changes done from junit testing, then use @Rollback(false) annotation over method

```
@Test
@Transactional
@Rollback(false)
public void testmethod(){
 repo.deleteStudentByFirstName("SM");
}
```



## custom ID generator strategy
1. create class and implement IdentifierGenerator interface
2. override generate method which return Serializable
```
class CustomGenerator implements IdentifierGenerator{

@Override
public Serializable generate(SessionImplementor session,Object obj) throws HibernateException{
Random rm = new Random();
long id=0L;
id = rm.nextInt(1000000);
return id;
}
}
```
3. in Entity class for example employee
 ```
   @Entity
   @Table
   class Employee{

   @GenericGenerator(name="emp_id",strategy="full.class.path.of.custom.generator.CustomGenerator")
   @Id
   @GeneratedValue(generator="emp_id")
   private long id;

   }
 ```




## Composite key
```
@Embeddable                       ........this annotation makes composite key
class EmployeeIdentity{          ---------------composite key
   private String empId;
   private String companyId;
}

@Entity
@Table
class EMployee{

  @EmbeddedId                     ...................... this annotation used to add composite key in entity class
  private EmployeeIdentity id;

  private String name;
  private String email;

}
```



## JPA Inheritance strategy Mapping (SINGLE_TABLE ,JOINED, TABLE_PER_CLASS)

1. SINGLE TABLE
```
create table payment(
id int PRIMARY KEY,
pmode varchar(2),
amount decimal(8,3) ,
cardnumber varchar(20),
checknumber varchar(20)
);
```

```
@Inheritance(strategy=InheritanceTypr.SINGLE_TABLE)
@DiscrimatorColumn(name="mode",discriminatorType=DiscriminatorType.String)
abstract class Payment{
  private int id;
  private double amount;
}

@DisciminatorValue(value="ch")
class Check  extends Payment{
}

@DisciminatorValue(value="cc")
class creditCard  extends Payment{
}
```
2. TABLE_PER_CLASS
```
create table card(
id int PRIMARY KEY,
amount decimal(8,3),
cardnumber varchar(20)
)

create table bankcheck(
id int PRIMARY KEY,
amount decimal(8,3),
checknumber varchar(20)
)
```

```
@Inheritance(strategy=InheritanceTypr.TABLE_PER_CLASS)
abstract class Payment{
  private int id;
  private double amount;
}

class Check extends Payment{
}

class creditCard extends Payment{
}
```
3. JOINED strategy
```
create table payment(
id int PRIMARY KEY,
amount decimal(8,3)
id INT NOT NULL AUTO_INCREMENT
);

create table card(
id int ,
cardnumber varchar(20),
 FOREIGN KEY (id)
REFERENCES payment(id)
)

create table bankcheck(
id int ,
checknumber varchar(20),
FOREIGN KEY (id)
REFERENCES payment(id)
)
```

```

```
### Hibernate Component mapping
```
@Entity
class Employee{
 @Embedded
 private Address addr;
}

@Embeddable
class Address{

}
```
