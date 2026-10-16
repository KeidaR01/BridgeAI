# BridgeAI

**Tu plan de ChatGPT, conectado a tus aplicaciones locales.**

BridgeAI es una herramienta comunitaria para Windows que conecta aplicaciones y mods compatibles con solicitudes de chat de OpenAI a una cuenta de ChatGPT autorizada por el usuario.

Funciona como un puente: recibe mensajes en una dirección local, los adapta al servicio de OpenAI y devuelve el texto generado al programa que hizo la solicitud. Puede utilizarse, por ejemplo, para generar diálogos en juegos que cuenten con un mod o complemento adecuado.

El acceso se realiza con **Continue with ChatGPT**, mediante el flujo oficial de inicio de sesión y autorización de OpenAI. BridgeAI es un proyecto independiente; no es una aplicación oficial de OpenAI.

**Versión documentada: 1.3.5 · Estado: experimental.**

## Cómo funciona

```text
Aplicación o mod
       ↓
BridgeAI en tu PC — http://127.0.0.1:17863/v1
       ↓
OpenAI — cuenta y uso del plan autorizados por ti
       ↓
Respuesta de texto para tu aplicación
```

El puente se ejecuta en tu equipo. Los modelos generan las respuestas en los servicios de OpenAI, por lo que necesitas conexión a Internet.

## Qué puedes hacer

- Conectar tu cuenta mediante OAuth, sin entregar tu contraseña ni cookies de sesión de ChatGPT al puente.
- Consultar los modelos disponibles para tu cuenta y elegir uno desde el panel.
- Conectar clientes que admitan una Base URL personalizada, una clave local y mensajes de chat de texto.
- Elegir el puerto antes de iniciar el servidor.
- Mantener el puente funcionando en la bandeja junto al reloj al cerrar o minimizar su ventana.
- Pausar nuevas generaciones y renovar la clave local de acceso.
- Administrar las conexiones guardadas y cerrar sus sesiones desde el panel.

El servidor y el navegador se abren por elección del usuario. BridgeAI no se inicia automáticamente con Windows.

## Requisitos

- Windows de 64 bits. Probado en Windows 11; Windows 10 todavía requiere una prueba física de compatibilidad.
- Conexión a Internet y un navegador para completar el acceso.
- Una cuenta ChatGPT Plus o Pro elegible y autorización para usar el plan en esta integración. La disponibilidad depende de OpenAI y de la cuenta.
- Una aplicación o mod que admita el formato de chat de texto compatible descrito abajo.

El EXE portátil incluye su motor de ejecución. Para usarlo no necesitas instalar Node.js, Python ni Codex.

## Descarga

