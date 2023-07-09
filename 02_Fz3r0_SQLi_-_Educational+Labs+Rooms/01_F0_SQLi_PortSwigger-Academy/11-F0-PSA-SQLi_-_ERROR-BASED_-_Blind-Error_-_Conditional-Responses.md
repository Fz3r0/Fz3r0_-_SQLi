# `LAB`: Blind SQL injection with conditional responses

## Descripción:

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a "Welcome back" message in the page if the query returns any rows.

The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

To solve the lab, log in as the `administrator` user.  

## Hint:

You can assume that the password only contains **lowercase, alphanumeric characters**. 

### PortSwigger Cheastsheet:

- [PortSwigger - SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


---

### Explicación:

- Este tipo de vulnerabilidad es cuando no se muestra el error en pantalla y no sabemos bien cuál es el error que arroja SQL.
- Cuando escribo payloads como `'` o `-- -` o `' or 1 = 1 -- -` veo que regresa una página en blanco, pero sin errores (solo un `welcome back`). Esto quiere decir que posiblemente exista un error por detrás que yo no vea.
- Para este tipo de vulnerabilidades se utiliza `Burpsuite`

**IMPORTANTE:** Aquí la vulnerabilidad está en una `tracking cookie` la cual también contiene el SQL query. 



---

## Solución:

````py
# Vulnerabilidad y sanamiento


````

