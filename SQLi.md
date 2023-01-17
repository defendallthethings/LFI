# Sanitization:
mysqli::real_escape_string -- mysqli_real_escape_string — Escapes special characters in a string for use in an SQL statement, taking into account the current charset of the connection
```

<?php

mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);
$mysqli = mysqli_connect("localhost", "my_user", "my_password", "world");

$city = "'s-Hertogenbosch";

/* this query with escaped $city will work */
$query = sprintf("SELECT CountryCode FROM City WHERE name='%s'",
    mysqli_real_escape_string($mysqli, $city));
$result = mysqli_query($mysqli, $query);
printf("Select returned %d rows.\n", mysqli_num_rows($result));

/* this query will fail, because we didn't escape $city */
$query = sprintf("SELECT CountryCode FROM City WHERE name='%s'", $city);
$result = mysqli_query($mysqli, $query);
 
```
 

# Input Validation

```
<SNIP>
$pattern = "/^[A-Za-z\s]+$/";
$code = $_GET["port_code"];

if(!preg_match($pattern, $code)) {
  die("</table></div><p style='font-size: 15px;'>Invalid input! Please try again.</p>");
}

$q = "Select * from ports where port_code ilike '%" . $code . "%'";
<SNIP>

```

# User Privileges
The commands below add a new MariaDB user named user1 who is granted only SELECT privileges on the table3. We can verify the permissions for this user by logging in:
```
MariaDB [(none)]> CREATE USER 'user1'@'localhost';

Query OK, 0 rows affected (0.002 sec)


MariaDB [(none)]> GRANT SELECT ON database2.table3 TO 'user1'@'localhost' IDENTIFIED BY 'Summer@123';

Query OK, 0 rows affected (0.000 sec)

```

# Web Application Firewall

[WAFs can be open-source (ModSecurity) or premium (Cloudflare).](https://www.netnea.com/cms/apache-tutorial-6_embedding-modsecurity/) 

# Parameterized Queries

Another way to ensure that the input is safely sanitized is by using  parameterized queries. 
Parameterized queries contain placeholders for  the input data, which is then escaped and passed on by the drivers.  
Instead of directly passing the data into the SQL query, we use  placeholders and then fill them with PHP functions.
Consider the following modified code:
Code: php
```
<SNIP>
  $username = $_POST['username'];
  $password = $_POST['password'];

  $query = "SELECT * FROM logins WHERE username=? AND password = ?" ;
  $stmt = mysqli_prepare($conn, $query);
  mysqli_stmt_bind_param($stmt, 'ss', $username, $password);
  mysqli_stmt_execute($stmt);
  $result = mysqli_stmt_get_result($stmt);

  $row = mysqli_fetch_array($result);
  mysqli_stmt_close($stmt);
<SNIP>
```
