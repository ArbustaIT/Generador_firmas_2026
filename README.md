# ✦ Generador de Firma de Correo — Arbusta

Herramienta interna para que los integrantes de Arbusta generen su firma de correo electrónico corporativa de forma rápida, consistente y sin necesidad de editar código.

---

## 📋 Descripción

Una página web estática (un solo archivo `.html`) que permite completar los datos personales y generar automáticamente una firma de correo lista para copiar y pegar en Gmail o cualquier cliente de correo compatible con HTML.

La firma generada incluye el logo oficial de Arbusta, tipografías corporativas y el formato visual definido por el equipo.

---

## 🚀 Instalación y uso

En caso de usarlo local no necesita, dependencias ni servidor con backend. Es un archivo HTML estático funcional.

### Subir al servidor

1. Copiá el archivo `index.html` a tu servidor o hosting.
2. Accedé desde el navegador a la URL donde lo subiste.

```
https://firma.arbusta.net/
```

> El logo de Arbusta está **embebido en base64** dentro del HTML, por lo que no necesitás subir ningún archivo de imagen adicional.

---

## 🖥️ Cómo usar la herramienta

1. Abrí la página en el navegador.
2. Completá tus datos en el formulario de la izquierda:
   - Nombre y Apellido
   - Cargo / Rol
   - Empresa
   - Ciudad y País
   - Email
   - Teléfono
   - Usuario de LinkedIn
   - Sitio web
3. La firma se actualiza en tiempo real en el panel de vista previa.
4. Hacé clic en **"Copiar firma al portapapeles"**.
5. Pegá la firma en tu cliente de correo.

### Cómo pegar en Gmail

1. Ir a **Configuración** (ícono ⚙) → **Ver toda la configuración**
2. Ir a la pestaña **General** → sección **Firma**
3. Crear una firma nueva o editar una existente
4. Pegar con `Ctrl + V` (pegar con formato)
5. Guardar cambios al final de la página
---

## 🗂️ Estructura del proyecto

```
/
└── index.html   # Toda la aplicación en un solo archivo
```

El archivo contiene todo integrado:

- **CSS** — estilos y diseño de la interfaz (dentro de `<style>`)
- **HTML** — estructura de la página (formulario + preview)
- **JavaScript** — lógica de generación y copiado de la firma (dentro de `<script>`)
- **Logo** — imagen del logo de Arbusta embebida en base64 (no requiere archivo externo)

---

## ⚙️ Campos del formulario

| ID del campo | Descripción | Valor por defecto |
|---|---|---|
| `f-name` | Nombre y Apellido | `Nombre y Apellido` |
| `f-role` | Cargo o Rol | `Cargo` |
| `f-empresa` | Nombre de la empresa | `Arbusta` |
| `f-ciudad` | Ciudad y País | `Buenos Aires, AR` |
| `f-email` | Dirección de email | `mail@arbusta.net` |
| `f-phone` | Teléfono | `+54 11 0000-0000` |
| `f-linkedin` | Usuario de LinkedIn (sin URL) | `linkedin` |
| `f-web` | Sitio web | `arbusta.net` |

> **Comportamiento de los links en la firma:**
> - El **email** genera un enlace `mailto:` para abrir el cliente de correo.
> - El **teléfono** genera un enlace `wa.me/` para abrir una conversación de WhatsApp. Los caracteres no numéricos se eliminan automáticamente.

---

## 🎨 Diseño y tipografías

### Interfaz de la herramienta

| Tipografía | Uso |
|---|---|
| [Syne](https://fonts.google.com/specimen/Syne) | Títulos y headings de la UI |
| [DM Sans](https://fonts.google.com/specimen/DM+Sans) | Texto general de la interfaz |
| [DM Mono](https://fonts.google.com/specimen/DM+Mono) | Atajos de teclado (`kbd`) |

### Firma de correo

| Tipografía | Uso |
|---|---|
| [Figtree](https://fonts.google.com/specimen/Figtree) | Nombre y Cargo |
| [Martian Mono](https://fonts.google.com/specimen/Martian+Mono) | Datos de contacto, links |

#### Jerarquía de tamaños de la firma

| Elemento | Tamaño |
|---|---|
| Nombre | 16px |
| Rol / Cargo | 14px |
| Empresa · Ciudad | 12px |
| Email · Teléfono | 12px |
| LinkedIn · Web | 10px |

> ⚠️ **Nota importante:** Las tipografías de Google Fonts se visualizan correctamente en la **preview de la web**, pero Gmail y Outlook **no cargan fuentes externas**. En el correo real, los clientes de mail usarán el fallback definido (`Arial` para nombre/cargo, `monospace` para contacto). Esto es una limitación de los clientes de correo, no de la herramienta.

---

## 🔧 Personalización

### Cambiar los valores por defecto del formulario

Buscá los `input` en el HTML y modificá el atributo `value`:

```html
<input id="f-empresa" type="text" value="Arbusta" oninput="render()">
```

### Cambiar los colores de la firma

En la función `buildSig()` dentro del `<script>`, los colores están definidos como estilos inline.

#### Paleta de colores actual de la firma

| Elemento | Color | Hex |
|---|---|---|
| Nombre | Grape | `#7229bc` |
| Rol / Cargo | Aubergine | `#2A103E` |
| Ubicación | Graphite | `#2C2927` |
| Email, Teléfono, LinkedIn, Web | Aubergine | `#2A103E` |

### Cambiar el logo

El logo está embebido como base64 en la variable `logoSVG` dentro del `<script>`. Para reemplazarlo:

1. Convertí tu nueva imagen PNG a base64:
   ```bash
   python3 -c "import base64; print(base64.b64encode(open('logo.png','rb').read()).decode())"
   ```
2. Reemplazá el valor en `src="data:image/png;base64,..."` dentro de la variable `logoSVG`.

---

## 🌐 Compatibilidad

| Cliente | Vista previa de la web | Firma en correo |
|---|---|---|
| Gmail | ✅ | ✅ (fuentes fallback) |
| Outlook | ✅ | ✅ (fuentes fallback) |
| Apple Mail | ✅ | ✅ |
| Thunderbird | ✅ | ✅ |

**Navegadores soportados:** Chrome, Firefox, Safari, Edge (versiones modernas).

---

## 📦 Dependencias externas

La herramienta no tiene dependencias de npm ni librerías JavaScript. Solo carga recursos externos de Google Fonts (requiere conexión a internet para que se vean las tipografías de la UI).

```
https://fonts.googleapis.com  ← tipografías de la interfaz
```

---

## 👥 Contribución

Para proponer cambios en el diseño o los campos del formulario, abrí un issue o un PR en este repositorio describiendo la modificación.

---

*Herramienta interna de Arbusta · No requiere backend · Archivo único HTML*
