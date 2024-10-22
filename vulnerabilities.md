# Reporte de vulnerabilidades

## Resumen
- Vulnerabilidades encontradas en total: 5
- Criticas: 0
- Alta: 3
- Media: 2
- Baja: 0

## Detalles de las vulnerabilidades
### 1. Aplicación firmada con certificado de depuración.
- *Descripcion:* Aplicación firmada con un certificado de depuración. La aplicación de producción no debe enviarse con un certificado de depuración.
- *Gravedad:* Alta
- *Impacto:* Las aplicaciones firmadas con este certificado no son seguras. Las tiendas de aplicaciones no aceptan una aplicación que esté firmada con un certificado de depuración.
- *Pasos de reproduccion:*
  1. Generar una clave de firma de producción.
  2. Crear o seleccionar un Key Store de producción.
  3. Verificar la firma de la aplicación mediante un comando como apksigner verify --verbose  print-certs app.apk.
  4. Construir el APK firmado.
- *Correcciones:*
  1. Firmar la aplicación con un certificado de producción antes de publicarla.
  2. Verificar que no se utilice el certificado de depuración al generar builds de producción.

### 2. La aplicación se puede instalar en una versión vulnerable de Android actualizada Android 7.0, [minSdk=24]
- *Descripcion:* Esta aplicación se puede instalar en una versión anterior de Android que tiene múltiples vulnerabilidades no corregidas. Estos dispositivos no recibirán actualizaciones de seguridad razonables de Google. Admite una versión de Android => 10, API 29 para recibir actualizaciones de seguridad razonables.
- *Gravedad:* Alta
- *Impacto:* Los usuarios están expuestos a posibles ataques de seguridad, comprometiendo sus datos.
- *Pasos de reproduccion:*
  1. Configurar minSdkVersion igual o menor a 24 en el archivo build.gradle.
  2. Construir y generar un APK con la configuración de minSdkVersion.
  3. Instalar el APK en un dispositivo con Android 7.0 (PI 24).
  4. Verificar las vulnerabildiades de seguridad conocidas para Android 7.0.
- *Correcciones:*
  1. Cambiar la versión mínima de SDK (minSdkVersion) a 29 o superior en el archivo build.gradle.
  2. Sersiorarse que las dependencias sean compatibles con la nueva configuración de SDK.
  3. Realizar pruebas en dispositivos con Android 10 (API 29) o superior para confirmar la seguridad y estabilidad de la aplicación.
