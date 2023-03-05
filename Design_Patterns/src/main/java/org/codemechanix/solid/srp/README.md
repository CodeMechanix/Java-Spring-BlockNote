The Single Responsibility Principle (SRP) is a fundamental design principle in object-oriented programming that states
that **a class should have only one reason to change**. This principle **aims to ensure that each class has a clear and
concise responsibility, which helps improve code readability, maintainability, and testability**.

In Java, we can apply the SRP by designing classes that have a single responsibility and do not have multiple unrelated
responsibilities. Here are some tips on how to apply the SRP in Java:

1. **Identify the responsibilities of the class**: Before designing a class, identify the single responsibility it
   should have. A class should only have one responsibility, and its methods should only perform tasks related to that
   responsibility.

2. **Separate responsibilities into different classes**: If a class has multiple responsibilities, split them into
   separate classes. Each class should have its own set of responsibilities and not be responsible for tasks that belong
   to other classes.

3. **Encapsulate responsibilities**: Use encapsulation to hide implementation details and make sure that a class's
   responsibilities are not leaked to other classes. By using encapsulation, we can make sure that each class only
   exposes the minimum amount of information necessary for other classes to interact with it.

4. **Use interfaces**: Use interfaces to define the behavior that a class should implement. This allows you to separate
   the interface from the implementation and makes it easier to swap out different implementations of the same
   interface.

5. **Testability**: Applying SRP also results in better testability. Since each class has a single responsibility, it is
   easier to test that responsibility in isolation. This makes it easier to write automated tests that can verify that
   each class is working correctly.

By following the SRP in Java, we can create more maintainable and robust code that is easier to understand and modify
over time.

Let's consider an example of a class in Java that we can design based on the Single Responsibility Principle (SRP):

Suppose we have a class named "User" that is responsible for creating and managing user accounts in a web application.
We can apply the SRP by identifying its single responsibility as "user account management".

Here's how we can design the "User" class based on the SRP:

1. **Identify the responsibility of the class**:

The responsibility of the User class is to manage user accounts.

2. **Define the interface**:

We can define the interface of the User class to include methods such as createUser(), updateUser(), deleteUser(), and
getUserById(). These methods are related to the single responsibility of user account management.

```java
public interface IUserManager {
    public void createUser(User user);

    public void updateUser(User user);

    public void deleteUser(User user);

    public User getUserById(int userId);
}
```

3. Encapsulate the implementation details:

We can encapsulate the implementation details of the User class by using private fields to store the user data and
providing public getters and setters to access and modify the data. This helps to ensure that the implementation details
are not leaked to other classes.

```java
public class User {
    private int userId;
    private String username;
    private String password;
    private String email;

    // Getters and setters
    public int getUserId() {
        return userId;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}

```

4. Consider using composition:

If the User class has additional responsibilities such as authentication or authorization, we can split those
responsibilities into separate classes using composition. For example, we can create an AuthenticationManager class that
is responsible for user authentication, and a UserManager class that is responsible for user account management.

```java
public class AuthenticationManager {
    public boolean authenticate(User user) {
        // Authenticate the user
    }
}

public class UserManager implements IUserManager {
    private AuthenticationManager authManager;

    public UserManager() {
        authManager = new AuthenticationManager();
    }

    public void createUser(User user) {
        // Create the user
        if (authManager.authenticate(user)) {
            // Add user to the database
        }
    }

    // Implement other IUserManager methods
}

```

5. Write test cases:

Finally, we can write test cases to verify that the User class is working correctly. For example, we can write a test
case for the createUser() method to ensure that a new user account is created successfully.

```java
@Test
public void testCreateUser(){
        IUserManager userManager=new UserManager();
        User user=new User();
        user.setUsername("john");
        user.setPassword("password");
        user.setEmail("john@example.com");
        userManager.createUser(user);
        assertEquals(userManager.getUserById(user.getUserId()),user);
        }
```

By following these steps, we have designed the User class to adhere to the Single Responsibility Principle, which helps
to improve code quality and maintainability.

### Rules of Thumb?

1. If you cannot come up with a meaningful name for your class focused on single responsibility, then it's probably
   doing too much.
2. Every object in our web application should have a single responsibility, and all object's services should be focused
   on carrying that single responsibility(SRP).
3. If you put more than one functionality in one Class in Java it introduces coupling between two functionality and even
   if you change one functionality there is a chance you broke coupled functionality, which requires another round of
   testing to avoid any surprise on the production environment.




