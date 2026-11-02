# JARVIS HOME — asistente personal por voz

Sitio estático en GitHub Pages para conversar con el agente de voz de Fish Audio mediante una interfaz propia, sin el widget flotante predeterminado.

## Arquitectura actual

- **Frontend:** HTML/CSS/JavaScript estático en GitHub Pages.
- **Voz e inteligencia conversacional:** agente publicado en Fish Audio.
- **Transporte de audio en tiempo real:** WebRTC, administrado por `@fishaudio/agent-client`.
- **Autenticación:** modo de agente público de Fish Audio, protegido por el interruptor de acceso público y una lista de orígenes permitidos.
- **Servidor propio:** no es necesario para el modo público de demostración.

## Configuración del agente

El archivo `config.js` contiene únicamente el identificador público del agente:

```js
window.JARVIS_CONFIG = {
  agentId: "ID_PUBLICO_DEL_AGENTE"
};
```

No colocar claves API ni credenciales privadas en este archivo.

En Fish Audio, el agente debe:
1. Tener una versión publicada.
2. Tener activado **Acceso público**.
3. Tener permitido el origen exacto `https://somerito.github.io`.

Fish Audio verifica el origen del navegador al crear la sesión pública. La sesión se inicia desde el navegador con `AgentSession.start({ agentId })`.

## Interfaz de voz

La página utiliza el paquete oficial `@fishaudio/agent-client` (versión fijada en el import CDN de `index.html`) para iniciar una sesión directamente desde el botón central:

- Pulsa el núcleo central para iniciar una conversación.
- El navegador solicita permiso al micrófono.
- El SDK conecta audio bidireccional en tiempo real por WebRTC.
- JARVIS muestra transcripciones y responde por los altavoces con la voz configurada en Fish Audio.
- Pulsa **Finalizar conversación** para cerrar la sesión.

La interfaz propia sustituye el widget flotante `<fish-agent>`, por lo que no se abre una ventana superpuesta independiente.

## Publicación en GitHub Pages

Repositorio: https://github.com/SOMERITO/J.A.R.V.I.S

En **Settings → Pages**, seleccionar:
- Deploy from a branch
- Branch: `main`
- Folder: `/(root)`

Página: https://somerito.github.io/J.A.R.V.I.S/

## Seguridad y límites

- Nunca publicar `FISH_API_KEY` en HTML, JavaScript del navegador, historial Git o archivos públicos.
- El Agent ID público no es una API Key, pero permite identificar al agente configurado como público. Fish Audio aplica restricciones de origen y límites de uso.
- Las sesiones públicas se facturan al espacio de trabajo de Fish Audio y están sujetas a límites por IP y por agente.
- El navegador requiere HTTPS, permiso de micrófono, altavoces y conexión a Internet.
- Mantener abierta la pestaña durante la conversación.
- Esta versión todavía no escucha la palabra de activación en segundo plano ni controla dispositivos físicos. Eso requerirá un satélite de voz o integración futura con Home Assistant.

## Documentación oficial

- Fish Audio Web SDK: https://docs.fish.audio/agents/deploy/web-sdk
- Fish Audio Public Agents: https://docs.fish.audio/agents/deploy/public-agents
- Fish Audio Widget: https://docs.fish.audio/agents/deploy/widget
- SDK oficial: https://github.com/fishaudio/fish-agent-sdk-web
- GitHub Pages: https://docs.github.com/pages
