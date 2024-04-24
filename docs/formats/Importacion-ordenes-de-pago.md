# Archivos de intercambio para el recaudo de facturas

## Introducción

PlacetoPay es una plataforma que se comunica directamente con las redes financieras
permitiéndole un recaudo expedito de sus facturas. Al usar PlacetoPay usted puede
habilitar el recaudo con todos los medios de pago disponibles en Colombia así mismo
obvia los procesos de integración o desarrollo con las diferentes redes.

## Definición​ ​de​ ​los​ ​archivos​ ​de​ ​intercambio

Estos archivos contienen la relación de las facturas o los cobros autorizados para que sean​ ​recaudados​ ​a​ ​través​ ​de​ ​PlacetoPay.

Estos formatos permiten que la información sea consultada cuando se realice el recaudo independientemente del medio (Internet, sistema de audiorespuesta o punto de atención).

## Archivo​ ​de​ ​facturación​ ​[​ ​Formato​ ​Asobancaria​ ​2001​ ​]

A continuación se describe el formato de cargue de la información para recaudo, este formato está basado en la especificación de Asobancaria del 2001 con unas
modificaciones​ ​usando​ ​el​ ​campo​ ​de​ ​llenado.

Como regla general los archivos son de longitud fija, por lo cual para los valores
numéricos el valor debe tener un relleno de ceros a la izquierda para completar la
longitud. En tanto que para valores alfanuméricos el relleno debe ser con blancos a la derecha.

El​ ​formato​ ​posee​ ​la​ ​siguiente​ ​estructura:

```txt
Registro​ ​de​ ​encabezado​ ​de​ ​archivo
    Registro​ ​de​ ​encabezado​ ​de​ ​lote​ ​No.​ ​1
    Registro​ ​de​ ​detalle​ ​1
    ....
    Registro​ ​de​ ​detalle​ ​n
    Registro​ ​de​ ​control​ ​de​ ​lote​ ​No.​ ​1
    Registro​ ​de​ ​encabezado​ ​de​ ​lote​ ​No.​ ​n
    Registro​ ​de​ ​detalle​ ​1
    ....
    Registro​ ​de​ ​detalle​ ​n
    Registro​ ​de​ ​control​ ​de​ ​lote​ ​No.​ ​n
Registro​ ​de​ ​control​ ​de​ ​archivo
```

La​ ​longitud​ ​de​ ​cada​ ​registro​ ​es​ ​220​ ​caracteres​ ​y​ ​su​ ​contenido​ se​ ​precisa​ ​a​ ​continuación:

### Registro​ ​de​ ​encabezado​ ​de​ ​archivo

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo​ ​de registro | 2 | NUM | SI | 01 [constante] | ​Indica​ ​el​ ​tipo​  ​de​ ​registro
2 | NIT​ ​empresa recaudadora | 10 | NUM | SI | | NIT​ ​de​ ​la​ ​empresa​ ​que presenta​ ​la​ ​facturación
3 | NIT recaudador adicional | 10 | NUM | NO | | NIT​ ​de​ ​la​ ​empresa adicional​  ​que​ ​factura conjuntamente​ ​con​ ​la principal.​ **​No​ ​usado​ ​por PlacetoPay**
4 | Código​ ​de​ ​la entidad originadora | 3 | NUM | NO | | Código​ ​de​ ​la​ ​entidad financiera​ ​donde​ ​la Empresa​ ​tiene​ ​cuenta​ ​y desea​ ​que​ ​se​ ​le​ ​abone​ ​el recaudo​ ​por​ ​domiciliación. Este​ ​campo​ ​corresponde​ ​al código​ ​de​ ​tránsito​ ​de​ ​la entidad​ ​financiera.​ ​**No usado​ ​por​ ​PlacetoPay**
5 | Fecha​ ​del archivo | 8 | NUM | SI | AAAAMMDD | Fecha​ ​de​ ​creación​ ​del archivo
6 | Hora​ ​de grabación​ ​del archivo | 4 | NUM | SI | HHMM | Hora​ ​de​  ​grabación​ ​del archivo​ ​en​ ​formato​ ​de​ ​hora militar,​ ​es​ ​decir​ ​de​ ​0001 hasta​ ​las​ ​2400​ ​horas.
7 | Modificador​ ​de archivo | 1 | ALF | SI | A-Z,0-9 | Caracter​ ​que​ ​refleja​ ​el orden​ ​cronológico​ ​de grabación​ ​de​ ​los​ ​archivos​ ​y permite​ ​diferenciar​ ​varios archivos​ ​generados​ ​en​ ​un mismo​ ​día.​ ​Se​ ​debe emplear​ ​primero​ ​las​ ​letras mayúsculas​ ​(AZ)​ ​y posteriormente​ los números.
8 | Reservado | 182 | ALF | | | 

