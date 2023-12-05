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
Pageable pageable = new PageRequest(int pageIndex, int noOfRecordsOnPage);...... Pageable interface & PageRequest class

Page<Student> students = studentRepository.findAll(pageable);  .............Page<Studdent>

students.stream().forEach(e->sysout(e.getName));

```


## Native Query - simple sql query and named paramenter query exampl
```
public interface StudentRepo implements JpaRepository<customCLass,int>{

@Query(value = "select * from student", nativeQuery=true) ............simple query
{List<Student> findAllStudentNQ();
}

@Query(value = "select * from student where fnm =:firstName", nativeQuery=true) ............named parameter query
{ List<Student> findAllStudentNQ(@Param("firstName")String firstName);
}
}

```

## JPQL


### custom ID generator strategy
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

3. in class for example employee
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