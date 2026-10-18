

# Resumen de mecanismos de seguridad

| Situación                                    | Mecanismo apropiado  | ¿Qué protege?                                                              |
| :-------------------------------------------- | :------------------- | :--------------------------------------------------------------------------- |
| Contraseña de usuario                        | Hash ( crypt() )     | Impide almacenar credenciales en formato legible                             |
| RFC almacenado en una tabla                   | Cifrado simétrico   | Resguarda la identificación fiscal asegurando su posterior desencriptación |
| Consulta enviada desde un cliente al servidor | TLS                  | Blinda la información mientras transita por la red                          |
| Respaldo de una base de datos                 | Cifrado de respaldos | Bloquea el acceso no autorizado al contenido de las copias de seguridad      |
| Clave criptográfica                          | Gestor de secretos   | Previene la filtración y el uso indebido de llaves maestras                 |