Consulta la sección **Releases** de este repositorio para las versiones descargables y sus notas. Los enlaces de distribución del creador también se publican en [Ko-fi](https://ko-fi.com/keidar).

Si utilizas MediaFire, accede desde el enlace publicado por el creador en Ko-fi. Las copias ofrecidas en otros sitios podrían estar modificadas.

## Primeros pasos

1. Descarga `BridgeAI.exe` y guárdalo en una carpeta de tu elección.
2. Ábrelo y elige un puerto. El predeterminado para una instalación nueva es **17863**; puedes cambiarlo si está ocupado.
3. Pulsa **Iniciar** y después **Abrir panel**.
4. En el paso **01**, pulsa **Continue with ChatGPT**. Completa personalmente el inicio de sesión y el consentimiento en la página oficial de OpenAI.
5. En el paso **02**, selecciona un modelo y pulsa **Usar modelo**. El botón **Probar respuesta** envía una solicitud real y consume uso del plan.
6. Copia los datos del paso **03** a tu aplicación o mod.

### Configuración del cliente

| Campo | Valor |
|---|---|
| Base URL | `http://127.0.0.1:17863/v1`, o la dirección que muestre tu panel |
| API key | La clave local que aparece al pulsar **Mostrar clave** o **Copiar clave** |
| Modelo | `bridge-selected-model` |
| Streaming hacia el cliente | Desactivado: `stream: false` |

La clave local autoriza el acceso a BridgeAI en ese equipo. El modelo real se elige en el panel; `bridge-selected-model` es el nombre que utiliza el cliente para esa selección.

`127.0.0.1` identifica tu propia PC. Cambiar el puerto cambia la dirección que debes configurar en tus mods, pero no modifica el modelo ni su consumo. En otra PC necesitas ejecutar su propia copia del puente, iniciar sesión allí y utilizar la clave local de ese equipo.

## Uso del plan

BridgeAI no necesita una API key de pago de OpenAI para esta modalidad. Las solicitudes autorizadas consumen la cuota de tu plan de ChatGPT o los créditos disponibles, según tu configuración y las condiciones del servicio. Puedes revisar los permisos y límites en [ChatGPT → Configuración → Uso](https://chatgpt.com/settings/usage).

BridgeAI no cobra por las solicitudes ni cambia automáticamente a una API de pago. Tener una suscripción no garantiza generaciones ilimitadas, acceso a todos los modelos ni una cantidad fija de horas de juego. Usar la misma cuenta en varios equipos tampoco multiplica su cuota.

La disponibilidad para cuentas elegibles se describe en la [documentación oficial de Sign in with ChatGPT](https://developers.openai.com/cookbook/articles/sign-in-with-chatgpt).

## Cerrar, detener y actualizar

| Acción | Resultado |
|---|---|
| Cerrar con **X** o minimizar | Conserva el puente funcionando en la bandeja |
| Cerrar el navegador | Conserva el servidor funcionando |
| **Detener** | Apaga el servidor y mantiene abierta la aplicación |
| **Salir** o **Salir y desconectar** junto al reloj | Termina BridgeAI y conserva la sesión cifrada para el próximo inicio |
| **Cerrar sesiones y revocar acceso** en el panel | Intenta revocar todas las sesiones guardadas y elimina todas las conexiones de esa instalación |

Para actualizar, elige primero **Salir y desconectar** junto al reloj. Después abre el EXE nuevo y pulsa **Iniciar → Abrir panel**. La X solo oculta la ventana. Si otra compilación sigue abierta, BridgeAI muestra un aviso para evitar confusiones.

El cierre de sesiones del panel conserva el puerto y la clave local de los mods. Si la revocación remota no puede confirmarse, lo indica para que revises el acceso en ChatGPT.

## Compatibilidad

BridgeAI expone una parte del formato OpenAI-compatible:

- `GET /v1/models`
- `POST /v1/chat/completions`
- Autenticación mediante `Authorization: Bearer <clave-local>`.
- Mensajes de texto con roles `system`, `developer`, `user` y `assistant`.
- Respuesta de chat con `choices[0].message.content` y contadores de tokens.

La integración se ha utilizado en AliveNpcs para Stardew Valley y en un complemento de chat para HoneyCome. Los juegos, mods y complementos se instalan por separado; BridgeAI proporciona el puente de comunicación. Cada cliente necesita comprobarse con su versión y configuración.

Esta versión admite una generación a la vez y un límite local de 60 inicios de generación por minuto. Ese límite no equivale a un presupuesto de tokens.

No admite herramientas, imágenes, audio, salida estructurada ni streaming hacia el cliente. Los parámetros de temperatura, `top_p` y máximos de salida enviados por el cliente no se aplican en este adaptador. La compatibilidad parcial no garantiza que cualquier programa que utilice la API de OpenAI funcione sin ajustes.

## Privacidad y seguridad

- El servicio escucha únicamente en `127.0.0.1`; esta versión no lo publica en la red local ni en Internet.
- Las credenciales OAuth y la clave local se guardan cifradas con Windows DPAPI para tu usuario de Windows, en `%LOCALAPPDATA%\BridgeAI`.
- El panel requiere autorización del lanzador y utiliza una cookie local de administración. Contiene un valor aleatorio, no tokens de OpenAI. BridgeAI no lee cookies de ChatGPT ni tu contraseña.
- Al generar una respuesta, los mensajes proporcionados por tu aplicación se envían a OpenAI para procesarlos. El acceso OAuth descrito no importa tus conversaciones existentes de ChatGPT.
- La protección local no impide que malware ejecutado con tu mismo usuario o como administrador comprometa el equipo.

Mantén privada la clave local. Al renovarla tendrás que actualizarla en tus clientes. Para compartir el programa, distribuye el EXE o el paquete de publicación; conserva tus archivos de sesión y datos privados fuera del repositorio.

### Aviso de Windows SmartScreen

La versión 1.3.5 no tiene firma digital de editor y Windows puede mostrar **«Windows protegió su PC»** o **«Editor desconocido»**. Alojar el archivo en GitHub no elimina por sí solo ese aviso: SmartScreen evalúa la firma y la reputación del archivo. Consulta la [explicación de Microsoft](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/smartscreen-reputation).

## Problemas conocidos y ayuda

- **Puerto ocupado:** elige otro antes de pulsar Iniciar y actualiza la Base URL en tu cliente.
- **Panel bloqueado:** ábrelo desde **Abrir panel** en la ventana de BridgeAI.
- **Faltan modelos:** vuelve al panel y pulsa **Actualizar lista**. Si la cuenta ya aparece, evita repetir la autorización únicamente por una descarga lenta del catálogo.
- **Sesión revocada:** vuelve a conectar tu cuenta mediante **Continue with ChatGPT**.
- **`invalid_origin` al regresar de la autorización:** la versión 1.3.5 corrige el bloqueo reproducido en esa redirección. Comprueba que hayas salido de la compilación anterior y que la ventana muestre 1.3.5.

Se han observado tiempos de espera intermitentes al descargar el catálogo oficial; su causa completa todavía no está confirmada. La disponibilidad de red, modelos y permisos puede afectar el funcionamiento.

Al informar un problema, incluye la versión de BridgeAI, la versión de Windows, los pasos para reproducirlo y el código de error. Oculta correos y datos personales en las capturas y no publiques claves, tokens ni direcciones completas de autorización.

## Código y validación

El paquete de código incluye el lanzador de Windows, el servidor local, el panel y las pruebas en `source/`. Los scripts `Build.ps1`, `Test.ps1` y `Test-Package.ps1` permiten compilar y comprobar el proyecto. El motor exacto y su SHA-256 están fijados en `source/node-runtime.json`.

En la revisión 1.3.5 pasaron 31 pruebas automatizadas contando escenarios y grupos principales, las comprobaciones del paquete portátil y la regresión de navegador del retorno OAuth con una cuenta ficticia. Los informes `VALIDACION.md` y `SEGURIDAD.md` del paquete detallan qué se comprobó y sus límites. Las pruebas no constituyen una certificación de seguridad.

El código de BridgeAI se distribuye bajo **MIT**, según el archivo `LICENSE`. El motor incluido y sus componentes conservan sus licencias, recogidas en `NODE-LICENSE.txt`.

## Apoya el proyecto

Si te gusto esta herramienta puedes apoyar si gustas, de igual manera esto fue creado para la comunidad.

**[Apoyar en Ko-fi](https://ko-fi.com/keidar)**

## Referencias

- [Sign in with ChatGPT para aplicaciones locales y de código abierto](https://developers.openai.com/siwc/token-sharing-open-source)
- [Modelos e inferencia](https://developers.openai.com/siwc/token-sharing-open-source/models-and-inference)
- [Limitaciones de la integración](https://developers.openai.com/siwc/token-sharing-open-source/preview-limitations)
