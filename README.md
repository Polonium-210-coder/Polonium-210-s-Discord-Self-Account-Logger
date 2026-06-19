# Discord Self-Logger — Advanced Activity Monitor

[English](#english-version) | [Türkçe](#türkçe-versiyon)

---

# English Version

**Discord Self-Logger** is an advanced, automated activity logging utility that runs as a self-bot on your personal Discord account. It runs silently in the background, listening to all events your account is privy to, and logs them locally in structured markdown/JSON formats, as well as a local SQLite database with advanced search capabilities. It also includes a web-based dashboard and a FastAPI-powered REST API backend to search, filter, and inspect your logs.

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
- 🗄️ **SQLite Storage Backend:** Stores structured log events in a local SQLite database (`data/logs.db`) using batch inserts for high performance.
- 🔍 **FTS5 Full-Text Search:** Employs SQLite's FTS5 engine for lightning-fast keyword search across all logged messages.
- 🔌 **FastAPI Dashboard API:** A modular REST API backend providing analytics, media querying, message search, and session authentication.
- 📊 **Log Viewer Dashboard:** A responsive, beautiful dashboard (`viewer.html`) with advanced search, category filtering, stats overview, and message history.

---

## Installation

### Prerequisites
- **Python 3.8 or newer** installed on your system.
- **pip** (Python package installer).

### Automated Setup (Recommended)
1. Navigate to the project directory.
2. Double-click the **`setup.bat`** file.
3. The script will automatically check Python, upgrade `pip`, and install all required dependencies (including `discord.py-self`, `fastapi`, `uvicorn`, `aiosqlite`, and `aiohttp`).

### Manual Setup
Open your terminal/command prompt in the project folder and run:
```bash
pip install -r requirements.txt
```

---

## Configuration (`config.json` & `.env`)

You can configure the logger settings by editing the `config.json` file or utilizing environment variables via a `.env` file. Below are the key configuration variables:

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
| `storage_backend` | `"sqlite"` | Primary storage backend (`"sqlite"` or legacy file logging) |
| `api_enabled` | `false` | Enable the FastAPI dashboard API |
| `api_host` | `"127.0.0.1"` | Host address for the dashboard API |
| `api_port` | `8721` | Port number for the dashboard API |
| `api_key` | `""` | Password/key required for authenticating with the API |

You can also whitelist or blacklist specific guilds or channels by adding their IDs to `allowed_guilds`, `blocked_guilds`, `allowed_channels`, or `blocked_channels` in your config.

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

### 2. Running the Launcher (Recommended)
Double-click the **`start.bat`** file. It provides an interactive launcher menu:
- **`[1] Start Logger Bot only`**: Runs the Discord Selfbot Logger (`main.py`).
- **`[2] Start Dashboard API only`**: Runs the FastAPI backend (`app.py`).
- **`[3] Start Both`**: Launches both the bot and the API concurrently in separate windows.
- **`[4] Exit`**: Closes the launcher.

### 3. Running Manually
If you prefer running via terminal:
- **To start the Selfbot Logger:**
  ```bash
  python main.py
  ```
  If this is your first run and `config.json` lacks a token, you will be prompted to enter it interactively.
- **To start the Dashboard API server:**
  ```bash
  python app.py
  ```

---

## Log Viewer & API Dashboard

### 1. Classic Log Viewer (`viewer.html`)
To inspect file-based logs saved in the `logs/` directory visually:
- **Option A (Manual File Selection):** Simply double-click and open `viewer.html` in your web browser. Click the file input button inside the viewer and select the logs you want to display (e.g., select multiple files from the `logs/` folder).
- **Option B (Local Web Server):** Start a simple web server in the project directory:
  ```bash
  python -m http.server 8000
  ```
  Then go to `http://localhost:8000/viewer.html` in your browser. The dashboard will automatically fetch your local logs.

### 2. Advanced API Dashboard Backend (`app.py`)
When you run the Dashboard API (`app.py` / Option 2 or 3 in launcher):
- A FastAPI server starts on `http://127.0.0.1:8721`.
- You can access the **interactive API documentation** at `http://127.0.0.1:8721/docs` (Swagger UI) or `http://127.0.0.1:8721/redoc`.
- Endpoints are available for searching messages (`/api/search`), analyzing status trends (`/api/analytics`), viewing media lists (`/api/media`), and retrieving logs.

---
---

# Türkçe Versiyon

**Discord Self-Logger**, kişisel Discord hesabınız üzerinde bir self-bot olarak çalışan, gelişmiş ve otomatik bir aktivite günlükleme aracıdır. Arka planda sessizce çalışarak hesabınızın görebildiği tüm olayları dinler, bunları yerel diskinizde yapılandırılmış markdown/JSON formatlarında ve gelişmiş arama desteğine sahip yerel bir SQLite veritabanında saklar. Ayrıca loglarınızı aramak, filtrelemek ve analiz etmek için web tabanlı bir arayüz ile FastAPI destekli bir REST API sunar.

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
- 🗄️ **SQLite Depolama Katmanı:** Yapılandırılmış log olaylarını, yüksek performans için toplu yazma desteğiyle yerel bir SQLite veritabanında (`data/logs.db`) saklar.
- 🔍 **FTS5 Tam Metin Araması:** Kaydedilen tüm mesajlar arasında ışık hızında anahtar kelime araması yapmak için SQLite'ın FTS5 motorunu kullanır.
- 🔌 **FastAPI Dashboard API:** Kimlik doğrulama, medya sorgulama, mesaj arama ve analitik veriler sağlayan modüler bir REST API arka plan servisi.
- 📊 **Log Paneli (Dashboard):** Gelişmiş arama, kategori filtreleme, istatistik özetleri ve mesaj geçmişi sunan, duyarlı ve şık bir arayüz (`viewer.html`).

---

## Kurulum

### Gereksinimler
- Sisteminizde **Python 3.8 veya daha yeni bir sürümün** kurulu olması gerekir.
- **pip** (Python paket yöneticisi).

### Otomatik Kurulum (Önerilen)
1. Proje dizinine gidin.
2. **`setup.bat`** dosyasına çift tıklayın.
3. Betik otomatik olarak Python kurulumunu doğrulayacak, `pip` sürümünü güncelleyecek ve gerekli olan tüm kütüphaneleri (`discord.py-self`, `fastapi`, `uvicorn`, `aiosqlite`, `aiohttp`) kuracaktır.

### Manuel Kurulum
Terminali veya komut istemcisini proje klasöründe açın ve şu komutu çalıştırın:
```bash
pip install -r requirements.txt
```

---

## Yapılandırma (`config.json` ve `.env`)

Günlükleyici ayarlarını `config.json` dosyasını düzenleyerek veya bir `.env` dosyası aracılığıyla çevre değişkenlerini kullanarak yapılandırabilirsiniz. Başlıca yapılandırma seçenekleri şunlardır:

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
| `storage_backend` | `"sqlite"` | Birincil depolama yöntemi (`"sqlite"` veya eski dosya tabanlı günlükleme) |
| `api_enabled` | `false` | FastAPI tabanlı dashboard API'sini etkinleştirir |
| `api_host` | `"127.0.0.1"` | Dashboard API'sinin çalışacağı ana makine adresi |
| `api_port` | `8721` | Dashboard API'sinin çalışacağı port numarası |
| `api_key` | `""` | API erişimi için gerekli olan şifre/anahtar |

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

### 2. Başlatıcıyı Çalıştırma (Önerilen)
**`start.bat`** dosyasına çift tıklayın. Karşınıza etkileşimli bir başlatıcı menüsü çıkacaktır:
- **`[1] Start Logger Bot only`**: Yalnızca Discord Selfbot Günlükleyiciyi (`main.py`) çalıştırır.
- **`[2] Start Dashboard API only`**: Yalnızca FastAPI API servisini (`app.py`) çalıştırır.
- **`[3] Start Both`**: Botu ve API'yi eşzamanlı olarak ayrı pencerelerde başlatır.
- **`[4] Exit`**: Başlatıcıyı kapatır.

### 3. Manuel Çalıştırma
Eğer terminalden çalıştırmak isterseniz:
- **Günlükleyici Botu başlatmak için:**
  ```bash
  python main.py
  ```
  Eğer ilk kez çalıştırıyorsanız ve `config.json` dosyasında tokeniniz yoksa, terminalde etkileşimli olarak token girmeniz istenecek ve kaydedilecektir.
- **Dashboard API sunucusunu başlatmak için:**
  ```bash
  python app.py
  ```

---

## Log Görüntüleyici Panel ve API Dashboard

### 1. Klasik Log Arayüzü (`viewer.html`)
`logs/` klasöründeki dosya tabanlı kayıtları görsel olarak incelemek için:
- **Yöntem A (Manuel Dosya Seçimi):** `viewer.html` dosyasına çift tıklayarak tarayıcınızda açın. Tarayıcıların yerel dosya kısıtlamaları (CORS) nedeniyle panel içindeki dosya yükleme butonunu kullanın ve `logs/` klasöründen görüntülemek istediğiniz günlükleri seçin (birden fazla seçebilirsiniz).
- **Yöntem B (Yerel Sunucu ile):** Proje dizininde basit bir web sunucusu başlatın:
  ```bash
  python -m http.server 8000
  ```
  Ardından tarayıcınızdan `http://localhost:8000/viewer.html` adresine gidin. Arayüz, logları klasörden otomatik olarak çekecektir.

### 2. Gelişmiş API Dashboard Arka Planı (`app.py`)
Dashboard API'sini çalıştırdığınızda (`app.py` / Başlatıcıdan Seçenek 2 veya 3):
- `http://127.0.0.1:8721` adresinde bir FastAPI sunucusu başlar.
- **Etkileşimli API dökümantasyonuna** `http://127.0.0.1:8721/docs` (Swagger UI) veya `http://127.0.0.1:8721/redoc` adreslerinden erişebilirsiniz.
- Mesajlarda arama yapma (`/api/search`), durum analizleri (`/api/analytics`), indirilen medyaları listeleme (`/api/media`) ve logları çekme servislerinden yararlanabilirsiniz.
