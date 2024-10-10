<style scoped>
table {
  font-size: 13px;
}
</style>

#### **XX_PRNAVINFO_VW** 
| Record Name         | Description          |  
| ------------------- | -------------------- | 
| **XX_PRNAVINFO_VW** | Navigation View      |

| Num | Field Name         | Key | 
| --- | ------------------ | --- | 
|   1 | PORTAL_NAME        |     |
|   2 | MENUNAME           |     |
|   3 | PNLGRPNAME         |     |
|   4 | MARKET             |     |
|   5 | PORTAL_LABEL       |     |
|   6 | PORTAL_OBJNAME     |     |
|   7 | PORTAL_PRNTOBJNAME |     |
|   8 | PORTAL_REFTYPE     |     |
|   9 | XX_PORTAL_URLTEXT  |     |
|  10 | PORTAL_CNTPRV_NAM  |     |
|  11 | OBJECTOWNERID      |     |
|  12 | PORTAL_PRNTLABEL   |     |
|  13 | PORTAL_SOURCE      |     |
|  14 | PORTAL_NAVPATH     |     |

<font size="2">**SQL (Oracle Database)**</font> 

``` SQL
SELECT POR.PORTAL_NAME   
 , POR.PORTAL_URI_SEG1   
 , POR.PORTAL_URI_SEG2   
 , POR.PORTAL_URI_SEG3   
 , POR.PORTAL_LABEL   
 , POR.PORTAL_OBJNAME   
 , POR.PORTAL_PRNTOBJNAME   
 , POR.PORTAL_REFTYPE   
 , CAST(POR.PORTAL_URLTEXT AS VARCHAR(150))   
 , POR.PORTAL_CNTPRV_NAM   
 , POR.OBJECTOWNERID   
 , PNI.PORTAL_PRNTLABEL   
 , PNI.PORTAL_SOURCE   
 , PNI.PORTAL_NAVPATH   
  FROM PSPRSMDEFN POR   
  , PSPRSMNAVINFO PNI   
 WHERE POR.PORTAL_REFTYPE='C'   
   AND POR.PORTAL_REFTYPE = PNI.PORTAL_REFTYPE   
   AND POR.PORTAL_OBJNAME = PNI.PORTAL_OBJNAME
```