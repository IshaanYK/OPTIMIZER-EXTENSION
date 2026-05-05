# 🧠 Prompt Optimizer — Chrome Extension

A high-performance AI prompt optimizer that lives in your Chrome Side Panel. Write naturally, then let the extension transform your rough text into a clean, structured, token-efficient prompt — without leaving the chat page.

---

## ✨ Features

| Feature | Description |
|---|---|
| **Side Panel UI** | Opens as a Chrome side panel — stays alongside any chat page |
| **Auto-Detection** | Watches your active chat input as you type — no copy/paste needed |
| **Enter-to-Commit** | Press Enter and your chatbot input is replaced with the optimized prompt |
| **Multi-Provider** | Supports Gemini, Groq, Together AI, Mistral, xAI (Grok), and OpenAI |
| **3 Task Modes** | Optimize, Grammar Fix, and Code Prompt modes |
| **Streaming Output** | Results stream token-by-token in real time |
| **Token Metrics** | Shows original vs. optimized token count with % reduction |
| **History Panel** | Stores your 8 most recent prompts — collapsible, click to restore |
| **Copy / Apply** | Copy the result to clipboard or inject it directly into the chat input |
| **Fully Responsive** | Works on mobile, tablet, laptop, and wide desktop screens |

---

## 🚀 Getting Started

### 1. Install the Extension

#### Development (Unpacked)
```bash
# Install dependencies
npm install

# Build the extension
npm run build
```

Then in Chrome:
1. Open `chrome://extensions`
2. Enable **Developer mode** (top right toggle)
3. Click **Load unpacked**
4. Select the `dist/` folder


### 2. Get a Free API Key

