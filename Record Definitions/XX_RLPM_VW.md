# Custom Record Definitions
## Views
Add these custom record definition views

#### **XX_RLPM_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_RLPM_VW**      | Component Security |

| Num | Field Name         | Key | 
|   1 | ROLENAME           |     | 
|   2 | CLASSID            |     |
|   3 | DESCR              |     |
|   4 | CLASSDEFNDESC      |     |
|   5 | XX_ROLE_DESCR      |     |
|   6 | XX_CLASSID_DESCR   |     |
|   7 | ROLETYPE           |     |
|   8 | ROLESTATUS         |     |
|   9 | DESCRLONG          |     |
|  10 | TIMEOUTMINUTES     |     |

<font size="2">**SQL (All Databases)**</font> 

``` SQL 
SELECT RC.ROLENAME 
 , RC.CLASSID 
 , RD.DESCR 
 , CD.CLASSDEFNDESC 
 , RD.DESCR 
 , CD.CLASSDEFNDESC 
 , RD.ROLETYPE 
 , RD.ROLESTATUS 
 , RD.DESCRLONG 
 , CD.TIMEOUTMINUTES 
  FROM PSROLECLASS RC 
  , PSROLEDEFN RD 
  , PSCLASSDEFN CD 
 WHERE RC.ROLENAME = RD.ROLENAME 
   AND RC.CLASSID = CD.CLASSID
```