### Registro​ ​de​ ​encabezado​ ​de​ lote

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo​ ​de registro | 2 | NUM | SI | 05 [constante] | ​Indica​ ​el​ ​tipo​  ​de​ ​registro
2 | Código​ ​del servicio facturado | 13 | NUM | SI | Código EAN o NIT | ​El​ ​código​ ​EAN​ ​13​ ​es asignado​ ​por​ ​el​ ​IAC​ ​y​ ​se usa​ ​cuando​ ​la​  ​empresa factura​ ​dos​ ​o​ ​más​ ​servicios que​ ​deban​ ​ser diferenciados​ ​o discriminados​ ​ante​ ​el cliente​ ​receptor.​ ​El​ ​código EAN​ ​13​ ​identifica​ ​el​ ​país​ ​(3 posiciones),​ ​la​ ​empresa principal​ ​que​ ​factura​ ​(6),​ ​el tipo​ ​de​ ​servicio​ ​facturado (3)​ ​y​ ​características​ ​propias de​ ​cada​  ​convenio​ ​(1).​ ​El​ ​NIT solo​ ​puede​ ​ser​ ​empleado por​ ​aquellas​  ​Empresas​ ​que facturan​ ​un​ ​único​ ​servicio​ ​o que​ ​no​ ​manejen código EAN-13.
3 | Número​ ​de lote | 4 | NUM | SI | | Consecutivo​ ​del​ ​lote​ ​dentro del​ ​archivo.​ ​Cada​ ​archivo tiene​ ​su​ ​propia​ ​secuencia de​ ​numeración​ ​de​ ​lotes.
4 | Descripción del​ ​servicio Facturado | 15 | ALF | SI | | Nombre​ ​del​ ​servicio facturado​ ​que​ ​se​ ​le muestra​ ​al​ ​cliente​ ​receptor.
5 | Reservado | 186 | ALF | | |

### Registro de detalle

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo​ ​de registro | 2 | NUM | SI | 06 [constante] | ​Indica​ ​el​ ​tipo​  ​de​ ​registro
2 | Referencia principal del usuario | 48 | NUM | SI | | Es el código principal con el cual el documento a pagar es identificado en cada Empresa. Puede referirse al número de factura o al que designe la Empresa Originadora.
3 | Referencia secundaria del usuario | 30 | ALF | NO | |Es el código con el cual  el cliente es identificado en la Empresa.
4 | Períodos facturados | 2 | NUM | NO | | Indica el período facturado
5 | Ciclo | 3 | ALF | NO | | Indica el ciclo / zona
6 | Valor principal del servicio | 14 | NUM | SI | | Valor de la factura del servicio de la Empresa principal. 12 enteros, 2 decimales.
7 | Código del servicio facturado por Empresa adicional | 13 | NUM | NO | Código EAN13 | En los casos de empresas con facturación conjunta, se identifica la empresa adicional y su servicio. ****No usado por PlacetoPay****.
8 | Valor de servicio Adicional | 14 | NUM | NO | | Valor de la factura del servicio de la Empresa adicional. 12 enteros, 2 decimales. **No usado por PlacetoPay**.
9 | Fecha de Vencimiento | 8 | NUM | SI | AAAAMMDD | Fecha de vencimiento de la factura sin recargo
10 | Identificación de la EFR (banco del cliente) | 8 | NUM | NO | | Código que  identifica la entidad financiera donde el cliente domiciliado tiene su cuenta. **No usado por PlacetoPay**.
11 | No. cuenta del cliente pagador | 17 | ALF | NO | | Número de cuenta o de tarjeta de crédito del cliente que paga el servicio. **No usado por PlacetoPay**
12 | Tipo de cuenta del cliente pagador | 2 | NUM | NO | | Indica si el número de cuenta corresponde a ahorros, corriente o tarjeta de crédito. **No usado por PlacetoPay**.
13 | No. Identificación del cliente pagador | 10 | ALF | NO | | No. Identificación del cliente.
14 | Nombre del cliente pagador | 22 | ALF | NO | |
15 | Código de Entidad Financiera Originadora | 3 | NUM | NO | | Código de la entidad financiera donde la Empresa tiene cuenta y desea que se le abone el recaudo por domiciliación. Este campo corresponde al código de tránsito de la entidad financiera. Para recaudos por otros canales, este campo debe ir con espacios. **No usado por PlacetoPay**.
16 | Incremento al vencimiento | 10 | NUM | SI | | Valor del incremento diario a la factura, cuando es pagada después del vencimiento y hasta el corte. 6 enteros, 4 decimales. Si el valor es inferior a uno se supone porcentual, en caso contrario un valor fijo aplicado diariamente. Ej: 0000000150, representa el 1,5%.
17 | Fecha de corte | 8 | NUM | SI | AAAAMMDD | Corresponde a la fecha hasta la cual se recibe el pago de la factura. Esta fecha debe ser superior o igual a la fecha de vencimiento.
18 | Tipo de incremento al vencimiento | 1 | NUM | SI | 0 / 1 | Indica si el incremento al vencimiento es un valor fijo [1] o si es un valor diario [0]. 
19 | Reservado | 5 | ALF | NO | |

