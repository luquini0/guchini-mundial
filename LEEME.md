# Guchini Mundial — Guchinis Gratis

## Cómo probarlo local, antes de subirlo
El sitio es un solo archivo (`index.html`) que llama directo a Supabase, así que no hace falta instalar nada — solo un servidor estático (porque usa `import` de JS, que los navegadores bloquean si abrís el archivo con doble click, `file://`).

Con Python (ya instalado en la mayoría de las PCs):
1. Abrí una terminal en la carpeta donde está `index.html`.
2. Corré: `python3 -m http.server 8000` (o `python -m http.server 8000` en Windows).
3. Abrí `http://localhost:8000` en el navegador.

También podés ver la versión ya publicada directo, sin instalar nada: **https://oabyubpjyjajvvfrhlot.supabase.co/functions/v1/site**

Vas a estar probando contra la base de datos real (no hay "modo prueba" separado), así que cualquier registro que hagas queda guardado. Para borrar datos de prueba avisame y los limpio desde Supabase.

## Diseño y marca (actualizado)
Ya está aplicado el estilo real de Guchini: amarillo `#FCC443` y verde `#006A3B` en modo clásico, celeste/blanco en "Modo Selección". El logo circular, el logotipo "Guchini" y la mascota del footer son las imágenes reales de la marca (no dibujos hechos con CSS). Las imágenes se sirven desde funciones separadas en Supabase para que la página cargue rápido — no hace falta que hagas nada con eso, es automático.

## Cómo subirlo a GitHub / Cloudflare Pages
Preferiste que yo conecte GitHub y suba el código directo. Todavía no tengo el conector autorizado de tu lado — lo tenés que habilitar vos (no puedo completar ese login por vos). Una vez conectado, subo el `index.html` al repo `luquini0/guchini-mundial` y Cloudflare Pages lo despliega solo.

Mientras tanto, si preferís no esperar, la opción manual (2 minutos):
1. Andá a github.com/luquini0/guchini-mundial
2. "Add file" → "Upload files"
3. Subí `index.html` (está en esta carpeta) y confirmá el commit a `main`
4. Cloudflare Pages detecta el push y despliega en `https://guchini-mundial.pages.dev`

## El modelo: 1 QR fijo por sucursal, en dos estilos
Hay **3 sucursales × 2 estilos = 6 diseños de QR**, todos apuntando al mismo link fijo por sucursal (no hay que cambiarlos nunca por partido):

- `guchini_qr_mendoza-la-casa_clasico.png` / `guchini_qr_mendoza-la-casa_seleccion.png`
- `guchini_qr_chacras_clasico.png` / `guchini_qr_chacras_seleccion.png`
- `guchini_qr_nueva-cordoba_clasico.png` / `guchini_qr_nueva-cordoba_seleccion.png`

Todos están también en `qr_guchini_mundial_2026.zip`. Elegí el estilo que más te guste para imprimir en cada local (podés incluso usar el clásico en un local y el de Selección en otro, es el mismo QR funcionalmente).

*Nota:* quedaron en la carpeta los 3 PNG viejos de una sola versión (`guchini_qr_mendoza-la-casa.png`, etc.) y el `qr_guchini_mundial.zip` anterior — ya no hacen falta, avisame si querés que te pida permiso para borrarlos.

Cómo funciona en la práctica:
- **Sin concurso activo**: el QR solo registra a la persona en tu base de clientes (sin premio).
- **Vos (o un admin de esa sucursal) marcás "partido ganado"** desde el panel → ese QR pasa a modo concurso.
- Mientras está activo, los primeros 50 que escaneen y se registren entran a la lista y ganan medio Guchini.
- Al llegar a 50, esa sucursal se cierra sola automáticamente (vuelve a modo registro normal, sin que tengas que hacer nada).
- Si alguien ya tiene la app abierta y sesión iniciada, no tiene que volver a llenar el formulario: le aparece un botón de "Confirmar mi lugar en el concurso" con un solo toque.

## Roles de administrador
Definiste dos niveles:
- **Superadmin**: activa y cierra el concurso de cualquier sucursal, ve el detalle completo con datos de contacto (nombre, email, celular) y es el único que puede descargar el CSV.
- **Admin de sucursal (normal)**: por defecto ve su propia sucursal (pero puede cambiar y mirar las otras también), ve la lista en vivo de quién se va anotando al concurso — **sin** datos de contacto ni CSV. No puede activar ni cerrar concursos, solo mirar.

La lista en vivo se actualiza sola cada 4 segundos mientras el panel está abierto, tanto para super como para admin normal.

## Cómo se crean las cuentas de admin
No hay contraseñas predefinidas ni las genero yo — por seguridad, cada persona elige la suya al registrarse en el sitio (igual que cualquier cliente). Los pasos:

1. **Vos (superadmin)**: entrá a la home del sitio y registrate normalmente con `creadorinventivo@gmail.com` y la contraseña que quieras. Como ese email ya está cargado como superadmin en la base, en cuanto tengas cuenta vas a ver el link "Panel de administración" en `Mi cuenta`.
2. **Cada admin de sucursal**: que se registre también desde el sitio, con su propio email y su propia contraseña.
3. Una vez que se registró, pasame el email y la sucursal que le corresponde, y yo (o vos directo en Supabase) lo agrego a la tabla de admins con rol "normal". A partir de ahí, con su email y su contraseña ya entra directo al panel viendo su sucursal.

No puedo decirte "tu usuario y contraseña" porque no existen todavía — se crean cuando cada uno se registra por primera vez.

## Sin recuperación de contraseña
Como no hay email conectado (decidiste no usar Resend por ahora), si alguien olvida su contraseña no hay botón de "recuperar" — hay que avisarme para resetearla manualmente desde Supabase. Si en algún momento lo querés, se puede conectar Resend gratis sin costo.

## Qué hace el sitio, en resumen
- Landing con la promo + botón "Modo Selección" (celeste/blanco) vs marca clásica (amarillo/verde), con los logos e imágenes reales de la marca.
- 3 QR fijos, uno por sucursal, en dos estilos cada uno (ver arriba).
- Registro: nombre, email, celular, fecha de nacimiento, contraseña propia → entra directo a su cuenta.
- Login → historial propio + ranking en vivo de cualquier sucursal (nombres enmascarados para el público).
- Panel admin en `?view=admin`, con permisos distintos para super y normal (ver arriba).
- Cualquiera puede registrarse sin QR desde la home, para hacer crecer la base de clientes.
- Footer con la mascota real de Guchini en vez de texto.

## Partidos cargados
1. vs Cabo Verde (16avos)
2. Octavos (rival a confirmar)
3-5. Cuartos, semi y final (fechas a confirmar según avance el equipo)

Se pueden agregar, editar o borrar partidos y sucursales directamente en la base (Supabase, proyecto "guchini-mundial").

## Backend (Supabase)
El registro, login, roles y rankings corren sobre un proyecto Supabase separado ("guchini-mundial"), con seguridad revisada: nadie puede ver datos personales de otro usuario, los admins normales no pueden ver ni descargar datos de contacto, y solo el superadmin puede activar/cerrar concursos y exportar el CSV. Esto no depende de dónde termine alojado el frontend.

Las imágenes de marca (logo, mascota) se sirven desde funciones propias en Supabase (`img-badge-clasico`, `img-badge-seleccion`, `img-word-clasico`, `img-word-seleccion`, `img-footer-mascot`), públicas y cacheadas, para que el `index.html` sea liviano.
