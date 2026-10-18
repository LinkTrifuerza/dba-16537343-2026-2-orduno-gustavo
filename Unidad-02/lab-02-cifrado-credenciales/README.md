
## 1. Introducción

En este laboratorio se abordaron los problemas de seguridad relacionados con la exposición no autorizada de datos sensibles, el almacenamiento inadecuado de contraseñas en texto plano, la interceptación de tráfico en la red y la falta de políticas en la administración de llaves criptográficas dentro de un sistema gestor de bases de datos.

---

## 2. Protección de credenciales

- Texto claro: La información se guarda sin ningún tipo de protección, lo que permite que cualquier persona con acceso de lectura vea las claves directamente.
- Hash: Es un proceso unidireccional no reversible que transforma una entrada en una cadena fija, utilizado para validar claves sin guardarlas de forma explícita.
- Cifrado: Es un proceso bidireccional que altera los datos para que solo sean legibles utilizando una llave específica para su posterior descifrado.

---

## 3. Protección de datos sensibles

Se protegió el registro del RFC mediante cifrado simétrico con la extensión pgcrypto. La razón principal es que este tipo de información personal debe mantenerse restringida en reposo para cumplir con normativas de privacidad, asegurando al mismo tiempo que las aplicaciones autorizadas puedan recuperar el dato original mediante la llave correspondiente.

---

## 4. TLS

El protocolo TLS resuelve el problema del espionaje e interceptación de datos mientras transitan entre el cliente y el servidor en la red. En PostgreSQL se verificó la sesión actual mediante consultas a las vistas del sistema, validando el estado del parámetro ssl, la versión activa del protocolo y el algoritmo de cifrado aplicado a la conexión.

---

## 5. Gestión de claves

Las llaves criptográficas nunca deben almacenarse dentro de los scripts de la base de datos o en el código fuente. Hacerlo expone la llave a cualquier usuario o proceso con acceso al historial de consultas, archivos de registro o repositorios de código, lo que anula por completo la efectividad del cifrado.

---

## 6. Resultados

Se logró configurar el hashing de contraseñas con sal usando crypt y gen_salt, implementar el cifrado y descifrado de columnas específicas mediante pgp_sym_encrypt y pgp_sym_decrypt, validar el uso de conexiones cifradas TLS en el servidor y establecer directrices para la administración segura de secretos.

---

## 7. Problemas encontrados

Durante la ejecución se presentaron errores de sintaxis al probar funciones criptográficas por falta de habilitación previa del módulo pgcrypto en la base de datos de trabajo, lo cual se resolvió ejecutando la sentencia CREATE EXTENSION correspondiente.

---

## 8. Conclusiones

Se comprendió que la seguridad en bases de datos requiere un enfoque en capas donde el cifrado, el control de acceso y las conexiones seguras se complementan. En un entorno de producción aplicaría la integración de un gestor de secretos independiente, el uso obligatorio de conexiones cifradas TLS y la implementación de hashes robustos para la autenticación de usuarios.

---

## Preguntas de reflexión

### 1. ¿Por qué una contraseña no debe almacenarse como texto claro?

Porque si la base de datos o sus respaldos sufren una filtración, las contraseñas quedan totalmente expuestas para ser utilizadas por atacantes.

### 2. ¿Por qué un hash no es equivalente a un cifrado?

Porque el hash es una función unidireccional no reversible pensada para validar datos, mientras que el cifrado es bidireccional y permite recuperar el texto original con la llave correcta.

### 3. ¿Por qué el cifrado de una columna no sustituye al control de acceso?

Porque el cifrado protege los datos contra la extracción física del almacenamiento, mientras que el control de acceso limita qué usuarios autorizados dentro de la base de datos pueden ejecutar acciones o consultar información.

### 4. ¿Por qué TLS no sustituye a los mecanismos de autorización de PostgreSQL?

Porque TLS solo asegura que los datos no sean leídos o alterados mientras viajan por la red, pero no gestiona los permisos ni la identidad de los usuarios dentro del motor de la base de datos.

### 5. ¿Qué ocurriría si una organización pierde una clave utilizada para cifrar información?

Los datos cifrados con esa llave quedarían irrecuperables de forma permanente, provocando una pérdida definitiva de información.

### 6. ¿Qué ocurriría si una clave criptográfica se publica accidentalmente en GitLab?

La llave debe considerarse comprometida de inmediato, ya que cualquier persona con acceso al repositorio podría descifrar la información protegida que coincida con esa clave.

### 7. ¿Por qué un repositorio privado no debe considerarse un almacén de secretos?

Porque los repositorios guardan un historial permanente de cambios, son clonados en múltiples dispositivos y tienen permisos de lectura compartidos que aumentan el riesgo de filtración.

### 8. ¿Qué diferencia existe entre proteger información almacenada y proteger información durante su transmisión?

Proteger información almacenada previene la lectura en disco o base de datos ante una copia física o filtración, mientras que proteger la transmisión impide que la información sea interceptada o leída al viajar por la red.

### 9. ¿Por qué la gestión de claves es tan importante como el algoritmo criptográfico?

Porque por más fuerte que sea un algoritmo criptográfico, si la llave es expuesta, robada o almacenada de forma inadecuada, el mecanismo de protección se rompe de inmediato.

### 10. ¿Qué mecanismo adicional implementarías en una organización para proteger los respaldos de las bases de datos?

Implementaría el cifrado automático de los archivos de respaldo antes de transferirlos a ubicaciones secundarias y restringiría su almacenamiento a servidores aislados con control de acceso estricto.
