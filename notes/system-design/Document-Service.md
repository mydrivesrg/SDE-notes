To design a simple document service in Java, we need to define the classes and methods that allow users to create, read, edit, and delete documents, as well as manage access permissions. Here's a basic outline and implementation for this system.

### Class Definitions

1. **User**: Represents a user in the system.
2. **Document**: Represents a document with a name, content, owner, and access permissions.
3. **DocumentService**: Provides methods to create, read, edit, and delete documents, as well as manage access permissions.
4. **DocumentServiceApplication**: Contains the main method and provides a command-line interface for interacting with the document service.

### Implementation

#### User.java
```java
public class User {
    private String username;

    public User(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }
}
```

#### Document.java
```java
import java.util.HashMap;
import java.util.Map;

public class Document {
    private String name;
    private String content;
    private User owner;
    private Map<User, AccessLevel> accessControl;

    public enum AccessLevel {
        READ, EDIT
    }

    public Document(String name, String content, User owner) {
        this.name = name;
        this.content = content;
        this.owner = owner;
        this.accessControl = new HashMap<>();
    }

    public String getName() {
        return name;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public User getOwner() {
        return owner;
    }

    public Map<User, AccessLevel> getAccessControl() {
        return accessControl;
    }

    public void grantAccess(User user, AccessLevel accessLevel) {
        accessControl.put(user, accessLevel);
    }

    public void revokeAccess(User user) {
        accessControl.remove(user);
    }

    public boolean canRead(User user) {
        return user.equals(owner) || accessControl.getOrDefault(user, null) == AccessLevel.READ;
    }

    public boolean canEdit(User user) {
        return user.equals(owner) || accessControl.getOrDefault(user, null) == AccessLevel.EDIT;
    }
}
```

#### DocumentService.java
```java
import java.util.HashMap;
import java.util.Map;

public class DocumentService {
    private Map<String, Document> documents = new HashMap<>();

    public void createDocument(String name, String content, User owner) {
        if (documents.containsKey(name)) {
            throw new IllegalArgumentException("Document with this name already exists.");
        }
        Document document = new Document(name, content, owner);
        documents.put(name, document);
    }

    public String readDocument(String name, User user) {
        Document document = documents.get(name);
        if (document == null) {
            throw new IllegalArgumentException("Document not found.");
        }
        if (document.canRead(user)) {
            return document.getContent();
        } else {
            throw new SecurityException("Access denied.");
        }
    }

    public void editDocument(String name, String newContent, User user) {
        Document document = documents.get(name);
        if (document == null) {
            throw new IllegalArgumentException("Document not found.");
        }
        if (document.canEdit(user)) {
            document.setContent(newContent);
        } else {
            throw new SecurityException("Access denied.");
        }
    }

    public void deleteDocument(String name, User user) {
        Document document = documents.get(name);
        if (document == null) {
            throw new IllegalArgumentException("Document not found.");
        }
        if (document.getOwner().equals(user)) {
            documents.remove(name);
        } else {
            throw new SecurityException("Only the owner can delete the document.");
        }
    }

    public void grantAccess(String documentName, User owner, User targetUser, Document.AccessLevel accessLevel) {
        Document document = documents.get(documentName);
        if (document == null) {
            throw new IllegalArgumentException("Document not found.");
        }
        if (document.getOwner().equals(owner)) {
            document.grantAccess(targetUser, accessLevel);
        } else {
            throw new SecurityException("Only the owner can grant access.");
        }
    }

    public void revokeAccess(String documentName, User owner, User targetUser) {
        Document document = documents.get(documentName);
        if (document == null) {
            throw new IllegalArgumentException("Document not found.");
        }
        if (document.getOwner().equals(owner)) {
            document.revokeAccess(targetUser);
        } else {
            throw new SecurityException("Only the owner can revoke access.");
        }
    }
}
```

#### DocumentServiceApplication.java
```java
import java.util.Scanner;

public class DocumentServiceApplication {
    private static DocumentService documentService = new DocumentService();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("Choose an action: create, read, edit, delete, grant, revoke, exit");
            String action = scanner.nextLine().trim().toLowerCase();

            switch (action) {
                case "create":
                    System.out.print("Enter username: ");
                    String createUser = scanner.nextLine();
                    System.out.print("Enter document name: ");
                    String createName = scanner.nextLine();
                    System.out.print("Enter document content: ");
                    String createContent = scanner.nextLine();
                    documentService.createDocument(createName, createContent, new User(createUser));
                    System.out.println("Document created.");
                    break;

                case "read":
                    System.out.print("Enter username: ");
                    String readUser = scanner.nextLine();
                    System.out.print("Enter document name: ");
                    String readName = scanner.nextLine();
                    try {
                        String content = documentService.readDocument(readName, new User(readUser));
                        System.out.println("Document content: " + content);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                case "edit":
                    System.out.print("Enter username: ");
                    String editUser = scanner.nextLine();
                    System.out.print("Enter document name: ");
                    String editName = scanner.nextLine();
                    System.out.print("Enter new document content: ");
                    String editContent = scanner.nextLine();
                    try {
                        documentService.editDocument(editName, editContent, new User(editUser));
                        System.out.println("Document edited.");
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                case "delete":
                    System.out.print("Enter username: ");
                    String deleteUser = scanner.nextLine();
                    System.out.print("Enter document name: ");
                    String deleteName = scanner.nextLine();
                    try {
                        documentService.deleteDocument(deleteName, new User(deleteUser));
                        System.out.println("Document deleted.");
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                case "grant":
                    System.out.print("Enter owner username: ");
                    String grantOwner = scanner.nextLine();
                    System.out.print("Enter document name: ");
                    String grantName = scanner.nextLine();
                    System.out.print("Enter target username: ");
                    String grantUser = scanner.nextLine();
                    System.out.print("Enter access level (read/edit): ");
                    String grantAccess = scanner.nextLine();
                    try {
                        documentService.grantAccess(grantName, new User(grantOwner), new User(grantUser),
                                Document.AccessLevel.valueOf(grantAccess.toUpperCase()));
                        System.out.println("Access granted.");
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                case "revoke":
                    System.out.print("Enter owner username: ");
                    String revokeOwner = scanner.nextLine();
                    System.out.print("Enter document name: ");
                    String revokeName = scanner.nextLine();
                    System.out.print("Enter target username: ");
                    String revokeUser = scanner.nextLine();
                    try {
                        documentService.revokeAccess(revokeName, new User(revokeOwner), new User(revokeUser));
                        System.out.println("Access revoked.");
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                case "exit":
                    scanner.close();
                    System.out.println("Exiting...");
                    return;

                default:
                    System.out.println("Invalid action. Try again.");
            }
        }
    }
}
```

### Running the Application
1. Compile the Java files:
    ```sh
    javac User.java Document.java DocumentService.java DocumentServiceApplication.java
    ```
2. Run the application:
    ```sh
    java DocumentServiceApplication
    ```

The command-line interface will prompt you to choose actions such as creating, reading, editing, and deleting documents, as well as granting and revoking access. This setup provides a basic implementation of the document service with user management and access control.