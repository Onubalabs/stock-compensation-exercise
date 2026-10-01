# Trabajo en curso

> **Qué es este documento:** las decisiones que tomamos sobre la solución, a medida que las acordamos.
> Los datos de la plataforma proceden de un inventario interno de lo observado, que no se publica (confidencial). [HC] = artículo del Help Center sobre el score, incluido en el enunciado del ejercicio.
> Se distingue siempre entre **hecho** y **hipótesis**.

---

## 1. El problema

### 1.1 El encargo describe un síntoma
El enunciado lo plantea como un hueco de captura: *"no hay un sitio donde meterla"*.

- **Hecho:** no hay tipo de cuenta, línea de ingreso, categoría de documento ni pregunta sobre el empleador.
- **Hipótesis:** si solo creamos un sitio donde meterla, el diagnóstico seguiría sin entenderla. El problema de fondo es este:

> **Para los clientes en los que más importa, el diagnóstico no ve ni su mayor riesgo ni una de sus mayores fuentes de patrimonio.**

La oferta pide exactamente esta habilidad: *"spot when a request is really a symptom of a different problem"*.

### 1.2 Por qué es difícil: un objeto con cuatro caras que cambia con el tiempo
La stock compensation es a la vez:

| Cara | Por qué |
|---|---|
| **Ingreso** | Cada consolidación (*vesting*) es sueldo |
| **Activo** | Las acciones |
| **Gasto** | Impuestos al consolidar o ejercer; aportación al ESPP |
| **Riesgo** | El sueldo y el patrimonio dependen de la misma empresa |

Además **cambia con el tiempo**: lo no consolidado aún no es del cliente, las opciones caducan y la venta tiene ventanas.

**Lo que ya tiene la plataforma a favor (hecho):**
- el modelo de 4 dimensiones (activo, pasivo, ingreso, gasto) está pensado para objetos así, como el ejemplo de la casa del enunciado;
- el motor proyecta **mes a mes**, lo que encaja con un calendario de vesting.

**Conclusión:** no hace falta reinventar el sistema, sino enseñarle un objeto nuevo.

### 1.3 Caso conductor: John & Jane Doe
Todas las secciones del diseño aplican sus reglas a este caso (bloques **"Con John:"**), y el prototipo usa las mismas cifras. Parte del hogar de la demo (hechos) y añade una hipótesis de stock compensation.

> **Detalle completo en `08_Caso_conductor.md`**, la única fuente de datos del ejercicio: todos los datos de entrada sección por sección del cuestionario, los supuestos de cálculo, las cifras derivadas y los resultados del motor que no recalculamos. Aquí solo va el resumen.

| | Dato | Fuente |
|---|---|---|
| **Hogar** | John (40) y Jane (38), 3 hijos, acumulando patrimonio | Demo |
| **Sueldos** | John $195K, Jane $120K | Demo |
| **Cuentas actuales** | Checking $150K · Brokerage: VTI $450K + AGG $250K · 401k John $80K · 401k Jane $60K | Demo |
| **Empleador de John** | **Acme Corp.** (ficticia, cotiza a $150) | Hipótesis |
| **Acciones de Acme ya consolidadas** | **$400K** en la cuenta del plan + **$100K** dentro de su Brokerage = **$500K** | Hipótesis |
| **RSU pendientes** | 2.000 unidades (≈ $300K), trimestrales hasta 2029 | Hipótesis |
| **Opciones / empresa privada** | No | Hipótesis |
| **Jane** | Trabaja en Bluerock Pharma (ficticia, cotiza), sin stock compensation | Hipótesis |

**Cifras derivadas** (hipotéticas):
- **Net worth:** $1.865M de la demo + $500K de Acme = **$2.365M**. Las RSU pendientes ($300K) se muestran aparte (M2).
- **Base del check de concentración:** ≈ $990K en la demo (inferencia: VTI $450K ≈ 45 %) + $500K = **≈ $1.49M**. **Acme ≈ 34 %**, VTI ≈ 30 %.
- **Por qué estas cifras:** ninguna posición de Acme es la mayor por separado ($400K y $100K frente a los $450K de VTI), así que **hoy el check no las ve**. Sumadas ($500K) sí son la mayor exposición, y además John cobra de Acme y tiene $300K pendientes.

---

## 2. El encargo: cómo lo leemos

**Decisión:** los cuatro puntos del encargo describen **el recorrido del dato dentro del producto**.

| # | Punto del encargo | Lo que responde |
|---|---|---|
| 1 | **Cómo se introduce** | Cómo **entra** la stock compensation en la plataforma: qué pregunta el cuestionario al cliente, qué completa el asesor y por qué vía (formulario, subida de extracto…) |
| 2 | **Qué tipos** | **Qué** entra (RSU, opciones, ESPP…) y qué se queda fuera, y por qué |
| 3 | **Cómo se modeliza** | Qué **hace** el sistema con el dato: cómo cambian los cálculos que **ya existen** (activo, ingreso, gasto, net worth, score) |
| 4 | **Qué análisis** | Qué conclusiones **nuevas** obtiene el asesor gracias a la stock compensation (lo principal) y dónde se presentan (lo secundario) |

**Matices acordados:**
- **Punto 1 frente a entrevistas:** el punto 1 pide el **diseño de la captura** (pantallas y preguntas), no cómo investigar el problema. Las entrevistas con asesores y clientes son trabajo del Product Manager, pero van en el **proceso** y en los **siguientes pasos**:

  | Dónde | Qué va |
  |---|---|
  | Punto 1 (la respuesta) | Diseño de la captura |
  | Proceso (vídeo y página) | Cómo llegamos: recorrido de la plataforma, hipótesis explícitas, IA para ponerlas a prueba |
  | Siguientes pasos | Plan de validación: guion de entrevista para asesor y cliente, y qué cambiaría en el diseño según las respuestas |

- **Punto 3 frente a punto 4:** el 3 ajusta los cálculos existentes; el 4 añade análisis que antes no existían.
- **"Al asesor" (punto 4):** el diagnóstico observado es la **vista del cliente**. La vista del asesor no la hemos visto, así que lo que propongamos para ella es diseño nuevo, y hay que decirlo.

---

## 3. Alcance

### 3.1 En resumen
> **Identificamos todas las acciones que el cliente tiene de su empleador, añadimos sus RSU pendientes y relacionamos esa exposición con su sueldo.**

- **Incluimos** los alcances 1 (diagnóstico correcto) y 2 (riesgo de concentración). **Dejamos fuera** el alcance 3 (impuestos y eventos). Ver apartados 3.5 y 3.6.
- **Principio de diseño:** la propuesta debe hacer el diagnóstico **más honesto, nunca más favorecedor**.
  > *"Every change must make the diagnosis more honest, never more flattering."*

### 3.2 Qué incluimos

| Elemento | Qué hace |
|---|---|
| **Acciones que ya tiene** (de cualquier origen) | Pregunta "¿dónde trabajas?", detección automática y suma en todas sus cuentas, y recordatorio de añadir la cuenta del plan de acciones |
| **RSU pendientes** (empresa cotizada) | Bloque en el cuestionario; se modelizan como ingreso futuro, con su impuesto al consolidar |
| **PSU** | Se capturan como RSU (caso límite) |
| **Ingreso** | Separar salario y RSU en Income |
| **Opciones (NSO, ISO) y empresa privada** | Solo se pregunta si existen, y el diagnóstico avisa de que no están incluidas |
| **Concentración por el empleador** | El check de concentración toma **el mayor de dos valores**: la mayor posición (como hoy) y la **exposición total al empleador**, sumando cuentas y titulares. Fórmula, umbrales y pesos, igual que hoy. El bloque "Concentrated stock risk" nombra al empleador (ver apartado 4.3) |
| **Relación con el sueldo** | **En el análisis:** escenario de estrés (acciones + sueldo + RSU pendientes) y recomendación de diversificar por etapas. **En el score:** solo el criterio relativo ("nunca puntúa mejor si es el empleador"), sin cifras (ver apartado 4.3) |

