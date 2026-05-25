# Feature Flags

Hangi araçların açık olduğunu `NOTEFLOW_FEATURES` ile kontrol edersin. Varsayılan: yalnızca `notes:read`.

---

## Hazır Profiller

### Sadece okuma (önerilen başlangıç)
AI notlarını okur ama hiçbir şeyi değiştiremez.

```
NOTEFLOW_FEATURES=notes:read,projects:read,folders:read,tags:read,tasks:read,ai,calendar:read,voice:read
```

### Tam erişim
AI her şeyi okuyup yazabilir.

```
NOTEFLOW_FEATURES=notes:read,notes:write,projects:read,projects:write,folders:read,folders:write,tags:read,tasks:read,tasks:write,ai,calendar:read,calendar:write,voice:read
```

### Sadece not al
Yeni not oluştur ve ara.

```
NOTEFLOW_FEATURES=notes:read,notes:write
```

---

## Tüm Bayraklar

| Bayrak | Ne açar |
|---|---|
| `notes:read` | Notları listele, oku, ara |
| `notes:write` | Not oluştur, düzenle, sil |
| `projects:read` | Projeleri listele ve oku |
| `projects:write` | Proje oluştur ve güncelle |
| `folders:read` | Klasörleri listele ve oku |
| `folders:write` | Klasör oluştur |
| `tags:read` | Etiketleri listele, etikete göre filtrele |
| `tasks:read` | Görevleri listele |
| `tasks:write` | Görev oluştur ve taşı |
| `ai` | AI özeti ve semantik arama |
| `calendar:read` | Takvim etkinliklerini oku |
| `calendar:write` | Takvim etkinliği ekle |
| `voice:read` | Ses notlarını ve transkriptleri oku |
