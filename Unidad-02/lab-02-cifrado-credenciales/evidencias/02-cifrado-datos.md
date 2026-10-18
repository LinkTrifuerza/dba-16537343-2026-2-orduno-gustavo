
# Cifrado de información sensible

1. **¿Qué diferencia existe entre crypt() y pgp_sym_encrypt()?**`crypt()` se emplea para aplicar funciones de hash unidireccionales orientadas al almacenamiento seguro de contraseñas, donde la información no debe ser recuperada. Por el contrario, `pgp_sym_encrypt()` realiza un cifrado simétrico bidireccional, lo que permite transformar un dato sensible y desencriptarlo posteriormente cuando sea requerido.
2. **¿Cuál de los dos mecanismos permite recuperar el dato original?**`pgp_sym_encrypt()`, ya que está diseñado para revertir el proceso de cifrado utilizando la llave secreta correspondiente.
3. **¿Qué ocurre si se utiliza una clave incorrecta?**El sistema arroja un error al intentar el descifrado, debido a que la llave proporcionada no coincide con la que se usó originalmente para proteger el contenido.
4. **¿Qué problema de seguridad representa colocar la clave directamente en una consulta?**
   Deja la clave expuesta a la vista de cualquier persona o proceso con acceso al historial de la base de datos, a las auditorías o a los registros de transacciones (*logs*), lo que comprometería por completo la protección de los datos cifrados.
