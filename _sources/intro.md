# Noteflow MCP

**Noteflow MCP**, Claude Desktop, Claude Code CLI, Codex, Cursor ve VS Code gibi AI araçlarına Noteflow hesabına doğrudan erişim sağlar. Notlarınla, projelerinle, görevlerinle ve proje hafızanla doğal dilde konuşabilirsin.

> *"Geçen ay 'toplantı' etiketiyle açtığım notları özetle."*
> *"Q3 Planlama adında yeni bir proje oluştur, üç görev ekle."*
> *"Bu projedeki son kararları listele."*

---

## Kurulum

```bash
npm install -g noteflow-mcp
```

---

## 4 Adımda Başlangıç

### 1 — Giriş yap

```bash
noteflow login
```

### 2 — Repo'nu bağla (opsiyonel, Memory Commits için gerekli)

```bash
noteflow init
```

Proje klasöründe çalıştır. Noteflow projelerini listeler, seçtiğinle `.noteflow/project.json` oluşturur.

### 3 — AI aracına ekle

```bash
noteflow setup
```

Desteklenen araçlar ve nasıl yapılandırıldıkları:

| AI Aracı | Yapılandırma dosyası |
|---|---|
| Claude Desktop | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Claude Code CLI | `~/.claude.json` |
| Codex CLI | `~/.codex/config.toml` |
| Cursor | `.cursor/mcp.json` |
| VS Code | `.vscode/mcp.json` |

`noteflow setup` seçilen araca göre ilgili dosyayı otomatik günceller.

### 4 — AI aracını yeniden başlat

---

## Manuel Kurulum (Claude Desktop örneği)

`~/Library/Application Support/Claude/claude_desktop_config.json` dosyasına ekle:

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

Token almak için: Noteflow uygulaması → **Ayarlar → Geliştirici → API Token Kopyala**

Diğer araçlar için → [Claude Code](claude-code.md)

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
Noteflow uygulamasında oturumu kapat ve tekrar giriş yap, yeni token kopyala.

**Claude araçları görmüyor**
Config dosyasını kaydedip uygulamayı tamamen kapatıp yeniden aç.

**Sadece bazı araçları görmek istiyorum**
`NOTEFLOW_FEATURES` ile istediğin araçları seçebilirsin → [Feature Flags](feature-flags.md)