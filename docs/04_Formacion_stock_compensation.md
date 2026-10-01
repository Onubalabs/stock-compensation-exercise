# Formación: stock compensation (EE. UU.)

Lo justo para diseñar la propuesta y defenderla en la entrevista. Los términos van en inglés porque así los usarás en el vídeo.

> **⚠️ Avisos antes de leer**
> 1. **Fuentes:** este documento resume el conocimiento general de las reglas de EE. UU. sobre compensación en acciones. **No procede de Sherpas** ni de su plataforma o documentación.
> 2. **Verificar las cifras antes de citarlas:** retención del 22 %/37 % en RSU, descuento del ESPP de hasta el 15 %, límite de 25.000 $/año del ESPP, límite de 100.000 $ de las ISO y regla de 2 años + 1 año de las ISO. Son estándar, pero antes de usarlas en el vídeo o la entrevista conviene contrastar las que se citen con una fuente oficial (IRS) o especializada.
> 3. **No es un entregable:** es material de estudio. Parte de su contenido (qué tipos entran y cómo se modelizan) se convertirá en decisiones de la propuesta. La tabla final, con las celdas ❓, es un borrador para discutir.

---

## La idea en una frase
Parte del sueldo se paga en **acciones de la propia empresa** (o en derechos para conseguirlas). Para el cliente es a la vez **ingreso, activo, factura fiscal y riesgo**, y de ahí la dificultad.

## Vocabulario base

| Término | Qué es | Ejemplo |
|---|---|---|
| **Grant** | La concesión: "te damos X acciones/opciones" | 4.000 RSUs concedidas el 01/03/2025 |
| **Vesting** | Cuándo pasan a ser tuyas de verdad | 25 % al año, durante 4 años |
| **Cliff** | Periodo inicial sin nada; si te vas antes, lo pierdes todo | 1 año de cliff; luego trimestral |
| **Vested / Unvested** | Ya consolidado (tuyo) / pendiente (condicionado a seguir en la empresa) | |
| **FMV** (Fair Market Value) | Precio de mercado de la acción hoy | 150 $ |
| **Strike / Exercise price** | Precio al que una opción te deja comprar | 40 $ |
| **Spread / Intrinsic value** | FMV − strike (lo que "vale" la opción hoy) | 150 − 40 = 110 $ |
| **Exercise** | Ejecutar la opción: pagar el strike y recibir las acciones | |
| **Expiration** | Fecha en que caduca la opción (normalmente 10 años, o unos 90 días tras dejar la empresa) | |
| **Concentration** | Demasiado patrimonio en una sola acción | Regla habitual: más del 10–15 % del patrimonio en un solo valor ya es "concentrado" |

## Los tipos que importan

### 1. RSU (Restricted Stock Units): el más común
- **Qué es:** promesa de darte acciones cuando consoliden. No pagas nada.
- **Dónde:** casi todas las grandes cotizadas (Big Tech, farma, banca).
- **Fiscalidad:** al consolidar, el valor de mercado **tributa como salario**. La empresa retiene un **22 %** federal (37 % por encima de 1 M$ al año).
- **La trampa:** un cliente con ingresos altos tributa al 32–37 %, pero solo le retuvieron el 22 %. En abril le llega una **factura fiscal inesperada**. Es un análisis muy valioso y fácil de calcular (*withholding gap*).
- **Tras consolidar:** son acciones normales, que muchos no venden. Así se acumula la concentración.
- **Empresas privadas:** suelen ser *double-trigger*, es decir, solo consolidan si además hay IPO o venta. Hasta entonces no tienen valor líquido.

### 2. Opciones NSO / NQSO (Non-Qualified Stock Options)
- **Qué es:** derecho a comprar acciones a un precio fijo (strike).
- **Fiscalidad:** al ejercer, el spread tributa como salario.
- **Riesgos:** caducan; si la acción cae por debajo del strike, valen 0 (*underwater*); ejercer exige caja.

