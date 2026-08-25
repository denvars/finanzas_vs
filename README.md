# Finanzas

App web para llevar control de ingresos, gastos, presupuestos, tarjetas de crédito y metas de ahorro.

Funciona en un solo archivo HTML, sin servidor y sin conexión a internet.

## Privacidad

**Los datos no viven en este repositorio.** El código es público; tu información financiera no.

Cada persona que abre la app guarda sus datos en el `localStorage` de su propio navegador. Nada se envía a ningún servidor. Dos personas que abren la misma URL desde dispositivos distintos tienen datos completamente separados y no pueden verse entre sí.

Los archivos de respaldo (`finanzas-*.json`) sí contienen todo el detalle financiero. El `.gitignore` los bloquea para que no se suban por accidente. **Nunca los agregues al repo.**

## Qué incluye

- **Perfiles independientes** con PIN opcional, cada uno con sus propios datos
- **Movimientos**: ingresos, gastos y pagos de tarjeta, con categoría y forma de pago obligatorias
- **Presupuesto mensual** por categoría, con alertas al acercarse al límite
- **Tarjetas**: saldo calculado automáticamente, día de corte, día límite de pago y ranking de la más usada
- **Metas de ahorro** con barra de progreso
- **Respaldo** en archivo local para sincronizar entre dispositivos

## Cómo se calcula el saldo de una tarjeta

```
saldo = saldo inicial + cargos − pagos
```

Un gasto pagado con tarjeta **sube** el saldo. Un movimiento de tipo "Pago de tarjeta" lo **baja**.

El pago de tarjeta no cuenta como gasto ni consume presupuesto: la compra ya se contabilizó el día que se hizo. Contarla otra vez al pagar duplicaría el gasto.

Como el saldo se calcula en vez de guardarse, borrar un movimiento corrige el saldo automáticamente.

## Uso en el celular

Abre la URL en el navegador del teléfono y agrégala a la pantalla de inicio:

- **iPhone**: botón compartir → "Agregar a inicio"
- **Android**: menú ⋮ → "Agregar a pantalla principal"

Queda como app y funciona sin conexión.

## Sincronizar entre dispositivos

El `localStorage` es independiente por navegador, así que el celular y la computadora no se sincronizan solos aunque usen la misma URL.

Para pasar datos de uno a otro, usa la pestaña **Respaldo**:

1. En el dispositivo con los datos: "Descargar respaldo" y guarda el archivo en tu carpeta de Drive
2. En el otro dispositivo: "Cargar respaldo" y elige ese archivo

En Chrome y Edge de escritorio, "Vincular archivo en Drive" permite guardar directo en el mismo archivo con un clic.

## Limitaciones

- El PIN evita entradas casuales, pero no cifra nada. No es protección real si alguien tiene acceso al dispositivo.
- Si borras los datos de navegación del sitio, se pierden los movimientos. Haz respaldos con regularidad.
- El saldo inicial de una tarjeta es lo que debías el día que la registraste; de ahí en adelante se mueve solo.

## Desarrollo

Todo vive en `index.html`: HTML, CSS y JavaScript en un solo archivo, sin dependencias ni CDN. Las gráficas están dibujadas a mano en SVG para que funcione sin conexión.

Para probar cambios, ábrelo directamente en el navegador. No requiere build.
