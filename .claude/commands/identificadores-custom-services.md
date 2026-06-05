---
name: identificadores-custom-services
description: Forma de crear identificadores cuando se está construyendo una clase tipo Contract para usar en la generación de Custom Services
---

Para evitar conflictos respecto a idiomas, los identificadores de los atributos de las clases contract no utilizarán etiquetas.

Evitar:
```
[DataMember('@LBL:AccountNum')]
public AccountNum parmAccountNum(AccountNum _value = accountNum)
{
    accountNum = _value;
    return accountNum;
}
```

En su lugar realizar lo siguiente:
```
[DataMember('cuentaCliente')]
public AccountNum parmAccountNum(AccountNum _value = accountNum)
{
    accountNum = _value;
    return accountNum;
}
```
