# ibm-apiconnect-pipeline

** directory credentials-binary is safe**
becasue it mock id-secret

เริ่มจากการ List ก่อนว่า Server มี Identivty Provider อะไรที่ใช้งานได้บ้าง
เพื่อที่เราจะได้ Login ได้ถูกต้อง โดยต้องนำ Endpoint จาก Platform มาใช้งานเพื่อที่จะให้สามารถดึง API ได้
โดยเราสามารถดู config ของ local user ได้จาก ****-configurator ใน Openshift

https://www.ibm.com/docs/en/api-connect/10.0.5.x_lts?topic=tool-logging-in-management-server#rapic_cli_login__determine_idp

./apic identity-providers:list --scope provider --server https://xxxxxxxxxx.cloud.techzone.ibm.com  --fields title,realm --debug

ตัวอย่างผลลัพธ์ 
แต่เราจะต้องพยายามเลือกตัวที่ไม่เป็น OIDC คือ Login ด้วยแบบปกจิจะได้ login แบบใช้ passworf ทะลุเข้าไปโดยตรงได้

```bash
total_results: 2
results:
  - title: 'Cloud Manager User Registry'
    realm: 'admin/default-idp-1'
  - title: 'Common Services User Registry'
    realm: 'admin/common-services'
```

./apic client-creds:clear

ต้องอย่างลืมไปสร้าง User บน

./apic client-creds:set /Users/supakorn.t/ProjectCode/ibm/apiconnect/ibm-apiconnect-pipeline/credentials-binary/credentials.json

--password xxxxxxx

./apic login --username  wdrdres3qew5ts21  --server https://xxxxxxxxxx.cloud.techzone.ibm.com  --realm provider/default-idp-2 --debug



./apic apis:list-all --scope catalog --catalog sandbox  --server  https://xxxxxxxxxx.cloud.techzone.ibm.com --org bot


 ./credentials-binary/apic products:publish --server https://xxxxxxxxxx.cloud.techzone.ibm.com --catalog sandbox --org bot m.yaml

./apic products:list-all --server https://xxxxxxxxxx.cloud.techzone.ibm.com --catalog sandbox --org bot  --scope catalog



apic products:publish --server https://xxxxxxxxxx.cloud.techzone.ibm.com --catalog eai  --org bot ocb-product.yaml


oc cp apic jenkins-1-l7w2m:/tmp   