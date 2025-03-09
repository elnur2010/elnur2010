import org.telegram.telegrambots.bots.TelegramLongPollingBot
import org.telegram.telegrambots.meta.api.methods.send.SendMessage
import org.telegram.telegrambots.meta.api.objects.Update
import org.telegram.telegrambots.meta.api.objects.replykeyboard.ReplyKeyboardMarkup
import org.telegram.telegrambots.meta.api.objects.replykeyboard.buttons.KeyboardButton
import org.telegram.telegrambots.meta.api.objects.replykeyboard.buttons.KeyboardRow

class MyBot : TelegramLongPollingBot() {

    override fun getBotUsername(): String = "windowis_gaming_bot"
    override fun getBotToken(): String = "7700333527:AAGYvck2g92yotBcj3kWfiaRKMPyN0eD2cw"

    override fun onUpdateReceived(update: Update?) {
        if (update == null || !update.hasMessage() || !update.message.hasText()) return

        val chatId = update.message.chatId.toString()
        val text = update.message.text
        val sendMessage = SendMessage()
        sendMessage.chatId = chatId

        when (text) {
            "/start", "🔙 Orqaga" -> {
                sendMessage.text = "Asosiy menyu:"
                sendMessage.replyMarkup = mainMenu()
            }
            "🎮 O'yinlar" -> {
                sendMessage.text = "O'yin turini tanlang:"
                sendMessage.replyMarkup = gameMenu()
            }
            "💻 Dasturlar" -> {
                sendMessage.text = "Dasturlar bo'limini tanlang:"
                sendMessage.replyMarkup = softwareMenu()
            }
            "🚗 GTA" -> sendMessage.replyMarkup = gtaMenu().also { sendMessage.text = "Qaysi GTA o‘yinini tanlaysiz?" }
            "🏎 Poyga" -> sendMessage.replyMarkup = racingMenu().also { sendMessage.text = "Qaysi poyga o‘yinini tanlaysiz?" }
            "🔫 Otishma" -> sendMessage.replyMarkup = shooterMenu().also { sendMessage.text = "Qaysi otishma o‘yinini tanlaysiz?" }

            "GTA 5" -> sendMessage.text = "📥 GTA 5 yuklab olish: [GTA 5](https://www.gta5-mods.com/vehicles/vapid-torrence-add-on-replace-tuning)"
            "GTA 4" -> sendMessage.text = "📥 GTA 4 yuklab olish: [GTA 4](https://itorrents-igruha.org/44-44-gta-4.html)"
            "GTA SA" -> sendMessage.text = "📥 GTA SA yuklab olish: [GTA SA](https://itorrents-igruha.org/46-23-gta-san-andreas.html)"
            "Blur" -> sendMessage.text = "📥 Blur yuklab olish: [Blur](https://itorrents-igruha.org/1253-blur.html)"
            "Asphalt 9" -> sendMessage.text = "📥 Asphalt 9 yuklab olish: [Asphalt 9](https://itorrents-igruha.org/12281-asphalt-9-legends.html)"
            "Counter-Strike 1.6" -> sendMessage.text = "📥 CS 1.6 yuklab olish: [CS 1.6](https://itorrents-igruha.org/1131-counter-strike-16.html)"
            "CS:GO" -> sendMessage.text = "📥 CS:GO yuklab olish: [CS:GO](https://itorrents-igruha.org/904-counter-strike-global-offensive.html)"
            "Call of Duty" -> sendMessage.text = "📥 Call of Duty yuklab olish: [COD](https://itorrents-igruha.org/396-03-call-of-duty-1-repak-igruha-1.html)"
            // Dasturlar
            "🖥 Windows" -> sendMessage.replyMarkup = windowsMenu().also { sendMessage.text = "Qaysi Windows versiyasini tanlaysiz?" }
            "🐧 Linux" -> sendMessage.replyMarkup = linuxMenu().also { sendMessage.text = "Qaysi Linux distributivini tanlaysiz?" }
            "🛡 Antivirus" -> sendMessage.replyMarkup = antivirusMenu().also { sendMessage.text = "Qaysi antivirus dasturini tanlaysiz?" }
            "🌐 Brauzerlar" -> sendMessage.replyMarkup = browserMenu().also { sendMessage.text = "Qaysi brauzerni tanlaysiz?" }

            // Dasturlar yuklash havolalari
            "🟢 Windows 11" -> sendMessage.text = "📥 Windows 11 yuklab olish: [Windows 11](https://www.microsoft.com/software-download/windows11)"
            "🔵 Windows 10" -> sendMessage.text = "📥 Windows 10 yuklab olish: [Windows 10](https://www.microsoft.com/software-download/windows10)"
            "🐧 Ubuntu" -> sendMessage.text = "📥 Ubuntu yuklab olish: [Ubuntu](https://ubuntu.com/download)"
            "🐧 Debian" -> sendMessage.text = "📥 Debian yuklab olish: [Debian](https://www.debian.org/download)"
            "🛡 Kaspersky" -> sendMessage.text = "📥 Kaspersky yuklab olish: [Kaspersky](https://www.kaspersky.com/downloads)"
            "🛡 Avast" -> sendMessage.text = "📥 Avast yuklab olish: [Avast](https://www.avast.com/free-antivirus-download)"
            "Google Chrome" -> sendMessage.text = "📥 Chrome yuklab olish: [Chrome](https://www.google.com/chrome/)"
            "Mozilla Firefox" -> sendMessage.text = "📥 Firefox yuklab olish: [Firefox](https://www.mozilla.org/firefox/)"


            "🖥 Windows" -> sendMessage.replyMarkup = windowsMenu().also { sendMessage.text = "Qaysi Windows versiyasini tanlaysiz?" }
            "🐧 Linux" -> sendMessage.replyMarkup = linuxMenu().also { sendMessage.text = "Qaysi Linux distributivini tanlaysiz?" }
            "🛡 Antivirus" -> sendMessage.replyMarkup = antivirusMenu().also { sendMessage.text = "Qaysi antivirus dasturini tanlaysiz?" }
            "🌐 Brauzerlar" -> sendMessage.replyMarkup = browserMenu().also { sendMessage.text = "Qaysi brauzerni tanlaysiz?" }

            else -> sendMessage.text = "⚠️ Noma'lum buyruq!"
        }
        execute(sendMessage)
    }

