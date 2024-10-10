#### **XXPTSECRPT**

State Record: XX_SECMT_AET

##### XXPTSECRPT.MAIN 

<sub><sup>
| Section     | Step   | Commit After | Action |  
| ----------- | ------ | ------------ | -------|  
| MAIN        |
|             | SelRun | Default      | 
|             |        |              | SQL    |
</sup></sub>

``` SQL
%SelectInit(OPRID, RUN_CNTL_ID) 
 SELECT OPRID 
 , RUN_CNTL_ID 
  FROM %Table(SMC_RC_SEC_RPT) 
 WHERE OPRID = %OperatorId 
   AND RUN_CNTL_ID = %RunControl
```

| Section     | Step     | Commit After | Action       | Section Name | Program ID: |
| ----------- | -------- | ------------ | ------------ | ---          | ---         |
| MAIN        |
|             | 05DTbl   | After Step   |              |                     
|             |          |              | Call Section | 05DTbl       | XXPTSECRPT  |
|             | 10ITbl   | After Step   |              |                     
|             |          |              | Call Section | 05ITbl       | XXPTSECRPT  |
|             | 32INavig | After Step   |              |                     
|             |          |              | Call Section | 32INavig     | XXPTSECRPT  |
|             | 40URnSt  | After Step   |              |                     
|             |          |              | Call Section | 40URnSt      | XXPTSECRPT  |


| Section     | Step     | Commit After | Action       | Section Name | 
| ----------- | -------- | ------------ | ------------ | ---          | 
| 05DTbl      |
|             | Truncate | After Step   |              |                     
|             |          |              | Truncate     |              |             
|             |          |              |              | SQL          |       

``` SQL
%Execute(/)%TruncateTable(%Table(XX_MENUOBJ))/%TruncateTable(%Table(XX_MENUOBJ_CM))/%Truncate
Table(%Table(XX_EOEC_NAV))/%TruncateTable(%Table(XX_EOEC_NAV_ALL))
```
| Section     | Step     | Commit After | Action       | Message Set | Number | 
| ----------- | -------- | ------------ | ------------ | ----------- | ------ |
| 05DTbl      |
|             | Message  | Default      |              |                     
|             |          |              | Log Message  |             |             
|             |          |              |              | 22000       |  3     |

| Section     | Step     | Commit After | Action       |  |  | 
| ----------- | -------- | ------------ | ------------ | ----------- | ------ |
| 10ITbl      |
|             | MENU_CM  | After Step   |              |                     
|             |          |              | SQL          |                          

``` SQL
%InsertSelect(DISTINCT, XX_MENUOBJ_CM, XX_MENUOBJCM_VW) 
  FROM PS_XX_MENUOBJCM_VW 
  ORDER BY MENUNAME, BARNAME, ITEMNAME, PNLGRPNAME, MARKET
```

| Section     | Step     | Commit After | Action       |  |  | 
| ----------- | -------- | ------------ | ------------ | ----------- | ------ |
| 10ITbl      |
|             | MENU     | After Step   |              |                     
|             |          |              | SQL          |      

``` SQL
%InsertSelect(DISTINCT, XX_MENUOBJ, XX_MENUOBJ_VW) 
  FROM PS_XX_MENUOBJ_VW
```

| Section     | Step     | Commit After | Action       | Message Set | Number | 
| ----------- | -------- | ------------ | ------------ | ----------- | ------ |
| 10ITbl      |
|             | Message  | Default      |              |                     
|             |          |              | Log Message  |             |             
|             |          |              |              | 22000       |  4     |

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | PC_EOECB | After Step   |              |                     
|             |          |              | SQL          |    

``` SQL
%InsertSelect(XX_EOEC_NAV_ALL, XX_EOEC_NAV_VW ET)   
  FROM %Table(XX_EOEC_NAV_VW) ET
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | PC_EOEC  | After Step   |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(XX_EOEC_NAV_ALL, XX_EOEC_NAV_VW ET)   
  FROM %Table(XX_EOEC_NAV_VW) ET
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | U_URL    | After Step   |              |                     
|             |          |              | PeopleCode   | 

``` SQL
/* Declare Function ReportSQLError PeopleCode FUNCLIB_INEIP.ERROR_MSG FieldFormula; */

Local SQL &sqlURL_OBJECTS, &sqlPRTLDNAL;

&sqlURL_OBJECTS = GetSQL(SQL.XXPT_URL_OBJECTS);
&sqlPRTLDNAL = CreateSQL("UPDATE %Table(XX_EOEC_NAV_ALL) SET URL = :1 WHERE PORTAL_NAME = :2 AND PORTAL_REFTYPE = :3 AND PORTAL_OBJNAME = :4");
&sqlPRTLDNAL.TraceName = "XXPTSECMT.32INavig.XX_URL.XX_EOEC_NAV_ALL";

