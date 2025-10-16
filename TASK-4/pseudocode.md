# Öğrenci Ders Kayıt Sistemi Pseudocode

```
BAŞLA

// Öğrenci Girişi
GİRDİ öğrenci_no, şifre
EĞER öğrenci_no VE şifre DOĞRU İSE
    // Ana Menü
    TEKRARLA
        ders_listesi[] = Mevcut_Dersleri_Göster()
        seçim = Kullanıcı_Seçimi_Al()
        
        EĞER seçim = "Ders Ekle" İSE
            ders = Ders_Seç()
            
            // Kontrol Mekanizmaları
            kontenjan_uygun = Kontenjan_Kontrolü(ders)
            önkoşul_sağlandı = Önkoşul_Kontrolü(ders)
            zaman_çakışması_yok = Zaman_Çakışması_Kontrolü(ders)
            kredi_limiti_uygun = Kredi_Limiti_Kontrolü(ders)
            
            EĞER kontenjan_uygun VE önkoşul_sağlandı VE 
                 zaman_çakışması_yok VE kredi_limiti_uygun İSE
                
                EĞER öğrenci.GPA < 2.5 İSE
                    danışman_onayı = Danışman_Onayı_İste()
                    EĞER danışman_onayı = DOĞRU İSE
                        Ders_Ekle(ders)
                        "Ders başarıyla eklendi" YAZDIR
                    DEĞİLSE
                        "Danışman onayı alınamadı" YAZDIR
                    SON_EĞER
                DEĞİLSE
                    Ders_Ekle(ders)
                    "Ders başarıyla eklendi" YAZDIR
                SON_EĞER
            DEĞİLSE
                "Ders eklenemedi. Kontrol şartları sağlanamadı:" YAZDIR
                Hataları_Göster(kontenjan_uygun, önkoşul_sağlandı, 
                              zaman_çakışması_yok, kredi_limiti_uygun)
            SON_EĞER
            
        YOKSA_EĞER seçim = "Ders Çıkar" İSE
            ders = Ders_Seç()
            Ders_Çıkar(ders)
            "Ders başarıyla çıkarıldı" YAZDIR
            
        YOKSA_EĞER seçim = "Kayıt Özeti" İSE
            Kayıt_Özeti_Göster()
            
        YOKSA_EĞER seçim = "Kayıt Onayla" İSE
            Kayıt_Onayla()
            "Kayıt işlemi tamamlandı" YAZDIR
            DÖNGÜDEN_ÇIK
        SON_EĞER
        
    seçim = "Çıkış" OLANA_KADAR
    
DEĞİLSE
    "Giriş başarısız. Lütfen bilgilerinizi kontrol edin." YAZDIR
SON_EĞER

BİTİR

// Yardımcı Fonksiyonlar
FONKSİYON Kontenjan_Kontrolü(ders)
    EĞER ders.mevcut_öğrenci < ders.kontenjan İSE
        DÖNDÜR DOĞRU
    DEĞİLSE
        DÖNDÜR YANLIŞ
    SON_EĞER
SON_FONKSİYON

FONKSİYON Önkoşul_Kontrolü(ders)
    EĞER ders.önkoşul_dersi BOŞ İSE
        DÖNDÜR DOĞRU
    DEĞİLSE
        DÖNDÜR öğrenci.geçtiği_dersler İÇERİR ders.önkoşul_dersi
    SON_EĞER
SON_FONKSİYON

FONKSİYON Zaman_Çakışması_Kontrolü(ders)
    çakışma = YANLIŞ
    HER alınan_ders İÇİN öğrenci.mevcut_dersler İÇİNDE
        EĞER ders.zaman ÇAKIŞIYOR alınan_ders.zaman İSE
            çakışma = DOĞRU
            DÖNGÜDEN_ÇIK
        SON_EĞER
    SON_HER
    DÖNDÜR DEĞİL çakışma
SON_FONKSİYON

FONKSİYON Kredi_Limiti_Kontrolü(ders)
    toplam_kredi = öğrenci.mevcut_krediler + ders.kredi
    DÖNDÜR toplam_kredi <= 35
SON_FONKSİYON
```