### Registro de control de lote

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo de registro | 2 | NUM | SI | 08 [constante] | Indica el tipo de registro
2 | Total registros del lote | 9 | NUM | SI | | Número total de registros grabados en el lote
3 | Valor de servicio Principal | 18 | NUM | SI | | Valor de la facturación de la empresa principal para el lote. 16 enteros, 2 decimales.
4 | Valor de servicio Adicional | 18 | NUM | NO | | Valor de la facturación de la empresa adicional para el lote. 16 enteros, 2 decimales. **No usado por PlacetoPay**
5 | Número de lote | 4 | NUM | SI | | Consecutivo del lote dentro del archivo. Cada archivo tiene su propia secuencia de numeración de lotes. Debe ser igual al campo 3, del registro de encabezado de lote. 
6 | Reservado | 169 | ALF | | |

### Registro de control de archivo

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo de registro | 2 | NUM | SI | 09 [constante] | Indica el tipo de registro
2 | Total registros de detalle | 9 | NUM | SI | | Número total de registros tipo "6" grabados en el archivo
3 | Valor de servicio Principal | 18 | NUM | SI | | Valor de la facturación de la empresa principal para el lote. 16 enteros, 2 decimales.
4 | Valor de servicio Adicional | 18 | NUM | NO | | Valor de la facturación de la empresa adicional para el lote. 16 enteros, 2 decimales. **No usado por PlacetoPay**
5 | Reservado | 173 | ALF | | |

## Archivo​ ​de​ recaudo ​[​ ​Formato​ ​Asobancaria​ ​2001​ ​]

A continuación se describe el formato correspondiente a la información generada como resultado del proceso de recaudo, cuyo destinatario es la empresa facturadora.

Como regla general los archivos son de longitud fija, por lo cual para los valores
numéricos el valor debe tener un relleno de ceros a la izquierda para completar la
longitud. En tanto que para valores alfanuméricos el relleno debe ser con blancos a la derecha.

El formato posee la siguiente estructura:

```txt
Registro de encabezado de archivo
    Registro de encabezado de lote No. 1
        Registro de detalle 1
        Registro de detalle n
        ….
    Registro de control de lote No. 1
    Registro de encabezado de lote No. n
        Registro de detalle 1
        ….
        Registro de detalle n
        Registro de control de lote No. n
    Registro de control de archivo
```

La longitud de cada registro es de 162 caracteres y su contenido se detalla a
continuación:

