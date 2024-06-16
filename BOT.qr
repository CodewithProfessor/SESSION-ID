const PastebinAPI = require('pastebin-js'),
pastebin = new PastebinAPI('EMWTMkQAVfJa9kM-MRUrxd5Oku1U7pgL')
const {makeid} = require('./id');
const QRCode = require('qrcode');
const express = require('express');
const path = require('path');
const fs = require('fs');
let router = express.Router()
const pino = require("pino");
const {
	default: Wasi_Tech,
	useMultiFileAuthState,
	jidNormalizedUser,
	Browsers,
	delay,
	makeInMemoryStore,
} = require("@whiskeysockets/baileys");

function removeFile(FilePath) {
	if (!fs.existsSync(FilePath)) return false;
	fs.rmSync(FilePath, {
		recursive: true,
		force: true
	})
};
const {
	readFile
} = require("node:fs/promises")
router.get('/', async (req, res) => {
	const id = makeid();
	async function WASI_MD_QR_CODE() {
		const {
			state,
			saveCreds
		} = await useMultiFileAuthState('./temp/' + id)
		try {
			let Qr_Code_By_Wasi_Tech = Wasi_Tech({
				auth: state,
				printQRInTerminal: false,
				logger: pino({
					level: "silent"
				}),
				browser: Browsers.macOS("Desktop"),
			});

			Qr_Code_By_Wasi_Tech.ev.on('creds.update', saveCreds)
			Qr_Code_By_Wasi_Tech.ev.on("connection.update", async (s) => {
				const {
					connection,
					lastDisconnect,
					qr
				} = s;
				if (qr) await res.end(await QRCode.toBuffer(qr));
				if (connection == "open") {
					await delay(5000);
					let data = fs.readFileSync(__dirname + `/temp/${id}/creds.json`);
					await delay(800);
				   let b64data = Buffer.from(data).toString('base64');
				   let session = await Qr_Code_By_Wasi_Tech.sendMessage(Qr_Code_By_Wasi_Tech.user.id, { text: '' + b64data });
	
				   let WASI_MD_TEXT = `
*_Session Connected By TheProfessor-295_*
*_Made With 🤍_*
______________________________________
╔═════════════════════════════╗
║ 🌟 AMAZING! YOU'VE CHOSEN THE WHATSAPP BOT 🌟
║   You Have Completed the First Step to Deploy a WhatsApp Bot.
╚═════════════════════════════╝

╔═══════════════════════════════════╗
║ 🚀 NEED HELP? VISIT THE FOLLOWING: 🚀
║ 
║ 📺 YouTube: [youtube.com/@wasitech1](https://youtube.com/@wasitech1)
║ 👤 Owner: [Contact Owner](https://https://t.me/ItxVikas)
║ 📂 Repo: [GitHub Repository](https://github.com/TheProfessor-295/WHATSAPP-BOT)
║ 🗣️ WaGroup: [Join WhatsApp Group](https://chat.whatsapp.com/BGqcjzZafoO7CkfPxxC0rr)
║ 📢 WaChannel: [Visit WhatsApp Channel](https://whatsapp.com/channel/0029Vae3uZ3LSmbbhp07dR1U)
║ 🔌 Plugins: [GitHub Plugins](https://github.com/TheProfessor-295)
║ 
╚═══════════════════════════════════╝

╔═══════════════════════════╗
║ 🎉 GET STARTED NOW! 🎉
║  Deploy your bot and transform your WhatsApp experience.
╚═══════════════════════════╝

_____________________________________
	
_Don't Forget To Give Star To My Repo_`
	 await Qr_Code_By_Wasi_Tech.sendMessage(Qr_Code_By_Wasi_Tech.user.id,{text:WASI_MD_TEXT},{quoted:session})



					await delay(100);
					await Qr_Code_By_Wasi_Tech.ws.close();
					return await removeFile("temp/" + id);
				} else if (connection === "close" && lastDisconnect && lastDisconnect.error && lastDisconnect.error.output.statusCode != 401) {
					await delay(10000);
					WASI_MD_QR_CODE();
				}
			});
		} catch (err) {
			if (!res.headersSent) {
				await res.json({
					code: "Service is Currently Unavailable"
				});
			}
			console.log(err);
			await removeFile("temp/" + id);
		}
	}
	return await WASI_MD_QR_CODE()
});
module.exports = router
