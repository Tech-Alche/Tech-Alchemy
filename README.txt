1. In this program we are going to insert the records of the person and the things he owns in the table.
   So first of all, import the necessary modules.

2. Assign a declarative base function to a variable Base. 

3. Define a class Person, create a table named people and give the attributes ssn in integer and
   assign it as Primary Key for the table, firstname in string, gender in char, age in integer. 

4. Define a constructor in the Person class and all the pointers for the attributes of the table people. 

5. Define a constructor and print all the values of the attribute of the people table. 

6. Next Define a class Things, create a table named things and give the attributes tid in integer and assign it as Primary Key for the
   table, description in string, owner in integer and set it as Foreign Key with table people ssn. 
 
7. Do the same for the table things after creating the table. 

8. Create an engine as “sqlite:///mydb.db”. 

9. Add the values to the table and use commit to save the record.

10. For performing the operations give the table name in the session.query(tablename).all(). 
    For condition, session.query(tablename).filter(condition).

11. Print the result.
