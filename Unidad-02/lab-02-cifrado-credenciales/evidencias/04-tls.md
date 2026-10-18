
# Protección de datos durante la comunicación

1. **¿La conexión actual utiliza TLS?**Depende del valor devuelto por el parámetro ssl en la consulta: si arroja verdadero indica que la sesión está protegida, mientras que si arroja falso significa que se realiza en texto plano.
2. **¿Qué versión de TLS se está utilizando?**Corresponde exactamente al protocolo indicado dentro de la columna version.
3. **¿Qué algoritmo de cifrado aparece?**Es el conjunto de protocolos criptográficos que se detalla explícitamente en la columna cipher.
4. **¿Qué diferencia existe entre una conexión protegida con TLS y una sin TLS?**
   Mediante TLS, toda la información que viaja por la red se cifra de extremo a extremo, previniendo la intercepción o lectura maliciosa. En cambio, sin TLS, los datos transitan de forma completamente legible, quedando vulnerables ante cualquier intento de espionaje en el trayecto.