### Registro​ ​de​ ​encabezado​ ​de​ ​archivo

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo​ ​de registro | 2 | NUM | SI | 05 [constante] | ​Indica​ ​el​ ​tipo​  ​de​ ​registro
2 | NIT empresa facturadora | 10 | NUM | SI | | NIT de la empresa a la cual se le realiza el recaudo
3 | Fecha del recaudo | 8 | NUM | SI | AAAAMMDD | Fecha de la operación de recaudo.
4 | Código entidad financiera recaudadora | 3 | NUM | SI | TTT | Código de compensación (tránsito) de la entidad financiera recaudadora.
5 | Número de cuenta | 17 | ALF | SI | | Cuenta en la cual la entidad recaudadora le abona los dineros recaudados a la Empresa
6 | Fecha del archivo | 8 | NUM | SI | AAAAMMDD | Fecha de creación del archivo
7 | Hora de grabación del archivo | 4 | NUM | SI | HHMM | Hora de grabación del archivo en formato de hora militar, es decir de 0001 hasta las 2400 horas.
8 | Modificador de archivo | 1 | ALF | SI | A-Z,0-9 | Caracter que refleja el orden cronológico de grabación de los archivos y permite diferenciar varios archivos generados en un mismo día. Se emplean primero las letras mayúsculas (A-Z) y posteriormente los números.
9 | Tipo de cuenta | 2 | NUM | | | Indica si el número de cuenta corresponde a ahorros o corriente. 01 AHORROS 02 CORRIENTE 03 TARJETA DE CRÉDITO 
10 | Reservado | 107 | ALF | | |

### Registro​ ​de​ ​encabezado​ ​de​ lote

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo​ ​de registro | 2 | NUM | SI | 05 [constante] | ​Indica​ ​el​ ​tipo​  ​de​ ​registro
2 | Código​ ​del servicio recaudado | 13 | NUM | SI | Código EAN o NIT | ​El​ ​código​ ​EAN​ ​13​ ​es asignado​ ​por​ ​el​ ​IAC​ ​y​ ​se usa​ ​cuando​ ​la​  ​empresa factura​ ​dos​ ​o​ ​más​ ​servicios que​ ​deban​ ​ser diferenciados​ ​o discriminados​ ​ante​ ​el cliente​ ​receptor.​ ​El​ ​código EAN​ ​13​ ​identifica​ ​el​ ​país​ ​(3 posiciones),​ ​la​ ​empresa principal​ ​que​ ​factura​ ​(6),​ ​el tipo​ ​de​ ​servicio​ ​facturado (3)​ ​y​ ​características​ ​propias de​ ​cada​  ​convenio​ ​(1).​ ​El​ ​NIT solo​ ​puede​ ​ser​ ​empleado por​ ​aquellas​  ​Empresas​ ​que facturan​ ​un​ ​único​ ​servicio​ ​o que​ ​no​ ​manejen código EAN-13.
3 | Número​ ​de lote | 4 | NUM | SI | | Consecutivo​ ​del​ ​lote​ ​dentro del​ ​archivo.​ ​Cada​ ​archivo tiene​ ​su​ ​propia​ ​secuencia de​ ​numeración​ ​de​ ​lotes.
4 | Reservado | 143 | ALF | | |

