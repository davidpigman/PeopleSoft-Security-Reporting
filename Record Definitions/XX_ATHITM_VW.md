#### **XX_ATHITM_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_ATHITM_VW**    |                    |

| Num | Field Name         | Key | 
| --- | ------------------ | --- | 
| 1   | CLASSID            | Asc |
| 2   | MENUNAME           | Asc |
| 3   | BARNAME            | Asc |
| 4   | ITEMNAME           | Asc |
| 5   | PNLITEMNAME        | Asc |
| 5   | DISPLAYONLY        |     |
| 6   | AUTHORIZEDACTIONS  |     |
| 7   | XX_AUTH_ACTION     |     |

 <font size="2">**SQL (All Databases)**</font> 
 
``` SQL
SELECT CLASSID 
 , MENUNAME 
 , BARNAME 
 , BARITEMNAME 
 , PNLITEMNAME 
 , DISPLAYONLY 
 , AUTHORIZEDACTIONS 
 , CASE AUTHORIZEDACTIONS WHEN 1 THEN 'A' WHEN 2 THEN 'UD' WHEN 4 THEN 'UDA' WHEN 8 THEN 'C' WHEN 3 THEN 'A UD' WHEN 5 THEN 'A 
UDA' WHEN 9 THEN 'A C' WHEN 6 THEN 'UD UDA' WHEN 10 THEN 'UD C' WHEN 12 THEN 'UDA C' WHEN 7 THEN 'A UD UDA' WHEN 11 THEN 'A UD 
C' WHEN 13 THEN 'A UDA C' WHEN 14 THEN 'UD UDA C' WHEN 15 THEN 'A UD UDA C' END 
  FROM PSAUTHITEM
```
