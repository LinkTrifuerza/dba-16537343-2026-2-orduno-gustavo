
# Cuestionario de Hardening

1. ¿Cuál era la principal superficie de ataque?
   El puerto 5432 abierto a todas las interfaces sin cifrado TLS activado.
2. ¿Qué configuración representaba el mayor riesgo?
   Que listen_addresses estuviera configurado en todas las interfaces combinado con el cifrado TLS apagado, exponiendo datos y credenciales en texto plano.
3. ¿Qué cambio produjo la mayor reducción de exposición?
   Limitar las interfaces de escucha a localhost y activar el cifrado TLS.
4. ¿Qué diferencia existe entre firewall y pg_hba.conf?
   El firewall filtra a nivel de red y sistema operativo bloqueando conexiones antes de llegar, mientras que pg_hba.conf controla el acceso a nivel de base de datos especificando quién puede conectarse a qué base de datos.
5. ¿Qué diferencia existe entre autenticación y autorización?
   La autenticación verifica quién eres mediante credenciales, y la autorización determina qué puedes hacer mediante roles y permisos.
6. ¿Por qué una cuenta de aplicación no debe ser SUPERUSER?
   Porque si la aplicación sufre una vulnerabilidad, el atacante tomaría control total del motor de base de datos y del sistema operativo.
7. ¿Por qué cambiar el puerto de PostgreSQL no constituye hardening suficiente?
   Porque se basa en ocultación y un simple escaneo de puertos detectará el puerto nuevo de inmediato si las interfaces y credenciales siguen vulnerables.
8. ¿Por qué listen_addresses con asterisco puede ser innecesario?
   Porque la mayoría de las aplicaciones se conectan localmente o desde una dirección específica, por lo que permitir conexiones desde cualquier interfaz expone el servicio sin necesidad.
9. ¿Qué papel tiene el sistema operativo en la seguridad de PostgreSQL?
   Administra los permisos de los archivos de configuración, los registros del sistema, el cortafuegos y los recursos asignados al proceso del gestor.
10. ¿Qué controles deberían revisarse periódicamente?
    Los permisos de los usuarios y roles, los registros de acceso en el archivo de configuración de red, la vigencia de certificados y las actualizaciones de seguridad del motor.
