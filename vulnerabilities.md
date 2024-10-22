# Reporte de vulnerabilidades

## Resumen
- Vulnerabilidades encontradas en total: 6
- Criticas: 0
- Alta: 3
- Media: 3
- Baja: 0

## Detalles de las vulnerabilidades
### 1. Solicitud firmada con certificado de depuración
- *Descripcion:* Aplicación firmada con certificado de depuración. La aplicación de producción no debe enviarse con un certificado de depuración.
- *Gravedad:* Alta
- *Impacto:* Los certificados de depuración no deben utilizarse en aplicaciones de producción porque están diseñados para uso en desarrollo. Un atacante podría explotar esta vulnerabilidad para inyectar código malicioso o modificar la aplicación. 
- *Pasos de reproduccion:*
  1. Instalar la aplicación en un dispositivo o emulador.
  2. Navegar a la configuración del dispositivo y habilitar las opciones de desarrollador.
  3. Verificar la firma de la aplicación mediante un comando como apksigner verify --verbose --print-certs app.apk.
- *Correcciones:*
  1. Firmar la aplicación con un certificado de producción antes de publicarla.
  2. Verificar que no se utilice el certificado de depuración al generar builds de producción.
