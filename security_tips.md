# Security Tips 

## 1. Protección contra Ataques de Inyección SQL
- **Descripción:** Se han implementado consultas preparadas para evitar la concatenación directa de entradas del usuario en consultas SQL.
- **Cómo mejora la seguridad:** Esto previene que un atacante pueda inyectar código SQL malicioso en las consultas, protegiendo así la base de datos de accesos no autorizados y alteraciones.

## 2. Autenticación y Autorización Seguras
- **Descripción:** Se ha implementado el uso de OAuth 2.0 y JWT para manejar la autenticación de usuarios y la autorización basada en roles.
- **Cómo mejora la seguridad:** Esto asegura que solo los usuarios autenticados puedan acceder a recursos sensibles y que se apliquen políticas de acceso basadas en el rol del usuario, reduciendo el riesgo de accesos no autorizados.

## 3. Protección contra Ataques de Red (MITM)
- **Descripción:** Se ha habilitado HTTPS para todas las comunicaciones y se ha implementado HSTS para forzar el uso de conexiones seguras.
- **Cómo mejora la seguridad:** Esto protege los datos en tránsito contra ataques de intermediarios, asegurando que la información sensible no sea interceptada ni alterada durante su transmisión.