**Por qué el tipo de stock compensation casi no importa:** todos los tipos acaban convirtiéndose en acciones normales, y una vez que el cliente las tiene, lo que importa es que son de su empleador. Los tipos solo difieren mientras son derechos futuros. Detalle en el apartado 4.1.

**Hecho:** las acciones que ya tiene se pueden introducir hoy como una posición con ticker. Lo nuevo es saber que son **de su empleador** y **sumarlas**. Para el cuestionario el cambio es pequeño; el valor está en que el diagnóstico entienda lo que ya tenía delante.

### 3.3 El valor que aporta

**Para el asesor:**
1. **Un diagnóstico correcto.** Ve el patrimonio y el ingreso reales: aparecen las acciones de la empresa y las RSU pendientes, el sueldo deja de mezclar salario y RSU, y la proyección incluye los impuestos al consolidar.
2. **Ve un riesgo que hoy es invisible.** La exposición total a su empleador, sumando todas las cuentas. El check deja de mirar solo la mayor posición, que en la demo es un fondo diversificado (VTI).
3. **Distingue a John de Ana.** Sabe que las acciones y el sueldo dependen de la misma empresa, y el escenario de estrés cuantifica el golpe: acciones, sueldo y RSU pendientes a la vez (ver apartado 3.4).
4. **Llega a la conversación preparado.** Una recomendación de diversificar por etapas, con cifras y con la empresa por su nombre.
5. **Puede fiarse del diagnóstico.** Lo que no se modeliza (opciones, empresa privada) se avisa, no se oculta.

**Para Sherpas:** reutiliza piezas que ya existen (buscador de tickers, alta de cuentas, check de concentración, bloque "Concentrated stock risk", recomendación "Trim concentration… in stages"). Completa el producto en vez de añadir pantallas.

### 3.4 Qué significa "riesgo de concentración en el empleador"
- **Concentración:** demasiado patrimonio en una sola cosa. Si cae, te arrastra.
- **Exposición total a la empresa:** sumar todas las acciones de la empresa del cliente, estén donde estén (brokerage, RSU, ESPP, 401(k)…). Cada trozo parece pequeño; juntos, no.
- **Relación con el sueldo:** si la empresa va mal, el cliente sufre tres golpes a la vez: caen sus acciones, puede perder el empleo y pierde lo no consolidado.
- **En el score (hecho):** el check actual mide la **mayor posición** [HC]. En la demo salta con VTI, un fondo con miles de empresas, mientras que acciones de una sola empresa repartidas en varios sitios no se verían.
- **En el análisis (hecho):** ya existen el bloque "Concentrated stock risk" y la recomendación "Trim concentration… in stages". Los alimentamos con la empresa del cliente y añadimos un escenario de estrés.

#### Cómo se relacionan estas acciones con el sueldo

La idea de fondo es que **tu sueldo y esas acciones dependen de lo mismo: que a tu empresa le vaya bien.**

**Con un ejemplo (hipotético)**

John trabaja en Acme. Cobra **$195K al año** de sueldo y tiene **$500K en acciones de Acme**, más **$300K en RSU pendientes** (caso conductor, apartado 1.3).

**Si a Acme le va bien:** la acción sube, su patrimonio crece y su empleo está seguro. Todo va bien a la vez.

**Si a Acme le va mal**, los golpes llegan **a la vez**:
1. La acción cae y sus $500K pasan a valer, por ejemplo, $250K.
2. Acme recorta plantilla y John puede perder el empleo, y con él los $195K al año.
3. Si pierde el empleo, **pierde las RSU pendientes**, porque solo consolidan si sigue en la empresa: $300K que desaparecen.
4. Y justo cuando necesitaría sus ahorros, parte de ellos (las acciones) valen la mitad.

**La comparación que lo aclara**

| | Ana: tiene $500K en acciones de **otra** empresa | John: tiene $500K en acciones de **su** empresa |
|---|---|---|
| Si esa empresa va mal | Pierde parte de sus acciones | Pierde parte de sus acciones… |
| Su sueldo | **Sigue cobrando** | …**y puede perder el sueldo** |
| Sus RSU pendientes | No tiene | **Las pierde** |
| Para amortiguar el golpe | Tiene su sueldo | No tiene nada que lo compense |

Las dos tienen la misma cantidad invertida, pero **John arriesga mucho más**, porque sus acciones y su sueldo **caen juntos**. Es lo contrario de diversificar: diversificar es que, cuando algo cae, otra cosa te sostenga.

**Por qué importa para Sherpas**

Hoy la plataforma ve el sueldo de John (en Income) y, si las registra, sus acciones (en Investments), pero **no sabe que dependen de la misma empresa**. Por eso trataría a John y a Ana exactamente igual. La propuesta lo corrige con una sola pregunta: **"¿Dónde trabajas?"**. Con ese dato se identifican y suman sus acciones de Acme y se relacionan con su sueldo.

### 3.5 Qué dejamos fuera y por qué

| Elemento | Por qué |
|---|---|
| **Cifras del score:** cuánto penaliza el empleador, umbrales, pesos | Calibración de Sherpas, que tiene el score en beta [HC]; no conocemos sus umbrales |
| **Coste fiscal de vender** según el origen de las acciones (RSU, ESPP, ISO) | Exige saber de dónde viene cada acción y cuándo se consiguió; es planificación fiscal (alcance 3). La recomendación de diversificar avisa de ello (apartado 4.1) |
| Modelizar las **NSO** | Piden strike y caducidad, y ejercer es una decisión fiscal (planificación) |
| Modelizar las **ISO** | El motor no calcula el AMT |
| Modelizar la **empresa privada** | No tiene precio de mercado; habría que inventar una valoración |
| **ESPP en curso** (aportación) | Importes pequeños; a los pocos meses son acciones que ya detectamos |
| **Impuestos y eventos:** calendario, *withholding gap*, avisos al asesor | Pide datos detallados que el cliente no suele saber; es planificación, no diagnóstico |
| **RSA/83(b), SAR/phantom, carried interest** | Nicho |
| **NQDC/409A** | No es equity; es otra categoría |

**Fuera del cálculo, pero no del radar:** lo que puede cambiar mucho la exposición (opciones y empresa privada) no se modeliza, pero **se pregunta si existe y se avisa**. Así, dejarlo fuera no hace el diagnóstico más favorecedor. Es lo que ya hace Sherpas con los datos que faltan: no los inventa y el resultado se basa en menos información [HC].

### 3.6 Cómo llegamos a este alcance: las tres opciones consideradas

Se plantearon **tres alcances acumulativos**: cada uno incluye el anterior y añade algo nuevo. Los tres tienen captura, modelización y análisis; cambia **qué problema del asesor resuelven**.

