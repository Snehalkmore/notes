Hibernate mapping
1. one to onr
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

@OneToMany mapping

