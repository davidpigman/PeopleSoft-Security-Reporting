
<style scoped>
table {
  font-size: 13px;
}
</style>

# Custom Fields
Add these custom fields to support the record definitions

| Field Name            | Field Type | Field Length | Format Type | 
| --------------------- | ---------- | -----------: | ----------- |
| **XX_ALLOWPSWDEMAIL** | Character  |            1 | Uppercase   |

| Label ID | Long Name | Short Name | Def |
| -------------- | ----------------------------- | ------------- | --- |
| ALLOWPSWDEMAIL | Allow Password to be Emailed? | OK pswd email | [x] |

| Field Name         | Field Type | Field Length | Format Type | 
| ------------------ | ---------- | -----------: | ----------- |
| **XX_AUTH_ACTION** | Character  |           30 | Uppercase   |

| Label ID       | Long Name         | Short Name  | Def |
| -------------- | ----------------- | ----------- | --- |
| XX_AUTH_ACTION | Authorized Action | Auth Action | [x] |

&nbsp;

| Field Name            | Field Type | Field Length | Format Type | 
| --------------------- | ---------- | -----------: | ----------- |
| **XX_CLASSID_DESCR**  | Character  |           30 | Mixedcase   |

| Label ID       | Long Name                   | Short Name  | Def |
| -------------- | --------------------------- | ----------- | --- |
| CLASSID_DESCR  | Permission List Description | Perm Descrn | [x] |
| DESCRIPTION    | Description                 | Descr       | [ ] |

&nbsp;

| Field Name            | Field Type | Field Length | Format Type | 
| --------------------- | ---------- | -----------: | ----------- |
| **XX_COMP_DESCR**     | Character  |           30 | Uppercase   |

| Label ID       | Long Name                   | Short Name  | Def |
| -------------- | --------------------------- | ----------- | --- |
| XX_COMP_DESCR  | Component Description       | Comp Descr  | [x] |

&nbsp;

| Field Name         | Field Type | Field Length | Format Type | 
| ------------------ | ---------- | -----------: | ----------- |
| **XX_OPRID_DESCR** | Character  |           30 | Mixedcase   |

| Label ID       | Long Name                   | Short Name  | Def |
| -------------- | --------------------------- | ----------- | --- |
| OPRID_DESCR    | Operator Description        | Oprid Descr | [x] |
| NAME           | Name                        | Name        | [ ] |
| DESCRIPTION    | Component Description       | Comp Descr  | [ ] |

&nbsp;

| Field Name          | Field Type     | Field Length | Format Type    | 
| ------------------- | -------------- | -----------: | -------------- |
| **XX_PIA_LBL_PATH** | Long Character |         1300 | Long Character |

| Label ID       | Long Name                   | Short Name  | Def |
| -------------- | --------------------------- | ----------- | --- |
| PIA_LBL_PATH   | PIA Label Navigation        | PIA LNav    | [x] |

&nbsp;

| Field Name      | Field Type     | Field Length | Format Type    | 
| --------------- | -------------- | -----------: | -------------- |
| **XX_PIA_PATH** | Character      |         254  | Uppercase      |

| Label ID       | Long Name                   | Short Name  | Def |
| -------------- | --------------------------- | ----------- | --- |
| PIA__PATH      | PIA Menu Path               | PIA Path    | [x] |

&nbsp;

| Field Name        | Field Type     | Field Length | Format Type    | 
| ----------------- | -------------- | -----------: | -------------- |
| **PNLGRP_ACTION** | Character      |           30 | Uppercase      |

| Label ID       | Long Name                   | Short Name  | Def |
| -------------- | --------------------------- | ----------- | --- |
| PNLGRP_ACTION  | Panel Group Action          | PnlGrp Actn | [x] |

&nbsp;

| Field Name            | Field Type     | Field Length | Format Type    | 
| --------------------- | -------------- | -----------: | -------------- |
| **XX_PORTAL_NAVPATH** | Character      |          254 | Uppercase      |

| Label ID       | Long Name                   | Short Name      | Def |
| -------------- | --------------------------- | --------------- | --- |
| PORTAL_NAVPATH | Portal Navigation Path      | Prtl Navig Path | [x] |

&nbsp;

| Field Name            | Field Type     | Field Length | Format Type    | 
| --------------------- | -------------- | -----------: | -------------- |
| **XX_PORTAL_URLTEXT** | Character      |          150 | Character      |

| Label ID       | Long Name                   | Short Name      | Def |
| -------------- | --------------------------- | --------------- | --- |
| PORTAL_URLTEXT | Portal URL Logical Text     | Prtl URL Txt    | [x] |

&nbsp;

| Field Name            | Field Type     | Field Length | Format Type    | 
| --------------------- | -------------- | -----------: | -------------- |
| **XX_ROLE_DESCR**     | Character      |           30 | Character      |

| Label ID       | Long Name                   | Short Name      | Def |
| -------------- | --------------------------- | --------------- | --- |
| ROLE_DESCR     | Role Description            | Role Descr      | [x] |
| DESCRIPTION    | Description                 | Descr           | [ ] |

&nbsp;

| Field Name            | Field Type     | Field Length | Format Type    | 
| --------------------- | -------------- | -----------: | -------------- |
| **XX_STARTAPPSERVER** | Character      |            1 | Uppercase      |

| Label ID       | Long Name                    | Short Name      | Def |
| -------------- | ---------------------------- | --------------- | --- |
| STARTAPPSERVER | Can Start Application Server | StartAppSrv     | [x] |

&nbsp;

| Field Name            | Field Type     | Field Length | Format Type    | 
| --------------------- | -------------- | -----------: | -------------- |
| **XX_TIMEOUTMINUTES** | Character      |            5 | Uppercase      |

| Label ID       | Long Name                    | Short Name      | Def |
| -------------- | ---------------------------- | --------------- | --- |
| TIMEOUTMINUTE  | Time-out Minutes             | Time-out        | [x] |
| MAXPROCESSTIME | Max Processing Time          | Max Prcs Time   | [x] |
| EXPIRE         | Expiration Time in minutes   | Expiration Time | [x] |