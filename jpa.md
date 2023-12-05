# JPA notes

custom id generator strategy
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
   private long id;

   }
   ```
