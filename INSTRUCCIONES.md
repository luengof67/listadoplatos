# Recetario de cocina — Cómo generar el APK con Capacitor

La app ya está lista dentro de la carpeta `www/`. Estos pasos empaquetan ese HTML
como una aplicación Android instalable (APK). Solo hay que hacerlos una vez;
después, cada cambio se actualiza con dos comandos.

## 1. Qué necesitas instalar (una sola vez)

1. **Node.js** (versión 20 o superior): https://nodejs.org — instalador normal, siguiente-siguiente.
2. **Android Studio**: https://developer.android.com/studio — durante la instalación acepta
   los componentes por defecto (SDK, emulador no hace falta).

## 2. Preparar el proyecto (una sola vez)

Abre una terminal (en Windows: "Símbolo del sistema" o PowerShell) dentro de esta carpeta y ejecuta:

```
npm install
npx cap add android
```

Esto descarga Capacitor y crea la carpeta `android/` con el proyecto nativo.

## 3. Generar el APK

```
npx cap sync
npx cap open android
```

Se abrirá Android Studio (la primera vez tarda unos minutos en preparar todo).
Cuando termine de cargar:

1. Menú **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
2. Al acabar aparece un aviso abajo a la derecha: pulsa **"locate"**.
3. El archivo está en `android/app/build/outputs/apk/debug/app-debug.apk`.

## 4. Instalarlo en los móviles del restaurante

- Pásate el `app-debug.apk` por WhatsApp, correo o cable USB.
- Al abrirlo, Android pedirá permiso para "instalar apps de origen desconocido": acéptalo.
- Listo: la app "Recetario" queda instalada y funciona sin internet.

## 5. Cuando quieras cambiar algo de la app

1. Sustituye `www/index.html` por la versión nueva.
2. Ejecuta `npx cap sync` y vuelve a generar el APK (paso 3).

Los datos NO se pierden al actualizar la app: se guardan en el dispositivo (IndexedDB).

## Notas importantes

- **Cada móvil tiene su propio recetario** (los datos son locales). Usa el botón
  **⇅ Copia** de la app para exportar el recetario de un dispositivo e importarlo
  en otro, o como copia de seguridad.
- **Imprimir menús**: en Android, el botón de imprimir usa el servicio de impresión
  del sistema (Wi-Fi Direct / Google Cloud Print / Guardar como PDF). Si tu
  impresora no aparece, instala la app de impresión de tu marca (HP Smart, Epson
  iPrint, etc.). También puedes exportar el menú a PDF y compartirlo.
- El APK de tipo "debug" es perfecto para uso interno. Si algún día quisieras
  publicarla en Google Play, habría que firmarla ("release") — dímelo y te
  preparo los pasos.
