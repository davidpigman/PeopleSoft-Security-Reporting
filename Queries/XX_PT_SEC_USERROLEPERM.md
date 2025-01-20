#### XX_PT_SEC_USERROLEPERM

**Chosen Records**
| Alias | Record      | 
| ----- | ----------- |
|     A | PSOPRDEFN   |
|     C | PSROLECLASS |
|     D | PSCLASSDEFN |
|     E | PSROLEDEFN  |
|     B | PSROLEUSER  |

**Fields**
| Col | Record.Fieldname | Heading Text    |
| --- | ---------------- | --------------- |
|   1 | B.ROLEUSER       | User ID         |
|   2 | A.OPRDEFNDESC    | Description     |
|   3 | B.ROLENAME       | Role Name       |
|   4 | E.DESCR          | Descr           |
|   5 | D.CLASSID        | Permission List |
|   6 | D.CLASSDEFNDESC  | Class Descr     |

**Criteria**
| Logical | Expression1 | Condition Type | Expression 2 |
| ------- | ----------- | -------------- | ------------ |
|         | A.OPRID     | equal to       | B.ROLEUSER   |
| AND     | B.ROLENAME  | equal to       | C.ROLENAME   |
| AND     | C.CLASSID   | equal to       | D.CLASSID    |
| AND     | B.ROLENAME  | equal to       | E.ROLENAME   |
| AND     | E.ROLENAME  | equal to       | CASE :1 WHEN '' THEN E.ROLENAME ELSE :1 END |
| AND     | D.CLASSID   | equal to       | CASE :2 WHEN '' THEN D.CLASSID ELSE :2 END  |
| AND     | A.OPRID     | equal to       | CASE :3 WHEN '' THEN A.OPRID ELSE :3 END    |