    private fun mainMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("🎮 O'yinlar"), KeyboardButton("💻 Dasturlar")))
    )).apply { resizeKeyboard = true }

    private fun gameMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("🚗 GTA"), KeyboardButton("🏎 Poyga"))),
        KeyboardRow(listOf(KeyboardButton("🔫 Otishma"), KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun gtaMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("GTA 5"), KeyboardButton("GTA 4"))),
        KeyboardRow(listOf(KeyboardButton("GTA SA"), KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun racingMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("Blur"), KeyboardButton("Asphalt 9"))),
        KeyboardRow(listOf(KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun shooterMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("Counter-Strike 1.6"), KeyboardButton("CS:GO"))),
        KeyboardRow(listOf(KeyboardButton("Call of Duty"), KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun softwareMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("🖥 Windows"), KeyboardButton("🐧 Linux"))),
        KeyboardRow(listOf(KeyboardButton("🛡 Antivirus"), KeyboardButton("🌐 Brauzerlar"))),
        KeyboardRow(listOf(KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun windowsMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("🟢 Windows 11"), KeyboardButton("🔵 Windows 10"))),
        KeyboardRow(listOf(KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun linuxMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("🐧 Ubuntu"), KeyboardButton("🐧 Debian"))),
        KeyboardRow(listOf(KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun antivirusMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("Avast"), KeyboardButton("Kaspersky"))),
        KeyboardRow(listOf(KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }

    private fun browserMenu() = ReplyKeyboardMarkup(listOf(
        KeyboardRow(listOf(KeyboardButton("Google Chrome"), KeyboardButton("Mozilla Firefox"))),
        KeyboardRow(listOf(KeyboardButton("🔙 Orqaga")))
    )).apply { resizeKeyboard = true }
}