| Provider | Free Tier | Get Key |
|---|---|---|
| **Gemini** | ✅ Yes | [aistudio.google.com](https://aistudio.google.com/app/apikey) |
| **Groq** | ✅ Yes | [console.groq.com](https://console.groq.com/keys) |
| **Together AI** | ✅ Yes | [api.together.xyz](https://api.together.xyz/settings/api-keys) |
| **Mistral** | 🔸 Trial | [console.mistral.ai](https://console.mistral.ai/api-keys/) |
| **xAI (Grok)** | ❌ Paid | [console.x.ai](https://console.x.ai/) |
| **OpenAI** | ❌ Paid | [platform.openai.com](https://platform.openai.com/api-keys) |

> **Recommended for beginners:** Start with Gemini (free, no credit card required).

---

### 3. Configure the Extension

1. Click the extension icon in your Chrome toolbar
2. The **Side Panel** will open (or click the `+` button inside)
3. Go to **Settings (Key)** tab
4. Select your provider and paste your API key
5. Click **Save** — you're ready!

---

## 🖥️ How It Works

```
You type in ChatGPT / Claude / Gemini / any chatbot
          ↓
Extension detects input (debounced, 280ms)
          ↓
Side panel sends text to AI via streaming API
          ↓
Optimized prompt appears in the side panel (real-time)
          ↓
Press Enter OR click "Go" → your chat input is replaced
```

### Auto-Sidebar Trigger
When you type more than 30 characters in a supported chat input, the side panel opens automatically.

### Enter-to-Commit
If an optimized result is ready when you press `Enter` (without Shift), it replaces your draft with the optimized version before sending.

---

## 📐 Supported Chatbots

The content script detects input fields using a broad selector set:

- **ChatGPT** (`textarea`, `.ProseMirror`)
- **Claude** (`[contenteditable="true"]`)
- **Gemini** (`[role="textbox"]`)
- **Perplexity**, **Grok**, **Poe**, **Copilot**
- Any site using `textarea`, contenteditable, or `[role="textbox"]`

---

## 🧩 Extension Structure

```
src/
├── manifest.json          # Extension manifest (MV3)
├── index.css              # Global design system (CSS variables, animations)
│
├── background/
│   └── index.js           # Service worker: API streaming, sidebar opening
│
├── content/
│   └── index.jsx          # Content script: input detection, Enter-to-Commit
│
├── sidepanel/
│   ├── index.html         # Side panel HTML entry
│   ├── index.jsx          # Main React app (all panels + history)
│   └── sidepanel.css      # Fully responsive panel styles
│
├── popup/
│   ├── index.html         # Popup/options page HTML
│   └── index.jsx          # Popup app (settings only)
│
├── components/
│   ├── SettingsDrawer.jsx  # Provider + API key configuration UI
│   ├── MetricsPanel.jsx    # Token count & intent display
│   ├── PipelineStages.jsx  # Optimization progress indicator
│   ├── OptimizedOutput.jsx # Output display component
│   └── OptimizerLogo.jsx   # SVG logo component
│
└── lib/
    ├── aiRouter.js         # Universal streaming fetch (SSE + JSON)
    ├── providers.js        # Provider configs & model normalization
    ├── optimizer.js        # Prompt-building & output parsing
    ├── tokenizer.js        # Rough token estimation
    └── gemini.js           # Gemini-specific helpers
```

---

## 🎛️ Task Modes

| Mode | What it does |
|---|---|
| **Optimize** | Compresses and structures your prompt for maximum AI clarity |
| **Grammar** | Fixes grammar and spelling while preserving meaning |
| **Code** | Rewrites your instructions as a precise technical coding prompt |

---

## 📱 Responsive Design

The extension is fully responsive across all form factors:

| Context | Behavior |
|---|---|
| Chrome Side Panel (narrow) | Fluid, full-height layout |
| Popup (380×640) | Fixed card layout |
| Mobile (≤320px) | Single-column hero, compact dock |
| Landscape mobile | Compressed header and dock |
| Tablet / Wide panel (≥460px) | Centered card with max-width |
| Desktop browser (≥769px) | Larger card, optimized spacing |

---

## 🕘 Recent Prompts (History)

- The extension stores your **8 most recent** input/output pairs in `chrome.storage.local`
- The **Recent** section appears on the Home tab when no optimization is running
- Click **▾ Collapse** to minimize the history bar — it remembers the toggle per session
- Click any history item to restore that prompt and its optimized output

---

## 🔧 Development

```bash
# Install deps
npm install

# Dev build with watch
npm run dev

# Production build
npm run build
```

After building, reload the extension in `chrome://extensions` → click the ↺ reload icon.

### Tech Stack
- **React 18** — UI components
- **Vite** + `vite-plugin-web-extension` — build pipeline
- **Vanilla CSS** — responsive design system
- **Chrome MV3** — service worker background, side panel API

---

## ⚠️ Common Issues

| Issue | Fix |
|---|---|
| "Missing API Key" error | Open Settings, paste a valid key, click Save |
| Side panel doesn't open | Make sure you've enabled the extension and clicked the toolbar icon |
| Optimized prompt not applied | Click "Go" in the panel, or press Enter while the result is shown |
| Extension not detecting input | Refresh the chat page; content scripts need a fresh load |
| API error on Gemini | Your key may be expired — create a new one at AI Studio |
| Wrong model error | Open Settings → Advanced → select a valid model from the dropdown |

---

## 📄 Permissions

| Permission | Reason |
|---|---|
| `storage` | Save your API key and history locally |
| `sidePanel` | Open and control the side panel |
| `tabs` | Send the optimized prompt to the active tab |
| `activeTab` | Read the active tab ID to inject results |
| Host permissions | Make API calls to AI providers |

---

## 👤 Author

**Ishaan** — [ishaanyk.github.io/portfolio-me](https://ishaanyk.github.io/portfolio-me/)

---

## 📝 License

MIT — free to use, modify, and distribute.

<img width="545" height="841" alt="Screenshot 2026-05-03 215006" src="https://github.com/user-attachments/assets/856801f4-1134-4e37-952d-44b2ac205265" />
<img width="550" height="845" alt="Screenshot 2026-05-03 215030" src="https://github.com/user-attachments/assets/1f0cd2de-4194-417e-96fb-834f81fc5e0a" />
<img width="554" height="839" alt="Screenshot 2026-05-03 215046" src="https://github.com/user-attachments/assets/0eb589a3-7bb6-418a-ac2d-1c02742e7745" />
<img width="555" height="849" alt="Screenshot 2026-05-03 215109" src="https://github.com/user-attachments/assets/bdd65706-589f-4fcb-9c0f-654d9efb7d75" />
<img width="578" height="847" alt="Screenshot 2026-05-03 215119" src="https://github.com/user-attachments/assets/521dcb08-5594-48bd-8eb0-7743db476932" />