| | Alcance 1 · Diagnóstico correcto | Alcance 2 · Riesgo de concentración | Alcance 3 · Impuestos y eventos |
|---|---|---|---|
| **Pregunta** | ¿Cuánto tiene y gana de verdad mi cliente? | ¿Cuánto depende de una sola empresa? | ¿Qué le va a pasar y cuánto le costará? |
| **Qué añade** | La stock compensation entra en **todos los cálculos que ya existen**: net worth, ingreso, impuestos, ahorro, liquidez | La **exposición total a la empresa del cliente**, cruzada con su sueldo, en el score y en el análisis | **Calendario** de consolidaciones y caducidades, **factura fiscal** de cada evento y **avisos** al asesor |
| **Valor que aporta** | El asesor ve el **patrimonio y el ingreso reales** del cliente: el diagnóstico deja de omitir o deformar la stock compensation. Es la base de datos que necesitan los alcances siguientes | El asesor **detecta el riesgo que más daño puede hacer** (perder a la vez acciones, sueldo y lo no consolidado) y tiene un argumento concreto para hablar de diversificar: cuánto, en qué empresa y por qué | El asesor **se anticipa**: sabe qué va a pasar y cuándo, evita facturas fiscales inesperadas al cliente y tiene motivos concretos para contactarle en el momento oportuno |
| **A favor** | Hoy el diagnóstico de estos clientes es incorrecto; esto lo arregla. Es lo más barato | Ataca el riesgo principal. Completa lo que ya existe. Pide pocos datos: valor, empresa, consolidado o no | Muy accionable: da al asesor motivos para llamar al cliente. El motor mes a mes encaja |
| **En contra** | El mayor riesgo sigue sin verse; no aporta una conclusión nueva | Toca más piezas | Pide datos detallados (calendarios, strikes) que el cliente quizá no sabe. Sin AMT, las ISO quedan fuera |
| **Decisión** | ✅ **Incluido** | ✅ **Incluido** | ❌ **Fuera** |

**Por qué no solo el alcance 1:**
1. **Inferencia:** el alcance 1 solo puede empeorar el diagnóstico. Si las acciones de la empresa suman al net worth y cuentan como activo líquido, mejoran Liquidity y Protection (el seguro de vida más los activos líquidos). El score **subiría** justo cuando el riesgo real es mayor.
2. No ofrece análisis nuevos, y el punto 4 del encargo los pide explícitamente.
3. En un ejercicio de selección, quedarse ahí puede parecer poco ambicioso.

**Por qué no el alcance 3:** pide datos que el cliente probablemente no sabe y choca con el motor fiscal (sin AMT). Como los alcances son acumulativos, la decisión se justifica por **coste, riesgo y cantidad de datos que hay que pedir**, no por "aporta más valor".

**Por qué no hablamos de MVP y fases:** simplifica la propuesta y el vídeo. Solo hay dos listas: lo que incluimos y lo que dejamos fuera.

### 3.7 Dónde se ve cada cosa
- **Hecho:** lo observado es la **vista del cliente**. La vista del asesor existe (la describe [HC]), pero no tenemos acceso ni con el enlace del cuestionario ni con el usuario de John Doe.
- **Idea para discutir:** el análisis de concentración iría en el diagnóstico compartido (score e Investment analysis); los avisos operativos, solo para el asesor. Lo que pongamos solo para el asesor es **diseño nuevo**.

---

## 4. Diseño funcional

Cómo responde el alcance (apartado 3) a los 4 puntos del encargo. Define **qué hace** el producto, no cómo se construye: *"Engineering decides how to build it. You decide, precisely, what it needs to do."*

En este documento se sigue el orden del encargo. El orden de presentación en Notion se decide al montar la entrega.

### 4.1 Tipos (punto 2 del encargo)

> ⚠️ Las reglas fiscales de este apartado son conocimiento general del dominio (ver 04), no de Sherpas. Hay que verificarlas antes de citarlas.

#### La idea clave: lo que ya es tuyo frente a lo que te prometen

| | **Acciones que ya tiene** | **Derechos futuros** |
|---|---|---|
| Ejemplos | RSU consolidadas, compras del ESPP, opciones ya ejercidas | RSU pendientes, opciones sin ejercer, ESPP en curso |
| ¿Son suyas? | Sí | Todavía no |
| ¿Las pierde si deja la empresa? | No | Sí, normalmente |
| ¿Tienen precio? | Sí, el de la acción | Depende: las RSU sí; las opciones dependen del strike |
| ¿Impuestos pendientes? | Solo al vender, por lo que hayan subido | Sí: al consolidar o ejercer, como sueldo |
| ¿Cada tipo funciona distinto? | **No:** son una acción con ticker | **Sí:** cada tipo tiene sus reglas |

Todos los tipos acaban convirtiéndose en **acciones normales**: las RSU al consolidar, el ESPP al comprar y las opciones al ejercer. Una vez que el cliente las tiene, lo que las hace especiales no es su origen, sino **de quién son: de su empleador**. Ese riesgo es idéntico venga de donde venga la acción.

#### ¿Hacemos bien en no distinguir el origen de las acciones que ya tiene?

**Para lo que incluimos (diagnóstico y concentración), sí.** El riesgo depende de la empresa, no de cómo se consiguió la acción: $1 de Acme procedente de una RSU cae exactamente igual que $1 de Acme comprado en bolsa.

**Donde el origen sí importa: el coste fiscal de vender.**
- **RSU consolidadas:** ya tributaron como sueldo al consolidar. Al vender solo tributa la subida desde entonces.
- **Acciones del ESPP y de ISO ejercidas:** si se venden antes de cierto plazo, parte de la ganancia tributa como sueldo, que es más caro, en lugar de como plusvalía.

Nos afecta porque **incluimos la recomendación de diversificar por etapas**, y cuánto le cuesta al cliente vender depende de ese origen.

**Decisión:**
1. **No distinguimos el origen** en la captura ni en el cálculo de la concentración.
2. La recomendación de diversificar **no calcula el coste fiscal de vender**. Solo avisa: *"El coste fiscal depende de cómo obtuviste cada acción; revísalo antes de vender."*
   - Hecho: Sherpas ya menciona los lotes con menos ganancia en su recomendación actual (empezar por los lotes con menos ganancia). ❓ No sabemos de dónde saca ese dato: el cuestionario solo pide el saldo.
3. El **coste fiscal de vender según el origen** queda fuera (apartado 3.5), porque exige saber de dónde viene cada acción y cuándo se consiguió, y eso es planificación fiscal (alcance 3).

#### Criterio para decidir qué derechos futuros modelizamos
1. **¿Aumenta la exposición a la empresa del cliente?** Es la base del alcance.
2. **¿Se puede valorar sin inventar?** Hace falta precio de mercado. Hecho: la plataforma tiene precios de mercado de acciones individuales.
3. **¿El motor actual lo modeliza sin engañar?** Hecho: calcula impuestos federal, estatal, FICA y plusvalías, mes a mes, **sin AMT**.

#### Cada tipo: qué es, cómo lo tratamos y por qué

