
# Analizar un escenario de seguridad

1. **¿Cuáles son los principales riesgos?**Prácticamente todos los puntos vulnerables están presentes, dejando la información confidencial totalmente descubierta y accesible para cualquier atacante o personal sin autorización.
2. **¿Qué mecanismo utilizarías para cada elemento?**

   - **Nombre y correo:** Control de acceso basado en roles y permisos estrictos.
   - **Contraseña:** Hash seguro mediante algoritmos robustos como bcrypt o Argon2.
   - **RFC:** Cifrado simétrico a nivel de columna.
   - **Información financiera:** Cifrado de datos y políticas estrictas de acceso.
   - **Claves criptográficas:** Uso de un gestor de secretos externo.
   - **Conexiones:** Protocolo TLS con validación completa del servidor.
   - **Respaldos:** Cifrado de copias y almacenamiento restringido.
3. **¿Cuál de los problemas consideras más crítico y por qué?**Guardar las contraseñas en texto claro, debido a que si se vulnera el sistema o se extrae la tabla, cualquier persona puede obtener las claves de inmediato y comprometer las cuentas de los usuarios.
4. **¿Tener correctamente configurados los usuarios y permisos elimina estos riesgos?**
   Solo de forma parcial, ya que no resuelven la falta de cifrado en reposo ni protegen los datos frente a una extracción directa del almacenamiento o por un manejo deficiente de las llaves criptográficas.
