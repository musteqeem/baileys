<div align="center">

<b>Bismillah ar-Rahman ar-Rahim</b><br><br>

<!-- GRADIENT BANNER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,20,24&height=200&section=header&text=@musteqeem%2Fbaileys&fontSize=40&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Enterprise+WhatsApp+API+for+Node.js&descAlignY=55&descSize=16" />

<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=1500&color=00E5FF;8B5CF6;10B981&center=true&vCenter=true&width=650&lines=Built+to+help+businesses+serve+people+better%2C;InshaAllah" alt="Typing SVG" />

<img src="https://files.catbox.moe/bkvkel.jpeg" width="150" alt="BAILEYS Logo"/>

@musteqeem/baileys

<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&duration=2500&pause=1000&color=00E5FF;8B5CF6;10B981&center=true&vCenter=true&multiline=true&width=650&height=80&lines=A+premium+Baileys+made+by+Musteqeem;The+Enterprise+WhatsApp+API+for+Node.js;Built+for+AI%2C+Automation%2C+and+Scale" alt="Typing SVG" />

**Engineered for Production. Optimized for AI. Trusted at Scale.**

<a href="https://www.npmjs.com/package/@musteqeem/baileys"><img src="https://img.shields.io/npm/v/@musteqeem/baileys.svg?style=for-the-badge&logo=npm&color=00E5FF" alt="npm version"></a>
<a href="https://www.npmjs.com/package/@musteqeem/baileys"><img src="https://img.shields.io/npm/dt/@musteqeem/baileys.svg?style=for-the-badge&color=8B5CF6" alt="npm downloads"></a>
<a href="https://github.com/musteqeem/baileys/stargazers"><img src="https://img.shields.io/github/stars/musteqeem/baileys?style=for-the-badge&color=FFD700&logo=github" alt="GitHub stars"></a>
<a href="https://github.com/musteqeem/baileys/network/members"><img src="https://img.shields.io/github/forks/musteqeem/baileys?style=for-the-badge&color=EC4899&logo=github" alt="GitHub forks"></a>

<br><br>

<!-- GITHUB STATS BANNER -->
<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=musteqeem&repo=baileys&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=00E5FF&icon_color=8B5CF6" height="165" alt="GitHub Stats"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=musteqeem&repo=baileys&layout=compact&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=00E5FF" height="165" alt="Top Languages"/>
</p>

<!-- GITHUB STREAK -->
<p align="center">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=musteqeem&theme=tokyonight&hide_border=true&background=0D1117&ring=00E5FF&fire=FFD700&currStreakLabel=8B5CF6" alt="GitHub Streak"/>
</p>

</div>

---

⚡ Why Enterprises Choose @musteqeem/baileys

This is not another fork. This is a production-hardened re-engineering of Baileys designed for developers building AI agents, customer support systems, and high-volume automation at scale.

Unlike legacy libraries, we fix what breaks in production.

Key Production Enhancements
- **✅ Critical Newsletter Media Fix**: Patched media upload pipeline. No more 400 errors on channels.
- **🤖 Full Interactive Protocol**: Native support for Buttons, Lists, CTA, and Flows. Ready for AI agents.
- **📁 Album & Media Suite**: Send/Receive albums, documents, audio, video, stickers with zero workarounds.
- **🛡️ Enterprise Anti-Ban**: Intelligent backoff, session rotation, and multi-device stability for 24/7 uptime.
- **⚡ 40+ Extended Message Types**: Full coverage of the latest WhatsApp Web payloads.
- **🔄 Persistent Sessions**: `multi-file-auth-state` for serverless, Docker, and PM2 deployments.

---

📦 Installation

