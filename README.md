# PLTV — Puntland State TV & Radio

Android app-ka rasmiga ah ee Telefishinka iyo Raadiyaha Dowladda Puntland.
Wararka, TV-ga tooska ah, raadiyaha iyo jadwalka barnaamijyada — hal app.

**Designed & built by Hudayfi Mohamed Isse — Somali Digital** · somalidigital.so

---

## Soo dejinta APK-ga

APK kasta oo cusub wuxuu ka soo baxaa [**Releases**](../../releases).
Telefoonkaaga Android ku fur bogga Releases, soo deji faylka `.apk`, kadibna
fasax u sii **"Install unknown apps"** marka la ku weydiiyo.

Haddii aad rabto build-ka ugu dambeeyay ee aan weli la sii deynin, ka eeg
[**Actions**](../../actions) → build-ka ugu dambeeyay → `PLTV-apk`.

## Waxa app-ku leeyahay

| Qaybta | Faahfaahin |
|---|---|
| **Hoyga** | Warka ugu weyn, ticker degdeg ah, liiska wararka iyo xayeysiis |
| **Wararka** | Qaybaha (Puntland, Soomaaliya, Caalamka, Siyaasad, Doorasho, Bulsho, Dhaqaale, Ciyaaraha) iyo raadin |
| **Toos** | TV-ga tooska ah (HLS) iyo jadwalka maanta |
| **Chat** | Diyaar u ah marka server-ka newsroom-ku shaqeeyo |
| **Raadiyo** | Raadiyaha Puntland (marka stream-ka la geliyo) |
| **Luqado** | Soomaali · English · العربية (RTL) |

App-ku wuxuu ka shaqeeyaa **xog la'aan** (offline): wararka iyo jadwalka
waxay ku jiraan app-ka gudihiisa. Internet-ka waxaa loo baahan yahay oo keliya
TV-ga tooska ah, raadiyaha, iyo cusboonaysiinta wararka.

## Qaab-dhismeedka

```
app/src/main/
├─ java/so/pl/pltv/MainActivity.java   Shell-ka Android (WebView, fullscreen, back)
├─ assets/www/
│  ├─ index.html                       App-ka oo dhan (UI + JS)
│  ├─ hls.min.js                       Player-ka HLS ee TV-ga tooska ah
│  ├─ data/content.json                Wararka, jadwalka, xayeysiiska, settings
│  └─ img/                             Astaanta PLTV
└─ res/                                Icon, theme, splash
```

### Beddelidda wararka iyo dejinta

Wax walba waxaa laga maamulaa `app/src/main/assets/www/data/content.json`:

- `settings.liveUrl` — link-ga HLS ee TV-ga tooska ah (`.m3u8`)
- `settings.radioUrl` — stream-ka raadiyaha (haddii ay madhan tahay, waa la qariyaa)
- `settings.remoteUrl` — haddii la geliyo, app-ku wuxuu halkaas ka soo qaadanayaa
  wararka cusub mar kasta oo la furo (isla qaab-dhismeedka JSON-ka)
- `settings.schedule` — jadwalka barnaamijyada
- `news[]` — wararka

Marka faylkaas la beddelo oo la **push** gareeyo, GitHub Actions ayaa si toos ah
u dhisaya APK cusub.

## Dhisidda

Si toos ah (GitHub Actions) mar kasta oo `main` la push gareeyo, ama gacanta:

```bash
./gradlew assembleRelease
# app/build/outputs/apk/release/
```

Baahiyaha: JDK 17, Android SDK (compileSdk 34). minSdk 23 (Android 6.0 kor).

## Saxiixa (signing)

Build-yada hadda waxay isticmaalaan furaha **debug**, kaas oo app-ka rakibmaya
laakiin aan ku habboonayn qeybinta rasmiga ah. Si aad u isticmaasho furahaaga
rasmiga ah, ku dar afartan **secret** (Settings → Secrets and variables →
Actions → New repository secret):

| Secret | Qiimaha |
|---|---|
| `KEYSTORE_B64` | Faylka keystore-ka oo base64 ah |
| `KEYSTORE_PASSWORD` | Furaha keystore-ka |
| `KEY_ALIAS` | `pltv` |
| `KEY_PASSWORD` | Furaha keystore-ka |

Marka la geliyo, build-ka xiga wuxuu si toos ah u isticmaalayaa furahaas.

> **Digniin:** marka furaha saxiixa la beddelo, waa in app-kii hore la saaraa
> (uninstall) ka hor inta aan kan cusub la rakibin.

## Ogeysiisyo

- **TV-ga tooska ah:** stream-ka hadda la isticmaalo waa `http://` (ma aha HTTPS).
  Browser-ka ku jira bog HTTPS ah wuu xannibaa, app-kuse wuu furi karaa.
  Marka link HTTPS ah la helo, ku beddel `content.json`.
- **Sawirrada wararka:** hadda waa naqshado midab ah. Marka sawirro rasmi ah
  la helo, waxaa lagu dari karaa `assets/www/img/` iyo `content.json`.

---

© 2026 Puntland State TV & Radio · Warbaahinta Dowladda Puntland
