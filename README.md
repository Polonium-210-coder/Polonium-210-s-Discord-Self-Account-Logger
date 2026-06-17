# Discord Self-Logger — Advanced Activity Monitor

[English](#english-version) | [Türkçe](#türkçe-versiyon)

---

# English Version

**Discord Self-Logger** is an advanced, automated activity logging utility that runs as a self-bot on your personal Discord account. It runs silently in the background, listening to all events your account is privy to, and logs them locally in structured markdown and JSON formats. It also includes a stunning web-based dashboard (`viewer.html`) to search, filter, and inspect your logs.

> [!WARNING]
> **Discord Terms of Service Alert:** Running a self-bot is a violation of Discord's Terms of Service (ToS). Using this tool may lead to your Discord account being banned or terminated. Use it entirely at your own risk.

---

## Features

- 💬 **Message Logging:** Sent, received, edited, deleted, and bulk deleted messages across all accessible DMs, Group DMs, and Server channels.
- 🔊 **Voice Tracking:** Join, leave, move, and state changes (mute/deafen) in voice channels.
- 🟢 **Presence & Status:** Tracks status changes (Online, Idle, DND, Offline) and activities (games played, Spotify listening status, custom statuses) of friends and server members.
- 😊 **Reactions:** Logs reaction additions, removals, and reaction clears.
- 👥 **Relationships:** Tracks friend request status, additions, removals, and blocks.
- 📦 **Media Auto-Downloader:** Downloads attachments, images, custom server emojis, and member avatars directly to your local drive.
- 🏠 **Guild/Server Events:** Tracks member joins/leaves/bans, role updates, and channel creations/deletions.
- 📊 **Log Viewer Dashboard:** A responsive, beautiful dashboard (`viewer.html`) with advanced search, category filtering, stats overview, and message history.

---

## Installation

### Prerequisites
- **Python 3.8 or newer** installed on your system.
- **pip** (Python package installer).

### Automated Setup (Recommended)
1. Navigate to the project directory.
2. Double-click the **`setup.bat`** file.
3. The script will automatically check Python, upgrade `pip`, and install the required **`discord.py-self`** library.

### Manual Setup
Open your terminal/command prompt in the project folder and run:
```bash
pip install -r requirements.txt
```

---

## Configuration (`config.json`)

You can configure the logger settings by editing the `config.json` file:

| Key | Default | Description |
| :--- | :--- | :--- |
| `token` | `""` | Your Discord User Account Token (leave empty for interactive setup) |
| `log_own_messages` | `true` | Log messages sent by you |
| `log_dms` | `true` | Log Direct Messages |
| `log_group_dms` | `true` | Log Group Direct Messages |
| `log_guilds` | `true` | Log server events (member lists, channel changes, etc.) |
| `log_voice` | `true` | Log voice channel connections |
| `log_presence` | `true` | Log member presence & custom status updates |
| `log_reactions` | `true` | Log message emoji reactions |
| `download_media` | `true` | Automatically download and save attachments/avatars |
| `log_format` | `"markdown"` | Log output format (`"markdown"` or `"json"`) |
| `max_log_size_mb` | `50` | Maximum size of a single log file before rotation |
| `max_log_days` | `30` | Number of days to keep old logs |

You can also whitelist or blacklist specific guilds or channels by adding their IDs to `allowed_guilds`, `blocked_guilds`, `allowed_channels`, or `blocked_channels`.

---

## Usage

### 1. Extracting Your Discord Token
Your user token is required for the bot to run as your account.
1. Open Discord in your web browser or open the desktop app.
2. Press **`Ctrl` + `Shift` + `I`** (or `Cmd` + `Option` + `I` on macOS) to open Developer Tools.
3. Go to the **Console** tab, paste the following line, and press **Enter**:
   ```javascript
   localStorage.getItem('token').replaceAll('"', '')
   ```
4. If it returns `null` or doesn't work, go to the **Application** (or **Storage**) tab -> **Local Storage** -> select `https://discord.com` -> search for `token` in the key list -> copy the value.

> [!CAUTION]
> **Never share your Discord token with anyone.** Anyone with your token can log into your account, steal your data, and perform actions on your behalf.

### 2. Running the Logger
- Run the program by executing:
  ```bash
  python main.py
  ```
- If it is your first time running it and the `config.json` is empty, it will ask for your token interactively in the terminal and save it.
- Once connected, it will begin logging events. You can stop the logger anytime by pressing **`Ctrl` + `C`** in the terminal.

---

## Log Viewer Dashboard (`viewer.html`)

The logs are saved in the `logs/` directory. To view them in a visual dashboard:

1. **Option A (Manual File Selection):**
   Simply double-click and open `viewer.html` in your web browser. Due to browser security (CORS) rules on local files (`file://`), click the file input button inside the viewer and select the logs you want to display (e.g., select multiple files from the `logs/` folder).

2. **Option B (Automatic Load via Local Server):**
   Start a simple web server in the project directory:
   ```bash
   python -m http.server 8000
   ```
   Then open your browser and go to `http://localhost:8000/viewer.html`. The dashboard will automatically fetch and load all category logs.

---
---

# Türkçe Versiyon

**Discord Self-Logger**, kişisel Discord hesabınız üzerinde bir self-bot olarak çalışan, gelişmiş ve otomatik bir aktivite günlükleme aracıdır. Arka planda sessizce çalışarak hesabınızın görebildiği tüm olayları dinler ve bunları yerel diskinizde yapılandırılmış markdown ve JSON formatlarında saklar. Ayrıca, loglarınızı aramak, filtrelemek ve incelemek için harika bir web arayüzü (`viewer.html`) içerir.

> [!WARNING]
> **Discord Hizmet Şartları Uyarısı:** Bir kullanıcı hesabını otomatikleştirmek (self-bot çalıştırmak) Discord Hizmet Şartları'nı (ToS) ihlal eder. Bu aracı kullanmak, Discord hesabınızın askıya alınmasına veya tamamen kapatılmasına neden olabilir. Tüm sorumluluk size aittir.

---

## Özellikler

- 💬 **Mesaj Günlükleme:** DMs (Özel Mesajlar), Grup DM'leri ve Sunucu kanallarında gönderilen, alınan, düzenlenen, silinen ve toplu silinen mesajların tamamını kaydeder.
- 🔊 **Ses Kanalı Takibi:** Ses kanallarına katılma, ayrılma, taşınma ve susturma/sağırlaştırma gibi durum değişikliklerini günlüğe kaydeder.
- 🟢 **Çevrimiçi Durum & Aktivite:** Arkadaşlarınızın ve sunucu üyelerinin durumlarını (Çevrimiçi, Boşta, Rahatsız Etmeyin, Çevrimdışı) ve aktivitelerini (oynanan oyunlar, Spotify dinleme durumları, özel durum mesajları) takip eder.
- 😊 **Reaksiyonlar:** Mesajlara eklenen, kaldırılan ve temizlenen reaksiyon emojilerini kaydeder.
- 👥 **İlişkiler:** Arkadaşlık isteklerini, arkadaş eklemeleri, çıkarmaları ve engellemeleri takip eder.
- 📦 **Medya Otomatik İndirici:** Mesaj eklerini, resimleri, özel sunucu emojilerini ve üye avatarlarını otomatik olarak yerel diskinize indirir.
- 🏠 **Sunucu Olayları:** Üye giriş/çıkış/yasaklamalarını, rol güncellemelerini ve kanal oluşturma/silme olaylarını takip eder.
- 📊 **Log Paneli (Dashboard):** Gelişmiş arama, kategori filtreleme, istatistik özetleri ve mesaj geçmişi sunan, duyarlı ve şık bir arayüz (`viewer.html`).

---

## Kurulum

### Gereksinimler
- Sisteminizde **Python 3.8 veya daha yeni bir sürümün** kurulu olması gerekir.
- **pip** (Python paket yöneticisi).

### Otomatik Kurulum (Önerilen)
1. Proje dizinine gidin.
2. **`setup.bat`** dosyasına çift tıklayın.
3. Betik otomatik olarak Python kurulumunu doğrulayacak, `pip` sürümünü güncelleyecek ve gerekli olan **`discord.py-self`** kütüphanesini kuracaktır.

### Manuel Kurulum
Terminali veya komut istemcisini proje klasöründe açın ve şu komutu çalıştırın:
```bash
pip install -r requirements.txt
```

---

## Yapılandırma (`config.json`)

Günlükleyici ayarlarını `config.json` dosyasını düzenleyerek değiştirebilirsiniz:

| Anahtar | Varsayılan | Açıklama |
| :--- | :--- | :--- |
| `token` | `""` | Discord Kullanıcı Hesabı Tokeniniz (boş bırakılırsa ilk çalıştırmada sorar) |
| `log_own_messages` | `true` | Kendi gönderdiğiniz mesajları da kaydeder |
| `log_dms` | `true` | Özel mesajları (DM) kaydeder |
| `log_group_dms` | `true` | Grup mesajlarını kaydeder |
| `log_guilds` | `true` | Sunucu olaylarını kaydeder (üye listeleri, kanal değişiklikleri vb.) |
| `log_voice` | `true` | Ses kanalı hareketlerini kaydeder |
| `log_presence` | `true` | Üyelerin çevrimiçi durumlarını ve özel durum yazılarını kaydeder |
| `log_reactions` | `true` | Mesajlara eklenen emojileri kaydeder |
| `download_media` | `true` | Mesaj eklerini ve kullanıcı avatarlarını otomatik indirir |
| `log_format` | `"markdown"` | Çıktı formatı (`"markdown"` veya `"json"`) |
| `max_log_size_mb` | `50` | Rotasyona girmeden önce bir log dosyasının ulaşabileceği maksimum MB |
| `max_log_days` | `30` | Eski logların saklanacağı gün sayısı |

Ayrıca belirli sunucuları veya kanalları beyaz listeye almak veya engellemek için sunucu/kanal ID'lerini `allowed_guilds`, `blocked_guilds`, `allowed_channels` veya `blocked_channels` listelerine ekleyebilirsiniz.

---

## Kullanım

### 1. Discord Tokeninizi Alma
Botun hesabınız olarak çalışabilmesi için kullanıcı tokeninize ihtiyacı vardır.
1. Tarayıcınızdan Discord'u açın veya masaüstü uygulamasını çalıştırın.
2. Geliştirici Araçlarını açmak için **`Ctrl` + `Shift` + `I`** (macOS'ta `Cmd` + `Option` + `I`) tuşlarına basın.
3. **Console (Konsol)** sekmesine gelin, aşağıdaki satırı yapıştırın ve **Enter** tuşuna basın:
   ```javascript
   localStorage.getItem('token').replaceAll('"', '')
   ```
4. Eğer `null` dönerse veya çalışmazsa, **Application (Uygulama)** -> **Local Storage (Yerel Depolama)** -> `https://discord.com` yolunu izleyin -> anahtar listesinden `token` değerini arayın ve kopyalayın.

> [!CAUTION]
> **Discord tokeninizi asla hiç kimseyle paylaşmayın.** Tokeninize sahip olan herkes hesabınıza giriş yapabilir, verilerinizi çalabilir ve sizin adınıza işlemler gerçekleştirebilir.

### 2. Günlükleyiciyi Başlatma
- Programı çalıştırmak için terminale yazın:
  ```bash
  python main.py
  ```
- Eğer ilk kez çalıştırıyorsanız ve `config.json` dosyasında tokeniniz yoksa, terminalde sizden etkileşimli olarak token girmeniz istenecek ve kaydedilecektir.
- Bağlantı sağlandıktan sonra olaylar kaydedilmeye başlar. Günlükleyiciyi durdurmak için terminalde **`Ctrl` + `C`** tuşlarına basabilirsiniz.

---

## Log Görüntüleyici Panel (`viewer.html`)

Kayıtlar `logs/` klasörüne kaydedilir. Logları görsel bir arayüz ile incelemek için:

1. **Yöntem A (Manuel Dosya Seçimi):**
   `viewer.html` dosyasına çift tıklayarak tarayıcınızda açın. Tarayıcıların yerel dosya kısıtlamaları (CORS) nedeniyle panel içindeki dosya yükleme butonunu kullanın ve `logs/` klasöründen görüntülemek istediğiniz günlükleri seçin (birden fazla seçebilirsiniz).

2. **Yöntem B (Yerel Sunucu ile Otomatik Yükleme):**
   Proje dizininde basit bir web sunucusu başlatın:
   ```bash
   python -m http.server 8000
   ```
   Ardından tarayıcınızdan `http://localhost:8000/viewer.html` adresine gidin. Arayüz, logları klasörden otomatik olarak çekecektir.
