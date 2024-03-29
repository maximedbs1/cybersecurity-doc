# Website SQL Injection Attack

Attack websites by executing our own SQL queries in text areas 

Try to fill forms with SQL commands to retrieve info, connect as admin...
- Identify the field that can be injected
- Identify the SGBD in use to know the syntax
- Try basic commands to retreive table name / schema

## Basic usage

Ex in username field of a login form by entering:
```
admin' OR 1=1 --
```
- admin : username with which we want to be connected
- ' to finish the SQL chain
- OR 1=1 to validate the command
- -- to comment the rest of the normal command (password verification etc...)
And then we are connected as admin

`/!\ Don't forget to fill the other fields with junk text to make your request valid in client side /!\`

## Advanced usage with UNION query

The idea here is to select tables and fields as we want

UNION is an SQL command to perform 2 select in the same row but it needs to have the same number of parameters left and right

So we need to :
- find a field open for SQL injection
- Determine the number of parameters to pass after the "UNION SELECT" (use one or more "null" paramters until no errors)
- Find which paramters can be displayed in the page (try to replace null by strings to see if it is fetched somewhere)
- Try to retrieve fields from other tables such as Users table by replacing the parameters that can be displayed

Ex to retreive username from User table in the category filter :

(Injection in the URL directly, we know that it requires 2 parameters and have identified the first paramter as the one that can be displayed)

```
site.com/filter?category=Gift' UNION SELECT username, null FROM Users --
```
