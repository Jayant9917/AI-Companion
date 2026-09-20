# Desktop Dev Cat
<p align="center">
  <img src="./Companion%201.png" alt="Desktop Dev Cat companion" width="24%" />
  <img src="./Companion%202.png" alt="Desktop Dev Cat interaction" width="24%" />
  <img src="./Companion%203.png" alt="Desktop Dev Cat interface" width="24%" />
  <img src="./Companion%204.png" alt="Desktop Dev Cat feature" width="24%" />
</p>

> A friendly desktop companion cat for developers, with reminders, desktop interactions, and optional local AI through Ollama.

Desktop Dev Cat is a Windows desktop companion built with Electron, React, TypeScript, and PixiJS. A small animated cat stays above the desktop, reacts to interaction, provides reminders, and is being extended with a privacy-first local AI companion powered by Ollama.

## What the project does

- Runs as a transparent, frameless, always-on-top desktop window.
- Renders an interactive cat with sprite animations and motion effects.
- Supports dragging, stretch/release behavior, idle movement, happy reactions, and edge effects.
- Provides reminders, popup notifications, and a hidden reminder panel.
- Includes tray-style controls for showing, hiding, pausing, resetting, focus mode, startup, and logs.
- Stores application settings locally with Electron Store.
- Detects developer activity signals from terminal/build workflows.
- Includes a local AI provider abstraction with Ollama support for future explanations, chat, and developer assistance.

The application is designed for Windows first. It is a desktop application, not a normal browser website.

## Current status

The project is in active Phase 1/Phase 2 foundation development. The desktop shell, cat renderer, interaction system, reminders, settings, local persistence, logging, and AI provider foundation are present. Windows packaging and continued UI/animation polish are still in progress.

## Technology stack

- Electron — desktop window, tray, IPC, and main process
- React — UI structure and control panels
- TypeScript — application and shared types
- PixiJS — cat and effects rendering
- Zustand — renderer state management
- Electron Store — local settings persistence
- Vite — renderer development and bundling
- Vitest — tests
- Ollama — optional local AI runtime

## Repository layout

```text
src/
  ai/          AI provider abstraction, Ollama integration, redaction, memory
  cat/         cat state machine, renderer, assets, animation, motion
  main/        Electron main process, preload, IPC, tray, settings
  renderer/    React entry point, application UI, styles
  shared/      shared constants, settings, developer-signal types
  assets/      cat sprites, effects, and reusable sprite parts
scripts/       development launcher and terminal activity tracking
public/        packaging resources such as the tray icon
tests/         Vitest unit tests
docs/organized/ project requirements, architecture, plans, assets, and handoff notes
```

## Requirements

- Windows 10 or Windows 11
- Node.js 20 or newer recommended
- npm 10 or newer recommended
- Git
- Ollama only if you want to use the local AI features

## Install and run

```bash
git clone https://github.com/Jayant9917/AI-Companion.git
cd AI-Companion
npm install
npm run dev
```

`npm run dev` starts the Vite renderer, TypeScript watch compilation, and Electron together. Do not open `index.html` directly with `file:///`; use the development command or a packaged Electron build.

## Validation and builds

```bash
npm test          # run unit tests
npm run lint      # run ESLint
npm run build     # build renderer and Electron files
npm run format    # format source files
```

Windows packaging commands:

```bash
npm run package:win             # Windows installer build
npm run package:win:portable    # portable build
npm run package:win:installer   # NSIS installer build
```

Build output is generated into ignored directories such as `dist/` and `dist-electron/`.

## Ollama and local AI

The application uses Ollama at `http://localhost:11434` by default and currently defaults to the model `llama3.2:3b`. Ollama is optional for the base cat, reminders, rendering, and settings features.

Follow the complete setup guide here:

- [Local AI and Ollama setup](./docs/organized/05-operations-handoff/OLLAMA-SETUP.md)

The AI integration is local-first: prompts are sent to the Ollama service running on the user's own computer. Do not assume that Ollama is available; the application handles provider unavailability and request timeouts.

## Interaction shortcuts

- Tap the cat three times quickly for a happy reaction.
- Tap the cat eight times quickly to reveal the reminder launcher.
- Drag the cat to interact with it and trigger stretch/release motion.

## Documentation

The organized documentation index is at [docs/organized/README.md](./docs/organized/README.md). Start with [PROJECT-CONTEXT.md](./docs/organized/PROJECT-CONTEXT.md), then read the requirements and architecture documents.

## Contributing

1. Create a branch for your change.
2. Keep renderer, main-process, and preload responsibilities separated.
3. Run `npm test`, `npm run lint`, and `npm run build` before committing.
4. Do not commit `node_modules`, build output, local runtime data, secrets, or `.env` files.
5. Update the relevant document in `docs/organized/` when behavior or architecture changes.

## License and project status

This repository is under active development and is released under the [MIT License](./LICENSE).


