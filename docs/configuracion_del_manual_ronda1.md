# Ronda 1. Preparar el proyecto

## Paso 1.1 Crear el proyecto
```
$ flutter create tienda_talavera
$ cd tienda_talavera
$ flutter pub add model_viewer_plus shared_preferences flutter_secure_storage crypto
```
Si el manual muestra una versión que ya no existe, "flutter pub add" siempre elige una compatible. Revisa pub.dev para confirmar que los paquetes siguen mantenidos.

```
📄 pubspec.yaml
name: tienda_talavera
description: Tienda de artesanías de Dolores Hidalgo con carrito, pagos, perfil y "Ver en tu espacio" (RA).
publish_to: none
version: 1.0.0

environment:
  sdk: ">=3.0.0 <4.0.0"

# Si "flutter pub get" se queja de una versión, borra la línea y ejecuta:
#   flutter pub add model_viewer_plus shared_preferences flutter_secure_storage crypto
dependencies:
  flutter:
    sdk: flutter
  model_viewer_plus: ^1.9.3
  shared_preferences: ^2.3.0
  flutter_secure_storage: ^9.2.2
  crypto: ^3.0.3

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0

flutter:
  uses-material-design: true
```

## Paso 1.2 Permisos para realidad aumentada
model_viewer_plus muestra el modelo dentro de un WebView. Para que funcione:

- Android: en android/app/src/main/AndroidManifest.xml agrega <uses-permission android:name="android.permission.INTERNET"/> y, dentro de <application>, android:usesCleartextTraffic="true" SOLO si pruebas con un servidor local (en producción usa https). El modo AR usa Scene Viewer, que requiere un teléfono compatible con ARCore y la app "Google Play Services for AR".
- iOS: AR Quick Look necesita un archivo .usdz. No requiere permisos especiales de cámara en Info.plist para el visor, pero si luego usas la cámara directamente agrega NSCameraUsageDescription.
- Android minSdkVersion: revisa en la documentación del paquete el mínimo vigente (históricamente 21 o superior).
⚠️ Cuidado

El simulador NO soporta AR real. Prueba "Ver en tu espacio" en un teléfono físico. El visor 3D sí se ve en el emulador, pero el botón de AR no aparecerá o no abrirá la cámara.


## Paso 1.3 Comprobar que todo corre
```
$ flutter test
```
