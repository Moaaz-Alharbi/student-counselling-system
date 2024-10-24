# Student Counselling System API Documentation

This README contains documentation for the Student Counselling System, explaining its architecture, core components, and providing code snippets for clarification.

## Table of Contents

1. [System Architecture](#system-architecture)
2. [Core Components and Modules](#core-components-and-modules)
   - [Audit_details](#audit_details)
   - [Choice](#choice)
   - [ChoicesData](#choicesdata)
   - [CounsellingResult](#counsellingresult)
   - [db](#db)
   - [Emp](#emp)
   - [Login](#login)
   - [MainMenu](#mainmenu)
   - [Result](#result)
   - [StudentData](#studentdata)
   - [StudentInformation](#studentinformation)
   - [Users](#users)
3. [Usage Examples](#usage-examples)

---

## System Architecture

The Student Counselling System is built using Java and Swing, employing a graphical user interface (GUI) for user interactions. The system is designed to handle student information management, counselling preferences, and auditing operations. 

The system primarily includes the following components:

- **Database Connection**: `db.java` manages the connection to the SQLite database.
- **Authentication and User Management**: Classes such as `Login` and `users` handle user authentication and interaction with user data.
- **Student Information Management**: `StudentInformation` manages student details.
- **Audit Management**: `Audit_details` is responsible for displaying audit-related information.
- **User Preferences**: Classes like `Choice` and `ChoicesData` manage user selections and preferences.
- **Results Generation**: `CounsellingResult` and `Result` display results based on user input.

---

## Core Components and Modules

### Audit_details

This class displays audit records within a table format.

#### Key Method: 

- **Update_table3()**: Fetches data from the audit table and updates the table model.
  
  ```java
  private void Update_table3() {
      try {
          String sql = "SELECT * FROM Audit";
          pst = conn.prepareStatement(sql);
          rs = pst.executeQuery();
          tbl_3.setModel(DbUtils.resultSetToTableModel(rs));
      } catch (Exception e) {
          JOptionPane.showMessageDialog(null, e);
      } finally {
          try {
              rs.close();
              pst.close();
          } catch (Exception e) {
              // Handle exception
          }
      }
  }
  ```

### Choice

This class allows users to select their college and branch choices.

#### Key Methods:

- **Choice()**: Initializes the form and populates choices.
  
  ```java
  public Choice(String dat) {
      initComponents();
      this.jTextField1.setText(dat);
  }
  ```

- **jButton1ActionPerformed()**: Handles the button click for processing selections.
  
  ```java
  private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {
      // Process choices and initiate counselling results
  }
  ```

### ChoicesData

This class manages the storage of user choices in a file.

#### Key Methods:

- **Store(String txt)**: Stores choices in a file called `choices.txt`.
  
  ```java
  public void Store(String txt) throws IOException {
      ChoicesWriter = new FileWriter("choices.txt", true);
      // Write choices to file
      ChoicesWriter.flush();
      ChoicesWriter.close();
  }
  ```

### CounsellingResult

This class displays the results of the counselling process based on user data.

#### Key Methods:

- **CounsellingResult(String value)**: Initializes the result display based on student ID.
  
  ```java
  public CounsellingResult(String value) throws FileNotFoundException {
      initComponents();
      this.jTextField2.setText(value);
      // Additional code to fetch results
  }
  ```

### db

Handles the database connection for the application.

#### Key Method:

- **java_db()**: Establishes a connection to the SQLite database.
  
  ```java
  public static Connection java_db() {
      try {
          Class.forName("org.sqlite.JDBC");
          Connection conn = DriverManager.getConnection("jdbc:sqlite:studentInfo.sqlite");
          return conn;
      } catch (Exception e) {
          JOptionPane.showMessageDialog(null, e);
          return null;
      }
  }
  ```

### Emp

Stores the employee ID for tracking the logged-in user.

```java
public class Emp {
    public static int empId;
}
```

### Login

Manages the login process for users.

#### Key Methods:

- **currentDate()**: Sets the current date and time on the login screen.
  
  ```java
  public void currentDate() {
      Calendar cal = new GregorianCalendar();
      // Set date and time
  }
  ```

- **jButton1ActionPerformed()**

```java
- **jButton1ActionPerformed()**: Handles the login logic, validating credentials and updating the interface based on user roles.

```java
private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {
    String access;
    access = this.txt_combo.getSelectedItem().toString();
    
    String p = String.valueOf(this.txt_password.getPassword());
    if (access.equals("Admin") && this.txt_username.getText().equals("admin") && p.equals("admin")) {
        // Grant access to admin interface
    } else if (access.equals("Student")) {
        // Validate and grant access to student interface
    }
}
```

### MainMenu

Represents the main menu after a successful login, allowing users to access various functionalities.

#### Key Methods:

- **jButton1ActionPerformed()**: Navigates to the student management interface.

```java
private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {
    StudentInformation j = new StudentInformation();
    j.setVisible(true);
    this.dispose();
}
```

- **jMenuItem1ActionPerformed()**: Opens the audit details interface when selected from the menu.

```java
private void jMenuItem1ActionPerformed(java.awt.event.ActionEvent evt) {
    Audit_details j = new Audit_details();
    j.setVisible(true);
}
```

### Result

Displays the counselling result for a student, including their allotted college and branch.

#### Key Methods:

- **CounsellingResult(String value)**: Initializes the result form and fetches user data from a file.

```java
public CounsellingResult(String value) throws FileNotFoundException {
    initComponents();
    this.jTextField2.setText(value);
    // Fetch data and set fields for display
}
```

### StudentData

Handles the storage of student data in a file.

#### Key Methods:

- **Store()**: Writes student information to a text file named `output.txt`.

```java
public void Store() throws FileNotFoundException, IOException {
    newWriter = new FileWriter("output.txt", true);
    // Write student data to file
    newWriter.flush();
    newWriter.close();
}
```

### StudentInformation

This class manages the student information input form.

#### Key Methods:

- **cmd_saveActionPerformed()**: Saves the student information to the file.

```java
private void cmd_saveActionPerformed(java.awt.event.ActionEvent evt) {
    // Get input data and call StudentData.Store()
}
```

- **txt_search1KeyReleased()**: Searches for a student by ID and updates the GUI accordingly.

```java
private void txt_search1KeyReleased(java.awt.event.KeyEvent evt) {
    // Fetch student data based on ID input
}
```

### Users

Manages user records and provides functionalities for adding, updating, and deleting users.

#### Key Methods:

- **cmd_addActionPerformed()**: Adds a new user record to the database.

```java
private void cmd_addActionPerformed(java.awt.event.ActionEvent evt) {
    // Adds user information to the database
}
```

- **cmd_deleteActionPerformed()**: Deletes a selected user from the database.

```java
private void cmd_deleteActionPerformed(java.awt.event.ActionEvent evt) {
    // Deletes user record from the database
}
```

---

## Usage Examples

### Connecting to the Database

To establish a connection to the SQLite database, use the following method:

```java
Connection conn = db.java_db();
```

### Adding a New User

To add a new user, create an instance of `users` and call the respective methods:

```java
users user = new users();
user.cmd_addActionPerformed(evt);
```

### Viewing Audit Records

To view audits, simply create an instance of `Audit_details`:

```java
Audit_details auditDetails = new Audit_details();
auditDetails.setVisible(true);
```

### Saving Student Information

To save student data, use the `StudentData` class as follows:

```java
StudentData

studentData = new StudentData(firstname, surname, dob, studentId, email, tel, address, add2, apt, pc);
```

### Searching for a Student

To search for a student record based on their ID:

```java
txt_search1.setText(studId);
txt_search1KeyReleased(evt);
```

---

## Conclusion

The Student Counselling System provides a comprehensive platform for managing student information and counselling records. The provided APIs enable integration with various functionalities like auditing, user management, and student result processing. This documentation ensures clarity and ease of understanding for any student or developer looking to understand or contribute to this project.
