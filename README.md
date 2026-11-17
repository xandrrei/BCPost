[README.md](https://github.com/user-attachments/files/34971641/README.md)
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

## Nº de biopsia
Cada pieza lleva su número de biopsia con formato **B00-000000** (sin siglas del paciente). Se escribe al añadir la pieza, en la lista de piezas pendientes de repartir o en la tarjeta del residente. Vale escribirlo abreviado («b26 1234» se convierte en «B26-001234»), y si el formato no es válido, el campo se marca en rojo. Sale en las tarjetas, en «Piezas por incluir», en la imagen PNG y en la columna «Ref Biopsia» del Excel.

## Información clínica de cada pieza
- Cuando POST pasa una pieza prevista al reparto, la pieza lleva su ficha de DÍA **sin el nombre del paciente**: edad, sexo, neoadyuvancia, posible intraoperatoria, localización y otros datos. El nombre solo está en la pestaña DÍA, para reconocer la pieza cuando llega.
- La ficha se ve en la tarjeta de cada residente, en «Pendientes de días anteriores» y en «Piezas por incluir».
- En **«Info clínica»** cualquiera puede **añadir información**. Cada nota queda con su autor, fecha y hora, se comparte por la carpeta y sigue a la pieza si pasa al día siguiente.
- La ficha y las notas no salen en la imagen PNG ni en el Excel.

## Orden de la lista de trabajo
En la tarjeta de cada residente (mañana y tarde por separado), en «Pendientes de días anteriores» y en la imagen PNG: primero las **urgentes retrasadas**, luego las **urgentes nuevas**, y después de la **más antigua a la más nueva** (más días de espera primero).

## En descalcificación
Cada pieza del reparto (y de «Pendientes de días anteriores») tiene una casilla **«En descalcificación»**, compartida por todos. Las piezas marcadas salen con borde discontinuo y en el recuadro **«En descalcificación»**, con su residente y la fecha desde la que están. La marca pasa con la pieza al día siguiente hasta que se marque como incluida o se desmarque.

**Horas de las piezas en descalcificación:** mientras una pieza está en descalcificación **cuenta 0 minutos** en el reparto, en los totales y en las campanas (se ve como «0 min (45 min al tallar)»), y **se queda con el residente que la empezó**, aunque fuera de POST o Tarde 2. El día que se talla, se quita la marca y la pieza vuelve a contar su tiempo entero ese día: si ya es de días anteriores, cuenta en la mañana de su residente y en su reserva de campana («Sale de descalcificación: cuenta hoy»).

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

### Previstas que no llegan el día previsto
- **En DÍA**, el recuadro **«Sin llegar de días anteriores»** muestra las previstas de días anteriores (hasta 14 días) que nadie ha marcado como llegadas, con toda su ficha. «Pasar a mi lista» las copia a las previstas de hoy («Rescatada del 23/10»), para que las vea POST del siguiente día laborable. «No llegará» las quita.
- **En POST**, el desplegable **«Previstas de días anteriores sin llegar»** permite añadir al reparto una prevista atrasada que llega ese día por sorpresa. Entra como pieza nueva, con la etiqueta «Llegó con retraso · prevista el 23/10».

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

### Organización de inclusión (campanas)
- Campanas 1 y 2, de **9 a 20h**, por medias horas: mañana 9–16h y tarde 16–20h.
- **Reserva automática** («Reservar campanas según el reparto»): por la mañana, a cada residente le reserva el tiempo de sus piezas de ese día que aún no ha incluido, redondeado a medias horas; por la tarde, la Campana 1 a POST y la 2 a Tarde 2:
  - por la mañana, en **un solo bloque** si cabe, en la **misma campana** y en sus **franjas preferidas**;
  - si no cabe seguido, lo divide en bloques, pero nunca dos bloques seguidos en campanas distintas (no tiene que cambiarse de campana a media inclusión) ni dos a la vez;
  - respeta las reservas hechas a mano; si se vuelve a pulsar, rehace solo las automáticas (las que llevan la nota «Reserva automática»).
- **Tarde (16–20h):** la Campana 1 es para POST y la Campana 2 para Tarde 2, toda la tarde. Por eso, en el reparto, quien ayuda con «el resto» sin ser POST ni Tarde 2 (p. ej. la rotación de NECRO) incluye sus piezas por la mañana.
- **Preferencias de horario:** solo de la mañana, con las franjas 9–11, 11–13 y 13–16 para cada residente. Sin marcar = sin preferencia (lo más temprano posible).
- Con la carpeta compartida, las reservas (`campanas_AAAA-MM-DD.json`) y las preferencias (`preferencias.json`) se comparten entre todos. Sigue existiendo la opción de la hoja de Google.

## Animal de cada residente
Arriba, junto a tu nombre, está tu animal; pulsándolo eliges otro. Sale en tu tarjeta del reparto, en las campanas y en las listas, y se comparte con todos.

## Ajustes (dentro de la pestaña POST: retrasos y correos)
- **Umbral de retraso** en días.
- **Correos** de los residentes, para «Enviar por correo» (se guardan solo en ese navegador).
- El planning y las rotaciones están en la pestaña «Planning».

## Pestaña «Planning»
- **Guardias del mes**, editables en la propia app: DÍA, POST, Tarde 2, autopsia (hasta dos personas), Out y festivo. Sirve para los cambios puntuales, sin volver a importar el PDF. Los cambios de última hora hechos en la pestaña POST (tarjeta «Día a repartir» y «Autopsia hoy») cambian lo mismo.
- **Rotaciones del mes** y rotación de NECRO.
- Con la carpeta compartida conectada, el planning se guarda en ella (`planning.json`) y lo ven todos en un minuto. **No hace falta subir nada a GitHub.** Se junta día a día: si dos personas cambian días distintos a la vez, se guardan los dos cambios. Cada día cambiado indica quién lo cambió y cuándo.

### Importar el planning de un mes nuevo
1. En la pestaña Planning, «Importar el planning de un mes nuevo»: el PDF o el Excel del planning de siempre (fila «Mes» y columnas DÍA · POST · TARDE 2 · N. ADULTO · N. FETAL · Out; valen nombres o iniciales). Si no tienes el Excel, descarga la **plantilla** y rellénala.
2. Revisa las guardias, las rotaciones y los avisos que salgan. Ya está: se guarda en la carpeta y lo ven todos.
- «Descargar copia (planning.json)» queda como copia de seguridad. Si algún día no hubiera carpeta compartida, ese archivo subido a GitHub junto al HTML también reparte el planning a todos.

## Publicar en GitHub Pages
1. Sube `index.html` (y `planning.json` cuando lo tengas) a la raíz del repositorio.
2. Ve a **Settings → Pages**, elige la rama `main` y la carpeta `/ (root)`, y guarda.
3. La página queda en `https://<usuario>.github.io/<repositorio>/`. Los cambios tardan unos minutos en verse.

## Archivos
| Archivo | Qué es |
|---|---|
| `index.html` | La aplicación completa: estilos, código, tabla de tiempos y los meses incluidos. |
| `planning.json` | (Opcional, normalmente no hace falta) Copia del planning para publicarlo en GitHub si no hay carpeta compartida. |
| `README.md` | Este documento. |

En la **carpeta compartida** del hospital (no en GitHub) la página guarda `planning.json`, `preferencias.json`, `de_dia_AAAA-MM-DD.json`, `reparto_AAAA-MM-DD.json` y `campanas_AAAA-MM-DD.json`. Los archivos de días de más de 14 días se borran solos. **Esto no borra piezas atrasadas:** cada día, lo pendiente se copia al reparto del día nuevo con sus días de espera, historial, ficha, notas y descalcificación, así que una pieza atrasada siempre está en el archivo del día actual. Lo pendiente se trae del último día con reparto (hasta 14 días atrás), aunque algún día laborable nadie haya abierto el reparto, y se suman los días laborables que hayan pasado.

## Notas
- Con la carpeta compartida conectada, el planning, las previstas de DÍA y el reparto de cada día se comparten entre todos. Sin carpeta, solo se guardan en el navegador de cada uno.
- Para leer el planning en PDF, la página carga pdf.js desde cdnjs, así que hace falta conexión a internet. El Excel se lee sin conexión.
- Si el repositorio es público, el HTML y el planning.json (con los nombres de los residentes) son visibles para cualquiera. Los datos de pacientes nunca van en estos archivos.
