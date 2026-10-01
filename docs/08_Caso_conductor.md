# Caso conductor: John & Jane Doe

> **Qué es este documento:** los datos de entrada del Prototipo, completos y en un solo sitio. Es la **única fuente**: el cuestionario del Prototipo arranca con estos datos y el diagnóstico del Prototipo es su consecuencia.
> **Si cambias un dato en el cuestionario del Prototipo, el diagnóstico no cambia:** muestra siempre el resultado de este caso.
> Los datos de la plataforma proceden de un inventario interno de lo observado, que no se publica (confidencial). [HC] = artículo del Help Center sobre el score, incluido en el enunciado del ejercicio. M1–M7, C1–C10 y A1–A6 remiten a `07_Trabajo_en_curso.md`.

---

## 0. Reglas: Demo, Caso y Prototipo

### 0.1 Vocabulario
| Término | Qué es |
|---|---|
| **Plataforma** | Sherpas, la aplicación real |
| **Demo** | El diagnóstico real de John & Jane en la Plataforma |
| **Caso** | Este documento: los datos de entrada del ejercicio |
| **Prototipo** | Nuestros dos HTML: el cuestionario (`prototipo/index.html`) y el diagnóstico (`prototipo/diagnostico.html`) |

### 0.2 Para qué sirve cada pieza
| Pieza | Regla |
|---|---|
| **Demo** | Solo es la **referencia inicial**: de ella salen el hogar de John & Jane, los textos y los resultados del motor que no sabemos recalcular. No se muestra como tal en ningún sitio |
| **Caso** | Es la **única fuente de datos** del ejercicio. `prototipo/caso.js` es su copia exacta: si cambia un dato, se cambia en los dos a la vez |
| **Cuestionario del Prototipo** | **Arranca con los datos del Caso.** Solo se pueden editar las secciones con cambios de la propuesta (Documents, Income e Investments); el resto se muestra sin poder modificarse. Lo que se cambie no llega al diagnóstico |
| **Diagnóstico del Prototipo** | Es la **consecuencia del Caso** y no se recalcula. No tiene controles que cambien datos: lo que no forma parte del Caso (por ejemplo, C6 = Yes) solo aparece como ejemplo en una nota |

### 0.3 Tipos de información

**En los datos de entrada** (este documento), cada dato lleva su origen:

| Etiqueta | Significado |
|---|---|
| **Demo** | Se toma tal cual de la Demo |
| **Deducido** | Se calcula a partir de cifras de la Demo; se indica cómo |
| **Completado** | La Demo no lo muestra y el cuestionario lo necesita. Lo elegimos nosotros y **no influye** en el diagnóstico |
| **Hipótesis** | El escenario de stock compensation que añadimos (Acme, las RSU, el empleador de Jane) |
| **Supuesto** | Parámetro de cálculo nuestro, ilustrativo (apartado 2) |
| ❓ | Desconocido: no lo muestra la Demo ni se observó en la Plataforma |

**En las pantallas del Prototipo:**

| Qué se ve | Significado |
|---|---|
| Fondo ámbar con borde discontinuo y código (C1–C10, A1–A6) | **Lo nuevo** de la propuesta |
| Pestaña en ámbar (cuestionario, modo Propuesta) | Sección con cambios |
| Texto ámbar con línea discontinua | **Nota** que explica la propuesta. Se oculta con el botón Notas |
| Texto gris pequeño | Lo **existente** en la Plataforma y lo que no pudimos observar (❓) |
| Panel **Datos de entrada** | Resumen del Caso en lenguaje llano |

**Junto a cada cifra del diagnóstico**, su origen:

| Marca | Significado |
|---|---|
| ↻ | **Calculada** por nosotros sobre el Caso (aritmética, no la produce el motor) |
| S1–S4 | Depende de un **supuesto** (apartado 2) |
| ❓ | **Resultado del motor** de Sherpas, que no conocemos: se muestra el valor de la Demo, sin recalcular (apartado 4) |
| ✎ | **Texto de la Demo** con las cifras que el Caso contradice ya cambiadas (apartado 4) |

Las marcas y las notas se ocultan con el botón Notas; el modo **Hoy** muestra la Plataforma actual, sin lo nuevo. Al pasar el ratón por un icono (↻, S, ❓, ✎, "NUEVO") o por un botón de la barra (Datos de entrada, Hoy, Propuesta, Notas) aparece una definición breve.

