#### **XX_PNLDEFN_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_PNLDEFN_VW**   | Navigation View    |

| Num | Field Name         | Key | 
| --- | ------------------ | --- | 
|   1 | PNLNAME            | Asc |
|   2 | PNLTYPE            |     |
|   3 | DESCR              |     |
|   4 | OBJECTOWNERID      |     |
|   5 | DESCRLONG          |     |

<font size="2">**SQL (All Databases)**</font> 

``` SQL
SELECT PNLNAME 
 , PNLTYPE 
 , DESCR 
 , OBJECTOWNERID 
 , DESCRLONG 
  FROM PSPNLDEFN
```