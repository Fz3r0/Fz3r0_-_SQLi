# Lab: SQL injection UNION attack, determining the number of columns returned by the query

- [Lab: SQL injection UNION attack, determining the number of columns returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns)

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a `SQL injection UNION` attack that returns an additional row containing null values.

---

### Explicación:





Es prácticamente el ejercicio anterior, pero en el anterior puse Fz3r0 y ahora piden un string en paricular:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/183aaf72-8873-40bb-bc09-07ea29316f6c)
