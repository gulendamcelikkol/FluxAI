# AI VEHICLE COUNTER — ÜRÜN GEREKSİNİMLERİ DOKÜMANI (PRD)
**Sürüm:** 2.0  
**Güncelleme:** 07.03.2025  
**Hazırlayan:** Mobil + Backend Geliştirme Ekibi

---

# 1. PROJE ÖZETİ
AI Vehicle Counter, kamera görüntüleri üzerinden yapay zekâ tarafından tespit edilen araç sayılarını mobil uygulama üzerinden kullanıcıya sunan bir sistemdir.  

Bu PRD, üç ana bileşeni kapsar:
- Mobil uygulama (Flutter)
- Backend API (Node.js / Python vb.)
- SQL veritabanı sistemi

Sistem, kamera → AI model → Backend → Mobil uygulama şeklinde çalışır.

Mobil uygulamanın görevi **veri üretmek değil**, **backenden gelen veriyi göstermek** ve kullanıcıya modern bir arayüz sunmaktır.

---

# 2. SİSTEM MİMARİSİ
Kamera → AI Modeli → Backend API → SQL Database → Flutter Mobil Uygulama

### Bileşenler:
- **AI Modeli:** Araç sayısını tespit edip backend'e gönderir.
- **Backend API:** AI modelinden gelen veriyi işler, saklar ve mobil uygulamaya sunar.
- **SQL Database:** Araç sayımı geçmişini saklar.
- **Mobil Uygulama:** Kullanıcıya bu veriyi gerçek zamanlı gösterir.

---

# 3. MOBİL UYGULAMA (FLUTTER) GEREKSİNİMLERİ

## 3.1 Özellikler

### A) Home Screen
- Anlık araç sayısını gösterir.
- Son güncelleme zamanını sunar.
- Yenileme (Refresh) butonu.
- Backend’ten veri çeker.

### B) History Screen
- Geçmiş araç sayımı kayıtlarını gösterir.
- Tarih, saat, araç sayısı bilgisi içerir.
- Liste veya grafik görünümü desteklenebilir.

### C) Settings Screen
- Tema (light/dark) seçimi.
- Uygulama bilgileri.
- API bağlantı bilgisi (isteğe bağlı gösterim).

### D) Splash Screen
- Uygulama logosu.
- 1.5 – 2 saniyelik geçiş animasyonu.

---

# 4. BACKEND & API GEREKSİNİMLERİ

## 4.1 API ENDPOINTLERİ

### ✔ GET /vehicle-count  
En güncel araç sayımını döner.

**Response:**
```json
{
  "count": 45,
  "camera_id": 1,
  "timestamp": "2025-03-07T14:30:00Z"
}
```

### ✔ GET /history  
Tüm veya son N adet geçmiş kaydını döner.

**Response:**
```json
{
  "history": [
    {
      "id": 1,
      "camera_id": 1,
      "count": 37,
      "timestamp": "2025-03-07T14:00:00Z"
    },
    {
      "id": 2,
      "camera_id": 1,
      "count": 42,
      "timestamp": "2025-03-07T13:50:00Z"
    }
  ]
}
```

### ✔ POST /vehicle-count  
AI modeli bu endpoint’e POST atar.

**Body:**
```json
{
  "camera_id": 1,
  "count": 48
}
```

---

# 5. SQL VERİTABANI TASARIMI

## 5.1 vehicle_logs tablosu
| Alan Adı      | Tipi          | Açıklama |
|---------------|---------------|----------|
| id            | INT (PK)      | Oto artan |
| camera_id     | INT           | Kamera kimliği |
| count         | INT           | Araç sayısı |
| timestamp     | DATETIME      | Kayıt zamanı |

---

# 6. BACKEND İŞLEVSEL GEREKSİNİMLER
- Gerçek zamanlı veri alma  
- Veri doğrulama  
- JSON formatında cevap  
- Hata yönetimi  
- 200ms altında API yanıt süresi  

---

# 7. MOBİL – API UYUM KURALLARI
- Anahtarlar **snake_case** olacak.
- timestamp **ISO8601** formatında olacak.
- Null değer döndürülmeyecek.
- API her zaman JSON dönecek.

---

# 8. UI/UX TASARIM GEREKSİNİMLERİ
- Material 3 kullanılacak.
- Light/Dark tema desteği.
- Modern tipografi ve spacing.

---

# 9. PROJE KLASÖR YAPILARI

## Flutter
```
lib/
  ui/screens/
  ui/widgets/
  themes/
  models/
  services/
  utils/
```

## Backend
```
src/
  routes/
  controllers/
  services/
  database/
  models/
```

---

# PRD SONU