**Fecha de referencia del Caso:** 20 de septiembre de 2026, la fecha del diagnóstico de la Demo, que el Prototipo conserva. La primera consolidación de las RSU es en diciembre de 2026 (S2).

---

## 1. Datos de entrada, sección por sección del cuestionario

Las secciones 0, 3 y 4 llevan cambios de la propuesta (C1–C10). El resto se reproduce sin cambios y en el Prototipo no se puede modificar.

### Sección 0 · Documentos (con cambios)
| Dato | Valor | Origen |
|---|---|---|
| Documentos subidos | Ninguno. "Stock plan statements" (C1) es opcional | Completado |

### Sección 1 · Personal information
| Dato | Valor | Origen |
|---|---|---|
| Cliente | John Doe | Demo |
| Co-cliente | Jane Doe | Demo |
| Fecha de nacimiento de John | 05/04/1986 (40 años) | Año deducido: "John (40)" y jubilación a los 60 en 2046. Día y mes: completado |
| Fecha de nacimiento de Jane | 1988 (38 años) | Deducido: "Jane (38)" y jubilación a los 58 en 2046. ❓ No sabemos si el cuestionario la pide (solo se vio una fecha, sin co-cliente) |
| Dependientes | 3: Ava (9), Liam (6), Chad (3) | Nombres: Demo (marcadores de la gráfica). Edades deducidas: la universidad empieza cuando John tiene 49, 52 y 55 años, y entran a los 18 (supuesto S5) |
| Código postal | 94110 | Completado (es el ejemplo del propio campo). ❓ La Demo no lo muestra |

### Sección 2 · Goals
| Dato | Valor | Origen |
|---|---|---|
| Edad de jubilación | John 60 · Jane 58 (2046) | Demo |
| Universidad por hijo | $60,000 | Demo |
| Universidad: años | Ava 2035–2038 · Liam 2038–2041 · Chad 2041–2044 | Inicio deducido (marcadores); 4 años de duración: supuesto S5 |
| Comprar una casa | $800,000 en 2030 | Demo |
| Comprar un vehículo | $40,000 en 2028 | Demo |
| Vacaciones | $8,000 al año, desde 2027 | Importe: Demo. Inicio deducido: marcador a los 41 años de John |

### Sección 3 · Income (con cambios)
| Dato | Valor | Origen |
|---|---|---|
| Ingreso laboral bruto (solo salario, C2) | John $195,000 · Jane $120,000 | Demo. ❓ No sabemos si el cuestionario lo pide por persona |
| Empleador (C3) | John: **Acme Corp.** (ACME, cotiza a $150) · Jane: **Bluerock Pharma** (BLRX) | Hipótesis (empresas ficticias) |
| ¿Recibís acciones por el trabajo? (C4) | Yes | Hipótesis |
| RSU pendientes (C5) | John · **2,000** unidades · hasta **2029** · **Quarterly** → ≈ $300,000 a precio de hoy | Hipótesis |
| Opciones o empresa privada (C6) | No | Hipótesis |
| Otros ingresos actuales | Rental property: $24,000 al año (Joint) | Demo. ❓ No se vieron los campos de este chip |
| Ingresos futuros | Social Security, John y Jane, desde los 67, importe calculado automáticamente | Demo (textos de Retirement & Goals) |
| | Annuity | Demo (un texto menciona *"the annuity stream"*). ❓ Importe y titular desconocidos: el chip se marca sin importe |

### Sección 4 · Investments (con cambios)
| Cuenta | Tipo | Custodio | Titular | Posiciones | Origen |
|---|---|---|---|---|---|
| Checking | Checking account | Fidelity Investments | John | Cash $150,000 | Demo |
| Brokerage | Brokerage account | Vanguard | Joint | VTI $450,000 · AGG $250,000 | Demo |
| | | | | **ACME $100,000** (C9: "Your employer") | Hipótesis |
| 401k - John | 401k - Traditional | Fidelity Investments | John | SWYNX $80,000 | Demo. Tipo deducido de "401k - Traditional Savings" |
| 401k - Jane | 401k - Traditional | Fidelity Investments | **Jane** | SWYJX $60,000 | Demo. El Caso usa Jane como titular |
| **Acme stock plan** | **Stock plan account** (C8) | — | John | **ACME $400,000** | Hipótesis |

| Dato | Valor | Origen |
|---|---|---|
| Aportaciones al 401(k) | $22,000 al año en total | Demo. ❓ Reparto entre John y Jane y aportación de la empresa: desconocidos. En el Prototipo, campos vacíos |
| Resumen por empresa (C9) | "Acme Corp (your employer): $500,000 across 2 accounts" | Calculado de lo anterior |
| Nivel de riesgo | Moderate (2/4) | Deducido: *"your stated moderate risk posture"* |

