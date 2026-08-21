<div align="center">

@musteqeem/baileys

<img src="https://files.catbox.moe/bkvkel.jpeg" width="120" alt="Baileys Logo"/>

The Enterprise-Grade WhatsApp Web API for Node.js
**Built for AI Agents, Automation, and Production Bots**

<a href="https://www.npmjs.com/package/@musteqeem/baileys"><img src="https://img.shields.io/npm/v/@musteqeem/baileys.svg?style=for-the-badge&logo=npm" alt="npm version"></a>
<a href="https://www.npmjs.com/package/@musteqeem/baileys"><img src="https://img.shields.io/npm/dt/@musteqeem/baileys.svg?style=for-the-badge" alt="npm downloads"></a>
<a href="#"><img src="https://img.shields.io/badge/AI%20Ready-ChatGPT%20%7C%20Gemini%20%7C%20Claude-00C853?style=for-the-badge&logo=openai" alt="AI Ready"></a>

</div>

---

⚡ Why Production Teams Choose This

A battle-tested, lightweight fork of Baileys optimized for reliability, speed, and AI integration. Used to power 24/7 customer support bots, AI assistants, and automation pipelines.

Core Capabilities
- **🤖 AI-Native**: Plug-and-play with OpenAI, Gemini, Claude, LangChain, and custom LLMs
- **⚡ Multi-Device v2**: Persistent sessions. QR once, run forever with `multi-file-auth-state`
- **🛡️ Anti-Disconnect**: Smart auto-reconnect, QR rotation, and rate-limit handling
- **📁 Full Media Suite**: Images, Video, Voice Notes, Documents, Stickers, Polls, Buttons, AiBadge
- **👥 Group OS**: Create, manage, promote, demote, get metadata, send announcements
- **🔄 Real-time Events**: `messages.upsert`, `groups.update`, `presence.update`, `creds.update`

📦 Installation
```bash
npm i @musteqeem/baileys
🚀 Quick Start: AI Assistant Bot
import { default as makeWASocket, useMultiFileAuthState, DisconnectReason } from '@musteqeem/baileys'
import { Boom } from '@hapi/boom'

const startBot = async () => {
    const { state, saveCreds } = await useMultiFileAuthState('auth_info')
    const sock = makeWASocket({
        auth: state,
        printQRInTerminal: true // Set to false in production
    })

    sock.ev.on('creds.update', saveCreds)

    sock.ev.on('messages.upsert', async ({ messages }) => {
        const msg = messages[0]
        if(!msg.message || msg.key.fromMe) return

        const text = msg.message.conversation || msg.message.extendedTextMessage?.text || ''

        // Example: Send to your AI and reply
        const aiResponse = await getAIResponse(text) // Your AI function
        await sock.sendMessage(msg.key.remoteJid, { text: aiResponse })
    })

    sock.ev.on('connection.update', ({ connection, lastDisconnect }) => {
        if(connection === 'close') {
            const shouldReconnect = (lastDisconnect.error as Boom)?.output?.statusCode!== DisconnectReason.loggedOut
            if(shouldReconnect) startBot()
        }
    })
}

startBot()
```
📊 Feature Matrix
Feature	Enterprise Support
**Multi-Device Auth**	Persistent, file-based session storage
**Media Handling**	Send/Download all WhatsApp media types
**Group Management**	Full CRUD for groups and participants
**Event System**	20+ events for full bot control
**Dependencies**	Zero bloat. Pure http://Node.js + WebSockets
🛠️ Requirements
- `Node.js >= 18.0.0`
- Stable Internet Connection

🌐 Other Premium Projects by Musteqeem

If you build AI + Automation, check these out:
Project	Description
**https://github.com/CEOcybershieldquad/XADON-AI**	Advanced Multi-Agent AI Framework. Build GPT-4 powered WhatsApp/Telegram AI employees
**https://github.com/musteqeem/XADON_AI**	The core XADON AI Engine. Voice, Vision, and Tool-use for next-gen bots
📚 Documentation
For full API reference, see the https://github.com/musteqeem/Baileys/wiki

🤝 Contributing
PRs, issues, and sponsorships welcome. This package is maintained for the professional bot developer community.
**😁 Please Star the Repo**

📄 License
`MIT` © 2026 Musteqeem. Built with ❤️ for serious developers.

---
<div align="center">
Made for Builders. Trusted in Production.
</div>