### Registro de detalle

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo​ ​de registro | 2 | NUM | SI | 06 [constante] | ​Indica​ ​el​ ​tipo​  ​de​ ​registro
2 | Referencia principal del usuario | 48 | NUM | SI | | Es el código principal con el cual el documento a pagar es identificado en cada Empresa. Puede referirse al número de factura o al que designe la Empresa Originadora.
3 | Valor recaudado | 14 | NUM | SI | | Valor recaudo. 12 enteros, 2 decimales.
4 | Procedencia del pago | 2 | NUM | SI | | Indica el tipo de institución que recibió el pago del cliente. 01 PAGO A TRAVÉS DE BANCOS 02 PAGO A TRAVÉS DE CORPORACIÓN DE AHORRO Y VIVIENDA 03 PAGO A TRAVÉS DE ACH COLOMBIA 04 PAGO A TRAVÉS DE ASCREDIBANCO 05 PAGO A TRAVÉS DE ATH 06 PAGO A TRAVES DE CENIT 07 PAGO A TRAVÉS DE RED MULTICOLOR 08 PAGO A TRAVÉS DE SERVIBANCA
5 | Medios de pago | 2 | NUM | SI | | Indica el medio por el cual se recibió el pago. 11 DÉBITO EN CUENTA POR SISTEMA DE AUDIORESPUESTA 15 DÉBITO EN CUENTA POR INTERNET 21 TARJETA CRÉDITO POR SISTEMA DE AUDIORESPUESTA 25 TARJETA CRÉDITO POR INTERNET
6 | No de operación | 6 | NUM | NO | | Número de cheque o número que identifica la transacción en los dispositivos electrónicos. Corresponde al número o consecutivo asignado por los dispositivos electrónicos
7 | No de autorización | 6 | NUM | NO | | Número de autorización dada por la entidad del cliente (emisora o autorizadora), cuando el pago se efectúa por canales electrónicos (ATM, POS, audioservicio).
8 | Código de la entidad financiera debitada | 3 | NUM | NO | 000 | Código de compensación de la entidad financiera del cliente donde se efectuó el débito. No  usado por PlacetoPay.
9 | Código de sucursal | 4 | NUM | SI | 0000 | Código que identifica la sucursal, ciudad o  terminal (ATM, POS) donde se efectuó el pago. **PlacetoPay siempre reportará 000**.
10 | Secuencia | 7 | NUM | SI | | Secuencia de grabación de registro; inicia en 2
11 | Causal de devolución | 3 | ALF | NO | | **No usado por PlacetoPay**.
12 | Reservado | 65 | ALF | NO | |

### Registro de control de lote

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo de registro | 2 | NUM | SI | 08 [constante] | Indica el tipo de registro
2 | Total registros del lote | 9 | NUM | SI | | Número total de registros grabados en el lote
3 | Valor total recaudado en lote | 18 | NUM | SI | | Suma total de los valores de pago de los registros de detalle en el lote. 16 enteros, 2 decimales.
4 | Número de lote | 4 | NUM | SI | | Consecutivo del lote dentro del archivo. Cada archivo tiene su propia secuencia de numeración de lotes. 
5 | Reservado | 129 | ALF | | |

### Registro de control de archivo

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Tipo de registro | 2 | NUM | SI | 09 [constante] | Indica el tipo de registro
2 | Total registros recaudados en archivo | 9 | NUM | SI | | Número total de registros tipo "6" grabados en el archivo
3 | Valor total recaudado en lote | 18 | NUM | SI | | Suma total de los valores de pago de los registros de detalle. 16 enteros, 2 decimales.
4 | Reservado | 133 | ALF | | |

## Archivo de facturación [ Formato CSV-propietario ] 

Este formato nace del requerimiento de nuestros clientes por facilitar el cargue de facturas, en un mecanismo más intuitivo y que pueda ser fácilmente ajustado al tamaño de la compañía que lo desea cargar, sin implicar mayores esfuerzos y con la posibilidad de usar una hoja de cálculo como motor de generación.

En sí mismo el archivo contiene los campos básicos usados por la plataforma para el
proceso del pago de una factura.

Como regla general el archivo es de longitud variable, usando la coma (,) como separador de campo y la comilla doble como delimitador de campo para las cadenas de
caracteres. En los casos en que un campo no posea valor este deberá dejarse en blanco (,,). Cuando requiera para un valor númerico establecer una cifra decimal, debe usar el punto. Una posible variación a este formato es usar el punto y coma (;) para separar los campos y la coma (,) para las cifras decimales. Tenga en cuenta que el orden de los campos es estricto.

El formato posee la siguiente estructura:

