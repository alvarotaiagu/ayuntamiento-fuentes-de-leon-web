# Ayuntamiento de Fuentes de León · propuesta de web «Puerta abierta» (v3)

Maqueta de la web municipal del **Ayuntamiento de Fuentes de León** (Badajoz, 2.118 habitantes, INE 2025), hecha con la plantilla «Puerta abierta» v3 (`plantilla-ayuntamiento-puerta-abierta-web`, rama `master`) y con sus datos reales. Se le propone por correo.

- **No es la web oficial.** Lleva en todas las páginas la banda «Propuesta de diseño… no es la web oficial» y `noindex, nofollow`.
- **Publicada** el 5-10-2026 en <https://alvarotaiagu.github.io/ayuntamiento-fuentes-de-leon-web/> (repo `alvarotaiagu/ayuntamiento-fuentes-de-leon-web`, Pages sobre `master`; con `?revision` sale el mando). `actualizar.yml` hace que un bot comitee a diario: `git pull --rebase origin master` antes de cada push.
- Las fuentes de cada dato, el inventario de sus webs actuales y sus errores están **fuera de esta carpeta**, en `../ayuntamiento-fuentes-de-leon-bocetos/`: `DATOS.md`, `INVENTARIO.md`, `ERRORES.md` y `CORREO.md`.

```bash
npm install                     # Playwright y axe-core (solo para los scripts)
node scripts/aplicar.mjs        # genera la web desde municipio.json, marca/, contenido/ y media/
node scripts/servir.mjs         # http://127.0.0.1:4192/  ·  con ?revision, el mando
node scripts/verificar.mjs      # todas las comprobaciones
```

`municipio.json` lo escriben, en este orden, `../ayuntamiento-fuentes-de-leon-bocetos/_scripts/construir_municipio.py` (sobre el borrador de `nuevo-municipio.mjs`, con `datos_agentes.json` y `pueblo.json`) y `v3-datos.py` (los campos de la v3). El tablón sale de `node scripts/tablon.mjs --desde <copia de /board>` y sus títulos claros de `_scripts/titulos-claros.py`; la lectura fácil, de `_scripts/facil.py`.

---

## El concepto

**La puerta del Ayuntamiento, abierta todo el día.** El arco de medio punto encalado es el único motivo dibujado y enmarca la Casa Consistorial en la portada. El panel «Hoy en Fuentes» dice tres cosas: si el Ayuntamiento está abierto (con la hora real), lo próximo de la agenda y el último aviso.

Por qué le encaja a Fuentes de León:
- **Tiene dos webs y ninguna está completa.** `fuentesdeleon.es` (la de la Diputación, la «oficial») está casi vacía: «No hay información» en noticias, agenda y tablón. `aytofuentesdeleon.com` sí se actualiza, pero 23 de sus 62 entradas son solo un cartel en imagen. Aquí hay **una sola puerta**: lo importante de las dos webs y de la sede, en texto y ordenado.
- **Su tablón oficial está en la sede (Gestiona) y está vivo** (esta semana: una convocatoria de pleno, unas bases de empleo). La maqueta lo enseña en lenguaje claro («Anuncio de la convocatoria» → «Convocatoria del Pleno extraordinario del 9 de octubre») y deja fuera lo que lleva datos personales.
- **Lo que el vecino busca, ordenado:** 111 trámites con buscador en palabras normales, el listín entero con las urgencias primero (y una hoja para la nevera), la biblioteca con su horario nuevo, las Cuevas con su visita guiada y «El pueblo» (historia, patrimonio, fiestas, rutas), con las dudas de las fuentes sin esconder.

**Marca: el azur de los chorros de la fuente.** El escudo es oro (el campo), plata (la fuente y la punta) y gules (el león, la cruz de Santiago y la corona).
- El oro nunca es marca: no llega a AA como texto.
- El gules, que gana por área, es el color de las alertas: la franja urgente y el 112.
- La plata no sirve.
- Quedan el azur de los dos chorros de la fuente que da nombre al pueblo y el sinople de las esmeraldas de la corona. Se ha elegido el azur. Está forzado con `--principal azur` y el motivo escrito en `marca/marca.json`.

**Cortina: «El escudo a su sitio»** (`"cortina": "escudo"`). Solo en la portada, una vez por sesión, ≤ 1,2 s; se salta con clic, tecla o rueda y no existe con movimiento reducido. Si prefieren no abrir con el escudo, `"cortina": "puerta"`.

## Mapa de páginas