| Tipo | Qué es | Cómo lo tratamos | Por qué |
|---|---|---|---|
| **RSU** (empresa cotizada) | Promesa de acciones gratis que consolidan según un calendario; al consolidar tributan como sueldo | **Consolidadas:** acción del empleador. **Pendientes:** ✅ se modelizan como ingreso futuro, con su impuesto al consolidar | Cumple los tres criterios. Es el tipo más común (hipótesis por validar) |
| **PSU** | RSU que dependen de objetivos de la empresa | ✅ Se capturan como RSU, con el número objetivo | Mismo tratamiento; la incertidumbre del objetivo es un caso límite |
| **ESPP** | Compra de acciones con descuento mediante aportaciones en nómina | **Compradas:** acción del empleador. **En curso:** ❌ fuera | Las aportaciones en curso son pequeñas y en pocos meses son acciones que ya detectamos |
| **NSO** | Derecho a comprar acciones a un precio fijo (strike); al ejercer, la ganancia tributa como sueldo | **Ejercidas:** acción del empleador. **Sin ejercer:** ⚠️ se pregunta si existen y se avisa | Piden strike y caducidad, y ejercer es una decisión fiscal (planificación) |
| **ISO** | Como las NSO, con ventaja fiscal, pero pueden generar AMT | **Ejercidas:** acción del empleador. **Sin ejercer:** ⚠️ se pregunta y se avisa | El motor no calcula el AMT |
| **Empresa privada** (acciones u opciones) | Equity de una empresa que no cotiza | ⚠️ Se pregunta si existe y se avisa | No tiene precio de mercado; habría que inventar una valoración |
| **RSA/83(b), SAR/phantom, carried interest** | Fórmulas para fundadores, bonus ligados a la acción, participación en fondos | ❌ Fuera | Nicho |
| **NQDC/409A** | Sueldo aplazado a futuro | ❌ Fuera | No es equity; es otra categoría |

**Fuera del cálculo, pero no del radar:** lo que puede cambiar mucho la exposición (opciones sin ejercer y empresa privada) no se modeliza, pero se pregunta si existe y se avisa. Así, dejarlo fuera no hace el diagnóstico más favorecedor.

> **Con John:** sus **$500K de Acme ya consolidados** se tratan igual vengan de RSU consolidadas o de compras: son acciones de su empleador. De sus derechos futuros, solo sus **2.000 RSU pendientes** se modelizan. No tiene opciones ni equity de empresa privada; si las tuviera, respondería "Yes" en C6 y el diagnóstico avisaría de que su exposición real es mayor.

### 4.2 Captura (punto 1 del encargo)

**Se lee junto al prototipo** (`prototipo/index.html`): cada código C1–C10 es la etiqueta ámbar de la pantalla. Las tablas siguen el orden del cuestionario.

**Principios de la captura:**
- **Reutilizar lo que existe:** pregunta sí/no que abre campos (Vehicles), filas repetibles con "+ Add…", buscador de tickers, titular por elemento, categorías de documentos y tipos de cuenta por fiscalidad.
- **Pedir solo lo que el cliente sabe:** empresa, unidades, año final y frecuencia. Nada de strikes ni calendarios exactos.
- **Quién:** el cliente, en el cuestionario. El asesor ve y edita estos campos como cualquier otro dato en *Data & Assumptions* [HC]; no es un cambio nuestro.
- **Vías:** a mano, más la categoría de documento (C1). No se especifica extracción automática: ❓ no sabemos si existe.

#### Pantalla 0 · Documentos

| Código | Qué es | Propuesta | Hoy (hecho) | Por qué |
|---|---|---|---|---|
| **C1** | Categoría de documento | *"Stock plan statements"*, con el subtítulo *"Vesting schedule or statement from your company's stock plan"*. Novena categoría | 8 categorías, ninguna de acciones | Las RSU pendientes no son una cuenta, así que no tienen el "Upload statement" de las cuentas: esta es la única vía de subir el calendario de consolidación. El asesor comprueba o completa C5 con él. Límite: ❓ si no hay extracción automática, alguien tiene que leerlo |

#### Pantalla 1 · Personal information
Sin cambios, pero **vinculada:** el co-cliente determina cuántas preguntas de empleador hay en C3 (una por persona), la columna Owner de C5 y los titulares de las cuentas (cliente, co-cliente y Joint).

#### Pantalla 3 · Income
Justo debajo del ingreso laboral, porque la stock compensation es sueldo. El resto de la sección no cambia: otros ingresos actuales, ingresos futuros y Social Security.

| Código | Qué es | Propuesta | Hoy (hecho) | Por qué |
|---|---|---|---|---|
| **C2** | Texto de ayuda del ingreso laboral | *"Gross annual, before taxes. Salary and cash bonus only — don't include company stock."* | *"Gross annual, before taxes."* | Evita que el cliente sume las RSU al salario |
| **C3** | Empleador | *"Who is your employer?"*, una por persona con ingreso laboral (patrón Owner). Buscador de empresas cotizadas (ticker, nombre y precio); si no aparece, *"Add '…' as a private company"*. O cotizada o privada, nunca las dos | No se pregunta en ningún sitio del camino observado. Solo existe "Employer contribution" en el 401k | Sin empleador no se pueden identificar sus acciones ni relacionarlas con el sueldo. Se pregunta a todos para detectar también las acciones del empleador compradas en bolsa o en el 401(k) |
| **C4** | Pregunta filtro | *"Do you get company stock through work?"* (con co-cliente: *"Do you or Jane get…"*), con la ayuda *"For example RSUs, stock options or an employee stock purchase plan (ESPP)."* Yes / No | No existe | "Through work" incluye el ESPP, que no es "cobrar en acciones". **Solo** decide si se muestran C5–C7; la detección (C9) no depende de ella. Es **una pregunta del hogar**, no por persona: con co-cliente, la pregunta es una sola para el hogar (decisión 16); el recordatorio C7 nombra solo al empleador de quien tiene RSU en C5 (decisión 20) |
| **C5** | RSU pendientes | *"RSUs not yet vested"*. Una fila por concesión: **Owner** (solo si hay co-cliente) · **Units** · **Vesting ends (year)** · **Frequency** (Monthly, Quarterly, Semi-annual, Annual) · papelera. Valor calculado al lado: *"≈ $300,000 at today's price"*. *"+ Add grant"*. Solo si el empleador cotiza | No existe | Es lo único que hoy no se puede introducir de ninguna forma. El cliente lo ve en el portal de su plan. El valor usa el precio de mercado y las consolidaciones se reparten en partes iguales. Las PSU se introducen aquí |
| **C6** | Opciones y empresa privada | **Empleador cotizado:** *"Do you also have unexercised stock options, or equity in a private company you work or worked for?"* Yes / No; con Yes: *"We'll flag these to your advisor. They're not included in the analysis yet."* **Empleador privado:** sin C5 ni pregunta; mensaje directo: *"[Employer] is a private company, so its RSUs or options can't be valued yet…"* | No existe | Fuera del cálculo, pero no del radar (apartado 3.5). La empresa privada puede ser el empleador actual o uno anterior (una startup). Un negocio propio no entra aquí: va en el chip "Business" |
| **C7** | Recordatorio (solo texto) | En Income: *"Shares you already own (vested RSUs, ESPP purchases, exercised options) go in Investments. Add your stock plan account there."* En Investments, si C4 = Yes: *"Don't forget your stock plan account at [employer]."*, con el empleador de quien tiene RSU en C5 (si nadie, todos) | No existe | Las acciones que ya tiene se registran en Investments. No puede listarlas en Income porque Income (sección 3) va antes que Investments (sección 4): el resumen de lo registrado está en C9 |

#### Pantalla 4 · Investments

