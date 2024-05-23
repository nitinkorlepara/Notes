# JAVA PERSISTANT API 
### JPA Dev Process
-   Steps
    - create entitiy Classes
    - Map
- MYSQL Connections
```
    String url="jdbc:mysql://localhost:3306/census";
    String user="root";
    String password="admin";
    Connection connection=DriverManager.getConnection(url,user,password);
```
- MONGO DB

### SPring Implentation
```
    private SessionFactory sessionFactory;
    @Autowired
    public CustomerDAOImpl(EntityManagerFactory entityManagerFactory) {
        this.sessionFactory = entityManagerFactory.unwrap(SessionFactory.class);
    }
    
    Session session=this.sessionFactory.openSession();
    Transaction transaction= session.beginTransaction();
    session.save(object);
    transaction.commit();
    session.close();

```
