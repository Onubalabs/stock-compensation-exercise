# Glosario

Términos que Alejandro ha pedido definir durante el ejercicio.

**Formato:**
- **Orden alfabético estricto** en una sola lista, sin agrupar por temas. Las cifras van primero y los símbolos se ignoran al ordenar ([HC] se ordena como HC).
- Cada entrada es **un solo párrafo breve, de 2 o 3 líneas como máximo**: qué es, cómo aparece en Sherpas (con su fuente) y, si cabe, el ejemplo de John & Jane.
Los datos de la plataforma proceden de un inventario interno de lo observado, que no se publica (confidencial). [HC] = artículo del Help Center sobre el score, incluido en el enunciado del ejercicio.

---

## 401(k)
Plan de jubilación que ofrece la empresa en EE. UU.: el empleado aporta por nómina y la empresa suele añadir un *match* (*Traditional*: tributa al retirar; *Roth*: al aportar). En Sherpas hay tipos 401k Traditional, Roth y Solo; John y Jane tienen $80K y $60K.

## AMT (Alternative Minimum Tax)
Segundo cálculo del impuesto sobre la renta que garantiza un mínimo; se paga el mayor de los dos. Al ejercer ISO, la ganancia puede generar AMT **sin haber vendido nada**. El motor fiscal de Sherpas no lo incluye.

## Brokerage (cuenta de brokerage)
Cuenta de inversión normal en un bróker, **sin ventaja fiscal**: dividendos y plusvalías tributan cada año. En Sherpas se agrupa como *Taxable*. John y Jane tienen una conjunta en Vanguard con $700K (VTI + AGG).

## Captura (de datos)
Cómo **entra** un dato en la plataforma: qué se pregunta, quién responde y por qué vía (punto 1 del encargo, "cómo se introduce"). En Sherpas: cuestionario del cliente, alta de cuentas manual / enlace / extracto y subida de documentos.

## Cash flow (flujo de caja)
Área del score (ver *Financial Health Score*): dinero que entra frente al que sale. Sherpas mira la tasa de ahorro, la sostenibilidad de las retiradas y los compromisos fijos [HC].

## Caso conductor (Caso)
Los datos de entrada del Prototipo: el hogar de la **Demo** como referencia inicial + la **hipótesis** de stock compensation (Acme, RSU) + **supuestos** de cálculo. Es la única fuente del ejercicio: el diagnóstico del Prototipo es su consecuencia (`08_Caso_conductor.md`).

## Consolidar / consolidación (vesting)
Momento en que las acciones o las opciones concedidas **pasan a ser tuyas de verdad**, según un calendario y si sigues en la empresa; lo no consolidado (*unvested*) se pierde si te vas. Ej.: 4.000 RSU al 25 % anual son 1.000 acciones tuyas cada año. No aparece en Sherpas.

## Debt (deuda)
Área del score: lo que se debe; importa cuánto cuesta, cuánto pesa frente al ingreso y para qué se usó. Sherpas mira el tipo de cada deuda, los saldos *revolving* y el coste de la vivienda [HC].

## Demo
El diagnóstico **real** de John & Jane en la **Plataforma** (Sherpas, la aplicación real), visto con las credenciales del ejercicio. Solo es la referencia inicial del Caso: sus textos y los resultados del motor que no sabemos recalcular se muestran marcados con ❓.

## Enablement (guía para el asesor)
Material que **prepara al usuario para usar una funcionalidad nueva**: cuándo usarla, cómo leer lo que muestra y cómo explicárselo a su cliente, con preguntas frecuentes. En Sherpas el usuario es el asesor; la oferta lo pide como parte de la *route to market*. Ej.: cómo presentarle a John su concentración en Acme.

## Equity
Literalmente, **propiedad**. Tres usos: (1) acciones o renta variable, como "Equity - US" en Investment analysis; (2) *equity compensation*, sinónimo de stock compensation, que no aparece en Sherpas; (3) valor neto de un bien, p. ej. *home equity* = casa − hipoteca.

## ESPP (Employee Stock Purchase Plan)
Plan para **comprar acciones de tu empresa con descuento** (hasta ~15 %) mediante aportaciones por nómina en periodos de ~6 meses, a menudo con *lookback*. Es a la vez ahorro mensual y activo. No aparece en Sherpas. ⚠️ Cifras por verificar (ver 04).