### Sección 5 · Expenses
| Dato | Valor | Origen |
|---|---|---|
| Gastos esenciales | $6,000 al mes | Deducido: Lifestyle Exp. $72K al año ÷ 12 |

### Sección 6 · Primary home & personal property
| Dato | Valor | Origen |
|---|---|---|
| Vivienda habitual | Own · valor $600,000 · hipoteca $125,000 | Demo. ❓ No se vieron los campos de "Own" |
| Gastos de vivienda | $47,850 al año (≈ $48K): hipoteca $24,000 ($2,000 al mes) · HOA $9,600 · impuestos de la vivienda $9,500 · seguro $4,750 | Demo (Statements, Cash Flow) |
| Inmueble en alquiler | $350,000 | Demo. ❓ No sabemos en qué pregunta se introduce |
| Vehículos | Yes · Tesla $50,000 con préstamo de $20,000 al 7 %, cuota $450 al mes · Ford $43,000 sin préstamo | Valores y tipo: Demo. Cuota deducida: *Vehicle loans* $5,400 al año ÷ 12 |
| Bienes de alto valor | Yes · Jewelry $20,000 | Demo |

### Sección 7 · Other debt
| Dato | Valor | Origen |
|---|---|---|
| Tarjeta con saldo | Yes · Chase CC $25,000 al 18 %, cuota $500 al mes | Saldo: Demo. Tipo: Demo (desglose de Debt). Cuota deducida: *Credit cards* $6,000 al año ÷ 12 |
| Préstamo de estudios | Yes · Berkeley $18,000, cuota $500 al mes | Saldo: Demo. Cuota deducida: *Student loans* $6,000 al año ÷ 12 |
| Otros préstamos | No (el préstamo del Tesla va con el vehículo) | Completado. ❓ La Demo lo clasifica como "Personal loan" |
| Cuota mensual total | $3,450 = hipoteca $2,000 + tarjeta $500 + estudios $500 + vehículo $450 | Demo. La suma de las cuotas deducidas coincide |

### Sección 8 · Insurance
| Dato | Valor | Origen |
|---|---|---|
| Seguro de vida | Yes · John $250,000 · Jane ninguno | Demo |
| Umbrella | No | Demo |
| Otros seguros (coche, incapacidad) | Sin marcar | Completado. ❓ La Demo no los muestra |

---

## 2. Supuestos de cálculo

| # | Supuesto | Valor | Por qué |
|---|---|---|---|
| **S1** | Precio de Acme | **$150, constante** | Decisión M4: no especular con la acción |
| **S2** | Calendario de las RSU | **13 consolidaciones trimestrales**, de diciembre de 2026 a diciembre de 2029: 12 de 154 unidades y 1 de 152 (≈ $23,100 cada una; ≈ $92,000 al año) | El cliente solo da unidades, año final y frecuencia (C5); se reparten en partes iguales |
| **S3** | Impuestos al consolidar | **≈ 36 %**: federal 24 % + estatal 9,3 % + Medicare 2,35 % | Solo para ilustrar: en el producto lo calcularía el motor. ⚠️ Tipos por verificar antes de citarlos |
| **S4** | Caída en el escenario de estrés | **40 %** | Decisión AN1 |
| **S5** | Universidad | Empieza a los 18 años y dura 4 | Para deducir las edades de los hijos y los años de cada objetivo |

---

## 3. Cifras derivadas (aritmética sobre el Caso)

En el Prototipo llevan la marca ↻: no las produce el motor de la Plataforma, sino nuestro cálculo.