| Código | Qué es | Propuesta | Hoy (hecho) | Por qué |
|---|---|---|---|---|
| **C8** | Tipo de cuenta | Nueva opción *"Stock plan account"* en el desplegable Type → Brokerage (*Taxable*). Al elegirla, la primera posición **se rellena con la acción del empleador** (C3); el cliente solo pone el saldo | Brokerage: Brokerage account · Custodial UGMA · Custodial UTMA | Da nombre a la cuenta donde suelen estar las RSU consolidadas y las compras del ESPP. El empleador no se elige en la cuenta: sale de C3 |
| **C9** | Detección automática y resumen | Las posiciones cuyo ticker es el del empleador (C3) se marcan solas con *"Your employer"* (o *"Jane's employer"*), en cualquier cuenta y con independencia de C4; el cliente puede quitar la etiqueta (✕). Al final de la lista de cuentas, un resumen: *"Acme Corp (your employer): $500,000 across 2 accounts"*, con el nombre de cada cuenta | Las posiciones muestran ticker, nombre y logo. No hay ningún total por empresa | Es lo que permite sumar por empresa aunque ninguna posición sea la mayor. El resumen enseña al cliente la cifra que usará el diagnóstico y le deja corregirla antes de enviar |
| **C10** | Aviso de coherencia | Si elige "Stock plan account" y respondió No en C4: *"You said you don't get company stock through work. Is this account from [employer]?"* → *"Yes, update my answer"* (pone C4 = Yes) / *"No, it's from a former employer"* | No existe | No bloquea: pregunta. Si es de un empleo anterior, esas acciones cuentan en la concentración como cualquier acción, sin relación con el sueldo actual |

> **Con John**, recorriendo el prototipo:
> - **Documents:** puede subir el calendario de su plan en "Stock plan statements" (C1). Es opcional.
> - **Income:** escribe **$195,000** (solo salario, C2). Empleador: John → **Acme (ACME)**, Jane → **Bluerock Pharma (BLRX)** (C3). "Do you or Jane get company stock through work?" → **Yes** (C4). Una concesión: John · **2,000** · **2029** · **Quarterly** → *"≈ $300,000 at today's price"* (C5). Opciones o empresa privada → **No** (C6). Ve el recordatorio (C7).
> - **Investments:** ve *"Don't forget your stock plan account at Acme Corp"* (C7). Añade la cuenta "Acme stock plan", tipo **Stock plan account** (C8): se rellena ACME y pone **$400,000**. En su Brokerage (VTI $450K, AGG $250K) añade **ACME $100,000**, que se marca sola como *"Your employer"* (C9). Al final: *"Acme Corp (your employer): **$500,000** across 2 accounts"* (C9). C10 no aparece porque respondió "Yes" en C4.

**Cómo funciona la lista de cuentas (existente):** cada cuenta tiene nombre, tipo, custodio (buscador), titular y saldo. Al añadirla se elige cómo rellenarla: *Add manually · Link account · Upload statement*. Con "Add manually" se añaden posiciones (buscador de valores + saldo) y, en cuentas 401k, las aportaciones del titular y de la empresa. El saldo de la cuenta es la suma de sus posiciones. ❓ No observado: el botón de borrar cuenta (supuesto en el prototipo) y el funcionamiento de "Link account" y "Upload statement".

**Pendiente de observar:** ❓ no sabemos si el ingreso laboral se pide por persona. En el cuestionario vimos una sola cifra, pero el diagnóstico de la demo separa a John ($195K) y a Jane ($120K). C3 supone que sí.

### 4.3 Modelización (punto 3 del encargo)
Qué hace el diagnóstico con los datos capturados. Siete decisiones (M1–M7), todas guiadas por el principio "más honesto, nunca más favorecedor".

#### M1 · Las cuatro dimensiones

| Elemento | Activo | Pasivo | Ingreso | Gasto |
|---|---|---|---|---|
| **Acciones del empleador ya poseídas** | Posición en su cuenta, **marcada como del empleador** | — | — (igual que hoy) | — (el impuesto al vender queda fuera, apartado 3.5) |
| **RSU pendientes** | **No** en el net worth; línea aparte (M2) | — | **Sueldo en cada consolidación:** unidades × precio de hoy (M4) | **Impuestos** de cada consolidación: federal, estatal y FICA, que el motor ya calcula |
| **Tras cada consolidación** | Pasa a acciones del empleador, neta de impuestos (M3) | — | — | — |

#### M2–M7 · Reglas

| # | Pregunta | Decisión | Por qué | Alternativa descartada |
|---|---|---|---|---|
| **M2** | ¿Las RSU pendientes suman al net worth? | **No.** Se muestran aparte (*"+ $300K unvested"*) y entran en la proyección a medida que consolidan | Todavía no son suyas y se pierden si deja la empresa. Sumarlas inflaría el patrimonio | Sumarlas enteras, o con descuento (un descuento sería una cifra inventada) |
| **M3** | ¿Qué pasa al consolidar? | Se convierten en acciones del empleador, **netas de impuestos, y el cliente las conserva** | Es lo que ocurre si el cliente no hace nada. El diagnóstico enseña hacia dónde va la concentración, y la recomendación propone cambiarlo | Suponer que las vende: daría una trayectoria diversificada que no es la real |
| **M4** | ¿A qué precio se valoran las consolidaciones futuras? | **Al de hoy, constante** | No especula con la acción. Se puede comprobar y es coherente con un modelo de un solo escenario | Aplicar la rentabilidad esperada de la renta variable: supone que la acción sube |
| **M5** | ¿Cuentan en Liquidity y Protection? | **Liquidity:** las acciones del empleador **nunca cuentan como reserva**. **Protection:** las consolidadas cuentan como cualquier otra inversión; las pendientes, nunca | El golpe que obliga a tirar de la reserva (perder el empleo) es el mismo que hunde la acción. En caso de fallecimiento, las acciones consolidadas sí valen para la familia | Tratarlas como cualquier inversión: el score subiría justo cuando más riesgo hay |
| **M6** | ¿Las RSU cuentan como ahorro? | **Neutral:** la tasa de ahorro se calcula sin RSU, ni como ingreso ni como ahorro. En Statements (Cash Flow) aparecen como entrada (*RSU vesting*) y salidas (impuestos y *retained as company stock*); la caja libre no cambia, porque no es efectivo | La tasa de ahorro mide la disciplina con el sueldo. Contarlas como ahorro la inflaría con ahorro concentrado; contarlas solo como ingreso la hundiría injustamente | Contarlas como ahorro (favorecedor) o solo como ingreso (penaliza) |
| **M7** | ¿Qué mide el check de concentración? | **El mayor de dos valores:** (a) la mayor posición, como hoy, y (b) la exposición total al empleador, sumando cuentas y titulares (si John y Jane trabajan en la misma empresa, se suma). **Solo lo consolidado:** lo pendiente va al análisis (4.4). Umbrales de Sherpas, sin cambios | Un hogar sin acciones del empleador puntúa igual que hoy (criterio 2 del score) | Medir "por empresa" para todos: cambiaría el score de hogares sin stock compensation, por ejemplo al dejar de marcar VTI |

> **Con John:**
> - **Net worth:** $2.365M, con sus $500K de Acme. Las **$300K de RSU pendientes se muestran aparte** y no suman (M2).
> - **Cada trimestre hasta 2029:** consolidan ≈ 154 RSU (≈ $23K; ≈ $92K al año). Entran como sueldo, el motor resta sus impuestos (federal, estatal y FICA) y el resto se suma a sus acciones de Acme, a $150 constante (M3, M4). La proyección muestra su exposición a Acme **creciendo cada trimestre**.
> - **Liquidity:** su reserva siguen siendo los $150K en efectivo; los $500K de Acme no cuentan (M5). **Protection:** los $500K de Acme cuentan como cualquier inversión; los $300K pendientes, no.
> - **Ahorro:** la tasa se calcula sobre los $315K de sueldos, sin RSU (M6). En Statements (Cash Flow) aparecen ≈ $92K/año de *RSU vesting*, sus impuestos y lo *retained as company stock*; la caja libre no cambia.
> - **Concentración:** el check toma el mayor entre VTI (≈ 30 %) y **Acme (≈ 34 %)**: **Acme** (M7). Hoy, sin la propuesta, el check vería VTI y no Acme, porque ninguna posición de Acme es la mayor. Además, Acme es su empleador, así que se aplica el criterio de que nunca puntúa mejor que otra empresa (ver Score).

