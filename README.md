# Dike 🦞

A desktop interface for [OpenClaw](https://github.com/openclaw/openclaw) - a self-hosted local AI assistant. Dike wraps the OpenClaw gateway in a polished, installable Electron app with a built-in chat interface, conversation history, and file output panel.

---

## Prerequisites

Before you start, make sure you have the following installed:

- **Node.js** `v22.12.0` (exact version — use nvm to manage this)
- **npm** `v10.9.0+`
- **OpenClaw** installed globally (`npm install -g openclaw@latest`)
- An **Anthropic or OpenAI API key**

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/nomsou/dike.git
cd dike
```

### 2. Use the correct Node version

```bash
nvm install 22.12.0
nvm use 22.12.0
```

> If you don't have nvm, install it from https://github.com/nvm-sh/nvm

### 4. Install dependencies

```bash
npm install
```

<!-- ### 4. Start OpenClaw gateway

In a separate terminal, run:

```bash
openclaw onboard --install-daemon
openclaw gateway --port 18789
```

Keep this running. Dike connects to it on startup. -->

### 5. Run Dike in development mode

```bash
npm run dev
```

The app window will open automatically.

---

## Build for production

```bash
# macOS
npm run build:mac

# Windows
npm run build:win

# Linux
npm run build:linux
```

Outputs are written to the `dist/` folder.

---

## Project structure

```
src/
├── main/              # Electron main process
│   ├── index.ts       # App lifecycle, IPC handlers
│   ├── agent.ts       # OpenClaw WebSocket connection manager
│   └── store.ts       # electron-store config persistence
├── preload/
│   └── index.ts       # contextBridge — safe IPC bridge to renderer
└── renderer/
    └── src/
        ├── App.tsx
        ├── main.tsx
        ├── components/    # Sidebar, ChatWindow, Composer, etc.
        ├── store/         # Zustand global state
        └── screens/       # Onboarding, Settings
```

---

## Tech stack

| Package                  | Purpose                                    |
| ------------------------ | ------------------------------------------ |
| Electron + electron-vite | App shell + bundler                        |
| React + TypeScript       | Renderer UI                                |
| Tailwind CSS v3          | Styling                                    |
| Zustand                  | State management                           |
| electron-store           | Config persistence                         |
| ws                       | WebSocket client (main process → OpenClaw) |
| react-markdown           | Markdown rendering in chat                 |
| electron-builder         | Packaging + installers                     |

---

## Notes

- Node version must be exactly `v22.12.0` — other versions will throw engine warnings or fail to build
- OpenClaw gateway must be running before launching Dike
- API keys are stored via the in-app onboarding wizard, not in any config file
