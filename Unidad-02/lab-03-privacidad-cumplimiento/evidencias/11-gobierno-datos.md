

| Dato                    | Finalidad                                              | Responsable | Usuarios autorizados                  | Protección                    | Retención                               | Acción al finalizar                 |
| :---------------------- | :----------------------------------------------------- | :---------- | :------------------------------------ | :----------------------------- | :--------------------------------------- | :----------------------------------- |
| **nombre**        | Identificación del usuario en la plataforma y soporte | Operaciones | Atención al cliente, Dirección, DBA | Encriptación en base de datos | Mientras la cuenta esté activa + 1 año | Borrado definitivo (*DELETE*)      |
| **correo**        | Comunicación oficial y acceso a la cuenta             | Operaciones | Atención al cliente, Dirección, DBA | Cifrado y control de accesos   | Mientras la cuenta esté activa + 1 año | Borrado definitivo (*DELETE*)      |
| **telefono**      | Contacto rápido y avisos de servicio                  | Operaciones | Atención al cliente, DBA             | Acceso restringido             | Mientras la cuenta esté activa + 1 año | Borrado definitivo (*DELETE*)      |
| **rfc**           | Emisión de facturas y cumplimiento fiscal             | Finanzas    | Facturación, DBA                     | Encriptación estricta         | 5 años                                  | Archivo histórico o borrado seguro  |
| **edad**          | Estadísticas de uso y demografía                     | Analítica  | Analítica, DBA                       | Datos anonimizados             | 2 años                                  | Anonimización irreversible          |
| **ciudad**        | Logística y personalización regional                 | Operaciones | Atención al cliente, Analítica, DBA | Protección estándar en BD    | 2 años                                  | Borrado o conversión a zona general |
| **codigo_postal** | Cálculo de costos de envío y cobertura               | Operaciones | Atención al cliente, Analítica, DBA | Protección estándar en BD    | 2 años                                  | Borrado definitivo o generalización |
