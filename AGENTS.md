# AGENTS.md

## Regla obligatoria antes de cada commit

Antes de crear **cualquier commit**, se deben ejecutar las verificaciones estáticas, comprobar que el proyecto compila y validar su funcionamiento en Android.

No se permite crear un commit si alguna de estas verificaciones falla.

### Pasos obligatorios

1. **Verificación estática:**
   - `npm run typecheck`
   - `npm run lint`

2. **Verificar dependencias y configuración:**
   - `npx expo install --check`
   - Comprobar que no existan dependencias incompatibles con la versión actual de Expo SDK.
   - Verificar que no haya errores en la configuración de Expo.

3. **Construcción de la aplicación:**
   - Ejecutar `npx expo export --platform android` para comprobar que Metro puede resolver y generar el bundle de Android.
   - Si existen módulos nativos, cambios en configuración nativa o dependencias que requieran código nativo, realizar también una compilación Android mediante EAS Build o Gradle, según corresponda.

4. **Validación en Android:**
   - Instalar y ejecutar la aplicación en un emulador o dispositivo Android disponible.
   - Comprobar que la aplicación inicia correctamente.
   - Revisar los logs mediante `adb logcat`.
   - Verificar que no existan excepciones, errores de JavaScript, fallos de módulos nativos o problemas de inicialización.

5. **Verificar el funcionamiento:**
   - Comprobar las funcionalidades afectadas por los cambios.
   - Verificar navegación, interacción y persistencia de datos cuando corresponda.
   - Comprobar que no existan errores críticos durante la ejecución.

6. **Revisar los resultados:**
   - Corregir cualquier error encontrado.
   - Repetir las verificaciones correspondientes hasta obtener resultados satisfactorios.
   - No ignorar errores utilizando configuraciones que oculten problemas reales.

7. **Limpieza:**
   - Eliminar los artefactos temporales generados durante las verificaciones, cuando corresponda.
   - No eliminar archivos de configuración, dependencias ni datos persistentes del proyecto.

### Condiciones para crear un commit

Solo se permite crear el commit cuando:

- TypeScript no presenta errores.
- ESLint no presenta errores.
- Las dependencias son compatibles con Expo SDK.
- El bundle de Android se genera correctamente.
- La compilación nativa es satisfactoria cuando corresponde.
- La aplicación inicia correctamente y no presenta errores críticos en ejecución.
- Las funcionalidades afectadas fueron verificadas.

Si alguna verificación no puede realizarse por falta de emulador, dispositivo, credenciales o infraestructura, se debe informar explícitamente. No se debe considerar esa verificación como exitosa ni afirmar que se completó.

**Nunca crear un commit ignorando verificaciones fallidas.**
