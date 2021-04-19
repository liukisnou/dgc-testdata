# DGC Test Data Repository for Test Automation

To automate the generation and validation tests of COSE/CBOR Codes and it's base45/2D Code representations, a lot of data has to be collected to ensure the variance of the tests. This respository was established to collect a lot of different test data and related test cases of different member states in a standardized manner. Each member state can generate a folder in this section. 

## 2D Code

### Test Procedure

The test procedure has the following steps: 

1. Load RAW Data File X
2. Apply all test and validation rules to File X (from all countries). 
3. Fails one rule, the RAW Data File X is highlighted with the related Validation Rule/TestName Fail Status. 

The inline test procedure contains the steps: 

1. Load RAW File and load JSON Object, validate against schema.
2. Create CBOR from JSON Object. Validate against the CBOR content in the RAW File.
3. Sign with the JWK and compare the result to the COSE content.
4. Encode Cose to base45 and compare it to the BASE45 content. 
5. Apply the Prefix and Compare it to the PREFIX Content.
6. Reverse the process. 

### File Structure

/schema/**[Number]**.json <br>
**[COUNTRY]**/2DCode/raw/**[Number]**.json <br>
**[COUNTRY]**/2DCode/test/**[Number]_TestName**.js <br>
**[COUNTRY]**/2DCode/validation/**[Number]_RuleName**.js <br>
**[COUNTRY]**/2DCode/img/QR/**[Number]**.png

### Variables

COUNTRY is defined as the country code by ISO 3166. 

Number must be a unique number by country/type.


### JSON Schema

A number which identifies the used schema (used in the RAW Data).

### RAW Content

The  JSON Content under RAW is defined as: 
```
{
   "JSON":**JSON OBJECT**, 
   "CBOR":**CBOR (hex encoded)**, 
   "COSE":**COSE (hex encoded)**,  
   "BASE45": **BASE45 Encoded COMP**, 
   "PREFIX": **BASE45 Encoded Compression with Prefix HC(x):**, 
   "SCHEMA":**integer (USED SCHEMA)**, 
   "JWK":{"kty":"EC", 
          "crv":"P-256", 
          "x":"MKBCTNIcKUSDii11ySs3526iDZ8AiTo7Tu6KPAqv7D4",
          "y":"4Etl6SRW2YiLUrN5vfvVHuhp7x8PxltmWWlbbM4IFyM", 
          "d":"870MB6gfuTJ4HtUnUvYMyJpr5eUZNP4Bk43bVdj3eAE", 
          "kid":"1"}, 
}
 ```     
Example: 
```
{
 "JSON":{ "sub": { "gn": "Gabriele", "fn": "Musterfrau", "id": [ { "t": "PPN", "i": "12345ABC-321" } ], "dob": "1998-02-26", "gen": "female" }, "vac": [ { "dis": "840539006", "vap": "1119305005", "mep": "EU\/1\/20\/1528", "aut": "ORG-100030215", "seq": 1, "tot": 2, "dat": "2021-02-18", "cou": "AT", "lot": "C22-862FF-001", "adm": "Vaccination centre Vienna 23" }, { "dis": "840539006", "vap": "1119305005", "mep": "EU\/1\/20\/1528", "aut": "ORG-100030215", "seq": 2, "tot": 2, "dat": "2021-03-12", "cou": "AT", "lot": "C22-H62FF-010", "adm": "Vaccination centre Vienna 23" } ], "cert": { "is": "Ministry of Health, Austria", "id": "01AT42196560275230427402470256520250042", "vf": "2021-04-04", "vu": "2021-10-04", "co": "AT", "vr": "v1.0" } },"CBOR":"a4041a625eef58061a607dbbd801624154390103a101590207bf63737562bf62676e684761627269656c6562666e6a4d75737465726672617563646f626a313939382d30322d32366367656e6666656d616c656269649fbf61746350504e61696c31323334354142432d333231ffffff637661639fbf6364697369383430353339303036637661706a31313139333035303035636d65706c45552f312f32302f31353238636175746d4f52472d313030303330323135637365710163746f7402636c6f746d4332322d38363246462d303031636461746a323032312d30322d31386361646d781c56616363696e6174696f6e2063656e747265205669656e6e6120323363636f75624154ffbf6364697369383430353339303036637661706a31313139333035303035636d65706c45552f312f32302f31353238636175746d4f52472d313030303330323135637365710263746f7402636c6f746d4332322d48363246462d303130636461746a323032312d30332d31326361646d781c56616363696e6174696f6e2063656e747265205669656e6e6120323363636f75624154ffff6463657274bf626973781b4d696e6973747279206f66204865616c74682c204175737472696162696478273031415434323139363536303237353233303432373430323437303235363532303235303034326276666a323032312d30342d30346276756a323032312d31302d303462636f6241546276726476312e30ffff",
"COSE":"d2844da204489a024e6b59bf42ce0126a0590220a4041a625eef58061a607dbbd801624154390103a101590207bf63737562bf62676e684761627269656c6562666e6a4d75737465726672617563646f626a313939382d30322d32366367656e6666656d616c656269649fbf61746350504e61696c31323334354142432d333231ffffff637661639fbf6364697369383430353339303036637661706a31313139333035303035636d65706c45552f312f32302f31353238636175746d4f52472d313030303330323135637365710163746f7402636c6f746d4332322d38363246462d303031636461746a323032312d30322d31386361646d781c56616363696e6174696f6e2063656e747265205669656e6e6120323363636f75624154ffbf6364697369383430353339303036637661706a31313139333035303035636d65706c45552f312f32302f31353238636175746d4f52472d313030303330323135637365710263746f7402636c6f746d4332322d48363246462d303130636461746a323032312d30332d31326361646d781c56616363696e6174696f6e2063656e747265205669656e6e6120323363636f75624154ffff6463657274bf626973781b4d696e6973747279206f66204865616c74682c204175737472696162696478273031415434323139363536303237353233303432373430323437303235363532303235303034326276666a323032312d30342d30346276756a323032312d31302d303462636f6241546276726476312e30ffff5840cea198d7da5cb609f9b1d0622d3d2824d5a05b0a8cbd0f112ec8be8860be3944ab9f0a4614521328db093570bd64bc2c1d88decdd597578a329b2aa96fbfe906",
"BASE45":"NCFI.L3B6AP2YQ2QIN4U8X*8OVL9EM%9DVYD41QG.JFWRXFUB.NEPELVG5PE:NIEORLXCXXN*QEM7V5+G+W8CQFJRHQ O+ZLPUDBOR52PBH81T20/L./L6A1*HQ6I8//PZ-VBGW9ES-BF81VN%KEYKT6GY.J++TF4Q9:M$7R4FI12GQBP8JTIUTJ17%P9/5O87JYWDCURIVKX59B4K0.MC*FOMUFMPA*SH%QF%C/:ISDJKR93E6:52HAMH9GALFRY9WCCCTFVGTR76+FJ$H14YU ZE:F7Z/LH+P+$1MMK*$OOGHX 5J-IFLJI-Q170GP672F/B4NH0BBG44K*5F8WBJ9IJI8.8AO91KPT51RWC7%20UI0FCLB1T9PI/HM9SHA LFVM%0F+UOLTO 24CAC QGRZEY.87NE5WRX:NWWGIB24H52Q5RM4:69ZFBX45K 2$J8RFJG0CS:2UVUJWA4M89E0H6AM-696G:D5784W+J4+I$YJ1IL/*K$JND:O10RD$L$BRS$L6NV:OK$E744PM740V4VJH6BA+CM0JQT:2B+5 MBTXK: 6A*4NSHU62X+8I%9IC88ERX87BT8-XBB24G 0:F3RMCRTQN9VO1A00EB-3XQV6L05:5Y3KYCSIE6DCE7JR7NTCWN/VL3AWG8JJPU%MPGL2*4CL9DO:4BN7U0DK R*0W 8R0JSSI1DVS3%VI06NIR05",
"PREFIX":"HC1:NCFI.L3B6AP2YQ2QIN4U8X*8OVL9EM%9DVYD41QG.JFWRXFUB.NEPELVG5PE:NIEORLXCXXN*QEM7V5+G+W8CQFJRHQ O+ZLPUDBOR52PBH81T20/L./L6A1*HQ6I8//PZ-VBGW9ES-BF81VN%KEYKT6GY.J++TF4Q9:M$7R4FI12GQBP8JTIUTJ17%P9/5O87JYWDCURIVKX59B4K0.MC*FOMUFMPA*SH%QF%C/:ISDJKR93E6:52HAMH9GALFRY9WCCCTFVGTR76+FJ$H14YU ZE:F7Z/LH+P+$1MMK*$OOGHX 5J-IFLJI-Q170GP672F/B4NH0BBG44K*5F8WBJ9IJI8.8AO91KPT51RWC7%20UI0FCLB1T9PI/HM9SHA LFVM%0F+UOLTO 24CAC QGRZEY.87NE5WRX:NWWGIB24H52Q5RM4:69ZFBX45K 2$J8RFJG0CS:2UVUJWA4M89E0H6AM-696G:D5784W+J4+I$YJ1IL/*K$JND:O10RD$L$BRS$L6NV:OK$E744PM740V4VJH6BA+CM0JQT:2B+5 MBTXK: 6A*4NSHU62X+8I%9IC88ERX87BT8-XBB24G 0:F3RMCRTQN9VO1A00EB-3XQV6L05:5Y3KYCSIE6DCE7JR7NTCWN/VL3AWG8JJPU%MPGL2*4CL9DO:4BN7U0DK R*0W 8R0JSSI1DVS3%VI06NIR05",
}
```

### Test Content

Javascript tests which must be passed during the testing. The function body is defined as
```
function [name] ([RAW JSON]) {
    return [boolean]
}
```

### Validation Content

Javascript validation rules which must be passed during the testing of a 2D Code of the country. Each rule is applied on the decoded JSON Content. The function body is defined as
```
function [name] ([Decoded JSON Object]) {
    return [boolean]
}
```

### Image Content

Contains images of the generated base45 contents(PNG). 

### JWK Content

The key pair to sign and validate the data structures. 