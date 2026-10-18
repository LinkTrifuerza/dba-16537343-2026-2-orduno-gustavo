
# Informe del Laboratorio 1

## 19.1 Clasificación

Los datos que requieren protección son aquellos de carácter personal, confidencial o financiero, tales como nombres completos, registros federales de contribuyentes, correos electrónicos y detalles bancarios. Esto se debe a que su exposición indebida puede vulnerar la privacidad de los usuarios, facilitar el robo de identidad o incumplir con normativas de protección de datos.

## 19.2 Enmascaramiento

- Qué se ocultó: Se ocultaron parcial o totalmente caracteres sensibles como dígitos de tarjetas o fragmentos de contraseñas.
- Para quién: Para usuarios o roles que no necesitan visualizar el dato completo en su operación diaria.
- Por qué: Para prevenir la visualización innecesaria de información crítica en pantallas o reportes visuales.
- Qué mecanismo se utilizó: Funciones de truncamiento o sustitución de caracteres por símbolos comodín como asteriscos.

## 19.3 Seudonimización

- Cómo se generaron los tokens: Mediante funciones hash o identificadores únicos aleatorios que reemplazan los datos directos de identidad.
- Dónde se encuentra el mapa de correspondencia: En una tabla o base de datos auxiliar altamente restringida e independiente de los datos operativos.
- Quién debería poder acceder a él: Exclusivamente el personal con privilegios administrativos muy elevados y justificados.
- Por qué se separaron los permisos: Para evitar que un atacante o usuario interno con acceso a los datos seudonimizados pueda correlacionarlos directamente con la identidad real de las personas.

## 19.4 Anonimización

- Qué identificadores fueron eliminados: Nombres, números de teléfono, correos y cualquier dato de contacto directo.
- Qué atributos fueron generalizados: Rangos de edad o zonas geográficas amplias en lugar de fechas exactas o ubicaciones precisas.
- Qué grupos fueron suprimidos: Aquellos registros con características únicas que permitieran cruzar información para aislar a un individuo específico.
- Qué riesgo de reidentificación permanece: El riesgo de inferencia mediante el cruce de datos con fuentes externas o cuasi-identificadores restantes.

## 19.5 Retención

- Qué criterio se utilizó: El tiempo estrictamente necesario según necesidades operativas, contractuales o exigencias legales.
- Qué información debería conservarse: Aquellos registros obligatorios para auditorías, obligaciones fiscales o transacciones vigentes.
- Qué información podría eliminarse: Datos obsoletos, registros temporales o información de usuarios inactivos cuyo plazo legal haya expirado.
- Qué controles deberían existir antes de eliminarla: Autorizaciones formales, respaldos seguros y verificaciones de que ningún proceso activo dependa de dichos registros.

## 19.6 Conclusiones

- ¿Qué técnica utilizarías para un área de soporte? Enmascaramiento, para que puedan identificar al cliente de forma visual sin ver datos completos o sensibles.
- ¿Qué técnica utilizarías para un área de analítica? Seudonimización, permitiendo estudiar patrones de comportamiento sin comprometer identidades reales.
- ¿Qué técnica utilizarías para publicar estadísticas? Anonimización total, asegurando que ningún individuo pueda ser rastreado o reidentificado.
- ¿Por qué ninguna de estas técnicas sustituye al control de acceso? Porque operan sobre la forma o disponibilidad del dato, pero no administran los permisos ni la autenticación de quiénes pueden interactuar con los sistemas.

---

## 20. Preguntas de reflexión

### 1. ¿Cuál es la diferencia entre enmascaramiento y seudonimización?

El enmascaramiento oculta visualmente una parte del dato para la interfaz, mientras que la seudonimización sustituye de manera sistemática un identificador por un token único vinculado a un mapa de claves externo.

### 2. ¿Por qué la seudonimización no significa anonimización?

Porque los datos seudonimizados siguen estando vinculados a una identidad real a través de un mapa o llave de correspondencia, permitiendo revertir el proceso, a diferencia de los datos anónimos.

### 3. ¿Por qué eliminar nombre y RFC no garantiza que un conjunto de datos sea anónimo?

Porque los atributos restantes o cuasi-identificadores pueden cruzarse con otras bases de datos públicas para deducir y aislar la identidad de una persona.

### 4. ¿Qué función tienen los cuasi-identificadores?

Son variables que por sí solas no identifican a una persona, pero al combinarse aumentan drásticamente el riesgo de reidentificación.

### 5. ¿Por qué es importante separar el mapa de seudonimización?

Para evitar que una filtración en el almacenamiento principal comprometa la correspondencia entre los tokens y las identidades reales de los usuarios.

### 6. ¿Qué principio de seguridad se aplica al impedir que el analista acceda al mapa?

El principio de menor privilegio y separación de funciones, limitando el acceso solo a lo estrictamente necesario para la tarea.

### 7. ¿Por qué una vista puede ser preferible a entregar acceso directo a la tabla?

Porque permite filtrar columnas sensibles, aplicar enmascaramientos al vuelo y otorgar acceso controlado sin exponer la estructura completa de la tabla base.

### 8. ¿Qué diferencia existe entre proteger un dato para visualización y protegerlo contra acceso no autorizado?

El primero modifica cómo se muestra el contenido en pantalla o reportes, mientras que el segundo bloquea la posibilidad de consultar, extraer o modificar la información a nivel de permisos de base de datos.

### 9. ¿Por qué la retención forma parte de la protección de datos?

Porque conservar información innecesaria incrementa la superficie de ataque y el impacto potencial ante una filtración de seguridad.

### 10. ¿Qué riesgo existe si una organización conserva información indefinidamente?

Se incrementa la vulnerabilidad ante robos masivos de datos históricos, además de posibles incumplimientos legales con normativas de privacidad vigentes.
