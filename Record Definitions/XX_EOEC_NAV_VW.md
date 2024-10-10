#### **XX_EOEC_NAV_VW** 
| Record Name         | Description        |  
| ------------------- | ------------------ | 
| **XX_EOEC_NAV_VW**  | Navigation View    |

| Num | Field Name         | Key | 
| --- | ------------------ | --- | 
| 1   | PORTAL_NAME        | Asc |
| 2   | MENUNAME           | Asc |
| 3   | BARNAME            | Asc |
| 4   | ITEMNAME           | Asc |
| 5   | PNLGRPNAME         | Asc |
| 6   | MARKET             | Asc |
| 7   | PNLNAME            | Asc |
| 8   | PNLITEMNAME        |     |
| 9   | DFLTACTION         |     |
| 10  | PORTAL_LABEL       |     |
| 11  | PORTAL_OBJNAME     |     |
| 12  | PORTAL_PRNTOBJNAME |     |
| 13  | PORTAL_REFTYPE     |     |
| 14  | XX_PORTAL_URLTEXT  |     |
| 15  | PORTAL_CNTPRV_NAM  |     |
| 16  | OBJECTOWNERID      |     |
| 17  | XX_PORTAL_NAVPATH  |     |
| 18  | EOEC_FIND_NAV_GOTO |     |
| 19  | EOEC_FIND_NAV_HID  |     |

 <font size="2">**SQL (All Databases)**</font> 
 
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
