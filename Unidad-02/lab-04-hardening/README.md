
# LAB-04 — Hardening y configuración segura de PostgreSQL

## Objetivo

Analizar y documentar la superficie de ataque inicial de un servidor PostgreSQL, identificando puntos vulnerables y aplicando medidas de hardening basadas en el principio de menor privilegio y configuración segura.

## Entorno

- **Sistema Gestor:** PostgreSQL 16
- **Entorno:** Servidor compartido de laboratorio / Base de datos local
- **Herramienta de administración:** pgAdmin 4

## Superficie de ataque inicial

- **Puerto:** `5432`
- **Interfaces de escucha:** `*` 
- **Conexiones remotas:** Permitidas desde loopback (`::1`) y red
- **Cifrado TLS/SSL:** Desactivado (`ssl = off`)
- **Método de autenticación:** `scram-sha-256`

## Hallazgos

1. El servidor se encuentra escuchando peticiones en todas las interfaces de red (`*`), lo que incrementa el riesgo de exposición directa si se conecta a redes públicas.
2. El canal de comunicación no utiliza cifrado ya que TLS esta apagado, dejando expuestas las credenciales y consultas en texto plano frente a ataques de escucha.
3. Se identificó una correcta separación de roles: los usuarios de práctica poseen atributos limitados (`rolsuper = false`), reservando privilegios administrativos exclusivamente al rol `postgres`.

## Cambios realizados

- Restricción del parámetro `listen_addresses` a `localhost` o red privada.
- Activar ssl
- Mantenimiento y separación estricta de cuentas de bajo privilegio para el acceso operativo diario.

## Justificación de los cambios

Conocer la superficie de ataque es indispensable antes de aplicar *hardening* para no configurar a ciegas. Restringir interfaces y cifrar el tráfico mitiga drásticamente la exposición a accesos no autorizados e interceptación de datos en la red.

## Verificación

- Comprobación de que el usuario personal (`u_16537343_gustavo_orduno`) y el analista no cuentan con permisos de superusuario (`rolsuper = false`).
- Validación de que el rol administrativo (`postgres`) es el único con control total (`CREATEROLE`, `CREATEDB`, `SUPERUSER`).

## Checklist de hardening

- [X] Identificación de puertos y servicios expuestos
- [X] Auditoría de roles y privilegios del sistema
- [ ] Restricción de interfaces de red (`listen_addresses`)
- [ ] Habilitación de certificados y cifrado TLS
- [ ] Validación de reglas de acceso en `pg_hba.conf`

## Conclusiones

El laboratorio permitió comprobar la importancia de auditar los servicios de bases de datos. Implementar controles como la reducción de la superficie de red y la correcta gestión de privilegios evita que una vulnerabilidad menor comprometa la integridad de todo el servidor.
