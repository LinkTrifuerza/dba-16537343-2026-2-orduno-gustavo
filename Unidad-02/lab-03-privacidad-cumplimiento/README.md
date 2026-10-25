## 1. Introducción

Este laboratorio aborda el problema de la sobre-recolección, almacenamiento indefinido y acceso descontrolado a datos personales dentro de los sistemas de bases de datos. En las organizaciones es común acumular información por tiempo indefinido o dar accesos generales por facilidad operativa; sin embargo, esto genera vulnerabilidades graves, incumplimiento de leyes de privacidad y riesgos altos ante filtraciones de datos.

## 2. Inventario de Datos

Los datos identificados dentro de la plataforma se clasifican según su nivel de sensibilidad y función:

* **Datos de Identificación y Contacto :** nombre, correo, telefono.
* **Datos Fiscales y Contables :** rfc.
* **Datos Demográficos y Estadísticos :** edad, ciudad, codigo postal.

## 3. Finalidades

Cada dato recolectado debe responder a un propósito operativo o legal específico:

* nombre, correo, telefono : Identificación del usuario, autenticación en la cuenta y soporte técnico.
* rfc : Emisión de comprobantes fiscales y cumplimiento de obligaciones ante la autoridad tributaria.
* edad, ciudad, codigo postal : Análisis estadístico de la audiencia, logística de entregas y estimación de cobertura.

## 4. Minimización

* **Datos a limitar o eliminar:** Campos como edad u ocupacion en el registro inicial no deben ser obligatorios si no afectan el servicio principal.
* **Justificación:** La minimización dicta que solo debemos pedir lo estrictamente necesario, en la zona de analítica, se eliminen los datos identificables directos dejando únicamente datos agregados o anónimos.

## 5. Control de Acceso

Los permisos se estructuraron bajo el principio de menor privilegio:

* **Atención al cliente:** Acceso limitado a datos de contacto para brindar soporte.
* **Facturación:** Acceso exclusivo a datos fiscales e historial de pagos.
* **Analítica:** Acceso restringido a datos anónimos o agregados.
* **DBA:** Control técnico de infraestructura sin necesidad de consultar datos personales en texto plano.
* **Dirección:** Vista de reportes consolidados sin acceso a la base operativa cliente por cliente.

## 6. Derechos ARCO

Técnicamente, atender las solicitudes de Acceso, Rectificación, Cancelación u Oposición (ARCO) implica:

* Tener identificadas todas las tablas y réplicas donde se almacena la información del usuario.
* Diseñar scripts seguros para la eliminación definitiva o anonimización sin romper la integridad referencial de la base de datos.
* Mantener un registro o bitácora de la solicitud realizada sin conservar los datos cancelados.

## 7. Retención

El periodo de conservación se determina considerando tres factores:

1. **Requerimientos legales:** Plazos obligatorios por ley.
2. **Duración de la relación contractual:** El tiempo en que la cuenta permanezca activa.
3. **Plazos de prescripción legal:** Un periodo prudente tras la cancelación para responder a posibles aclaraciones o reclamaciones antes del borrado definitivo.

## 8. Gobierno de Datos

| Rol                                                    | Responsabilidad Principal en el Gobierno de Datos                                       |
| :----------------------------------------------------- | :-------------------------------------------------------------------------------------- |
| **Propietario del Dato (Negocio)**               | Define la finalidad de la información y aprueba quién puede acceder a ella.           |
| **Responsable de Privacidad / Oficial de Datos** | Vela por el cumplimiento de las normativas legales y gestiona las solicitudes ARCO.     |
| **Área Jurídica**                              | Establece los plazos de retención legal y evalúa los riesgos normativos.              |
| **DBA (Administrador de BD)**                    | Implementa físicamente los controles de seguridad, cifrado, roles y tareas de borrado. |

## 9. Evaluación Integral

Los principales riesgos identificados en el escenario analizado fueron:

1. Acceso directo del personal de analítica a datos identificables de 50,000 clientes.
2. Conservación de información por más de 12 años sin una política formal de retención.
3. Uso de bases de datos con información real de clientes en entornos de prueba y desarrollo.
4. Uso de correos para campañas promocionales sin el consentimiento previo del usuario.
5. Ausencia de trazabilidad o bitácoras sobre quién consulta la tabla principal de clientes.

