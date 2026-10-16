# BridgeAI

**Tu plan de ChatGPT, conectado a tus aplicaciones locales.**

BridgeAI es un puente local para Windows que conecta aplicaciones y mods compatibles con tu plan de ChatGPT. Incluye inicio de sesión autorizado, selección de modelos y un panel para administrar tus conexiones.

Es una herramienta comunitaria independiente. El puente funciona en tu PC y las respuestas se generan en los servicios de OpenAI.

## Descarga

Descarga **BridgeAI.exe** desde la sección **Releases** de este repositorio de GitHub. El ejecutable incluye lo necesario para funcionar; no necesitas instalar Node.js, Python ni Codex.

- **SmartScreen:** el EXE todavía no tiene firma digital de editor y Windows puede mostrar un aviso de aplicación desconocida. Descargarlo desde GitHub no elimina automáticamente ese aviso.

## Requisitos

- Windows de 64 bits. Probado en Windows 11; Windows 10 está pendiente de una prueba física.
- Conexión a Internet.
- Una cuenta ChatGPT Plus o Pro elegible para autorizar el uso del plan.
- Una aplicación o mod que permita configurar un servidor de chat OpenAI-compatible.

## Cómo usarlo

1. Abre **BridgeAI.exe** y elige un puerto. El predeterminado es **17863**.
2. Pulsa **Iniciar** y después **Abrir panel**.
3. Pulsa **Continue with ChatGPT** y completa el acceso en la página oficial de OpenAI.
4. Selecciona un modelo en el panel y pulsa **Usar modelo**.
5. Copia la configuración del panel a tu aplicación o mod:

| Campo | Configuración |
|---|---|
| Base URL | `http://127.0.0.1:17863/v1`, o la que muestre tu panel |
| API key | La clave local que muestra BridgeAI |
| Modelo | `bridge-selected-model` |

Si el cliente ofrece streaming, desactívalo. Esta versión admite chat de texto; la compatibilidad depende de cada aplicación.

**La X mantiene BridgeAI funcionando en la bandeja junto al reloj.** Para terminarlo o actualizarlo, elige **Salir y desconectar** en su icono. Cerrar el navegador tampoco detiene el puente.

## Antes de empezar

- **Uso del plan:** las solicitudes consumen la cuota o los créditos disponibles de tu plan, según tu configuración en ChatGPT. No se garantiza uso ilimitado.
- **Privacidad:** los mensajes enviados por tu aplicación se procesan en OpenAI. BridgeAI no pide tu contraseña ni cookies de sesión de ChatGPT; las credenciales se guardan cifradas para tu usuario de Windows. Mantén privada la clave local.


## Apoya el proyecto

Si BridgeAI te resulta útil, puedes apoyar su desarrollo en [Ko-fi](https://ko-fi.com/keidar). Tu aportación es voluntaria y ayuda a seguir mejorando esta herramienta para la comunidad. ¡Gracias por el apoyo!

## Licencia

BridgeAI se distribuye bajo la licencia **MIT**. El motor incluido conserva sus propias licencias.
