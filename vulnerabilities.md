# Reporte de vulnerabilidades

## Resumen
- Vulnerabilidades encontradas en total: 5
- Criticas: 0
- Alta: 3
- Media: 2
- Baja: 0

## Detalles de las vulnerabilidades
### 1. Aplicación firmada con certificado de depuración.
- **Descripción:** Aplicación firmada con un certificado de depuración. La aplicación de producción no debe enviarse con un certificado de depuración.
- **Gravedad:** Alta
- **Impacto:** Las aplicaciones firmadas con este certificado no son seguras. Las tiendas de aplicaciones no aceptan una aplicación que esté firmada con un certificado de depuración.
- **Pasos de reproducción:**
  1. Generar una clave de firma de producción.
  2. Crear o seleccionar un Key Store de producción.
  3. Verificar la firma de la aplicación mediante un comando como apksigner verify --verbose  print-certs app.apk.
  4. Construir el APK firmado.
- **Correcciones:**
  1. Firmar la aplicación con un certificado de producción antes de publicarla.
  2. Verificar que no se utilice el certificado de depuración al generar builds de producción.

### 2. La aplicación se puede instalar en una versión vulnerable de Android actualizada Android 7.0, [minSdk=24]
- **Descripción:** Esta aplicación se puede instalar en una versión anterior de Android que tiene múltiples vulnerabilidades no corregidas. Estos dispositivos no recibirán actualizaciones de seguridad razonables de Google. Admite una versión de Android => 10, API 29 para recibir actualizaciones de seguridad razonables.
- **Gravedad:** Alta
- **Impacto:** Los usuarios están expuestos a posibles ataques de seguridad, comprometiendo sus datos.
- **Pasos de reproducción:**
  1. Configurar minSdkVersion igual o menor a 24 en el archivo build.gradle.
  2. Construir y generar un APK con la configuración de minSdkVersion.
  3. Instalar el APK en un dispositivo con Android 7.0 (PI 24).
  4. Verificar las vulnerabildiades de seguridad conocidas para Android 7.0.
- **Correcciones:**
  1. Cambiar la versión mínima de SDK (minSdkVersion) a 29 o superior en el archivo build.gradle.
  2. Sersiorarse que las dependencias sean compatibles con la nueva configuración de SDK.
  3. Realizar pruebas en dispositivos con Android 10 (API 29) o superior para confirmar la seguridad y estabilidad de la aplicación.

### 3. Depuración habilitada para la aplicación [Android: depurable = verdadero]
- **Descripción:** La depuración se habilitó en la aplicación, lo que facilita a los ingenieros inversos conectarle un depurador. Esto permite volcar un seguimiento de la pila y acceder a clases auxiliares de depuración.
- **Gravedad:** Alta
- **Impacto:** Al estar habilitada la depuración, se vuelve vulnerable y puede ser víctima de ataques. Representa un riesgo para la privacidad de los usuarios.
- **Pasos de reproducción:**
  1. Verificar que android:debuggable esté configurado en true en el archivo AndroidManifest.xml.
  2. Construir el APK y ejecutarlo en un dispositivo.
  3. Conectar un depurador al dispositivo.
  4. Realizar la ingeniería inversa y rastreo de la aplicación.
- **Correcciones:**
  1. Desactivar la depuración en el archivo AndroidManifest.xml.
  2. Revisar el archivo build.gradle.

### 4. Se puede realizar una copia de seguridad de los datos de la aplicación [android:allowBackup=true]
- **Descripción:** Esta bandera permite a cualquiera hacer una copia de seguridad de los datos de su aplicación a través de adb. Permite a los usuarios que han habilitado la depuración USB copiar datos de la aplicación fuera del dispositivo.
- **Gravedad:** Medium
- **Impacto:** Al estar habilitada, los usuarios pueden extraer datos confidenciales de la aplicación y cualquier dato que pueda comprometer la seguridad del usuario.
- **Pasos de reproducción:**
  1. Verificar que android:allowBackup esté configurado en true en el archivo AndroidManifest.xml.
  2. Habilitar la depuración USB en un dispositivo.
  3. Conectar el dispositivo a una máquina con adb instalado.
  4. Ejecutar el comando de copia de seguridad de la aplicación.
  5. Restaurar la copia de seguridad en otro dispositivo.
- **Correcciones:**
  1. Deshabilitar la copia de seguridad en el archivo AndroidManifest.xml.
  2. Probar la aplicación con la configuración corregida.

### 5. Broadcast Receiver (androidx.profileinstaller.ProfileInstallReceiver) está protegido por un permiso, pero se debe verificar el nivel de protección del permiso. Permiso: android.permission.DUMP [android: exportado = verdadero]
- **Descripción:** Se descubre que un receptor de transmisión se comparte con otras aplicaciones en el dispositivo, por lo que es accesible para cualquier otra aplicación en el dispositivo. Está protegido por un permiso que no está definido en la aplicación analizada. Como resultado, se debe verificar el nivel de protección del permiso donde está definido. Si se configura como normal o peligroso, una aplicación maliciosa puede solicitar y obtener el permiso e interactuar con el componente. Si está configurado en firma, sólo las aplicaciones firmadas con el mismo certificado pueden obtener el permiso.
- **Gravedad:** Medium
- *Impacto:* Si el nivel del permiso es bajo, se puede ser víctima de ataques de tipo man-in-the-middle, o ejecutar código no autorizado.
- **Pasos de reproducción:**
  1. Verificar que el Broadcast Receiver esté configurado con android:exported=true.
  2. Verificar el nivel de protección del permiso android.permission.DUMP.
  3. Instalar una aplicación maliciosa en el dispositivo.
  4. Interceptar o manipular la transmisión.
- **Correcciones:**
  1. Verificar el nivel de protección del permiso.
  2. Cambiar android:exported a false si el receptor no necesita ser accesible externamente.
  3. Revisar y restringir los permisos de la aplicación.

Volver [Detalles ](Detalles.md)
