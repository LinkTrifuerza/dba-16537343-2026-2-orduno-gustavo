
# Propuesta de baseline de seguridad para PostgreSQL 16

Red

* Interfaces autorizadas: localhost o IP privada específica
* Puerto: 5432 o un puerto personalizado alternativo de gestión
* Firewall: reglas explícitas de filtrado a nivel de sistema operativo bloqueando acceso público directo
* Redes permitidas: rangos específicos de subred autorizados para la conexión legítima

Autenticación

* Método: scram-sha-256 obligatorio para almacenamiento cifrado de credenciales
* Políticas de credenciales: longitudes mínimas y rotación periódica obligatoria de contraseñas
* Cuentas administrativas: exclusividad de la cuenta postgres con uso restringido

Autorización

* Roles: separación estricta entre roles de sistema, analistas y administración
* Privilegios: aplicación estricta del principio de menor privilegio sin atributos globales innecesarios
* Cuentas de aplicación: usuarios operativos específicos sin permisos de superusuario ni creación de objetos globales

Configuración

* Parámetros relevantes: ajuste de logging, límites de conexiones concurrentes y tiempos de inactividad
* Extensiones: control y restricción de instalación de extensiones no autorizadas
* Conexiones: control estricto de accesos mediante el archivo de control de red

Sistema operativo

* Propietario de archivos: usuario y grupo exclusivo postgres para los procesos y datos
* Permisos: restricciones estrictas de lectura y escritura en los directorios del sistema de archivos
* Protección del directorio de datos: permisos 700 en directorios sensibles y 600 en archivos de configuración críticos

Cifrado

* TLS: activación obligatoria de cifrado en tránsito para todas las conexiones de red
* Protección de credenciales: prohibición de almacenamiento en texto plano en archivos de configuración o código fuente
* Protección de información sensible: enmascaramiento o cifrado de datos críticos a nivel de aplicación o base de datos

Mantenimiento

* Actualización: aplicación oportuna de parches de seguridad y versiones estables del motor
* Revisión periódica: auditorías frecuentes de roles, permisos y registros de actividad
* Documentación: registro actualizado de configuraciones base, cambios y arquitectura de red