While &sqlURL_OBJECTS.Fetch(&strPORTAL_NAME, &strPORTAL_CNTPRV_NAM, &strPORTAL_REFTYPE, &strPORTAL_OBJNAME, &strMARKET, &strMENUNAME, &strPNLGRPNAME, &strPNLNAME);
   
   &strURL = GenerateComponentContentURL(&strPORTAL_NAME, "ERP", @("MenuName." | &strMENUNAME), &strMARKET, @("Component." | &strPNLGRPNAME), @("Page." | &strPNLITEMNAME), "");
   
   If &sqlPRTLDNAL.Execute(&strURL, &strPORTAL_NAME, &strPORTAL_REFTYPE, &strPORTAL_OBJNAME) Then
      If &sqlPRTLDNAL.RowsAffected > 0 Then
         
      End-If;
   Else
      /* ReportSQLError(&sqlPRTLDNAL.Status); */
   End-If;
   
End-While;
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | INAV_EMP | After Step   |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(DISTINCT, XX_EOEC_NAV, XX_EOEC_NAV_ALL ET) 
  FROM %Table(XX_EOEC_NAV_ALL) ET 
 WHERE ET.PORTAL_NAME = 'EMPLOYEE' 
   AND NOT EXISTS ( 
 SELECT 'X' 
  FROM PS_XX_EOEC_NAV ET_ES 
 WHERE ET_ES.PORTAL_OBJNAME = ET.PORTAL_OBJNAME 
   AND ET_ES.PORTAL_PRNTOBJNAME = ET.PORTAL_PRNTOBJNAME)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | INAV_SUP | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(DISTINCT, XX_EOEC_NAV, XX_EOEC_NAV_ALL ET) 
  FROM %Table(XX_EOEC_NAV_ALL) ET 
 WHERE ET.PORTAL_NAME = 'SUPPLIER' 
   AND NOT EXISTS ( 
 SELECT 'X' 
  FROM PS_XX_EOEC_NAV ET_ES 
 WHERE ET_ES.PORTAL_OBJNAME = ET.PORTAL_OBJNAME 
   AND ET_ES.PORTAL_PRNTOBJNAME = ET.PORTAL_PRNTOBJNAME)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | INAV_CST | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(DISTINCT, XX_EOEC_NAV, XX_EOEC_NAV_ALL ET) 
  FROM %Table(XX_EOEC_NAV_ALL) ET 
 WHERE ET.PORTAL_NAME = 'CUSTOMER' 
   AND NOT EXISTS ( 
 SELECT 'X' 
  FROM PS_XX_EOEC_NAV ET_ES 
 WHERE ET_ES.PORTAL_OBJNAME = ET.PORTAL_OBJNAME 
   AND ET_ES.PORTAL_PRNTOBJNAME = ET.PORTAL_PRNTOBJNAME)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | INAV_MBL | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(DISTINCT, XX_EOEC_NAV, XX_EOEC_NAV_ALL ET) 
  FROM %Table(XX_EOEC_NAV_ALL) ET 
 WHERE ET.PORTAL_NAME = 'MOBILE' 
   AND NOT EXISTS ( 
 SELECT 'X' 
  FROM PS_XX_EOEC_NAV ET_ES 
 WHERE ET_ES.PORTAL_OBJNAME = ET.PORTAL_OBJNAME 
   AND ET_ES.PORTAL_PRNTOBJNAME = ET.PORTAL_PRNTOBJNAME)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | INAV_PAR | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(DISTINCT, XX_EOEC_NAV, XX_EOEC_NAV_ALL ET) 
  FROM %Table(XX_EOEC_NAV_ALL) ET 
 WHERE ET.PORTAL_NAME = 'PARTNER' 
   AND NOT EXISTS ( 
 SELECT 'X' 
  FROM PS_XX_EOEC_NAV ET_ES 
 WHERE ET_ES.PORTAL_OBJNAME = ET.PORTAL_OBJNAME 
   AND ET_ES.PORTAL_PRNTOBJNAME = ET.PORTAL_PRNTOBJNAME)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 32INavig    |
|             | INAV_SIT | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%InsertSelect(DISTINCT, XX_EOEC_NAV, XX_EOEC_NAV_ALL ET) 
  FROM %Table(XX_EOEC_NAV_ALL) ET 
 WHERE ET.PORTAL_NAME = 'PS_SITETEMPLATE' 
   AND NOT EXISTS ( 
 SELECT 'X' 
  FROM PS_XX_EOEC_NAV ET_ES 
 WHERE ET_ES.PORTAL_OBJNAME = ET.PORTAL_OBJNAME 
   AND ET_ES.PORTAL_PRNTOBJNAME = ET.PORTAL_PRNTOBJNAME)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 40URnSt     |
|             | RS_MNOB  | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%UpdateStats(XX_MENUOBJ, HIGH)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 40URnSt     |
|             | RS_MOBC  | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%UpdateStats(XX_MENUOBJ_CM, HIGH)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 40URnSt     |
|             | RS_ENAV  | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%UpdateStats(XX_EOEC_NAV, HIGH)
```

| Section     | Step     | Commit After | Action       |  
| ----------- | -------- | ------------ | ------------ | 
| 40URnSt     |
|             | RS_ENAVA | Default      |              |                     
|             |          |              | SQL          | 

``` SQL
%UpdateStats(XX_EOEC_NAV_ALL, HIGH)
```


