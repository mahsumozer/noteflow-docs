# Noteflow MCP

**Noteflow MCP**, Claude Desktop, Cursor ve VS Code gibi AI araçlarına Noteflow hesabına doğrudan erişim sağlar. Notlarınla, projelerinle ve görevlerinle doğal dilde konuşabilirsin.

> *"Geçen ay 'toplantı' etiketiyle açtığım notları özetle."*
> *"Q3 Planlama adında yeni bir proje oluştur, üç görev ekle."*
> *"API tasarımı ile ilgili ses kayıtlarımı bul."*

---

## Kurulum

```bash
npm install -g noteflow-mcp
```

Ya da kurulum yapmadan direkt çalıştır (npx her seferinde güncel versiyonu indirir):

```bash
npx noteflow-mcp --help
```

---

## 3 Adımda Başlangıç

### 1 — Token al

Noteflow uygulamasını aç → **Ayarlar → Geliştirici** → **API Token Kopyala** butonuna bas.

Token, hesabına özel bir anahtar. Kimseyle paylaşma.

---

### 2 — Claude Desktop'a ekle

`~/Library/Application Support/Claude/claude_desktop_config.json` dosyasını aç
(Windows'ta `%APPDATA%\Claude\claude_desktop_config.json`) ve şunu ekle:

```json
{
  "mcpServers": {
    "noteflow": {
      "command": "npx",
      "args": ["-y", "noteflow-mcp"],
      "env": {
        "NOTEFLOW_TOKEN": "buraya_tokenini_yapıştır"
      }
    }
  }
}
```

Dosyayı kaydet, **Claude Desktop'ı yeniden başlat**.

---

### 3 — Dene

Claude'a sor:

> *"Noteflow'daki son 5 notumu göster"*

Çalışıyorsa Claude notlarını listeleyecek.

---

## Cursor

`.cursor/mcp.json` dosyasına ekle:

```json
{
  "mcpServers": {
    "noteflow": {
      "command": "npx",
      "args": ["-y", "noteflow-mcp"],
      "env": {
        "NOTEFLOW_TOKEN": "buraya_tokenini_yapıştır"
      }
    }
  }
}
```

---

## VS Code (GitHub Copilot)

`.vscode/mcp.json` dosyasına ekle:

```json
{
  "servers": {
    "noteflow": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "noteflow-mcp"],
      "env": {
        "NOTEFLOW_TOKEN": "buraya_tokenini_yapıştır"
      }
    }
  }
}
```

---

## Hangi özellikler açık?

Varsayılan olarak yalnızca **not okuma** (`notes:read`) açıktır. Daha fazlasını açmak için `NOTEFLOW_FEATURES` ekle:

```json
"env": {
  "NOTEFLOW_TOKEN": "...",
  "NOTEFLOW_FEATURES": "notes:read,notes:write,projects:read,tasks:read,voice:read"
}
```

Tüm özelliklerin listesi → [Feature Flags](feature-flags.md)

---

## Sorun giderme

**Token hatası alıyorum**
Noteflow uygulamasında oturumunu kapat ve tekrar giriş yap, sonra yeni token kopyala.

**Claude araçları görmüyor**
Config dosyasını kaydedip Claude Desktop'ı tamamen kapatıp yeniden aç.

**Sadece bazı araçları görmek istiyorum**
`NOTEFLOW_FEATURES` ile istediğin araçları seçebilirsin → [Feature Flags](feature-flags.md)
