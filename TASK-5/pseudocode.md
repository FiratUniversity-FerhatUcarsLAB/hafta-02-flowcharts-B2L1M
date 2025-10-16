# IoT Tabanlı Akıllı Ev Güvenlik Sistemi Pseudocode

```
BAŞLA

// Ana sonsuz döngü (7/24 çalışma)
sistem_aktif = DOĞRU

TEKRARLA (sistem_aktif = DOĞRU OLDUĞU SÜRECE)
    // Sensör okuma döngüsü
    hareket_algılandı = Hareket_Sensörü_Oku()
    kapı_pencere_açık = Kapı_Pencere_Sensörü_Oku()
    
    // Ev sahibi kontrolü
    ev_sahibi_evde = Ev_Sahibi_Kontrol()
    
    // Tehdit değerlendirmesi ve alarm seviyesi belirleme
    EĞER hareket_algılandı VEYA kapı_pencere_açık İSE
        EĞER ev_sahibi_evde = YANLIŞ İSE
            // Alarm seviyesi belirleme
            alarm_seviyesi = Alarm_Seviyesi_Belirle()
            
            // Kamera aktivasyonu
            Kamera_Aktive_Et()
            
            // Alarm seviyesine göre bildirim gönderme
            EĞER alarm_seviyesi = 1 İSE  // Düşük
                Bildirim_Gönder("Düşük seviye alarm", "SMS")
            YOKSA_EĞER alarm_seviyesi = 2 İSE  // Orta
                Bildirim_Gönder("Orta seviye alarm", "SMS + App")
            YOKSA  // Yüksek (seviye 3)
                Bildirim_Gönder("YÜKSEK seviye alarm!", "SMS + App + Email")
                Alarm_Siren_Çalıştır()
            SON_EĞER
            
            // Alarm durumu kontrolü
            alarm_sıfırlandı = YANLIŞ
            TEKRARLA
                alarm_sıfırlandı = Alarm_Sıfırlama_Kontrolü()
                EĞER alarm_sıfırlandı = YANLIŞ İSE
                    BEKLE(60)  // 60 saniye bekle
                SON_EĞER
            alarm_sıfırlandı = DOĞRU OLANA_KADAR
            
        SON_EĞER
    SON_EĞER
    
    BEKLE(5)  // 5 saniye bekle ve tekrar kontrol et
SONSUZA_KADAR

BİTİR

// Yardımcı Fonksiyonlar
FONKSİYON Alarm_Seviyesi_Belirle()
    hareket_sayısı = Hareket_Sensörü_Sayısı()
    açık_giriş = Açık_Giriş_Sayısı()
    
    EĞER hareket_sayısı = 1 VE açık_giriş = 0 İSE
        DÖNDÜR 1  // Düşük seviye
    YOKSA_EĞER hareket_sayısı <= 2 VEYA açık_giriş = 1 İSE
        DÖNDÜR 2  // Orta seviye
    DEĞİLSE
        DÖNDÜR 3  // Yüksek seviye
    SON_EĞER
SON_FONKSİYON

FONKSİYON Bildirim_Gönder(mesaj, kanallar)
    EĞER kanallar İÇERİR "SMS" İSE
        SMS_Gönder(mesaj)
    SON_EĞER
    
    EĞER kanallar İÇERİR "App" İSE
        App_Bildirim_Gönder(mesaj)
    SON_EĞER
    
    EĞER kanallar İÇERİR "Email" İSE
        Email_Gönder(mesaj)
    SON_EĞER
SON_FONKSİYON
```
