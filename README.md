# JARVIS HOME — prototipo web de voz

Interfaz estática inicial para conversar por voz con JARVIS desde computadora o móvil, preparada para GitHub Pages y el widget web de Fish Audio Agents.

## Estado

Esta es la **base de interfaz**. Para habilitar la conversación todavía hace falta crear/publicar un agente de Fish Audio, si Agents está habilitado en la cuenta, y configurar el Agent ID público.

## Configuración

1. En Fish Audio, abre **Creativo → Agente** y comprueba si puedes crear un agente.
2. Configura el nombre como `JARVIS HOME`.
3. Instrucciones sugeridas para el agente:

   > Eres JARVIS, un asistente personal doméstico. Hablas siempre en español latinoamericano, con tono sereno, preciso, educado y natural. Responde como un asistente de voz: usa frases breves y fáciles de escuchar, evita listas largas salvo que te las pidan y pregunta una sola cosa cuando falte información esencial. No afirmes que controlaste luces, enchufes, cerraduras u otros dispositivos si no existe una herramienta conectada que confirme esa acción. En este prototipo puedes conversar y responder preguntas, pero todavía no tienes acceso a dispositivos físicos ni a las tareas del usuario.

4. En la configuración de voz selecciona **Jarvis (Latin American Spanish)**.
5. Prueba el agente dentro del builder.
6. Publica el agente y habilita acceso público si tu cuenta ofrece esa opción. Autoriza el origen de la web publicada, si existe una lista de dominios permitidos.
7. Copia el **Agent ID** (no el ID de la voz ni una API Key) en `config.js`:

   ```js
   window.JARVIS_CONFIG = {
     agentId: "ID_PUBLICO_DEL_AGENTE"
   };
   ```

8. Publica estos archivos en la raíz del repositorio y habilita GitHub Pages desde **Settings → Pages**.
9. Abre la URL HTTPS, inicia la sesión y concede permiso al micrófono.

## Seguridad

- **Nunca** publiques `FISH_API_KEY` ni `OPENAI_API_KEY` en HTML, JavaScript del navegador, repositorios públicos o commits.
- El Agent ID no sustituye una API Key. La seguridad del agente debe configurarse en Fish Audio (visibilidad, acceso público y restricciones por origen cuando estén disponibles).
- Si Fish Audio Agents no está habilitado o no permite acceso público, no expongas una API Key para intentar embeber TTS. En ese caso, la siguiente arquitectura será un backend (por ejemplo, Cloudflare Worker) con secretos configurados del lado del servidor.

## Límites del prototipo

- El navegador requiere HTTPS y permiso de micrófono.
- La conversación requiere Internet y mantener la pestaña abierta.
- No incluye escucha continua en segundo plano ni palabra de activación permanente.
- No controla dispositivos físicos ni se conecta todavía a Home Assistant o Tasky.
- La disponibilidad de Agents puede depender del acceso beta de Fish Audio.

## Publicación con GitHub Pages

En el repositorio: **Settings → Pages → Deploy from a branch → main → /(root) → Save**.

## Documentación

- Fish Audio Web Agent SDK: https://github.com/fishaudio/fish-agent-sdk-web
- Fish Audio Developers: https://fish.audio/developers/
- GitHub Pages: https://docs.github.com/pages
- Cloudflare Workers Secrets (para backend futuro): https://developers.cloudflare.com/workers/configuration/secrets/
