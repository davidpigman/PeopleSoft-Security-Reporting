#### **XX_MENUOBJCM_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_MENUOBJCM_VW**   | Navigation View    |

| Num | Field Name         | Key | 
| --- | ------------------ | --- | 
| 1   | MENUNAME           | Asc |
| 2   | BARNAME            | Asc |
| 3   | ITEMNAME           | Asc |
| 4   | PNLGRPNAME         | Asc |
| 5   | MARKET             | Asc |
| 6   | MENUGROUP          |     |
| 7   | MENULABEL          |     |
| 8   | BARLABEL           |     |
| 9   | ITEMLABEL          |     |
| 10  | XX_COMP_DESCR      |     |
| 11  | XX_PORTAL_URLTEXT  |     |
| 12  | XX_PIA_PATH        |     |
| 13  | XX_PIA_LBL_PATH    |     |
| 14  | ACTIONS            |     |
| 15  | XX_PNLGRP_ACTION   |     |

 <font size="2">**SQL (Oracle Databases)**</font> 

``` SQL
    
 SELECT MD.MENUNAME   
 , MI.BARNAME   
 , MI.ITEMNAME   
 , PG.PNLGRPNAME   
 , PG.MARKET   
 , MD.MENUGROUP   
 , MD.MENULABEL   
 , MI.BARLABEL   
 , MI.ITEMLABEL   
 , %Substring(GD.DESCR ,1 ,30)   
 ,'c/' %Concat RTRIM(MD.MENUNAME) %Concat '.' %Concat RTRIM(PG.PNLGRPNAME) %Concat '.' %Concat RTRIM(PG.MARKET)   
 , RTRIM(MD.MENUNAME) %Concat ' --> ' %Concat RTRIM(MI.BARNAME) %Concat ' --> ' %Concat RTRIM(MI.ITEMNAME) %Concat ' --> ' %Concat RTRIM(PG.PNLGRPNAME)   
 , RTRIM(MD.MENULABEL) %Concat ' --> ' %Concat RTRIM(MI.BARLABEL) %Concat ' --> ' %Concat RTRIM(MI.ITEMLABEL) %Concat ' --> ' %Concat RTRIM(PG.PNLGRPNAME)   
 , GD.ACTIONS   
 , CASE GD.ACTIONS WHEN 1 THEN 'A' WHEN 2 THEN 'UD' WHEN 4 THEN 'UDA' WHEN 8 THEN 'C' WHEN 3 THEN 'A UD' WHEN 5 THEN 'A UDA' WHEN 9 THEN 'A C' WHEN 6 THEN 'UD UDA' WHEN 10 THEN 'UD C' WHEN 12 THEN 'UDA C' WHEN 7 THEN 'A UD UDA' WHEN 11 THEN 'A UD C' WHEN 13 THEN 'A UDA C' WHEN 14 
THEN 'UD UDA C' WHEN 15 THEN 'A UD UDA C' ELSE CAST(GD.ACTIONS AS VARCHAR(30)) END AS XX_PNLGRP_ACTION   
  FROM PSMENUDEFN MD   
  , PSMENUITEM MI   
  , PSPNLGROUP PG   
  , PSPNLGRPDEFN GD   
 WHERE MD.MENUNAME = MI.MENUNAME   
   AND MI.ITEMNAME = PG.ITEMNAME  
   AND MI.PNLGRPNAME = PG.PNLGRPNAME   
   AND MI.MARKET = PG.MARKET   
   AND PG.PNLGRPNAME = GD.PNLGRPNAME   
  GROUP BY MD.MENUNAME, MI.BARNAME, MI.ITEMNAME, PG.PNLGRPNAME, PG.MARKET, MD.MENUGROUP, MD.MENULABEL, MI.BARLABEL, MI.ITEMLABEL, GD.DESCR, GD.ACTIONS
```