```txt
Registro de control de archivo
    Registro de detalle 1
    ….
    Registro de detalle n
```
### Registro​ ​de​ ​control de archivo

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Fecha del archivo | 8 | NUM | SI | AAAAMMDD | Fecha de creación del archivo
2 | Hora de grabación del archivo | 4 | NUM | SI | HHMM | Hora de grabación del archivo en formato de hora militar, es decir de 0001 hasta las 2400 horas
3 | Modificador de archivo | 1 | ALF | SI | A-Z,0-9 |Caracter que refleja el orden cronológico de grabación de los archivos y permite diferenciar varios archivos generados en un mismo día. Se debe emplear primero las letras mayúsculas (AZ) y posteriormente los números.
4 | NIT empresa recaudadora | 10 | NUM | SI | | NIT de la empresa que presenta la facturación
5 | Total de registros en archivo | 9 | NUM | SI | | Número total de registros de detalle grabados en el archivo.
6 | Código del servicio facturado | 13 | NUM | SI | Código EAN o NIT | El código EAN 13 es asignado por el IAC y se usa cuando la empresa factura dos o más servicios que  deban ser diferenciados o discriminados ante el cliente receptor. El código EAN 13 identifica el país (3 posiciones), la empresa principal que factura (6), el tipo  de servicio facturado (3) y características propias de cada convenio (1). El NIT solo puede ser empleado por aquellas Empresas que facturan un único servicio o que no manejen código EAN-13.
7 | Descripción del servicio Facturado | 15 | ALF | SI | | Nombre del servicio facturado que se le muestra al cliente receptor.
8 | Valor total facturado en el archivo | 18 | NUM | SI | | Suma total de los valores de pago de los registros de detalle. 16 enteros, 2 decimales.

### Registro de detalle

Campo | Nombre | Long | Tipo | Req | Valor | Descripción
---------|----------|----------|----------|----------|----------|----------
1 | Referencia principal del usuario | 48 | NUM | SI | | Es el código principal con el cual el documento a pagar es identificado en cada Empresa. Puede referirse al número de factura o al que designe la Empresa Originadora.
2 | Referencia secundaria del usuario | 30 | ALF | NO | |Es el código con el cual  el cliente es identificado en la Empresa.
3 | No. Identificación del cliente pagador | 10 | ALF | NO | | No. Identificación del cliente.
4 | Nombre del cliente pagador | 22 | ALF | NO | |
5 | Valor principal del servicio | 14 | NUM | SI | | Valor de la factura del servicio de la Empresa principal. 12 enteros, 2 decimales
6 | Fecha de vencimiento | 8 | NUM | SI | AAAAMMDD | Fecha de vencimiento de la factura sin recargo
7 | Incremento al vencimiento | 10 | NUM | SI | | Valor del incremento diario a la factura, cuando es pagada después del vencimiento y hasta el corte. 6 enteros, 4 decimales. Si el valor es inferior a uno se supone porcentual, en caso contrario un valor fijo aplicado diariamente. Ej: 0000000150, representa el 1,5%.
8 | Fecha de corte | 8 | NUM | SI | AAAAMMDD | Corresponde a la fecha hasta la cual se recibe el pago de la factura. Esta fecha debe ser superior o igual a la fecha de vencimiento.
9 | Tipo de incremento al vencimiento | 1 | NUM | SI | 0 / 1 | Indica si el incremento al vencimiento es un valor fijo [1] o si es un valor diario [0]. 
10 | Base devolución | 14 | NUM | NO | | Valor sobre el cual se calcula el IVA. 12 enteros, 2 decimales.
11 | IVA | 14 | NUM | NO | | Valor de IVA aplicado a el valor de la base devolución. 12 enteros, 2 decimales.
12 | Hora de vencimiento | 14 | ALF | NO | H:i:s | Hora de vencimiento de la factura.

## Archivo de facturación [ Formato UBL-Invoice 1.0 ]

Desde su aprobación como una recomendación de la W3C en 1998, XML ha sido adoptado en una serie de industrias como marco para la definición de los mensajes de intercambio en el comercio electrónico. El uso generalizado de XML ha conducido al desarrollo de múltiples versiones en XML de documentos básicos, tales como órdenes de compra, notas de envío y facturas.

Si bien el uso de formatos específicos para cada industria o necesidad tiene la  ventaja de la máxima optimización para el contexto del negocio, la existencia de diferentes formatos para lograr el mismo fin en diferentes ámbitos de negocio genera una serie de desventajas.

El OASIS Universal Business Language (UBL) se destina a ayudar a resolver estos problemas mediante la definición de un formato genérico de intercambio XML para documentos de negocio que puede ampliarse para satisfacer las necesidades de determinadas industrias.

PlacetoPay usa el modelo propuesto OASIS en su implementación de UBL-Invoice en la versión 1.0.