[README.md](https://github.com/user-attachments/files/34966506/README.md)
# Reparto de Inclusión

Herramienta web para repartir cada día la inclusión de piezas quirúrgicas entre los residentes de Anatomía Patológica, según el tiempo estimado de cada tipo de pieza, el planning de guardias y las rotaciones del mes.

Es una sola página (`index.html`), sin servidor ni instalación: se abre en el navegador y funciona también desde GitHub Pages.

## Quién eres y reparto compartido
- Al abrir, la página pregunta **«¿Quién eres?»** (cada vez, porque los ordenadores del hospital son compartidos; recuerda el último nombre). Arriba muestra tu papel de hoy según el planning: POST, Tarde 2, de día, autopsia, rotación… En el reparto, tu tarjeta sale la primera y destacada. «Solo mirar» entra sin nombre.
- Al abrir, «POST» va directo a la fecha de hoy si está en el planning. Cada fecha tiene su propio reparto.
- Con la carpeta compartida conectada, el reparto de cada día se guarda en ella (`reparto_AAAA-MM-DD.json`). Normalmente lo hace quien está de POST, pero **cualquiera puede cambiarlo**. Se ve quién hizo el último cambio y a qué hora, y los demás lo reciben en un minuto como mucho (o con «Actualizar ahora»). Si dos personas cambian a la vez, queda el último cambio.

## Piezas incluidas y pendientes
- Cada pieza del reparto tiene una casilla **«Incluida»**. Cada tarjeta muestra cuántas lleva incluidas (p. ej. «2/3 incluidas»). Varias personas pueden marcar a la vez desde ordenadores distintos: las marcas se juntan pieza a pieza.
- Al abrir el reparto **del día de hoy**, se trae una sola vez lo que quedó sin marcar el día laborable anterior:
  - Las piezas que POST o Tarde 2 tenían **por su papel de POST/Tarde 2** vuelven a «Piezas pendientes de repartir» y se reparten de nuevo contando horas.
  - El resto (rotación, rotación de NECRO, asignadas a mano) **sigue con su residente** en «Pendientes de días anteriores», sin contar en las horas del día. Si tampoco se incluyen ese día, pasan al siguiente.
  - En ambos casos los días de espera suben en 1, así que lo que se acumula acaba marcado como retrasado.
- Con carpeta compartida, se trae lo pendiente después de leer la carpeta; sin carpeta, con lo guardado en ese navegador.

## Colores de las piezas
| Color | Significado |
|---|---|
| Verde | Nueva: recibida el día anterior (0 días de espera) |
| Naranja | 1 a 3 días de espera |
| Rojo | Más de 3 días de espera, o pieza urgente con 1 o más días de espera (manda sobre los demás colores) |
| Morado | Urgente y nueva (0 días de espera): marcada como urgente, protocolo linfoma (HEM) o neuro (NR) |

## Información clínica de cada pieza
- Cuando POST pasa una pieza prevista al reparto, la pieza lleva su ficha de DÍA **sin el nombre del paciente**: edad, sexo, neoadyuvancia, posible intraoperatoria, localización y otros datos. El nombre solo está en la pestaña DÍA, para reconocer la pieza cuando llega.
- La ficha se ve en la tarjeta de cada residente, en «Pendientes de días anteriores» y en «Piezas por incluir».
- En **«Info clínica»** cualquiera puede **añadir información**. Cada nota queda con su autor, fecha y hora, se comparte por la carpeta y sigue a la pieza si pasa al día siguiente.
- La ficha y las notas no salen en la imagen PNG ni en el Excel.

## Orden de la lista de trabajo
En la tarjeta de cada residente (mañana y tarde por separado), en «Pendientes de días anteriores» y en la imagen PNG: primero las **urgentes retrasadas**, luego las **urgentes nuevas**, y después de la **más antigua a la más nueva** (más días de espera primero).

## En descalcificación
Cada pieza del reparto (y de «Pendientes de días anteriores») tiene una casilla **«En descalcificación»**, compartida por todos. Las piezas marcadas salen con borde discontinuo y en el recuadro **«En descalcificación»**, con su residente y la fecha desde la que están. La marca pasa con la pieza al día siguiente hasta que se marque como incluida o se desmarque.

## Carteles de advertencia
Arriba, en todas las pestañas, para la fecha elegida en «POST»:
- **Rojo:** piezas urgentes (marcadas, hemato o neuro) con 1 o más días de espera.
- **Azul:** piezas con más de 5 días en descalcificación. Hay que confirmar con «Sigue en descalcificación» o quitar la marca con «Ya no». Una vez confirmada, el aviso vuelve cada 2 días, y cada día a partir de los 10 días de descalcificación.

## Pestaña «Piezas por incluir»
Todo lo que queda sin marcar como incluido en la fecha elegida en «POST»: lo repartido ese día, lo que sigue de días anteriores y lo que aún no se ha repartido. Arriba, un resumen: piezas y tiempo por incluir, de días anteriores, en descalcificación y en rojo. Se puede filtrar por residente, especialidad, «solo en descalcificación» y «solo de días anteriores». La columna **Historial** muestra en qué listas de trabajo ha estado cada pieza, día a día (p. ej. «29/10 Kasia → 30/10 Dani»). Ordenada por prioridad: rojo, morado, naranja, verde.

## Pestañas

### Consulta
Tabla de tiempos por tipo de pieza, filtrable por especialidad y con buscador.

- Datos de **diciembre 2025 – noviembre 2026** (n = 2.640).
- **Tiempo de reparto** = media del tipo de pieza, con los valores por encima del p95 topeados (en tipos con menos de 10 casos, al p95 de su especialidad), redondeada a 5 min.
- **1 punto = 10 min.** Es el tiempo de un residente ya formado. Para un R1 en sus primeros meses hay que multiplicar por 1,2.
- ⚠ = n bajo (menos de 10 casos). La pieza técnica cuenta con un tiempo fijo de 10 min.

### DÍA (piezas previstas)
Quien está de día apunta las piezas que espera de quirófano (nombre sin apellidos, edad, sexo, cirugía, neoadyuvancia, posible intraoperatoria, localización y otros datos clínicos). Al día siguiente aparecen en «POST» para marcar las que han llegado.

> **Privacidad:** estos datos se guardan en el navegador de quien los apunta y, si está conectada, en la carpeta compartida del servicio (red del hospital). Nunca se suben a GitHub ni salen en la imagen ni en el Excel, y se borran solos a los 14 días.

**Carpeta compartida del servicio (Edge o Chrome):** en «DÍA», «Conectar carpeta» y elegir una subcarpeta de la unidad de red (p. ej. `Y:\AP\Reparto`). Cada día de recepción se guarda como `de_dia_AAAA-MM-DD.json` en esa carpeta, y al día siguiente «POST» lo lee desde cualquier ordenador con la carpeta conectada. Si dos ordenadores apuntan el mismo día, las piezas se juntan; las borradas no reaparecen. Los archivos de más de 14 días se borran solos. El permiso se recuerda por navegador; si lo vuelve a pedir, «Reconectar carpeta». No funciona dentro de claude.ai. Sin carpeta, sigue estando «Guardar copia» / «Cargar copia».

### POST (reparto del día)
1. Elige mes y fecha. POST, Tarde 2, Día y Out salen del planning y se pueden cambiar en el momento.
2. Marca quién tiene autopsia hoy.
3. Añade las piezas: las previstas de «DÍA» o a mano (especialidad, tipo, cantidad, días de espera, urgente, compleja, neoplásica, nota o asignación directa).
4. Pulsa **«Calcular reparto del día»**. Cada pieza se puede mover luego a otra persona o franja.
5. Exporta: **imagen PNG**, **Excel (.xlsx)** o **enviar por correo**.

**Reglas del reparto**
- Las especialidades con residente de rotación ese mes van directas a esa persona. Si hay varias, incluye la más pequeña, y la mayor solo incluye la mitad si ese día está de POST o Tarde 2. Quien «repite» rotación solo las incluye por la tarde los días que está de POST o Tarde 2.
- El resto se reparte entre la persona de la rotación de NECRO (hasta 4 h, o 0 si tiene autopsia o está de día), POST y Tarde 2, equilibrando por tiempo.
- Tarde 2 asume ~1 h más que POST por la tarde.
- Quien tiene autopsia o está de día queda limitado a ~2 h, salvo si es Tarde 2. POST nunca hace necropsia.
- Protocolo linfoma (HEM), piezas de neuro (NR) y piezas urgentes van siempre a POST por la mañana.
- Las piezas retrasadas (más días de espera que el umbral de Ajustes) se marcan con ⚠ o, si son neoplásicas, con ‼, y suben al principio de la lista de tarde.
- Las piezas técnicas solo se reparten entre POST y Tarde 2.
- Capacidad: 2 estaciones; mañana 8–16 h (6 h 30 útiles tras comida y sesión) y tarde 16–20 h.

### Organización de inclusión
Reserva de campanas (Campana 1 y 2, de 8 a 16 h, en franjas de 30 min). Muestra lo que cada residente tiene asignado por la mañana para reservar ese tiempo.

- **Modo local** (por defecto): las reservas solo se ven en ese ordenador.
- **Compartido:** se guardan en una hoja de Google mediante Apps Script. Los pasos están en la propia pestaña («Configurar reservas compartidas»), con un botón para descargar el script.

## Ajustes (dentro de la pestaña POST)
- **Rotaciones del mes:** quién está en cada especialidad. Admite varias personas, días concretos (p. ej. «16-30») y «repite».
- **Rotación de NECRO** del mes.
- **Umbral de retraso** en días.
- **Correos** de los residentes, para «Enviar por correo» (se guardan solo en ese navegador).
- **Planning del mes**, editable día a día.

## Cargar el planning de un mes nuevo
1. En Ajustes, **«1 · Importar planning»**: el PDF o el Excel del planning de siempre (fila «Mes» y columnas DÍA · POST · TARDE 2 · N. ADULTO · N. FETAL · Out; valen nombres o iniciales). Si no tienes el Excel, descarga la **plantilla** y rellénala.
2. Revisa las rotaciones y los avisos que salgan.
3. Pulsa **«3 · Descargar planning.json»** y súbelo a este repositorio, **en la misma carpeta que `index.html`**, sustituyendo el anterior. Al abrir la página, todo el mundo recibe el planning nuevo sin tocar el HTML.

## Publicar en GitHub Pages
1. Sube `index.html` (y `planning.json` cuando lo tengas) a la raíz del repositorio.
2. Ve a **Settings → Pages**, elige la rama `main` y la carpeta `/ (root)`, y guarda.
3. La página queda en `https://<usuario>.github.io/<repositorio>/`. Los cambios tardan unos minutos en verse.

## Archivos
| Archivo | Qué es |
|---|---|
| `index.html` | La aplicación completa: estilos, código, tabla de tiempos y los meses incluidos. |
| `planning.json` | (Opcional) Planning compartido de los meses importados, generado desde la propia página. |
| `README.md` | Este documento. |

## Notas
- Lo que cada uno cambia (planning editado a mano, piezas del día, reparto calculado) se guarda en el `localStorage` de su navegador.
- Para leer el planning en PDF, la página carga pdf.js desde cdnjs, así que hace falta conexión a internet. El Excel se lee sin conexión.
- Si el repositorio es público, el HTML y el planning.json (con los nombres de los residentes) son visibles para cualquiera. Los datos de pacientes nunca van en estos archivos.
