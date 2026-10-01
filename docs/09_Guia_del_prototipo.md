# Guía del prototipo

> Versión de trabajo, en español. El prototipo publicado está en `prototype/`, cifrado: ábrelo con el enlace del README y la contraseña de la página de Notion.

## Qué es
Dos pantallas de la plataforma con la propuesta integrada, sobre un caso de ejemplo: **John & Jane Doe**. John trabaja en Acme, tiene **$500K en acciones de Acme** y **2.000 RSU** pendientes de consolidar.
- **Parte 1, el cuestionario:** dónde se captura la stock compensation.
- **Parte 2, el diagnóstico:** qué ve el asesor como resultado.

**Cómo abrirlo:** descarga la carpeta `prototipo/` completa y abre `index.html` en el navegador. Los dos HTML necesitan el fichero `caso.js`, que está en la misma carpeta.

## Recorrido recomendado (5 minutos)
| Paso | Dónde | Qué mirar |
|---|---|---|
| 1 | Cuestionario → **3 · Income** | El empleador de cada persona, la pregunta "Do you get company stock through work?" y la fila de RSU, con su valor calculado |
| 2 | Cuestionario → **4 · Investments** | La cuenta "Stock plan account", las posiciones de Acme marcadas como "Your employer" y el resumen final: **$500K en 2 cuentas** |
| 3 | Cuestionario → **Envío** | El enlace a la Parte 2 |
| 4 | Diagnóstico → **Financial health** | El net worth con las RSU aparte, la trayectoria de Acme si no hace nada y, en **View more** del score, el área **Investing** |
| 5 | Diagnóstico → **Investment analysis** y **Statements** | La exposición total a Acme, la recomendación de diversificar, qué pasa si Acme cae un 40 % y las RSU en el balance y en el flujo de caja |

## Los botones de la barra
- **Datos de entrada:** resumen del caso, es decir, los datos que producen el diagnóstico.
- **Hoy / Propuesta:** compara la plataforma actual con la propuesta.
- **Notas:** muestra u oculta las explicaciones.

## Cómo leer lo que ves
- **Lo resaltado en ámbar es nuevo.** Cada elemento lleva un código: C = captura, A = análisis.
- **Las notas en ámbar** explican cada elemento nuevo. **El texto gris** describe lo que ya existe en la plataforma.
- **Junto a las cifras del diagnóstico**, un icono indica su origen: ↻ calculada, S supuesto, ❓ resultado del motor de Sherpas, ✎ texto adaptado.
- **Pasa el ratón por cualquier icono o botón** para ver qué significa.

## Qué no hace
- **El diagnóstico no se recalcula.** Siempre muestra el resultado del caso, aunque cambies datos en el cuestionario.
- **Solo se pueden editar las secciones con cambios:** Documents, Income e Investments. Sus pestañas aparecen en ámbar.
- **No es la interfaz real.** Es una reproducción de lo observado; las empresas y los precios son ficticios.

Las reglas completas del prototipo y el origen de cada dato están en el documento [Caso conductor](08_Caso_conductor.md).
