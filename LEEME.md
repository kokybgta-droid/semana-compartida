# Semana Compartida — puesta en marcha

La base de datos ya está creada en Supabase (proyecto **semana-compartida**, región São Paulo, plan gratuito).
Faltan 3 pasos que solo se pueden hacer desde los paneles web (~15 min).

## 1. Publicar la app en GitHub Pages
1. En GitHub (cuenta `kokybgta-droid`) crea un repositorio nuevo, por ejemplo `semana-compartida`.
2. Sube todos los archivos de esta carpeta (index.html, manifest.json, sw.js, icon.svg, icon-192.png, icon-512.png).
3. Settings → Pages → Source: *Deploy from a branch* → `main` / `(root)` → Save.
4. Tu URL quedará: `https://kokybgta-droid.github.io/semana-compartida/`

## 2. Crear credenciales de Google (Google Cloud Console)
1. https://console.cloud.google.com → crea un proyecto ("Semana Compartida").
2. APIs y servicios → **Pantalla de consentimiento OAuth** → Externo → nombre de la app, tu correo → guardar.
   Publícala ("Publicar app") para que funcione con cualquier Gmail (o agrega el Gmail de la mamá como usuario de prueba).
3. APIs y servicios → **Credenciales** → Crear credenciales → *ID de cliente OAuth* → tipo **Aplicación web**.
   - Orígenes JavaScript autorizados: `https://kokybgta-droid.github.io`
   - URI de redireccionamiento autorizados: `https://tfemsghfhurvrphjmqgb.supabase.co/auth/v1/callback`
4. Copia el **Client ID** y el **Client Secret**.

## 3. Activar Google en Supabase
En https://supabase.com/dashboard/project/tfemsghfhurvrphjmqgb
1. Authentication → **Sign In / Providers** → Google → Enable → pega Client ID y Secret → Save.
2. Authentication → **URL Configuration**:
   - Site URL: `https://kokybgta-droid.github.io/semana-compartida/`
   - Redirect URLs: agrega `https://kokybgta-droid.github.io/semana-compartida/**`

## Uso
1. Entra tú primero con tu Gmail → completa "Configurar" (nombre de tu hijo, día de cambio, con quién está esta semana, y el Gmail de la mamá).
2. Envíale el enlace. Cuando ella entre con ese Gmail queda conectada automáticamente.
3. En el celular: abrir el enlace → menú del navegador → **"Agregar a pantalla de inicio"** (queda como app).

## Qué incluye
- **Calendario mensual** con cada semana coloreada según a quién le toca; tocar un día permite agregar cita o intercambiar esa semana.
- **Citas** (médico, terapia, colegio, actividad) con lugar, quién lo lleva, notas y repetición semanal.
- **Gastos** por mes: total de cada casa, gastos compartidos con % de división, foto del comprobante y saldo "quién le debe a quién".
- **Ficha**: medicamentos, rutinas, lo que le ayuda, lo que lo desregula, contactos de médicos/terapeutas.
- **Bitácora** de la semana con ánimo (😣→😄) para el traspaso.

## Seguridad
- Cada tabla tiene Row Level Security: solo los dos miembros de la familia ven o editan sus datos (probado: un tercer usuario no ve ni puede insertar nada).
- Los comprobantes se guardan en un bucket privado y se abren con enlaces temporales de 5 minutos.
- También hay ingreso por enlace al correo como alternativa a Google.
