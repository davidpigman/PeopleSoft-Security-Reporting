#### **XX_MENUOBJ_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_MENUOBJ_VW**   | Navigation View    |

| Num | Field Name         | Key | 
| --- | ------------------ | --- | 
| 1   | MENUNAME           | Asc |
| 2   | BARNAME            | Asc | 
| 3   | ITEMNAME           | Asc |
| 4   | PNLGRPNAME         | Asc |
| 5   | MARKET             | Asc |
| 6   | PNLNAME            | Asc |
| 7   | PNLITEMNAME        | Asc |
| 8   | MENUGROUP          |     |
| 9   | MENULABEL          |     |
| 10  | BARLABEL           |     |
| 11  | ITEMLABEL          |     |
| 12  | XX_COMP_DESCR      |     |
| 13  | PAGELABEL          |     |
| 14  | XX_PORTAL_URLTEXT  |     |
| 15  | XX_PIA_PATH        |     |
| 16  | XX_PIA_LBL_PATH    |     |
| 17  | ACTIONS            |     |
| 18  | XX_PNLGRP_ACTION   |     |

 <font size="2">**SQL (Oracle Databases)**</font> 
 
``` SQL
SELECT POR.PORTAL_NAME   
 , MNU.MENUNAME   
 , MNU.BARNAME   
 , MNU.ITEMNAME   
 , MNU.PNLGRPNAME   
 , MNU.MARKET   
 , PNL.PNLNAME   
 , PNL.ITEMNAME   
 , GRP.DFLTACTION   
 , POR.PORTAL_LABEL   
 , POR.PORTAL_OBJNAME   
 , POR.PORTAL_PRNTOBJNAME   
 , POR.PORTAL_REFTYPE   
 , CAST(POR.PORTAL_URLTEXT AS VARCHAR(150))   
 , POR.PORTAL_CNTPRV_NAM   
 , POR.OBJECTOWNERID   
 , CAST(PNI.PORTAL_NAVPATH AS VARCHAR(254))   
 , ' '   
 , 'N'   
  FROM PSPNLGROUP PNL   
  , PSMENUITEM MNU   
  , PSPNLGRPDEFN GRP   
  , PSPRSMDEFN POR   
  , PSPRSMNAVINFO PNI   
 WHERE PNL.PNLGRPNAME=MNU.PNLGRPNAME   
   AND POR.PORTAL_REFTYPE='C'   
   AND PNL.PNLGRPNAME=GRP.PNLGRPNAME   
   AND PNL.MARKET=GRP.MARKET   
   AND POR.PORTAL_URI_SEG1=MNU.MENUNAME   
   AND POR.PORTAL_URI_SEG2=GRP.PNLGRPNAME   
   AND POR.PORTAL_URI_SEG3=GRP.MARKET   
   AND POR.PORTAL_NAME = PNI.PORTAL_NAME  
   AND POR.PORTAL_REFTYPE = PNI.PORTAL_REFTYPE   
   AND POR.PORTAL_OBJNAME = PNI.PORTAL_OBJNAME   
   AND PNL.SUBITEMNUM = (   
 SELECT MIN(PNL2.SUBITEMNUM)   
  FROM PSPNLGROUP PNL2   
 WHERE PNL2.PNLGRPNAME=PNL.PNLGRPNAME   
   AND PNL2.HIDDEN=0)
```
