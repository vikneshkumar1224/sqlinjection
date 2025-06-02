# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

### OUTPUT :

![image](https://github.com/user-attachments/assets/2bb6a55d-5f29-41c7-82ef-86a2c946815c)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

### OUTPUT :

![image](https://github.com/user-attachments/assets/ab3a31ea-23c8-459e-a43a-bb679e301c94)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:

### OUTPUT :

![image](https://github.com/user-attachments/assets/fed81f4d-cbf8-4015-ac74-98a8ef57c7bc)
Click on the menu Login/Register and register for an account

### OUTPUT :

![image](https://github.com/user-attachments/assets/70ae2e19-f753-4ff8-966d-0d72796b8fe4)
Click on the link “Please register here”

### OUTPUT :

![image](https://github.com/user-attachments/assets/bdf76efd-9028-4082-b0ed-a7390485f528)
Click on “Create Account” to display the following page:

### OUTPUT :
![image](https://github.com/user-attachments/assets/bd3d68e6-c267-407a-8dae-f7ff8be801c3)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

### OUTPUT :

![image](https://github.com/user-attachments/assets/9e60addf-3cdd-44a2-a12b-041c31cc2100)
Click “Login”. The logged in page will show as below:

### OUTPUT :

![image](https://github.com/user-attachments/assets/7f9612f8-1734-4bb5-8290-9a05dd56c1e1)

### The username field is vulnerable. Put (thiru2’ #) or (thiru2’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “vike.”

### OUTPUT :
![image](https://github.com/user-attachments/assets/eaf590c8-f3b4-4c3a-8fde-8c231c99862e)

This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]: cd / sudo nano /var/www/mutillidae/config.inc Type msfadmin when prompted for the root password. Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure below

![image](https://github.com/user-attachments/assets/db1a564f-14fd-411a-944d-75c3afad8653)
Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

### OUTPUT :

![image](https://github.com/user-attachments/assets/e88bace8-926b-4f26-9ef5-4020989f8870)
Save and exit the config.inc Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file Restart the Apache server To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM. sudo /etc/init.d/apache2 reload

### OUTPUT : 

![image](https://github.com/user-attachments/assets/43275d79-ee1c-492b-a92f-c398ef193429)
Reset Mutillidae database Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.

### OUTPUT : 

![image](https://github.com/user-attachments/assets/b1074fbb-3167-49e5-b612-d9b93ac16aa4)

Test the new configuration Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

The Mutillidae database error no longer appears

===============================================================

Now after logging out you will see the login page. In the login page give thiru2’ # . You can see the page now enters into the administrator page as before when giving the password.

### OUTPUT :

![image](https://github.com/user-attachments/assets/805bfb00-7729-49c6-9b4f-ade0e866cd89)
Click the login button and you will see it enter into the administrator page.

### OUTPUT :

![image](https://github.com/user-attachments/assets/f0a27a52-01d9-48fa-99c8-a73951460de0)

### Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statemet like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:

### OUTPUT :
![image](https://github.com/user-attachments/assets/e1edc06f-a586-4394-8258-f9cab114f3eb)

### OUTPUT :
TO VIEW ACCOUNT DETAILS
![image](https://github.com/user-attachments/assets/f40560ba-7a7e-4912-9c43-5795d8d6261b)
WITHOUT PASSWORD TO SEE ACCOUNT DETAILS
![image](https://github.com/user-attachments/assets/024e177c-b5e9-4ce3-b821-1688976dcb9b)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
```
http://192.168.203.1/mutillidae/index.php?page=user-
info.php&username=thiru2%27order%20by%205%23&password=&user-info-php-submit
-button=View+Account+Details
```

### OUTPUT :
After adding the order by 6 into the existing url , the following error statement will be obtained:
![image](https://github.com/user-attachments/assets/7e7fc0ec-2a24-4ea0-a2d9-3300b600e88a)

### OUTPUT :

![image](https://github.com/user-attachments/assets/dc84cd74-92c3-43ed-b341-d3ffb79de492)
As it is having 5 columns the query worked fine and it provides the correct result

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

### OUTPUT :

![image](https://github.com/user-attachments/assets/875e4eba-3c6c-4deb-bcba-3abc5af916db)

### OUTPUT :

![image](https://github.com/user-attachments/assets/24431d1b-f3cb-4943-a330-9f053274e584)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

### OUTPUT :

![image](https://github.com/user-attachments/assets/abf6471f-c815-4100-964e-fda6d4ca6186)
The column names of the accounts is displayed below for the following url:

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

### OUTPUT :

![image](https://github.com/user-attachments/assets/caadb460-e41d-4528-9f84-840a42b5d3f9)

### OUTPUT :
![image](https://github.com/user-attachments/assets/d482093c-bf3d-416a-973f-63f7ba2726a3)

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

### OUTPUT :

![image](https://github.com/user-attachments/assets/1a0106f7-ddb9-45b7-ba21-8a33914db430)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