#### Score

| Nivel | Qué cambia | Decisión |
|---|---|---|
| **0. No tocar nada** | Nada | ❌ La concentración por empresa no llegaría al score, y John seguiría puntuando como si no tuviera riesgo |
| **1. Ampliar lo que mide el check existente** | El check toma **el mayor** entre la mayor posición (como hoy) y la **exposición total al empleador**, sumando cuentas y titulares (M7). Fórmula, umbrales y pesos, igual que hoy | ✅ |
| **2. Tratar distinto al empleador** | La exposición al empleador pesa más que la misma exposición a otra empresa | ✅ Solo como **criterio**, sin cifras |

**Principio:** a igual exposición, estar concentrado en tu empleador **nunca puntúa mejor** que estarlo en otra empresa.

**Criterios de aceptación** (relativos, verificables sin conocer las cifras internas):
1. **Comparación:** dados dos hogares idénticos salvo que en A la empresa concentrada es el empleador y en B no lo es, cuando se calcula el score, la puntuación del check de concentración de A es **menor o igual** que la de B.
2. **Sin efectos colaterales:** un hogar sin acciones de su empleador obtiene **exactamente el mismo score que hoy**. Coherente con *"same data, same score"* [HC].
3. **Explicable:** cuando el empleador influye, el panel View more lo dice. Por ejemplo: *"$500K of your investments are in Acme, which also pays your salary."*

**No especificamos** cuánto baja la puntuación ni con qué umbrales. Lo decide Sherpas, que está calibrando el score en beta [HC]. Queda como pregunta abierta para ellos.

### 4.4 Análisis (punto 4 del encargo)
**Estado: definitivo** (decisiones 17 y 22). Se lee junto a la parte 2 del prototipo (`prototipo/diagnostico.html`): cada código A1–A6 es una etiqueta ámbar.

Todo va en el **diagnóstico que ya existe** (vista de cliente), en componentes que ya existen; no hay pantallas nuevas.

| # | Análisis | Dónde (existente) | Con John |
|---|---|---|---|
| **A1** | **Exposición total al empleador**, con desglose por cuenta, RSU pendientes y sueldo | Investment analysis → *What your portfolio should be doing* → bloque **"Concentrated stock risk"**, junto al de sector | *"$500K of your investments (about 34% of them) is in Acme: $400K in your stock plan and $100K in your brokerage. Another $300K in RSUs is still vesting through 2029, and John's $195K salary depends on the same company…"* |
| **A2** | **Escenario de estrés del empleador** | Investment analysis → *How each allocation behaves*, junto a los escenarios de mercado | Si Acme cae un 40 %: **−$200K** en acciones, **−$120K** en RSU pendientes y **$195K/año de sueldo en riesgo** |
| **A3** | **Trayectoria si no hace nada** | Financial health → Retirement & Goals, junto a *Projected net worth* | Acme pasa de $500K a ≈ $515K (2026), $574K, $633K y ≈ **$692K (2029)**, a $150 constante e impuestos ≈ 36 % (ilustrativo) |
| **A4** | **Diversificar por etapas** | Investment analysis → *What we're recommending*, junto a *"Trim concentration… in stages"* | *"Consider selling new shares as they vest… then reducing the $500K in stages toward the well-controlled range… The tax cost depends on how you acquired each share"* |
| **A5** | **Explicación en el score** | Panel **View more** → desglose de **Investing** y **Liquidity** | *"$500K of your investments are in Acme, which also pays your salary. That makes it riskier than the same amount in another company."* · *"Your Acme shares are not counted as reserves…"* |
| **A6** | **Cifras y avisos** | Summary (tarjeta Net worth), Assets & Investments (tarjeta Assets), Savings & Expenses, Insurance & Protection (Emergency fund), panel *Accounts & holdings*, Statements (Balance y Cash Flow) | *"$2.4M total · + $300K unvested RSUs (not included)"* · fila *"Acme · your employer $500,000"* · líneas *RSU vesting ≈ $92K*, *Taxes on RSU vesting ≈ $33K*, *Retained as company stock ≈ $59K* (la caja libre no cambia) · aviso de lo no modelizado si C6 = Yes (en el prototipo se enseña como ejemplo en una nota, porque el Caso tiene C6 = No) |

**Decisiones del análisis:**
| # | Pregunta | Decisión | Por qué |
|---|---|---|---|
| **AN1** | ¿Qué caída usa el escenario de estrés? | **40 % fijo, presentado como ilustrativo** | Modelo de un solo escenario, sin probabilidades: simple, comprobable y fácil de explicar |
| **AN2** | ¿Hasta dónde recomienda reducir? | Hasta el **"well-controlled range"** de Sherpas, sin cifra propia | Es su expresión y sus umbrales no se ven [HC] |
| **AN3** | ¿Quién lo ve? | **Todo en el diagnóstico compartido** con el cliente | La vista del asesor no la hemos visto; los avisos al asesor son del alcance 3 (fuera) |

**Reglas del prototipo** (decisión n.º 18): para qué sirven la Demo, el Caso, el cuestionario y el diagnóstico del Prototipo, y qué significa cada tipo de información y cada marca, en el apartado 0 de `08_Caso_conductor.md`.

**Queda fuera del análisis** (alcance 3): calendario de eventos, *withholding gap*, ventanas de venta y avisos operativos al asesor.

---

## 5. La entrega

### 5.1 Piezas
| Pieza | Papel |
|---|---|
| **Página de Notion** (espacio de trabajo de Alejandro) | ✅ **Centro de la entrega.** Todo se lee desde aquí y enlaza al resto |
| **Prototipo clicable** | Pieza principal: enseña la captura y el análisis con John & Jane. Es la prueba de "uso la IA para prototipar". Fichero `prototipo/index.html` (HTML local, no publicado: reproduce la interfaz de Sherpas, que es confidencial). **Parte 1, captura:** ✅ hecha: Documents, Personal information, Income e Investments conectadas, con todos los elementos observados (lo no observado se marca ❓). **Parte 2, diagnóstico:** ✅ hecha (`prototipo/diagnostico.html`): Financial health (score y panel View more, Summary, Retirement & Goals, Assets & Investments, Savings & Expenses, Insurance & Protection), Investment analysis (Summary, snapshot, recomendaciones, escenarios, panel Accounts & holdings), Statements (Balance y Cash Flow) y Reports. **Caso conductor cerrado (01/10, decisión 18):** los dos HTML leen un único fichero de datos (`prototipo/caso.js`, copia del documento 08); el cuestionario muestra sin poder modificarlas las secciones sin cambios (Personal, Goals, Expenses, Primary home, Other debt, Insurance) y añade la pantalla de envío; en modo Propuesta se sombrean las secciones con cambios; panel **Datos de entrada** en los dos; cada cifra del diagnóstico lleva su origen (↻ calculada, S1–S5 supuesto, ❓ motor, ✎ texto adaptado). |
| **Vídeo** (3–5 min, en inglés) | El recorrido: qué proponemos, por qué, qué dejamos fuera y el proceso |
| **Repositorio privado en GitHub** | **Anexo** del punto 9 (proceso): documentación seleccionada y código del prototipo (ver apartado 5.3) |
| Miro · Excel | Opcionales |

