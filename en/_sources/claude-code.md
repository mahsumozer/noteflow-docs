# Claude Code ile Kullanım

Claude Code kullanıyorsan `/noteflow` slash komutuyla Noteflow'u doğrudan terminal oturumundan kullanabilirsin. Kod yazarken ayrı bir pencereye geçmene gerek kalmaz.

---

## Kurulum

`.claude/commands/noteflow.md` dosyasını oluştur:

```bash
mkdir -p ~/.claude/commands
```

Sonra `~/.claude/commands/noteflow.md` dosyasını aşağıdaki içerikle oluştur:

```
Bu bir Noteflow komutu. Kullanıcının isteği: $ARGUMENTS

MCP_SERVER: noteflow-mcp (npx ile çalıştır)
TOKEN: NOTEFLOW_TOKEN env var'ından al
FEATURES: notes:read,notes:write,projects:read,projects:write,
          folders:read,tags:read,tasks:read,tasks:write,
          ai,calendar:read,voice:read

İsteği analiz et, uygun MCP aracını JSON-RPC ile çağır,
sonucu Türkçe okunabilir şekilde sun.
```

Token'ı shell profile'ına ekle (kalıcı olsun):

```bash
echo 'export NOTEFLOW_TOKEN="tokenini_buraya_yaz"' >> ~/.zshrc
source ~/.zshrc
```

---

## Kullanım

```
/noteflow notlarımı listele
/noteflow "todo" içeren notları ara
/noteflow "claude deneme" adında yeni proje oluştur
/noteflow todo: projesindeki görevleri göster
/noteflow [not-id] notu özetle
```

---

## Örnek Akış

```
/noteflow projelerimi listele
→ 📁 todo: (6 görev)  📁 devonian (1 görev) ...

/noteflow todo: projesine "Login sayfasını düzelt" görevi ekle
→ ✅ Görev oluşturuldu

/noteflow geçen hafta açtığım notları listele
→ 5 not listelendi...
```

---

## Neden Kullanışlı?

Kod yazarken veya bir proje üzerinde çalışırken Noteflow uygulamasına geçmeden:
- Not alabilirsin
- Projeye görev ekleyebilirsin
- Ses notlarının transkriptini okuyabilirsin
- Notlarında arama yapabilirsin

Tüm bunlar Claude Code oturumundan çıkmadan, `/noteflow` komutuyla.