## FICA
Cotizaciones a la Seguridad Social (6,2 %, con tope anual de sueldo) y Medicare (1,45 %) que se descuentan del sueldo en EE. UU. También se pagan sobre las RSU al consolidar y sobre la ganancia de las NSO al ejercer. En Sherpas es la salida *FICA tax*.

## Financial Health Score
Diagnóstico de 0 a 100 que genera Sherpas. Agrupa sus checks en cinco áreas (Cash flow, Debt, Investing, Liquidity, Protection), cuyo máximo depende de la etapa vital del hogar [HC]:

| Área | Acumulando patrimonio | Jubilado |
|---|---|---|
| Cash flow | 30 | 25 |
| Debt | 20 | 10 |
| Protection | 20 | 20 |
| Liquidity | 15 | 20 |
| Investing | 15 | 25 |

## [HC]
No es un término financiero: es nuestra etiqueta de fuente para el artículo del **Help Center** *"How is the Financial Health Score calculated?"*, incluido en el enunciado del ejercicio. El resto del Help Center requiere cuenta de asesor.

## Investing (inversión)
Área del score: cómo está colocado lo invertido (asignación, concentración, efectivo ocioso y ubicación fiscal) [HC]. Es el área natural para la concentración en la acción de la propia empresa.

## ISO (Incentive Stock Options)
Opciones con **ventaja fiscal**, solo para empleados y típicas de startups: al ejercer no pagas impuesto normal, pero la ganancia puede generar **AMT**. No aparecen en Sherpas y, sin AMT en el motor, no se podrían modelizar bien. ⚠️ Reglas por verificar (ver 04).

## Liquidity (liquidez)
Área del score: capacidad de disponer de dinero rápido y sin pérdidas ante un imprevisto, sin vender inversiones en mal momento. Sherpas mira cuánto duran las reservas [HC].

## NSO / NQSO (Non-Qualified Stock Options)
Opciones **sin ventaja fiscal**: derecho a comprar acciones de tu empresa a un precio fijo (*strike*). Al ejercer, la ganancia tributa como sueldo; caducan y pueden valer 0 si la acción cae bajo el strike. No aparecen en Sherpas.

## Opciones sin ejercer (unexercised options)
Opciones que tienes pero que aún no has usado para **comprar** las acciones al *strike* (eso es "ejercer"). Hasta entonces solo vale la diferencia con el precio de mercado (*spread*): pueden caducar o quedarse en 0 si la acción cae bajo el strike. No aparecen en Sherpas.

## Protection (protección)
Área del score: cobertura frente a catástrofes (fallecimiento, incapacidad, demandas), sobre todo con seguros; *umbrella* es el seguro de responsabilidad civil "paraguas".

## Prototipo
Nuestros dos HTML, que reproducen la Plataforma con la propuesta resaltada: el **cuestionario** (`prototipo/index.html`) y el **diagnóstico** (`prototipo/diagnostico.html`). No es la Demo: arranca con los datos del Caso y el diagnóstico no se recalcula si se cambian.

## PSU (Performance Stock Units)
RSU cuya cantidad final **depende de cumplir objetivos** (ventas, rentabilidad de la acción frente a competidores…) durante un periodo, normalmente de 3 años; pueden acabar en 0 o superar lo concedido. Típicas de directivos y tributan como las RSU. No aparecen en Sherpas.

## Release notes (notas de versión)
Anuncio breve de **qué cambia en el producto**: qué hay nuevo, para quién, por qué importa y qué limitaciones tiene. Lo leen los usuarios (los asesores) y los equipos internos (ventas, soporte). Ej.: *"Sherpas now understands stock compensation…"*, con la exposición al empleador como novedad principal.

## RSU (Restricted Stock Units)
**Promesa de entregarte acciones** cuando consolidan (*vesting*), sin pagar nada; al consolidar tributan como sueldo y la retención estándar (22 %) puede quedarse corta. Luego son acciones normales y, si no se venden, se acumula concentración. No aparecen en Sherpas.

## VTI
*Ticker* del **Vanguard Total Stock Market ETF**, un fondo muy diversificado que replica toda la bolsa de EE. UU. El score lo trata como la mayor posición. John y Jane tienen $450K en su Brokerage.
