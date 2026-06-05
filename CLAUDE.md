## General

El código que se debe generar es en código X++ para el ERP Microsoft Dynamics 365 Finance And Operations.

## Identación

El código siempres debe ir identado en el margen izquierdo para poder distinguir el anidamiento de código 

## Tabulación

No deben tabularse las declaraciones de variables, parámetros, asignación o compración de valores, en su lugar solamente dejar un espacio.

1. Declaración de Variables

No permitida:

SalesTable          salesTable;
CustInvoiceJour     custInvoiceJour;

Permitida:

SalesTable salesTable;
CustInvoiceJour custInvoiceJour;

2. Asignación de valores

No Permitidas:

SalesTable.AccountNum       = custTable.AcccountNum;
SalesTable.SalesResponsible = custTable.SalesResponsible;

SalesTable.AccountNum =         custTable.AcccountNum;
SalesTable.SalesResponsible =   custTable.SalesResponsible;

Permitidas:

SalesTable.AccountNum = custTable.AcccountNum;
SalesTable.SalesResponsible = custTable.SalesResponsible;

3. Evaluación de expresiones

No Permitida:
```

select firstonly salesTable 
    where   salesTable.AccountNum           = custTable.AccountNum
    &&      salesTable.SalesResponsible     = custTable.SalesResponsible;

```

Permitido: 
```
select firstonly salesTable 
    where salesTable.AccountNum = custTable.AccountNum
    && salesTable.SalesResponsible = custTable.SalesResponsible;

```
4. Declaración de parámetros

No permitido:

Las tabulaciones y la alíneación de los parámetros por columna
```
public static void getSalesTableFromCustInfo(SalesResponsible       _salesResponsible
                                             CustAccount            _ custAccount)
```
Permitido:

Dejar un espacio entre el tipo y el parámetro y dejar un solo tabulador como lo haría la mayoría de editores de código:
```
public static void getSalesTableFromCustInfo(SalesResponsible _salesResponsible
    CustAccount _ custAccount)
```
## Priorizar la aplicación de guard clases para validación:

Cuando se necesiten realizar evaluaciones o validaciones en funciones siempre usar guard clauses para evitar anidamiento excesivo.

## Evitar validaciones en funciones de proceso y generar validaciones en funciones especificas

Si las validaciones a realizar supera el número 1, entonces generar una función que devuelvan el valor de la validación.

## Evitar utilizar dangling semicolon

En versiones anteriores de AX era usual utilizar un dangling semicolon o punto y coma huérfano para separar declaraciones y el resto del código, no utilizarlo en ninguna circunstancia en el código generado.

## No utilizar ListIterator o MapIterator en su lugar usar ListEnumerator o MapEnumerator

En operaciones con Listas o Mapas no utilizar el objeto ListIterator o MapIterator respectivamente para iterar Listas, en su lugar utilizar ListEnumerator y MapEnumerator

Esto es debido a que el Iterator requiere verificación, recuperación y movimiento en 3 instrucciones distintas, corriendo el riesgo que en revisiones se omita o se borre la instrucción next()
```
while(Iterator.more())
{
    var value = iterator.value();

    iterator.next();

}
```
Mientras que el enumerator solo requiere 2, verificación y movimiento en uno solo paso y recuperación
```
while (enumerator.moveNext())
{
    var value = enumerator.current();
}
```

## Declaración de variables 

Es un patrón conocido declarar las variables al inicio de la función, pero en la generación de código declararlas en la misma asignación

Evitar

```
public void processQuery(CustGroup _custGroup)
{
    Query q;
    QueryRun qr;
    QueryBuildDataSource custTableDS;
    QueryBuildRange custGroupRange;

    q = new Query();

    custTableDS = q.addDataSource(tableNum(CustTable));
    custGroupRange = custTableDS.addRange(_custGroup);

    qr = new QueryRun(q);


}

```

En su lugar realizar lo siguiente:

```
public void processQuery(CustGroup _custGroup)
{
    Query q = new Query();
    QueryBuildDataSource custTableDS = q.addDataSource(tableNum(CustTable));
    QueryBuildRange custGroupRange = custTableDS.addRange(_custGroup);

    QueryRun qr = new QueryRun(q);

}

```

## Generación de funciones que devuelven multiples valores

En los escenarios donde aplique, generar funciones que devuelvan un resultado y los valores asociados al resultado dependiendo si es verdadero o no, debe devolverse en un contenedor.
el resultado de la operación debe ser boolean y debe ser el primer elemento del contenedor.

Ejemplo de implementación:

```

public container calcTax(TaxTable _taxTable, Amount _base)
{

    
    if (taxTable.TaxCode == this.validTaxCode)
    {
        return [true, TaxEngine::calcTax(_base,  _taxTable.TaxCode)];
    }

    return [false, 0];

}

public void run()
{
    boolean result = false;
    Amount taxAmount;

    [result, taxAmount] = this.calcTax(TaxTable, Base);

    if (result)
    {
        this.RegisterTaxAmount(taxAmount);
    }

}


```

## Código de ejemplo obtenido de internet
Algunas secciones de código son obtenidas de foros y blogs, en su mayoría el código no cumple con las directrices establecidas en este archivo ni en ningún Skill, por lo que debe ignorarse cualquier patrón de desarrollo implementado en estos códigos de ejemplo, siempre deben priorizarse las directivas de los archivos CLAUDE.md y los skills establecidos, sin embargo esto no significa que al solicitar modificaciones en los archivos que contienene este código, este deba modificarse, solamente realizar los cambios puntuales siguiendo las directrices de este documento y los Skills.