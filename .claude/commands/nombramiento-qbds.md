---
name: nombramiento-qbds
description: Cuando se esté construyendo un objeto Query y se agreguen los respectivos QueryBuildDataSource para construir la consulta
---

Si se utilizan objetos QueryBuildDataSource deben ser nombrados consistentemente con la tabla que representarán con el sufijo 'DS'.

No permitido:

```
QueryBuildDataSource qbds;
```

Permitido:

```
QueryBuildDataSource custTableDS;
```
