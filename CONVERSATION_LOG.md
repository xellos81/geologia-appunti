# Geologia Appunti — Session Log

> Progetto: HTML di studio per esame di Geologia (Prof. Tondi, UNICAM, Beni Culturali)
> Repo: `xellos81/geologia-appunti` | GitHub Pages: [geologia_appunti.html](https://xellos81.github.io/geologia-appunti/geologia_appunti.html)
> Cartella: `/Users/pierpaolodiflorio/ai-projects/geologia/`

---

## ⚡ TL;DR

7 trascrizioni video Webex → HTML unico (1929 righe, 110KB) con 13 sezioni, 91 flashcard, 5 diagrammi CSS, 62 immagini, metodo Tondi. Mobile-first, dark theme marrone/oro, glassmorphism.

---

## 🔑 Decisioni Chiave (pesate)

### Critiche
1. **Whisper large-v3 su M4 Metal** per trascrivere 7 video — 2-3 sec l'uno ma produce code loopate su audio distorto. Script Python automatico di pulizia.
2. **HTML unico, no framework** — scroll verticale, mobile-first, niente React/Vue. L'utente studia da telefono.
3. **Immagini Wikimedia, NON AI-generated** — l'utente vuole foto reali. No SVG generati da IA.
4. **Subagent deepseek-v4-flash** per organizzare contenuti (più economico del modello principale). Timeout a 10 min, file incompleto → fix manuale.
5. **GitHub Pages** per hosting — veloce, gratis, già attivo su main branch.

### Importanti
6. **Webex API** per estrarre URL MP4 diretti (evitato DRM dei video protetti).
7. **Flashcard: carosello semplice orizzontale** (non infinito), flip al tocco, NO librerie JS esterne.
8. **Diagrammi solo CSS** — flow, timeline, branch, mirror, fault. No canvas/SVG/JS.
9. **Metodo Tondi in box oro** — 6 passi numerati, sezione 12.
10. **Countdown in navbar** — giorni/ore, JS updater ogni minuto, target configurato a 3 giorni residui.

### Correzioni (cose che ho sbagliato e l'utente ha corretto)
11. ⚠️ **Mai inviare HTML in chat Telegram** — mostrare solo cosa è stato fatto, non il codice.
12. ⚠️ **Mai perdere immagini nei merge** — la navbar è stata rifatta 3 volte perché ogni merge cancellava le foto.
13. ⚠️ **Wikimedia rate-limita pesantemente** (HTTP 429) — scaricare a batch piccoli, non in massa. O usare Google Immagini per studio personale.

---

## 📊 Stato Attuale

| Cosa | Stato |
|---|---|
| Sezioni 1-13 | ✅ Complete |
| Flashcard (91) | ✅ Tutte |
| Diagrammi CSS (5) | ✅ Tutti |
| Metodo Tondi | ✅ Sezione 12 |
| Navbar + countdown | ✅ Funzionante |
| Immagini locali (`img/`) | ✅ 32 file |
| Immagini Wikimedia (link esterni) | ⚠️ 40 ancora da scaricare |
| Sezioni future (14-17) | ⬜ Placeholder vuoti |

### Sezioni future (da popolare)
- Foto Rocce
- Foto Geologia
- Storia Appennino
- Understanding Earth

---

## 🗂️ Struttura File

```
/Users/pierpaolodiflorio/ai-projects/geologia/
├── geologia_appunti.html     # HTML principale (1929 righe, ~110KB)
├── img/                      # 32 immagini locali + 40 da scaricare
│   ├── Hutton_James_portrait_Raeburn.jpg
│   ├── Rock_cycle_nps.PNG
│   ├── Earth-cutaway-schematic-numbered.svg
│   ├── The_Earth_seen_from_Apollo_17.jpg
│   ├── fossil_trilobite.jpg
│   ├── mineral_quarzo.jpg
│   ├── ... (+25 altre)
├── trascrizioni/             # 7 file .txt originali + 7 _clean.txt
│   ├── 01_20240319.txt → 01_20240319_clean.txt
│   ├── 02_20240326.txt → ...
│   └── ...
└── CONVERSATION_LOG.md       # Questo file
```

---

## 🛠️ Workflow di Sviluppo

1. **Download video**: Webex API → URL MP4 → `curl`
2. **Trascrizione**: `ffmpeg` MP4→WAV → `whisper-cli large-v3` (ggml, Metal)
3. **Pulizia**: Script Python anti-loop su `.txt`
4. **Organizzazione**: Subagent deepseek-v4-flash riorganizza per argomenti
5. **HTML**: Generazione + CSS + immagini + flashcard + diagrammi
6. **Deploy**: `git push` su main → GitHub Pages auto-deploy

---

## ⚙️ Configurazione Progetto

- **Font**: Playfair Display (heading) + Inter (body) da Google Fonts
- **Palette**: `#1a1410` (bg), `#d4a853` (gold), `#e8cd8a` (gold light), `#f5f0eb` (text)
- **Effetti**: Glassmorphism (`backdrop-filter: blur(24px) saturate(180%)`)
- **Flashcard**: Carosello orizzontale con `transform: translateX()`, flip `rotateY(180deg)`
- **Lightbox**: Click su qualsiasi immagine → overlay fullscreen
- **Countdown**: `setInterval` 60s, data esame configurabile in JS

---

## 🔮 TODO / Prossimi Passi

1. **Scaricare le 40 immagini mancanti** — basta un cron job notturno (Wikimedia smette di rate-limitare dopo qualche ora)
2. **Popolare sezioni future** quando l'utente fornisce i contenuti
3. **Eventuali domande d'esame/riassunti** per ripasso finale
4. **Aggiungere più foto reali** di rocce e minerali (l'utente vuole "molte più immagini" in generale)

---

## 📝 Lezioni Apprese

- **Wikimedia va rate-limitato**: max 5-10 richieste consecutive, poi pausa di 10+ minuti. Per progetti personali (non pubblici), Google Immagini è più veloce.
- **Mai inviare codice HTML in chat**: Pier lo odia. Mostrare solo il risultato.
- **I merge distruggono le immagini**: ogni `git merge` o `patch` su sezioni grandi rischia di cancellare i tag `<img>`. Verificare sempre con `grep -c '<img'` dopo ogni modifica.
- **Subagent per organizzazione**: deepseek-v4-flash è OK ma timeout a 10 min non basta per file >70KB. Fare a pezzi.
- **Pier usa Telegram in mobilità**: il Mac è il server, non l'interfaccia. Le risposte devono essere concise e action-oriented.
