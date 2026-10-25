
# Registro de Cambios 

## 1. Interfaces de escucha

- **Actual:** `listen_addresses = '*'`
- **Cambio:** Configurar `listen_addresses = 'localhost'`
- **Objetivo:** Evitar exposición a conexiones directas desde Internet.

## 2. TLS

- **Actual:** `ssl = off`
- **Cambio:** Activar `ssl = on` y cargar certificados SSL.
- **Objetivo:** Cifrar las conexiones para proteger contraseñas y datos.

## 3. Control de usuarios

- **Actual:** Separación de usuarios probada (`postgres`, `u_16537343_gustavo_orduno` y `analista_gustavo`).
- **Cambio:** Mantener el principio de menor privilegio.
- **Objetivo:** No usar la cuenta `postgres` en aplicaciones para evitar accesos no autorizados.