### 5.2 Esqueleto de la página de Notion
0. **Resumen:** la propuesta en 5 líneas.
1. **El problema:** síntoma frente a problema, con el caso de John & Jane.
2. **Alcance:** qué incluimos y el valor que aporta. Al final, en breve, las tres opciones consideradas y por qué elegimos esta (opciones → tradeoffs → recomendación).
3. **Diseño funcional:** los 4 puntos del encargo (tipos · captura · modelización · análisis). (Orden por decidir; idea: empezar por el análisis e ir hacia atrás.)
4. **Qué dejamos fuera y por qué.**
5. **Especificación de lo que incluimos:** criterios de aceptación, casos límite y estados (`10_Specification.md`, en inglés).
6. **Prototipo:** enlace y guía de uso (`09_Guia_del_prototipo.md`).
7. **Salida al mercado:** release notes y guía para el asesor (`11_Launch_kit.md`, en inglés).
8. **Hipótesis y plan de validación:** entrevistas con asesor y cliente.
9. **Proceso:** cómo lo hicimos y dónde usamos la IA, en media página, con enlace al repositorio.

### 5.3 Repositorios de GitHub (anexo del proceso)
- **Público** (este): documentos de proceso limpios al exportar, la propuesta en inglés y el Prototipo cifrado (decisión 27).
- **Privado:** la copia de trabajo completa, con el inventario de la plataforma y el código del Prototipo.

---

## 6. Trabajo pendiente

### 6.1 Decisiones de modelización (punto 3 del encargo)
✅ Resuelto en el apartado 4.3 (M1–M7, decisión n.º 15). Los umbrales de concentración son los de Sherpas, sin cambios.

### 6.2 Detalle de la captura (punto 1 del encargo)
✅ Resuelto en el apartado 4.2 (decisión n.º 14).

### 6.3 Casos límite (para la especificación)
- **El co-cliente:** Jane también puede tener acciones de su empresa, **o trabajar en la misma empresa que John**, con doble concentración.
- **Ex-empleado o jubilado** que conserva acciones de su antigua empresa: hay concentración, pero ya no hay sueldo. Parcialmente cubierto: C6 pregunta por equity de una empresa privada anterior y C10 permite marcar una cuenta del plan como de un empleo anterior. Falta el ex-empleado de una empresa cotizada sin cuenta del plan: sus acciones cuentan como cualquier acción.
- Acciones de la empresa dentro del 401(k) como **fondo sin ticker** (*"company stock fund"*): la detección automática no las encontraría.

### 6.4 Hallazgos fuera de alcance que vale la pena mencionar
- **Doble concentración en la pareja:** si John y Jane trabajan en la misma empresa, M7 suma su exposición, pero la relación con dos sueldos a la vez se trata en el análisis (4.4).

---

## 7. Decisiones

