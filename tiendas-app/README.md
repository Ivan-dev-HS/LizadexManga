# Lizadex Tiendas (MVP)

Producto B2B independiente de Lizadex: un panel para que una tienda de manga
gestione las **reservas/pedidos de sus clientes** (qué han encargado, si ha
llegado a la tienda, si ya lo han recogido). No tiene nada que ver con la app
personal de seguimiento de colección — vive en su propia carpeta, su propia
rama de git y su propio backend, para no tocar nada de lo existente.

## Qué incluye esta v1

- **Login / registro** de empleados (Supabase Auth, email + contraseña).
- **Alta de tienda**: el primer usuario que se registra crea su tienda y
  queda como `owner`.
- **Multi-tienda real con aislamiento de datos**: cada tabla tiene Row Level
  Security en Postgres — el personal de una tienda nunca puede ver ni tocar
  los datos de otra, esto lo garantiza la base de datos, no el frontend.
- **Pedidos**: crear un pedido eligiendo/creando un cliente, buscando el
  manga en AniList (reutiliza el mismo patrón que la app personal), con
  edición/nota opcionales. Filtro por estado: Pendiente → Llegado → Recogido.
- **Clientes**: alta manual y listado.

## Lo que NO incluye (a propósito, para no construir a ciegas)

- **Notificaciones al cliente** (email/SMS/WhatsApp) cuando llega su pedido.
  Requeriría recoger el contacto del cliente con su consentimiento (RGPD) y
  un proveedor de envío (p. ej. Resend para email) — encaja como
  Edge Function de Supabase el día que se quiera añadir.
- **Invitar a más empleados** a una tienda ya creada (hoy cada usuario que se
  registra crea su propia tienda nueva; falta un flujo de invitación).
- **Inventario/stock** de la tienda en sí (esto es un gestor de pedidos de
  clientes, no un ERP de tienda).
- **Facturación** ni cobros.

## Infraestructura

- **Backend**: proyecto Supabase nuevo, `lizadex-tiendas`
  (`qvttuzsogjniajjqdxqf`), en la misma organización de Supabase del usuario.
  Nivel gratuito. Esquema: `stores`, `store_staff`, `customers`, `orders`,
  con RLS en las cuatro tablas.
- **Frontend**: HTML/JS estático sin build step (mismo espíritu que la app
  personal), con el cliente de `@supabase/supabase-js` v2 cargado desde el
  CDN de jsdelivr.
- **Clave usada en el frontend**: la clave "publishable" de Supabase, que
  está pensada para exponerse en el navegador — la seguridad real la da la
  Row Level Security de la base de datos, no el secreto de esa clave.

## Verificado

Probado de extremo a extremo con Playwright contra un backend simulado que
respeta el contrato real de la API de Supabase (signup, alta de tienda,
alta de cliente automática al crear un pedido, búsqueda en AniList, marcar
como llegado). No se ha podido probar contra el proyecto Supabase real
*desde este entorno* porque tiene bloqueado el acceso saliente a
`supabase.co` — pruébalo tú en el enlace desplegado para confirmarlo con el
backend de verdad.

## Siguientes pasos sugeridos

1. Probar el enlace desplegado de verdad: registrarte, crear tu tienda,
   añadir un pedido de prueba.
2. Decidir si quieres notificaciones al cliente y por qué canal (email es lo
   más simple de montar sin coste; SMS/WhatsApp tienen coste por mensaje).
3. Decidir el modelo de precio si esto se va a vender a otras tiendas
   (mensual por tienda es lo habitual en SaaS B2B pequeños).
