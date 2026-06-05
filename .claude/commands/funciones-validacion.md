---
name: funciones-validacion
description: Describe cómo realizar las validaciones de condiciones de tal forma que se puedan realizar todas las validaciones posibles para otorgar al usuario final retroalimentación más completa sobre los datos que se procesan y evitar hallazagos nuevos con cada ejecución.
---

Cuando se generen las funciones de validación se deben evitar los siguientes patrones:
```
public void validateContract(SalesContract _contract)
{
    if (strlen(_contract.parmCustAccount) == 0)
    {
        throw error("@LBL:CustAccountMissing");
    }

    if (strlen(_contract.parmCurrencyCode) == 0)
    {
        throw error("@LBL:CurrencyCodeMissing");
    }
}
```
En su lugar se debe utilizar 1 de los dos patrones siguientes:

Si el proceso forma parte de un proceso de la aplicación en Dynamics utilizar una función booleana que evalue todas las condiciones, no deben enviar error, únicamente advertir y finalmente devolver el resultado de las validaciones

```
public boolean validateContract(SalesContract _contract)
{
    boolean ret = true;

    if (strlen(_contract.parmCustAccount) == 0)
    {
        warning("@LBL:CustAccountMissing");
        ret = false;
    }

    if (strlen(_contract.parmCurrencyCode) == 0)
    {
        warning("@LBL:CurrencyCodeMissing");
        ret = false;
    }

    return ret;
}
```
para que en el bloque de código se pueda usar algo similar a:
```
boolean result = this.validateContract(contract);

if (result)
{
    return;
}
```
Si el proceso forma parte de un proceso de integración que necesite retornar mensajes serializados, utilizar una función que devuelva un contenedor, que evalue todas las condiciones, no deben enviar error, únicamente advertir y finalmente devolver el contenedor con el resultado de las validaciones y los mensajes de las validaciones no satisfechas. Siendo el resultado booleano el primer elemento del contenedor.

```
public container validateContract(SalesContract _contract)
{
    boolean ret = true;
    List msgs = new List(Types::String);

    if (strlen(_contract.parmCustAccount) == 0)
    {
        msgs.addEnd("@LBL:CustAccountMissing");
        ret = false;
    }

    if (strlen(_contract.parmCurrencyCode) == 0)
    {
        msgs.addEnd("@LBL:CurrencyCodeMissing");
        ret = false;
    }

    return [ret, msgs];
}
```
para que en el bloque de código se pueda usar algo similar a:
```
boolean result;
List msgs;

[result, msgs]  = this.validateContract(contract);

result.parmResult(result);
result.parmMessages(msgs);
```
