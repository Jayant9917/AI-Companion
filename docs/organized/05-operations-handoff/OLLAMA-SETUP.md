# Local AI and Ollama Setup

This guide explains how to enable Desktop Dev Cat's optional local AI features on another Windows computer. The base desktop cat works without Ollama; this setup is required for local chat, explanations, and other AI-assisted features.

## 1. Install prerequisites

Install the following first:

1. Windows 10 or Windows 11.
2. Node.js 20 or newer from https://nodejs.org/.
3. Git from https://git-scm.com/download/win.
4. Ollama for Windows from https://ollama.com/download.

After installing Node.js, open PowerShell and confirm:

```powershell
node --version
npm --version
```

## 2. Clone and install Desktop Dev Cat

```powershell
git clone https://github.com/Jayant9917/AI-Companion.git
Set-Location AI-Companion
npm install
```

## 3. Install and start Ollama

Install Ollama using its Windows installer. Ollama normally runs as a background service and exposes its local API at:

```text
http://localhost:11434
```

Confirm that the service responds:

```powershell
ollama list
```

If the command cannot connect, start Ollama from the Start menu, then try again. You can also check the API directly:

```powershell
Invoke-WebRequest http://localhost:11434/api/tags
```

## 4. Download the recommended Llama model

Desktop Dev Cat currently uses `llama3.2:3b` as its default Ollama model.

```powershell
ollama pull llama3.2:3b
```

The download may be several gigabytes and can take time depending on the internet connection. Confirm the model is installed:

```powershell
ollama list
```

You should see `llama3.2:3b` in the output. Test it independently before starting the app:

```powershell
ollama run llama3.2:3b
```

Ask it a short question, then type `/bye` to exit.

## 5. Start the application

With Ollama running and the model installed:

```powershell
npm run dev
```

The application connects to the local Ollama API when an AI request is made. The first request can be slower because Ollama may load the model into memory. The application allows up to 60 seconds for a request before timing out.

## 6. Optional model alternatives

The code currently defaults to `llama3.2:3b`. Other Ollama models may work, but they are not the documented or tested default. If a different model is used, it must first be downloaded:

```powershell
ollama pull <model-name>
ollama run <model-name>
```

Changing the model selection in the application should be treated as a configuration or code change until a user-facing model setting is added.

## 7. Troubleshooting

### Ollama is unavailable

Check that Ollama is running and that port `11434` is reachable:

```powershell
Invoke-WebRequest http://localhost:11434/api/tags
```

If needed, restart Ollama from the Windows Start menu and retry.

### The model is missing

Run:

```powershell
ollama pull llama3.2:3b
ollama list
```

The model name must match exactly: `llama3.2:3b`.

### The first response times out

Close memory-heavy applications, wait for the model to finish loading, and try again. The first request is normally slower than later requests.

### Windows Firewall or network tools interfere

The app communicates with Ollama on the same computer through localhost. Do not expose Ollama to the public internet. If security software blocks the local connection, allow the local Ollama service and keep the API bound to localhost.

### Reinstall the model

```powershell
ollama rm llama3.2:3b
ollama pull llama3.2:3b
```

Only remove the model if you are sure it is no longer needed; downloading it again can take time and bandwidth.

## Privacy and security

Ollama runs locally, so prompts are sent to the Ollama process on the same computer rather than to a hosted AI provider. Keep the Ollama service local, do not share credentials or secrets in prompts, and review the application's redaction behavior before using it with sensitive developer data.

## Running without AI

Ollama is optional. You can develop and use the cat, reminders, settings, animations, and tray controls without installing Ollama. AI requests will remain unavailable until the local service and model are installed.
