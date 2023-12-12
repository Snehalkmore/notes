# Hibernate Architecture


### Hibernate mapping
1. one to one
2. one to many
3. many to many

### fetching types for each relationship type which is applied by Hibernate by default.
```
OneToMany: LAZY
ManyToOne: EAGER
ManyToMany: LAZY
OneToOne: EAGER
```

### Cascade Types mean how the data should be kept between the two related entities. There are set of pre defined types:
```
CascadeType.PERSIST : Both save() or persist() operations cascade to related entities.
CascadeType.MERGE : Related entities are merged when the ownership entity is merged.
CascadeType.REFRESH : Does same thing for the refresh() operation.
CascadeType.REMOVE : Removes all related entities association with this setting when the ownership entity is deleted.
CascadeType.DETACH : Detaches all related entities if a “manual detach” occurs.
CascadeType.ALL : All of the above cascade operations.
```

## @OneToOne
in this mapping, one entity can have only one other entity. example, one person can have only one permanent address. User can have one address.

“@JsonIgnore” annotation was placed there for user property since I do not need to have the user object to be seen in Address data. Just to ignore that field from JSON object.
```
USER
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
  
    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "address_id", referencedColumnName = "id")
    Address address;
}

@Entity
@Table(name = "addresses")
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;

  @JsonIgnore
    @OneToOne(mappedBy = "address")
    User user;
}

```

## @OneToMany mapping
One post can have multiple comments but one comment have only post.
```
POST class 
@Entity
@Table(name = "posts")
public class Post {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
    String title;
    String description;

    @OneToMany(cascade = CascadeType.ALL, fetch = FetchType.EAGER)
    @JoinColumn(name = "post_id", referencedColumnName = "id")
    Set<Comment> comments = new HashSet<>();
}

Comment class
@Entity
@Table(name = "comments")
public class Comment {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
    String author;
    String content;

    @Column(name = "post_id")
    Long postId;
}
```

## @ManyToMany Mapping 
every employees have multiple roles and every role is assigned to multiple employees.

```
Employee class
@Table(name = "employees")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
    String name;
    String email;
    @ManyToMany(fetch = FetchType.EAGER, cascade = CascadeType.ALL)
    @JoinTable(
        name = "employee_roles",
        joinColumns = @JoinColumn(
            name = "employee_id", referencedColumnName = "id"
        ),
        inverseJoinColumns = @JoinColumn(
            name = "role_id", referencedColumnName = "id"
        )
    )
    Set<Role> roles = new HashSet<>();
}


Role

@Table(name = "roles")
public class Role {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
    String name;
    @ManyToMany(mappedBy = "roles")
    @JsonIgnore
    Set<Employee> employees = new HashSet<>();
```
