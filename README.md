# Detalle diario de metas

## Resumen

Prototipo independiente para revisar y probar la tabla de metas diarias de una semana retail. La página contiene datos de demostración de Arequipa, semana retail 10.

## Inicio rápido

Abre `index.html` directamente en un navegador moderno. No requiere instalación, servidor, credenciales, conexión a internet ni dependencias externas.

## Alcance y datos

- Permite editar, guardar, cancelar y eliminar metas diarias.
- Los cambios se conservan solo mientras la página permanece abierta. Al recargarla, vuelven los datos de demostración.
- No se conecta a la aplicación FollowUP ni a un servicio de datos.
- Los valores incluidos son demostrativos; no representan datos productivos.

## Modelo de cálculo

El estado diario conserva cinco bases internas: Venta, Entradas, Tickets, Artículos y Tráfico externo. Tickets, Artículos y Tráfico externo no se muestran como columnas editables independientes.

### Fórmulas de los KPI

- Artículos por ticket = Artículos ÷ Tickets.
- Tasa de conversión = (Tickets ÷ Entradas) × 100.
- Ticket promedio = Venta ÷ Tickets.
- Precio promedio = Venta ÷ Artículos. Es un valor derivado interno y no se muestra en la tabla.
- Tasa de captación = (Entradas ÷ Tráfico externo) × 100.

Al inicializar los datos de ejemplo, el prototipo deriva las bases internas así:

- Tickets = Venta ÷ Ticket promedio inicial.
- Artículos = Tickets × Artículos por ticket inicial.
- Tráfico externo = Entradas ÷ (Tasa de captación inicial ÷ 100).

### Efecto de editar un campo

Los KPI se actualizan mientras se edita. El campo modificado ajusta la base correspondiente y las demás bases se mantienen, excepto por los KPI que se derivan de ellas:

- **Meta de Venta:** actualiza Venta; recalcula Ticket promedio y Precio promedio.
- **Entradas:** actualiza Entradas; recalcula Tasa de conversión y Tasa de captación.
- **Artículos por ticket:** ajusta Artículos; recalcula Precio promedio.
- **Tasa de conversión:** ajusta Entradas manteniendo Tickets; recalcula Tasa de captación.
- **Tasa de captación:** ajusta Tráfico externo manteniendo Entradas.
- **Ticket promedio:** ajusta Venta manteniendo Tickets; recalcula Precio promedio.

El Precio promedio se calcula como Venta ÷ Artículos; no se usa como un valor fijo.

### Totales

La fila **Total / ratio** suma Venta, Entradas, Tickets, Artículos y Tráfico externo de los días cargados. Luego vuelve a calcular los KPI sobre esas sumas; no promedia los porcentajes ni los promedios diarios. Los días eliminados no participan en los totales. El redondeo se aplica al mostrar los valores, no a las operaciones internas.

### Validaciones

- Los valores no pueden ser negativos.
- Tickets, Entradas, Artículos y Tráfico externo deben ser mayores que cero para calcular los indicadores.
- Artículos por ticket debe ser al menos 1.
- Conversión y captación deben ser mayores que 0 % y no superar 100 %.
- Tickets no pueden superar Entradas; Entradas no pueden superar Tráfico externo.

## Verificación manual

No hay una suite automatizada incluida. Para una comprobación rápida:

1. Abre `index.html` y confirma que aparezcan los siete días y la fila de totales.
2. Edita cada tipo de KPI y verifica que los campos relacionados se actualicen según la sección **Efecto de editar un campo**.
3. Guarda un cambio; vuelve a editar otro día y cancélalo para confirmar que se restaure su valor.
4. Elimina un día, confirma la acción y verifica la alerta y el recálculo de totales.
5. Recarga la página y confirma que se restauren los datos de demostración.

## Git y publicación

La rama principal de este proyecto es `main`. No se incluye una URL de remoto: antes de subirlo, configura el remoto que corresponda al repositorio de destino. La identidad de Git se configura localmente en el repositorio y no se almacena en este README.

Antes de publicar el proyecto en un repositorio público, define si los datos de ejemplo pueden compartirse y qué licencia debe aplicarse. No se agregó una licencia porque esa decisión corresponde al propietario del proyecto.
