# colmena-figuras3d — 3D figures (Colmena extension)

A **pages-only** Colmena extension (`"parts": ["pages"]`, no MCP service). It registers the page prefix
`figura-` so an agent's figure viewers show up in Rooms' «🧩 Extensions» window under 🌀 **3D figures**, and
agents can open them beside the chat with `open_extension(extension="figuras3d", page?)`.

## Repo map

| File | What it is |
|---|---|
| `colmena-extension.json` | The manifest: id `figuras3d`, parts `pages`, prefix `figura-`, kind `preview`, button 🌀. |
| `README.md` | This file. |
| `.gitattributes` | Keeps files byte-for-byte (no line-ending changes), so the reviewed `tree_sha256` matches. |

There is no code here: the extension only tells Colmena which pages belong to it.

## How the pages get made

The agent (taller-3d) writes each figure's page itself in its pages folder, as
`data\pages\<agent>\figura-<name>\` with:

- `index.html`: the viewer (every version, solid or wireframe, side-by-side or overlaid, previews);
- `data.json`: `{"name": "<name>", ...}`;
- `vNNN.bin` or `vNNN.glb`: each version's model (GLB);
- `vNNN.png`: each version's preview image.

The generative engine is a CLI that lives **outside this repo** (on Amber's PC:
`I:\Privado\WebApps\ComfyUI_windows_portable\figuras3d\`). Flow: `visor.py <name>` builds the page, the agent
saves it with `save_page`, then `visor.py <name> --copiar-bin` copies the models in. The figures' store is
`C:\Users\Amber\Documents\Modelos 3D\figuras\<name>\`. None of the engine's code is copied here.

## Resumen (español)

Extensión de Colmena **solo de páginas** (sin servicio): registra el prefijo `figura-` para que los visores de
figuras del agente salgan en «🧩 Extensiones» como 🌀 **Figuras 3D** y se abran con
`open_extension(extension="figuras3d")`. El motor (CLI con ComfyUI/TRELLIS) vive fuera del repo; el agente escribe
cada página `figura-<nombre>` (index.html, data.json con "name", vNNN.bin o glb, vNNN.png) con `save_page` y
`visor.py <nombre> --copiar-bin`. Almacén: `C:\Users\Amber\Documents\Modelos 3D\figuras\<nombre>\`.