| Cifra | Valor | Cálculo | Dónde aparece |
|---|---|---|---|
| Activos totales | **$2,553,000** | $2,053,000 de la Demo + $500,000 de Acme | Assets & Investments (tarjeta Assets) · Statements (Balance) |
| Net worth | **$2,365,000** | $2,553,000 − $188,000 de deudas | Summary (tarjeta Net worth) · Statements |
| Activos invertibles (sin efectivo) | **$1,340,000** | $840,000 de la Demo + $500,000 | Summary (tarjeta Net worth) |
| Total invertido (con efectivo) | **$1,490,000** | $990,000 de la Demo + $500,000 | Investment snapshot · base de los porcentajes |
| Cuentas *Taxable* | **$1,200,000** | Brokerage $800,000 + Acme stock plan $400,000 | Investment snapshot · Statements |
| Exposición a Acme | **$500,000** | $400,000 + $100,000 | C9 · A1 · A4 · A5 · A6 |
| Peso de Acme | **34 %** | $500,000 / $1,490,000 = 33,6 %. Base: el total invertido con efectivo, la misma que usa el check de la Demo (VTI 45 % = $450K / $990K). En los textos nuevos se dice "of your investments" para no confundirla con los "investable assets" de la tarjeta, que excluyen el efectivo | A1 · A4 · A5 |
| Peso de VTI | **30 %** | $450,000 / $1,490,000 = 30,2 % | Textos adaptados de la Demo |
| Check de concentración | **Acme, 34 %** | El mayor entre VTI (30 %) y Acme (34 %) (M7). Sin la propuesta, el check vería VTI (30 %): ninguna posición de Acme es la mayor por separado | A5 |
| RSU pendientes | **$300,000** | 2,000 × $150 | Summary · Assets · Balance · A1 |
| RSU que consolidan al año | **$92,400** | 4 × 154 × $150 (S2) | A3 · Savings & Expenses · Cash Flow |
| Impuestos de las RSU | **$33,264 al año** | 36 % × $92,400 (S3) | Savings & Expenses · Cash Flow |
| Retenido como acciones | **$59,136 al año** | $92,400 − $33,264 | Cash Flow · A3 |
| Trayectoria de Acme si no hace nada | **≈ $515K (2026) · $574K · $633K · $692K (2029)** | $500,000 + lo retenido de cada consolidación, a $150 (S1–S3) | A3 |
| Entradas con RSU | **$431,400** | $339,000 de la Demo + $92,400 | Cash Flow |
| Estrés: acciones de Acme | **−$200,000** ($500K → $300K, el **23 %** de lo invertido tras la caída) | 40 % × $500,000; $300,000 / $1,290,000 (S4) | A2 |
| Estrés: RSU pendientes | **−$120,000** ($300K → $180K) | 40 % × $300,000 | A2 |
| Estrés: sueldo en riesgo | **$195,000 al año** | Sueldo de John | A2 |
| Reserva de liquidez | **$150,000** (sin cambios) | Las acciones de Acme no cuentan como reserva (M5) | Insurance & Protection (Emergency fund) |

---

## 4. Lo que no recalculamos: resultados del motor

Estas cifras las produce el motor de la Plataforma, que no conocemos. En el Prototipo se mantienen los **valores de la Demo, marcados con ❓**: son la respuesta del motor a un hogar sin Acme, no al Caso. Cada una deja una pregunta para Sherpas.

| Resultado del motor | Cómo cambiaría con el Caso | Pregunta para Sherpas |
|---|---|---|
| **Score** y puntos de cada área | Investing: el check pasa de VTI a Acme, con el criterio del empleador; la puntuación depende de umbrales que no vemos | ¿Qué umbrales usa el check de concentración y cómo encaja el criterio "el empleador nunca puntúa mejor"? |
| **Protection:** cobertura del seguro de vida más activos líquidos frente a la necesidad | Los $500K de Acme cuentan como inversión (M5), así que la cobertura subiría | ¿Qué activos cuentan como *liquid assets* en Protection? |
| **Proyección de net worth** (a la jubilación, al final del plan, año en que se agota) | Más patrimonio y RSU que consolidan: la curva subiría | ¿Puede el motor modelizar un ingreso que no es efectivo y se convierte en activo (las RSU)? |
| **Déficit de jubilación** | Bajaría | Igual que la anterior |
| **Impuestos** del hogar | Añadimos ≈ $33K de las RSU con un tipo ilustrativo (S3) | ¿Calcula el motor fiscal la renta de una consolidación dentro de su modelo (federal, estatal y FICA)? |
| **Investment analysis:** asignación, rentabilidad, volatilidad, escenarios, exposición por sector | Cambiaría con la posición de Acme | ¿De dónde sale la exposición por sector? |
| **Textos narrativos** | — | ¿Cómo se generan? |

*En la versión pública se omiten los valores que el motor dio para el hogar de la Demo.*

**Regla para los textos de la Demo:** se mantienen literales, salvo las cifras que el Caso contradice directamente: total invertido, número de cuentas, importe en cuentas *Taxable*, net worth, peso de VTI y las cifras en dólares de los escenarios. Esas cifras se recalculan con el Caso y el texto se marca como **adaptado** (✎); el resto del razonamiento no se toca.