## 10. Conclusiones

La privacidad no es un parche que se agrega al final, sino una decisión de diseño que debe integrarse desde el modelado de la base de datos. Una base de datos bien administrada no solo protege la información contra ciberataques, sino que garantiza que solo se use para lo acordado, por el personal autorizado y durante el tiempo justo.

---

## Preguntas de Reflexión

### 1. ¿Una base de datos técnicamente segura necesariamente cumple con todos los requisitos de privacidad?

No, la seguridad garantiza la confidencialidad pero la privacidad va más allá como por ejemplo si tenemos derecho a tener esos datos, si el usuario dio su consentimiento, si se usan solo para la finalidad acordada y si se borran a tiempo, una base de datos súper encriptada y con firewall puede estar violando la privacidad si conserva datos ilegales o innecesarios.

### 2. ¿Por qué el principio de mínimo privilegio también contribuye a la privacidad?

Porque al limitar el acceso de cada empleado se reduce el riesgo de que alguien dentro del equipo filtre informacion sensible.

### 3. ¿Por qué el DBA no debería decidir por sí solo la finalidad del tratamiento de los datos?

Porque la función del DBA es técnica, osea asegurarse de que todo funcione correctamente, las finalidades corresponden al área de negocio, privacidad, legal etc, quienes conocen los contratos y las leyes.

### 4. ¿Por qué los desarrolladores no deberían recibir automáticamente copias completas de bases de datos productivas?

Porque los entornos de desarrollo tienen niveles de seguridad mucho más bajos que los de producción. Darles copias reales expone información sensible de miles de clientes en laptops o servidores de prueba vulnerables a extravíos o ataques.

### 5. ¿Por qué una copia utilizada para desarrollo también puede representar un riesgo de privacidad?

Porque aunque esté en un servidor interno de pruebas, sigue conteniendo datos personales reales. Si ese entorno sufre una filtración, la empresa es exactamente igual de responsable legal y operativamente que si hubieran hackeado el sistema de producción.

### 6. ¿Por qué la retención debe formar parte del ciclo de vida de los datos?

Porque los datos no deben vivir para siempre en el sistema. Definir una etapa de retención asegura que la información pase de una zona activa a un archivo o borrado definitivo, reduciendo los costos de almacenamiento y los riesgos legales.

### 7. ¿Qué relación existe entre privacidad por diseño y diseño de bases de datos?

Que la privacidad debe influir directamente desde que se crean las tablas, relaciones y esquemas. Implica normalizar y segmentar campos sensibles, definir permisos por columna o vista, e incluir desde el principio atributos para gestionar fechas de caducidad o estado de consentimiento.

### 8. ¿Qué controles técnicos implementarías para reducir el riesgo de exposición de datos personales?

* Enmascaramiento de datos en pantalla para roles de soporte.
* Vistas anonimizadas para reportes y analítica.
* Cifrado en reposo para columnas sensibles.
* Generación de datos sintéticos (ficticios) para pruebas de desarrollo.
* Activación de bitácoras de auditoría (*logs*) inalterables.

### 9. ¿Qué información debería conocer un DBA para responder técnicamente a una solicitud ARCO?

Debe saber exactamente en qué tablas, vistas, réplicas y respaldos se encuentra el ID o dato del usuario, cuáles son las dependencias o llaves foráneas asociadas, y qué procedimiento aplicar (borrado directo o anonimización) sin corromper la base de datos.

### 10. ¿Qué responsabilidades deberían corresponder al DBA, al responsable de privacidad, al área jurídica y al propietario de los datos?

* **DBA:** Ejecutar las configuraciones técnicas de seguridad, vistas, respaldos y scripts de depuración.
* **Responsable de Privacidad:** Supervisar el cumplimiento normativo, gestionar las solicitudes ARCO y actualizar avisos de privacidad.
* **Área Jurídica:** Definir el marco legal de retención y defender a la empresa en caso de auditorías o litigios.
* **Propietario de los datos (Negocio):** Justificar la necesidad operativa de cada dato recopilado y autorizar qué roles de la empresa los consultan.
