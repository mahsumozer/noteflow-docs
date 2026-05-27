# Claude Code CLI ile Kullanım

Noteflow MCP'yi Claude Code CLI'ye bağlamak `noteflow setup` komutuyla birkaç saniye sürer.

---

## Kurulum

### 1 — Global install

```bash
npm install -g noteflow-mcp
```

### 2 — Giriş yap

```bash
noteflow login
```

Tarayıcıda Noteflow hesabınla oturum açılır, token otomatik kaydedilir.

### 3 — Repo'nu Noteflow projesine bağla

Proje klasöründe çalıştır:

```bash
noteflow init
```

Noteflow'daki projelerini listeler, seçtiğin projeyle `.noteflow/project.json` dosyası oluşturur.

### 4 — Claude Code CLI'ye ekle

```bash
noteflow setup
```

Listeden **Claude Code CLI** seçeneğini seç. Komut `~/.claude.json` dosyasına MCP sunucusunu otomatik yazar.

### 5 — Yeniden başlat

Claude Code oturumunu kapat ve yeniden aç.

---

## Kullanım

Artık Claude, Noteflow araçlarına doğrudan erişir:

```
noteflow_get_current_project_context   → hangi projedeyim, bağlam nedir
noteflow_list_memory_commits           → geçmiş kararlar neler
noteflow_create_memory_commit          → karar kaydet
```

Standart not/proje/görev araçları da kullanılabilir (`noteflow_notes_list`, `noteflow_tasks_create` vb.).

---

## Memory Commits

Bir AI önemli bir iş tamamladığında `noteflow_create_memory_commit` çağırır:

- **Git diff otomatik capture** edilir — kod değişiklikleri Firebase Storage'a yüklenir
- Başlık, özet, kararlar, nedenler, etkilenen dosyalar kaydedilir
- Noteflow web uygulamasının **Memory** sekmesinde GitHub Desktop tarzı diff viewer'da görünür

Bir AI'ın context'i dolup başka bir AI devralsa bile, `noteflow_list_memory_commits` ile önceki tüm kararları okuyabilir.

---

## Manuel kurulum (alternatif)

`noteflow setup` kullanmak istemiyorsan `~/.claude.json` dosyasını kendin düzenle:

```json
{
  "mcpServers": {
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

Token almak için: Noteflow uygulaması → **Ayarlar → Geliştirici → API Token Kopyala**