```bash
npm i @musteqeem/baileys
```
or
```bash
yarn add @musteqeem/baileys
```
🚀 Quick Start: Production Bot Template
```bash
import makeWASocket, { useMultiFileAuthState, DisconnectReason, Browsers } from '@musteqeem/baileys'
import { Boom } from '@hapi/boom'

const startSock = async () => {
    const { state, saveCreds } = await useMultiFileAuthState('baileys_auth')

    const sock = makeWASocket({
        auth: state,
        browser: Browsers.macOS('Chrome'), // Improves anti-ban
        printQRInTerminal: true,
        markMessagesAsRead: false
    })

    sock.ev.on('creds.update', saveCreds)

    // Example: AI Agent Reply
    sock.ev.on('messages.upsert', async ({ messages }) => {
        const msg = messages[0]
        if (!msg.message || msg.key.fromMe) return

        const text = msg.message.conversation || msg.message.extendedTextMessage?.text
        if (!text) return

        // 1. Send to your AI: OpenAI, Gemini, Claude
        // const aiReply = await yourAI(text)

        // 2. Reply with Interactive Button
        await sock.sendMessage(msg.key.remoteJid!, {
            text: `AI Response: Hello!`,
            footer: "Powered by @musteqeem/baileys",
            buttons: [{ buttonId: 'menu', buttonText: { displayText: 'Menu' }, type: 1 }],
            headerType: 1
        })
    })

    sock.ev.on('connection.update', ({ connection, lastDisconnect }) => {
        if(connection === 'close') {
            const shouldReconnect = (lastDisconnect?.error as Boom)?.output?.statusCode!== DisconnectReason.loggedOut
            if(shouldReconnect) startSock()
        }
    })
}
startSock()
```
🧠 Example: Send Album
```bash
await sock.sendMessage(jid, {
    album: [
        { image: { url: 'img1.jpg' }, caption: '1' },
        { image: { url: 'img2.jpg' }, caption: '2' }
    ]
})
```
😃 Example: Send to Newsletter Channel
```bash
await sock.newsletterMetadata("jid", "description")
await sock.sendNewsletterMessage("newsletter_jid", { text: "New Update" })
```

## 📊 @musteqeem/baileys vs WhiskeySocket

| Feature | @musteqeem/baileys | WhiskeySocket |
| :--- | :---: | :---: |
| **Newsletter Media Upload** | ✅ Fixed & Stable | ❌ Broken |
| **Interactive Buttons/Lists** | ✅ Full Native API | ⚠️ Partial |
| **Album Messages** | ✅ First-class Support | ❌ Not Supported |
| **Anti-Ban & Reconnect** | ✅ Enterprise Logic | ⚠️ Basic |
| **Node 20+ & ESM** | ✅ Modern Stack | ⚠️ Legacy |
| **Active Maintenance** | ✅ By Musteqeem | ⚠️ Sporadic |
---

🌐 Community

Join the professional developers building with us.

<div align="center">
<a href="https://chat.whatsapp.com/Ebd5NAkaJIDGb4GFNR23xs"><img src="https://img.shields.io/badge/WhatsApp%20Community-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" /></a>
<a href="https://t.me/xadontech"><img src="https://img.shields.io/badge/Telegram%20Channel-0088cc?style=for-the-badge&logo=telegram&logoColor=white" /></a>
<a href="https://t.me/xadonite"><img src="https://img.shields.io/badge/Contact%20Owner-6366F1?style=for-the-badge&logo=telegram&logoColor=white" /></a>
</div>

---

🌐 Other Premium Projects by Musteqeem AKA Future Scientist

If you build AI + Automation, these are for you:
Project	Description
https://github.com/CEOcybershieldquad/XADON-AI	Advanced Multi-Agent AI Framework. Deploy GPT-5 powered WhatsApp/Telegram AI employees with tool-use
https://github.com/musteqeem/XADON_AI	The core XADON AI Engine. Voice, Vision, RAG, and Memory for next-generation bots
---

🤝 Contributing

We welcome PRs from professional developers. Please read our contributing guidelines before submitting.

Don't Forget to ✨ *Star* 🌟 and *Fork* this repo to support the project

---

⚠️ Responsible Use
This library is for automation, customer support, and AI agents only.
Please follow WhatsApp's Terms of Service and local laws.
Do not use for spam, fraud, or harming others. _"And cooperate in righteousness and piety"_ [Qur'an 5:2]

---

📄 License
`MIT` © 2026 Musteqeem. _MUSTEQEEM MD • Cybershield Squad alive_

---
<div align="center">
Built for serious developers. Deployed in production worldwide.<br>
<i>You are ultimately welcomed 👑🤗</i>
</div>
