# Dataton BC 2018

*Dirección de Capacidades Analíticas y Gobierno de Información, Grupo Bancolombia*<br>
Esta versión: *2018-10-17*<br>
Documentación tablas

## Naturaleza de los datos

Los datos entregados en este reto corresponden a transacciones realizadas por clientes persona del banco vía [PSE](https://www.pse.com.co/inicio). Estas transacciones, a diferencia de las transacciones realizadas vía POS, no cuentan con un código [MCC](https://en.wikipedia.org/wiki/Merchant_category_code) atado a la transacción, que permite conocer la categoría de comercio a la que pertence el establecimiento de comercio donde se realiza la transacción. Adicionalmente, muchas de estas transferencias por PSE corresponden a transferencias de pagos de servicios públicos, seguros, colegios, arrendamientos, y otros gastos que pueden ser denominados como gastos grandes. En el marco de un sistema de gestión de finanzas personales, poder categorizar adecuadamente estas transacciones que se realizan por PSE es de suma importancia para contar con una foto completa de la actividad de gastos de los clientes. Para este reto, los equipos participantes tendrán acceso a una muestra de transacciones PSE que corresponden a algo más de 300 mil clientes (persona), seleccionados de manera aleatoria. La tabla de transacciones cuenta con 11.8 millones de registros (uno para cada transacción), realizados entre septiembre de 2016 y octubre de 2018.

**NOTA** Los datos han pasado por un proceso relativamente simple de curación, pero se han dejado algunos ruidos en la calidad de éstos con el fin de que los equipos también lleven a cabo un proceso de inspección y limpieza.

## Tablas

### dt_trxpse_personas_2016_2018_muestra_adjt

* Tabla con transacciones PSE durante 2016-09 a 2018-10 (muestra aleatoria de clientes persona -- 340 mil clientes --)

| **Campo**     | **Descripción**                    | **Tipo**       |
| ------------- |:----------------------------------:|:--------------:|
| id_trn_ach    | identificador único de transacción | string         |
| id_cliente    | id. único de cliente (pagador)     | bigint         |
| fecha         | fecha de transacción               | decimal(8,0)   |
| hora          | hora de transacción (HHMMSS)       | decimal(6,0)   |
| valor_trx     | valor ($) transacción              | double         |
| ref1          | texto libre referencia 1           | string         |
| ref2          | texto libre referencia 2           | string         |
| ref3          | texto libre referencia 3           | string         |
| sector        | sector eco. receptor               | varchar(24)    |
| subsector     | subsector eco. receptor            | varchar(62)    |
| descripcion   | descripción subsector receptor     | varchar(24)    |

### dt_info_pagadores_muestra

* Tabla con (alguna) información demográfica de los pagadores (muestra aleatoria de 340 mil clientes)

| **Campo**       | **Descripción**                    | **Tipo**       |
| --------------- |:----------------------------------:|:--------------:|
| id_cliente      | id. único de cliente (pagador)     | bigint         |
| seg_str         | segmento estructural               | string         |
| ocupacion       | ocupación                          | string         |
| tipo_vivienda   | tipo de vivienda                   | string         |
| nivel_academico | nivel académico                    | string         |
| estado_civil    | estado civil                       | string         |
| genero          | genero                             | string         |
| edad            | edad                               | int            |
| ingreso_rango   | rango de ingreso estimado          | string         |

El **seg_str** corresponde a la segmentación estructural, que solo depende de los ingresos reportados por el cliente y su tamaño comercial (volumen de activos y pasivos con el banco). Posibles valores son PERSONAL, PERSONAL PLUS, EMPRENDEDOR, PREFERENCIAL, OTRO (incluye también clientes no segmentados debido a falta de información de éstos).

**ocupacion**

| **Código** | **Descripción**           |
| ---------- |:-------------------------:|
| E          | SOCIO O EMPLEADO - SOCIO  |    		
| I          | DESEMPLEADO CON INGRESOS  |    		
| O          | OTRA                      |
| P          | INDEPENDIENTE             |          		
| S          | DESEMPLEADO SIN INGRESOS  |  		
| 1          | EMPLEADO                  |  		
| 2          | ESTUDIANTE                |  		
| 3          | INDEPENDIENTE             | 		
| 4          | HOGAR               		 |
| 5          | JUBILADO                  |  		
| 6          | AGRICULTOR                |  		
| 7          | GANADERO                  |  		
| 8          | COMERCIANTE               |  		
| 9          | RENTISTA DE CAPITAL       |

Si en los datos aparece algún otro código no listado en la tabla anterior, es posible asumir que se trata de un valor nulo, no disponible para el cliente en cuestión.

**tipo_vivienda**

| **Código** | **Descripción**           |
| ---------- |:-------------------------:|
| A          | ALQUILADA                 |
| R          | ALQUILADA                 |
| F          | FAMILIAR                  |
| I          | NO INFORMA                |
| P          | PROPIA                    |
| O          | PROPIA                    |

Si en los datos aparece algún otro código no listado en la tabla anterior, es posible asumir que se trata de un valor nulo, no disponible para el cliente en cuestión.

**nivel_academico**

| **Código** | **Descripción**           |
| ---------- |:-------------------------:|
| H          | BACHILLERATO              |
| B          | BACHILLERATO              |
| U          | UNIVERSITARIO             |
| E          | ESPECIALIZACION           |
| N          | NINGUNO                   |
| P          | PRIMARIA                  |
| S          | POSTGRADO                 |
| T          | TECNICO                   |
| I          | NO INFORMA                |

**estado_civil**

| **Código** | **Descripción**           |
| ---------- |:-------------------------:|
| S          | SOLTERO                   |
| M          | CASADO                    |
| F          | DESCONOCIDO               |
| I          | NO INFORMA                |
| D          | DIVORCIADO                |
| W          | VIUDO                     |
| O          | OTRO                      |

**genero**

| **Código** | **Descripción**           |
| ---------- |:-------------------------:|
| F          | FEMENINO                  |
| M          | MASCULINO                 |

## Categorización propuesta por el equipo de analítica de personas

En el Banco ya se han llevado a cabo esfuerzos por categorizar transacciones provenientes del canal POS (con tarjetas débito y crédito), lo cual ha incluído, entre otras cosas, una depuración y limpieza de los códigos MCC. A continuación mostramos, a manera de referencia, la categorización propuesta por el equipo.

1. Comida
2. Hogar
3. Cuidado personal
4. Entretenimiento
5. Educación
6. Transporte
7. Viajes
8. Ahorro
9. Pago de deudas
10. Ingresos
11. Retiros en efectivo
12. Mascotas
13. moda
14. Tecnología y comunicaciones
15. Otros

## NOTA IMPORTANTE

Recuerden que esta información aún contiene un elevado nivel de ruido. No solo no ha sido depurada de posibles datos atípicos (transacciones de valor muy elevado) fruto de errores o transacciones fallidas, sino que también cuenta con el ruido asociado al campo de referencia, donde se involucra el factor humano, ya que son campos de texto libre que pueden contener cualquier tipo de información.

Por seguridad, hemos eliminado cualquier número presente en dichos campos de referencia (cédulas, nits, montos, contratos, etc.).
