# Gastos de Viaje

App web instalable (PWA) para repartir gastos de un viaje entre varias personas. Funciona sin internet.

## Modo local
Abrí `index.html` desde un servidor web (por ejemplo GitHub Pages). Los datos se guardan en el dispositivo.

## Sincronización entre celulares (Firebase)
1. En https://console.firebase.google.com creá un proyecto y una **Web app** (`</>`).
2. Pegá el objeto `firebaseConfig` en `firebase-config.js` (reemplazando `export default null;`).
3. En **Build → Firestore Database** creá la base y, en la pestaña **Reglas**, pegá el contenido de `firestore.rules` y publicá.
4. Abrí la app: al crear un viaje aparece "Sincronizar entre celulares". El otro celular entra con **Unirme** (código o link).

Seguridad: no hay login. Cada viaje se identifica con un código aleatorio de 20 caracteres; las reglas impiden listar viajes, así que solo accede quien tenga el código.
