# Araçlar

Noteflow MCP, 25 araç sunar. Hepsi `NOTEFLOW_FEATURES` ile seçilebilir.

---

## Notlar (`notes:read`, `notes:write`)

Tüm not türlerini okuyup yönetebilirsin: metin, canvas, ses, görsel, çizim, sunum, sayfa, takvim.

**Yapabileceklerin:**
- Son notlarını listele, filtrele
- Başlığa, içeriğe veya etikete göre ara
- Yeni not oluştur, var olanı düzenle veya sil

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
> *"'Mobile App' projesinin sütunlarını listele"*

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
