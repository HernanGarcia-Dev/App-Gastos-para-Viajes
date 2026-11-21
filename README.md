# Gastos de Viaje

App web instalable (PWA) para repartir gastos de un viaje entre varias personas. Funciona sin internet.

## Modo local
Abrí `index.html` desde un servidor web (por ejemplo GitHub Pages). Los datos se guardan en el dispositivo.

## Sincronización entre celulares (Firebase)
1. En https://console.firebase.google.com creá un proyecto y una **Web app** (`</>`).
2. Pegá el objeto `firebaseConfig` en `firebase-config.js` (reemplazando `export default null;`).
3. En **Build → Firestore Database** creá la base y, en la pestaña **Reglas**, pegá el contenido de `firestore.rules` y publicá.
4. Abrí la app: al crear un viaje aparece "Sincronizar entre celulares". El otro celular entra con **Unirme** (código o link).

## Personas registradas
Cada celular se registra como una persona del viaje (identidad anónima de Firebase; hay que activar **Authentication → Anónimo**). Una vez registrada, esa persona queda bloqueada: nadie más puede usarla, y solo los celulares registrados pueden leer y escribir gastos.

Si un celular pierde su registro (se borran los datos del navegador o se cambia de teléfono), en la consola de Firebase borrá `trips/<código>/claims/<id de la persona>` y el documento correspondiente en `trips/<código>/members/`, y volvé a registrarlo.

## Protección de datos
- Nada se borra de verdad: los gastos borrados van a la **Papelera** (menú ⋯) y se restauran.
- Cada cambio deja una entrada en el **historial** (inmutable); desde un gasto → **Historial** se puede volver a cualquier versión.
- Las reglas de Firestore rechazan datos inválidos y la app ignora cualquier gasto mal formado en vez de romperse.

Seguridad: no hay login. Cada viaje se identifica con un código aleatorio de 20 caracteres; las reglas impiden listar viajes, así que solo accede quien tenga el código.