### 3. Opciones ISO (Incentive Stock Options)
- **Qué es:** como las NSO pero con ventaja fiscal. Solo para empleados; son típicas de **startups**.
- **Fiscalidad:** al ejercer no hay impuesto normal, pero el spread puede disparar el **AMT** (Alternative Minimum Tax, un impuesto mínimo paralelo). Si se mantienen las acciones más de 2 años desde el grant y más de 1 año desde el ejercicio (*qualifying disposition*), toda la ganancia tributa como plusvalía a largo plazo (más barata).
- **Complejidad:** alta. El cálculo del AMT depende de toda la declaración del cliente.

### 4. ESPP (Employee Stock Purchase Plan)
- **Qué es:** plan para comprar acciones de tu empresa con **hasta un 15 % de descuento**, mediante descuentos en nómina durante periodos de unos 6 meses. Muchos tienen *lookback*: pagas el precio menor entre el inicio y el final del periodo, con descuento.
- **Límite:** 25.000 $ al año de valor de mercado.
- **Para el modelo:** es a la vez un **gasto/ahorro mensual** (el descuento en nómina) y un **activo** (las acciones compradas).

### 5. Otros (probablemente fuera del MVP)
| Tipo | Qué es | Por qué fuera, de entrada |
|---|---|---|
| **PSU** (Performance Stock Units) | RSUs que dependen de objetivos (ventas, retorno de la acción…) | Solo para directivos; se pueden tratar como RSU con incertidumbre |
| **RSA + 83(b)** | Acciones entregadas de inicio, con opción de tributar ya | Nicho: fundadores y primeros empleados |
| **SAR / Phantom stock** | Pagan en efectivo la revalorización | Poco frecuentes; se parecen más a un bonus |
| **Private company equity** | Acciones u opciones de empresa no cotizada | Sin precio de mercado (solo una valoración 409A), ilíquidas; muy difícil de valorar |
| **Deferred comp (NQDC / 409A)** | Salario aplazado a futuro | No es equity; Sherpas lo tiene como categoría aparte |
| **Carried interest / profits interests** | Participación en beneficios de fondos o sociedades | Nicho (sector financiero) |

## Por qué le importa a un asesor patrimonial
1. **Concentración:** es el gran riesgo. Tu sueldo **y** tu patrimonio dependen de la misma empresa (casos Enron o Lehman). Si la empresa cae, pierdes las dos cosas a la vez.
2. **Impuestos:** facturas inesperadas (*withholding gap* de las RSU, AMT de las ISO) y decisiones de cuándo vender o ejercer.
3. **Liquidez y planificación:** el dinero que "tienes" no es todo disponible. Lo no consolidado se pierde si te vas, y lo privado no se puede vender.
4. **Momentos clave (triggers):** consolidaciones, caducidades, ventanas de venta (*blackout windows*), IPO o cambio de trabajo. Son oportunidades para que el asesor llame al cliente.
5. **Negocio del asesor:** los clientes con stock compensation suelen ser **HENRYs** (*High Earners, Not Rich Yet*: tech, pharma, finanzas), justo el cliente que las grandes firmas quieren captar.

## Encaje con el modelo de Sherpas (borrador para discutir)

| Elemento | Activo | Pasivo | Ingreso | Gasto |
|---|---|---|---|---|
| RSU consolidadas | Acciones × FMV | — | — | — |
| RSU no consolidadas | ❓ (¿condicionado?) | — | Consolidaciones futuras | Impuesto en cada consolidación |
| Opciones (NSO/ISO) | Valor intrínseco (spread) de las consolidadas | Impuesto latente al ejercer | Spread al ejercer | Coste de ejercer (strike) e impuestos |
| ESPP | Acciones compradas | — | Descuento obtenido | Aportación en nómina |

Las celdas con ❓ son justo las **decisiones de producto** que tomaremos juntos.