| Página | Qué tiene |
|---|---|
| `index.html` | Hero «Hoy en Fuentes» con la Casa Consistorial, la dehesa y el pueblo en el arco (una al azar). Trámites, tablón con filtros, agenda y listín corto, «¿Quién se ocupa de qué?», «Conocer Fuentes» |
| `tramites.html`, `facil.html` | Buscador global, «Por momentos», 5 temas y los 111 trámites. «Explicado fácil» de 3 trámites y del aviso de incidencias |
| `ayuntamiento.html` | Alcaldía (retrato como hueco diseñado y saluda de ejemplo), el pleno (PP 6, PSOE 5) y concejalías |
| `avisos.html`, `noticias.html` y `noticia-*.html`, `agenda.html` | Avisos y tablón de la sede, 7 noticias en texto, agenda con fiestas y el pleno del 9 de octubre |
| `telefonos.html` | Listín con 112, Ayuntamiento, seguridad, salud, servicios sociales y empleo, educación y cultura y deporte. **Instalaciones municipales**: piscina, polideportivo, biblioteca, escuelas y mayores |
| `pueblo.html` | Qué ver, Para visitar (Cuevas), historia, patrimonio, fiestas, gastronomía, personajes, rutas (con el Camino de Santiago del Sur), Dónde comer y dormir y el **mapa del término** |
| `contacto.html`, `incidencia.html`, `escribanos.html` | Dirección, horario, mapa bajo clic; avisar de un problema y escribir al Ayuntamiento, por correo y sin servidor |
| `transparencia.html`, `publicar.html`, `propuesta.html`, `suscribirse.html` | Transparencia (con el portal de la sede), página del personal, la página para la alcaldía y suscripción a la agenda |
| Legal y `404.html` | Aviso legal, privacidad, cookies (no usa) y declaración de accesibilidad |

## Lo que se ha adaptado

- **«El pueblo» solo en castellano**: no hay `contenido/pueblo.<lang>.json`, ni `pueblo-en.html` ni `pueblo-pt.html` (decisión del 5-10-2026).
- **Pruebas de `verificar.mjs` atadas a Ribera** (como en los otros casos): precio sin `<script>`, muestra de V16 con lugares de Fuentes y F25 con los lugares comprobados en OSM.
- **Verificación**: `node scripts/verificar.mjs --capturas` da **173 de 173** (5-10-2026). Además de lo anterior, `css/imprimir.css` lleva los ajustes de Segura para que el listín quepa en una A4 y la prueba de movimiento usa 375×480 (no hay lema); F22 no lleva un apartado `contratos` propio porque ya enlaza por defecto el perfil del contratante.

## Pendientes del Ayuntamiento

1. **Horario**: está publicado en su web `.com`; confirmar los martes y miércoles «al mes» (la web no dice cuáles).
2. **Correo de incidencias y de «Escríbanos»**: se ha puesto `ayuntamiento@fuentesdeleon.es`. Por confirmar.
3. **Pleno del 9-10-2026**: hora y orden del día (en la convocatoria de la sede).
4. **Corporación**: quién sustituyó a Gema María Lozano Adán (PP) y a Aurelio Aldeanueva Núñez (PSOE) y cuándo; quién lleva hoy Bienestar Social, Empleo y Desarrollo Local.
5. **Oficina de Turismo**: dirección vigente (Plaza de España, 3 o calle Galinda, 14) y horario; horario del Centro de Interpretación.
6. **Fotos propias**: castillo del Cuerno, iglesia por fuera, procesión del Corpus. Y el permiso para usar las de su web, si se quieren.
7. **Perfil del pie**: el dibujo del pueblo queda genérico; dibujarlo desde fotos reales es un paso aparte.
8. **`hoja.id`** (hoja de cálculo para publicar sin tocar la web) y **autorización por escrito para leer el tablón** de la sede (`tablon_autorizado`). Hoy el tablón es una copia del 5-10-2026.
9. **Autobús, guardias de farmacia, teléfono de la biblioteca, dirección de la guardería y de la piscina**: no constan en fuentes oficiales.
10. **Comprobar** las fichas de bares y alojamientos (son de 2022-2023) y el teléfono de los pisos tutelados.
11. **Escudo**: confirmar con el Ayuntamiento el dibujo vigente (en Commons hay dos: chorros azur y chorros grises).

## Créditos

- **Fotos**: Wikimedia Commons, con su autor y licencia en `media/creditos.json` y bajo cada foto (Adolfobrigido, Acuxhinu y Paulo Valdivieso).
- **Escudo**: Heraldica 1010, CC BY-SA 4.0 (Commons).
- **Plano del pie y mapa del término**: © colaboradores de OpenStreetMap (ODbL).
- Los **textos de noticias y avisos** son resúmenes con palabras propias de las entradas de `aytofuentesdeleon.com`, que enlazan a su original.
