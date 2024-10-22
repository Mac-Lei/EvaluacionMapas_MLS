# Reporte de vulnerabilidades

## Resumen
- Vulnerabilidades encontradas en total: 5
- Criticas: 0
- Alta: 3
- Media: 2
- Baja: 0

## Detalles de las vulnerabilidades
### 1. Aplicación firmada con certificado de depuración.
- *Descripcion:* 
Aplicación firmada con un certificado de depuración. La aplicación de producción no debe enviarse con un certificado de depuración.
- *Gravedad:* Alta
- *Impacto:* Las aplicaciones firmadas con este certificado no son seguras. Las tiendas de aplicaciones no aceptan una aplicación que esté firmada con un certificado de depuración.
- *Pasos de reproduccion:*
  1. Generar una clave de firma d eproducción.
  2. Crear o seleccionar un Key Store de producción.
  3. Verificar la firma de la aplicación mediante un comando como apksigner verify --verbose  print-certs app.apk.
  4. Construir el APK firmado.
- *Correcciones:*
  1. Firmar la aplicación con un certificado de producción antes de publicarla.
  2. Verificar que no se utilice el certificado de depuración al generar builds de producción.

