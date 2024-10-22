# EvaluacionMapas_MLS
# Descripción
Este proyecto es una aplicación Android que implementa medidas de seguridad para proteger 
contra vulnerabilidades comunes. 

## Vulnerabilidades Identificadas
- Aplicación firmada con certificado de depuración
- La aplicación se puede instalar en una versión vulnerable de Android actualizada Android 7.0, [minSdk=24]
- Depuración habilitada para la aplicación [Android: depurable = verdadero]
- Se puede realizar una copia de seguridad de los datos de la aplicación [android:allowBackup=true]
- Broadcast Receiver (androidx.profileinstaller.ProfileInstallReceiver) está protegido por un permiso, pero se debe verificar el nivel de protección del permiso. Permiso: android.permission.DUMP [android: exportado = verdadero]   

## Mejoras Implementadas
- Cifrado de datos sensibles 
- Comunicación segura (HTTPS) 
- Validación y sanitización de entradas  

## Documentación
- [Vulnerabilidades](vulnerabilities.md) 
- [Best Practices](best_practices.md) 
- [Security Tips](security_tips.md) 
- [Security Improvement Program](security_improvement_program.md) 

## Cómo Ejecutar la Aplicación de Forma Segura
1. Clonar el repositorio 
2. Importar el proyecto en Android Studio 
3. Ejecutar la aplicación en un dispositivo o emulador 
4. Asegurarse de que los permisos necesarios están configurados 

## Reporte de Vulnerabilidades 
El reporte detallado de las pruebas de vulnerabilidad realizadas se encuentra en el archivo [vulnerability_report.pdf](vulnerability_report.pdf)