| # | Fecha | Decisión | Motivo |
|---|---|---|---|
| 1 | 29/09/2026 | Leer los 4 puntos del encargo como el recorrido del dato en el producto (ver apartado 2) | Construcción gramatical paralela de los puntos; se nos dio el cuestionario para explorarlo; la oferta pide opciones y recomendación, *"not a question about requirements"* |
| 2 | 29/09/2026 | ~~Enfoque B como hilo conductor, con A y C descartados~~ **Sustituida por la 3** | A y C eran opciones de relleno, no alternativas serias |
| 3 | 29/09/2026 | Presentar la solución como **tres alcances acumulativos** (diagnóstico correcto → concentración → impuestos y eventos). El alcance final se fija en la decisión 8 (ver apartado 3.6) | Los tres aportan valor y cada uno suma al anterior |
| 4 | 29/09/2026 | Esqueleto de la entrega (ver apartado 5) | Cubre el enunciado (4 puntos, qué se deja fuera, proceso) y la oferta (opciones, especificación, prototipo, release notes y enablement) |
| 5 | 29/09/2026 | ~~**MVP** = alcance 1 + señal mínima de concentración · **Fase 2** = resto del alcance 2 · **Después / fuera** = alcance 3~~ **Sustituida por la 8** | Hablar de MVP y fases complicaba la propuesta y el vídeo |
| 6 | 29/09/2026 | **Página de Notion como centro** de la entrega, con el prototipo como pieza principal (ver apartado 5.1) | Sherpas la ofreció para eso y el enunciado está en Notion; el prototipo demuestra el uso de la IA para prototipar |
| 7 | 29/09/2026 | **Repositorio privado de GitHub** como anexo del proceso, con documentación seleccionada y el código del prototipo (ver apartado 5.3) | Enseña el proceso y el uso de la IA sin romper la confidencialidad; los evaluadores son de producto, así que el repositorio no es el centro |
| 8 | 30/09/2026 | **Alcance:** incluimos los alcances 1 (diagnóstico correcto) y 2 (riesgo de concentración, incluida la relación con el sueldo); dejamos fuera el alcance 3 (impuestos y eventos). Sin MVP ni fases: solo "incluimos" y "dejamos fuera" (ver apartados 3.2 y 3.5) | Simplifica la propuesta y el vídeo; la relación con el sueldo es la tesis y permite distinguir a John de Ana; el alcance 3 exige datos que el cliente no suele saber y el motor no calcula el AMT |
| 9 | 30/09/2026 | **Tipos:** las acciones que ya tiene entran siempre, vengan de donde vengan; de los derechos futuros solo se modelizan las **RSU pendientes** (PSU como RSU); de opciones y empresa privada solo se pregunta si existen y se avisa. **Score:** el check mide la mayor exposición a una empresa, y el empleador nunca puntúa mejor, sin fijar cifras (ver apartados 3.2 y 4.3) | Una vez que son acciones, el tipo no importa; avisar de lo no modelizado evita un diagnóstico más favorecedor; la calibración del score es de Sherpas (beta) |
| 10 | 30/09/2026 | Crear la sección **Diseño funcional** (apartado 4), organizada por los 4 puntos del encargo, con el detalle del score dentro de la modelización | Separar qué hacemos (alcance) de cómo funciona (diseño); "diseño funcional" en lugar de "implementación", porque el cómo técnico es de ingeniería |
| 11 | 30/09/2026 | Esqueleto de Notion: punto 2 **Alcance** (con las tres opciones consideradas como bloque breve al final), punto 3 **Diseño funcional**, punto 4 **Qué dejamos fuera y por qué** (ver apartado 5.2) | Alinea Notion con el documento de trabajo; mantiene las opciones que pide la oferta sin que sean el título |
| 12 | 30/09/2026 | **No distinguir el origen** de las acciones que ya tiene; la recomendación de diversificar avisa del coste fiscal sin calcularlo, y ese cálculo queda fuera (ver apartado 4.1) | Para el riesgo de concentración el origen no importa; el coste fiscal de vender sí depende de él, pero es planificación fiscal |
| 13 | 30/09/2026 | La maqueta de la captura es la **parte 1 del prototipo** (`prototipo/index.html`), con los modos Hoy / Propuesta y Notas; la parte 2 (diagnóstico) se añadirá en el mismo fichero (ver apartado 5.1) | Visualizar la captura ayudó a decidir; reutilizarla ahorra trabajo del jueves y enseña el proceso con IA |
| 14 | 30/09/2026 | **Captura** (C1–C10, apartado 4.2): en Income, empleador (cotizada o privada) + pregunta filtro que incluye el ESPP + RSU por concesión + existencia de opciones y empresa privada + recordatorio; en Investments, tipo "Stock plan account", detección automática independiente de C4 y aviso de coherencia; nueva categoría de documento. El asesor edita como cualquier otro dato | Reutiliza patrones existentes; pide solo lo que el cliente sabe; C4 no puede ocultar acciones del empleador ya registradas |
| 15 | 30/09/2026 | **Modelización** (M1–M7, apartado 4.3): RSU pendientes fuera del net worth y en la proyección a medida que consolidan; al consolidar se conservan como acciones del empleador, netas de impuestos, a precio de hoy constante; acciones del empleador nunca como reserva de liquidez; tasa de ahorro neutral; check de concentración = mayor entre la mayor posición y la exposición total al empleador. **Corrige la decisión 9**, que decía "en lugar de la mayor posición" | Más honesto, nunca más favorecedor; sin efectos colaterales en hogares sin stock compensation |
| 16 | 30/09/2026 | C4 sigue siendo **una pregunta del hogar**, no por persona | Lo más simple; el efecto (el recordatorio nombra a todos los empleadores) es inofensivo |
| 17 | 30/09/2026 | **Análisis** (A1–A6 y AN1–AN3, apartado 4.4), **aceptado provisionalmente** tras verlo en la parte 2 del prototipo | Aprovecha componentes existentes del diagnóstico; 40 % ilustrativo; sin cifras propias de concentración; todo visible para el cliente |
| 18 | 01/10/2026 | **El Caso como única fuente de datos** (`08_Caso_conductor.md`): la Demo es solo la referencia inicial. El cuestionario del Prototipo arranca con el Caso; solo se pueden editar las secciones con cambios (Documents, Income e Investments) y el resto (Personal, Goals, Expenses, Primary home, Other debt e Insurance) se muestra sin poder modificarse; en modo Propuesta se sombrean las secciones con cambios. El diagnóstico es la consecuencia del Caso y no se recalcula si se cambia el cuestionario (se avisa en los dos). Un panel **"Datos de entrada"** fuera de la interfaz (como Notas) resume en lenguaje llano el hogar, la hipótesis, los supuestos y el resultado; el origen de cada dato queda en el 08. Cada cifra lleva su origen: calculada (↻), ilustrativa (supuesto) o resultado del motor con el valor de la Demo (❓), y cada ❓ deja una pregunta para Sherpas. Vocabulario fijo: Plataforma, Demo, Prototipo, Caso | Un solo mundo coherente y explicable; los resultados del motor no se pueden recalcular sin inventarlos; convierte nuestras limitaciones en preguntas para la sesión |
| 19 | 01/10/2026 | **Guía de uso del Prototipo** en un documento propio (`09_Guia_del_prototipo.md`), en español de momento: qué es, recorrido de 5 pasos, botones, cómo leer lo que se ve y qué no hace. Va a Notion junto al enlace del Prototipo y el README remite a ella | Otro lector (quien evalúa) y otro propósito que el 08; una sola fuente para Notion y el repositorio |
| 20 | 01/10/2026 | El recordatorio **C7** en Investments nombra solo al empleador de quien tiene RSU en C5 (si nadie, a todos). **Matiza la 16**: C4 sigue siendo una pregunta del hogar | En el Caso, Jane no tiene stock compensation y el recordatorio le pedía una cuenta del plan en Bluerock |
| 21 | 01/10/2026 | Subagente **Validador** (modelo Fable 5.1, solo lectura) para auditorías independientes a petición; recibe solo el encargo, y su informe se revisa con espíritu crítico antes de aplicarlo. Primera auditoría de coherencia: 12 de 13 hallazgos aplicados (el 11, añadir S5 al panel, se descarta para mantenerlo simple) | Una segunda mirada sin nuestro contexto encuentra lo que se nos escapa (encontró un error de cálculo introducido en la corrección anterior) |
| 22 | 01/10/2026 | **Especificación en inglés** (`10_Specification.md`): alcance, 44 criterios de aceptación *Given/When/Then* (C1–C10, M1–M7, score, A1–A6), estados, casos límite y preguntas para Sherpas; el Caso solo como ejemplo verificable, con un recuadro inicial. La **4.4 pasa a definitiva** | La oferta pide *"a structured proposal and a spec"*; en inglés va directa a Notion y al vídeo; los documentos de trabajo siguen en español |
| 23 | 01/10/2026 | Segunda auditoría del Validador (especificación frente al 07 y al Prototipo): 19 hallazgos, todos aplicados. En el **Prototipo**: una cuenta de un empleo anterior (C10) deja de contar como exposición al empleador; cambiar el empleador ya no reasigna las RSU a la otra persona (quedan sin valorar si pasa a ser privado); rótulo *"employer of both"*; texto de A5 *"That makes it riskier…"*, coherente con "nunca puntúa mejor". En la **especificación**: AC-C3-4, AC-A6-2 (con C4 = Yes), nuevo AC-M4-2 (reparto de las consolidaciones como supuesto) y pregunta 7, M6 precisado, base de M7 marcada como inferida, alcance completado e inglés de EE. UU. Total: 45 criterios | Mantener especificación y Prototipo diciendo lo mismo |
| 24 | 01/10/2026 | Se aceptan los comportamientos que fijó la especificación sin estar en el 07: empleador opcional; concesión que termina este año (un solo punto en A3); concesión con 0 unidades (≈ $0, ignorada); cambio de empleador (revalorar o "not valued"); dos sueldos en A2 si comparten empresa; documento de C1 visible para el asesor y sin extracción; sin fila de RSU con empleador privado; C10 también sin empleador | Cierran casos que el diseño no resolvía, coherentes con "más honesto, nunca más favorecedor" |
| 25 | 01/10/2026 | **Launch kit** en un solo documento en inglés (`11_Launch_kit.md`): release notes (qué hay de nuevo y qué no incluye) y guía para el asesor (cuándo aparece, cómo leer A1–A6, tres mensajes para el cliente con el ejemplo de John y cinco preguntas frecuentes, que también sirven al equipo de atención al cliente) | La oferta pide *release notes* y *enablement* tres veces; breve, porque el peso de la entrega es la especificación |
| 26 | 01/10/2026 | **Página de Notion publicada** en inglés en el espacio de Alejandro: *Stock compensation in Sherpas*, con las secciones 0–9 (diseño funcional de análisis a tipos) y tres subpáginas (Specification, Prototype con la guía y el Caso, Launch kit). Cabecera con autor y fecha. Fuente: documentos 10–13 | Centro de la entrega (decisión 6); en inglés, como el vídeo |
| 27 | 01/10/2026 | **Repositorio público** aparte (`stock-compensation-exercise`), con historial limpio, para que quien evalúa acceda sin invitaciones: documentos limpios al exportar (sin referencias al inventario interno, sin resultados del motor de la Demo, sin citas literales ni defectos de la plataforma), el Prototipo **cifrado** (contraseña en Notion) y sin su código fuente. El privado sigue igual. **Matiza la 7** | Pedir usuarios de GitHub añadía fricción y riesgo de que no accedieran; el cifrado evita publicar en claro lo que Sherpas pidió mantener confidencial |
| 28 | 01/10/2026 | **Navegación en Notion:** favorita para Alejandro; índice y accesos rápidos arriba; enlaces *"See it in the prototype"* a cada código (A1–A6, C1–C10) y a cada paso del recorrido; enlaces al repositorio público (cómo trabajamos con IA, auditorías, decisiones y Caso, avisando del idioma). La contraseña se muestra junto a cada grupo de enlaces y el Prototipo la recuerda en el navegador. Estos enlaces no se copian a los ficheros 12 y 13, para no publicar la contraseña ni los enlaces de Notion en el repositorio | Quien lee una descripción puede verla en el Prototipo con un clic; un invitado no ve el árbol de páginas en la barra lateral |
