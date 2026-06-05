---
name: establecer-valores-boleanos-operacion
description: Describe la forma de establecer valores booleanos de acuerdo a condiciones evitando estructuras de control para el establecimiento de variables boleanas o asignación de valores en parámetros y solamente utilizando el resultado de una evaluación lógica
---

Si es necesario establecer un valor booleano evitar utilizar una estructura if - else o incluso una operación terciaria para establecer el valor por resultar redundante, en su lugar, asignarle el valor de la evaluación lógica.

Evitar:
```

boolean isOpen = false;

if (Table.Status == Status::Open)
{
    isOpen = true;
}
else
{
    isOpen = false;
}

```


Evitar por ser redundante:
```
boolean isOpen = Table.Status == Status::Open ? true : false;
```

En su lugar realizar la siguiente asignación:
```
boolean isOpen = Table.Status == Status::Open;
```
