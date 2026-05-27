# Araçlar

Noteflow MCP, 28 araç sunar. Hepsi `NOTEFLOW_FEATURES` ile seçilebilir.

---

## Memory & Context

Yapay zekaların proje hafızasını yönetmesi için araçlar. AI'lar arası bilgi sürekliliği sağlar.

**`noteflow_get_current_project_context`**
Bulunduğun workspace'i tespit eder (`.noteflow/project.json` veya `~/.noteflow/workspaces.json`), bağlı Noteflow projesini döner. Her session başında çağrılmalı.

**`noteflow_list_memory_commits`**
Projenin geçmiş memory commit'lerini listeler. Yeni bir işe başlamadan önce çağır — ne yapıldığını, neden yapıldığını öğren.

**`noteflow_create_memory_commit`**
Tamamlanan işi kaydet: başlık, özet, kararlar, nedenler, etkilenen dosyalar, taglar.

Git diff otomatik capture edilir — commit sırasında `git diff` çekilir, Firebase Storage'a yüklenir. Noteflow web uygulamasının **Memory** sekmesinde GitHub Desktop tarzı diff viewer'da görünür.

```json
{
  "title": "Add SafetyValidator before hardware write",
  "summary": "Invalid joint commands were reaching the bridge without validation.",
  "decisions": ["Validate before write, not after"],
  "reasons": ["Hardware safety — bad commands caused motor stalls"],
  "affectedFiles": ["src/bridge/hardware_bridge.py"],
  "tags": ["safety", "breaking-change"],
  "status": "approved"
}
```

`codeEvolution` alanı otomatik doldurulur — elle geçmene gerek yok.

---

## Notlar (`notes:read`, `notes:write`)

Tüm not türlerini okuyup yönetebilirsin: metin, canvas, ses, görsel, çizim, sunum, sayfa, takvim.

**Yapabileceklerin:**
- Son notlarını listele, filtrele
- Başlığa, içeriğe veya etikete göre ara
- Yeni not oluştur, var olanı düzenle veya çöpe taşı

**Örnek promptlar:**
> *"Bu hafta oluşturduğum notları göster"*
> *"'fikir' etiketli tüm notlarımı listele"*
> *"API entegrasyonu hakkında yeni bir not oluştur"*

---

## Projeler (`projects:read`, `projects:write`)

Kanban tarzı proje panolarına erişim.

**Yapabileceklerin:**
- Projelerini listele
- Proje detaylarını ve sütunlarını gör
- Yeni proje oluştur, güncelle

**Örnek promptlar:**
> *"Aktif projelerimi göster"*
> *"'Mobile App' projesinin detaylarını getir"*

---

## Klasörler (`folders:read`, `folders:write`)

Proje içindeki klasör hiyerarşisi.

**Yapabileceklerin:**
- Klasörleri listele ve içeriklerini gör
- Yeni klasör oluştur

---

## Etiketler (`tags:read`)

**Yapabileceklerin:**
- Tüm etiketleri listele
- Belirli bir etikete sahip notları bul

**Örnek promptlar:**
> *"Hangi etiketlerim var?"*
> *"'tasarım' etiketli notlarımı listele"*

---

## Görevler (`tasks:read`, `tasks:write`)

Proje panolarındaki görev kartları.

**Yapabileceklerin:**
- Görevleri listele ve detaylarını gör
- Yeni görev oluştur
- Görevi farklı sütuna taşı

**Örnek promptlar:**
> *"Yapılacaklar sütunundaki görevleri göster"*
> *"'Backend fix' görevini Tamamlandı sütununa taşı"*

---

## AI (`ai`)

Noteflow'un AI özelliklerini kullan.

**Yapabileceklerin:**
- Bir notun AI özetini al
- Semantik benzerlik araması yap (anlamsal, anahtar kelime değil)

**Örnek promptlar:**
> *"Bu notu özetle"*
> *"'async programming' ile ilgili notlarımı bul"*

---

## Takvim (`calendar:read`, `calendar:write`)

Takvim tipindeki notlardaki etkinlikler.

**Yapabileceklerin:**
- Takvim notlarındaki etkinlikleri listele
- Yeni etkinlik ekle

---

## Ses Notları (`voice:read`)

**Yapabileceklerin:**
- Ses kayıtlarını listele
- Transkripti olan notların içeriğini oku

**Örnek promptlar:**
> *"Ses notlarımı listele"*
> *"API tasarımı hakkında konuştuğum ses kaydını bul"*