<style scoped>
table {
  font-size: 13px;
}
</style>

#### **XX_RLPMUS_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_RLPMUS_VW**    | Component Security |

| Num | Field Name         | Key | 
|   1 | ROLENAME           | Asc | 
|   2 | CLASSID            | Asc | 
|   3 | ROLEUSER           | Asc | 
|   4 | DESCR              |     | 
|   5 | CLASSDEFNDESC      |     | 
|   6 | OPRDEFNDESC        |     | 
|   7 | XX_ROLE_DESCR      |     | 
|   8 | XX_CLASSID_DESCR   |     | 
|   9 | XX_ROLEUSER_DESCR  |     | 
|  10 | DYNAMIC_SW         |     | 
|  11 | ROLETYPE           |     | 
|  12 | ROLESTATUS         |     | 
|  13 | DESCRLONG          |     | 
|  14 | TIMEOUTMINUTES     |     | 
|  15 | EMPLID             |     | 
|  16 | EMAILID            |     | 
|  17 | OPRCLASS           |     | 
|  18 | ROWSECCLASS        |     | 
|  19 | ACCTLOCK           |     | 
|  20 | OPRTYPE            |     | 
|  21 | LASTSIGNONDTTM     |     | 
|  22 | LASTUPDDTTM        |     | 

<font size="2">**SQL (All Databases)**</font> 

``` SQL 
SELECT RC.ROLENAME 
 , RC.CLASSID 
 , RU.ROLEUSER 
 , RD.DESCR 
 , CD.CLASSDEFNDESC 
 , OD.OPRDEFNDESC 
 , RD.DESCR 
 , CD.CLASSDEFNDESC 
 , OD.OPRDEFNDESC 
 , RU.DYNAMIC_SW 
 , RD.ROLETYPE 
 , RD.ROLESTATUS 
 , RD.DESCRLONG 
 , CD.TIMEOUTMINUTES 
 , OD.EMPLID 
 , OD.EMAILID 
 , OD.OPRCLASS 
 , OD.ROWSECCLASS 
 , OD.ACCTLOCK 
 , OD.OPRTYPE 
 , OD.LASTSIGNONDTTM 
 , OD.LASTUPDDTTM 
  FROM PSOPRDEFN OD 
  , PSROLEUSER RU 
  , PSROLECLASS RC 
  , PSROLEDEFN RD 
  , PSCLASSDEFN CD 
 WHERE OD.OPRID = RU.ROLEUSER 
   AND RU.ROLENAME = RC.ROLENAME 
   AND RC.ROLENAME = RD.ROLENAME 
   AND RC.CLASSID = CD.CLASSID
```
