---
name: identificadores-sysoperation
description: Forma de crear identificadores cuando se está construyendo una clase tipo Contract para usar en la generación de procesos SysOperationFramework
---

Cuando se necesite generar clases Contract para implementaciones de SysOperationFramework se deben utilizar Etiquetas. Estas etiquetas además deben crearse utilizando el skill `generacion-etiquetas`.

Como se usa el parámetro, la etiqueta debe ser escrita en un texto que sea para usuario final.

Utilizar:

```
[DataMember('@LBL:AccountNum')]
public AccountNum parmAccountNum(AccountNum _value = accountNum)
{
    accountNum = _value;
    return accountNum;
}
```

La etiqueta debería quedar:

AccountNum=Número de cuenta
