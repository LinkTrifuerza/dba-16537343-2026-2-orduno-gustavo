## 1-¿Significa que tener los datos nos da permiso para usarlos en lo que sea?

Que ya tengamos guardados los datos del cliente para darle el servicio no significa que podamos usarlos para lo que queramos. Si nos dieron su correo o teléfono para darle soporte o enviarle sus compras, no podemos simplemente meterlos a una campaña de publicidad o crearle un perfil comercial sin avisarle antes y pedirle su permiso.

## 2-¿Qué preguntas debemos hacernos antes de implementar campañas?

Antes de que el equipo de marketing toque esos datos, hay que revisar:

* ¿En el aviso de privacidad original les dijimos que los usaríamos para publicidad?
* ¿Le dimos al usuario una opción clara para decir "no quiero que me manden publicidad"?
* ¿De verdad necesitamos ver quién es la persona o podemos hacer la campaña usando puros grupos o datos anónimos?

## 3-¿Qué datos serían realmente necesarios?

Para personalizar la publicidad no hace falta mostrarle toda la base de datos a marketing.

* **Lo que sí se necesita:** Historial de compras, qué tipo de cosas le interesan y un código anónimo para identificarlo.
* **Lo que NO deben ver:** RFC, dirección de su casa, teléfono personal o datos de control interno.

## 4-¿Cómo debe ser el acceso para el área de marketing?

El equipo de marketing nunca debe tener acceso directo a las tablas principales con los datos reales del cliente. Solo deben trabajar con vistas modificadas o bases de datos donde los nombres y correos se hayan ocultado o cambiado por códigos.

## 5-¿Qué medidas de protección y control debemos aplicar?

Para evitar fugas o malos usos al hacer campañas:

* Usar enlaces o códigos temporales para no exponer la lista completa de clientes.
* Ponerle contraseña y permisos estrictos a los reportes que use marketing.
* Borrar las listas de contactos temporales en cuanto termine la campaña.
