# Hastane Randevu ve Tahlil Sistemi Sözde Kodu

```
// Randevu Alma Modülü
MODÜL RANDEVU_AL()
    POLİKLİNİKLER = ["Dahiliye", "Göz", "KBB", "Ortopedi", ...]
    
    "Poliklinik listesi:" yaz
    i = 1
    TEKRAR
        i + ". " + POLİKLİNİKLER[i] yaz
        i = i + 1
    i = POLİKLİNİKLER.UZUNLUK olana kadar
    
    SEÇİLEN_POLİKLİNİK'i al
    
    EĞER SEÇİLEN_POLİKLİNİK geçerli İSE
        DOKTORLAR = POLİKLİNİK_DOKTORLARINI_GETİR(SEÇİLEN_POLİKLİNİK)
        
        "Doktor listesi:" yaz
        i = 1
        TEKRAR
            i + ". " + DOKTORLAR[i] yaz
            i = i + 1
        i = DOKTORLAR.UZUNLUK olana kadar
        
        SEÇİLEN_DOKTOR'u al
        
        EĞER SEÇİLEN_DOKTOR geçerli İSE
            UYGUN_SAATLER = BOŞ_SAATLERİ_GETİR(SEÇİLEN_DOKTOR)
            
            "Uygun saatler:" yaz
            i = 1
            TEKRAR
                i + ". " + UYGUN_SAATLER[i] yaz
                i = i + 1
            i = UYGUN_SAATLER.UZUNLUK olana kadar
            
            SEÇİLEN_SAAT'i al
            
            EĞER SEÇİLEN_SAAT geçerli İSE
                RANDEVU_KAYDET(TC_NO, SEÇİLEN_POLİKLİNİK, SEÇİLEN_DOKTOR, SEÇİLEN_SAAT)
                "Randevunuz oluşturuldu." yaz
                SMS_GÖNDER(TC_NO, "Randevunuz onaylanmıştır.")
                DÖNDÜR DOĞRU
            DEĞİLSE
                "Geçersiz saat seçimi!" yaz
                DÖNDÜR YANLIŞ
            SON_EĞER
        DEĞİLSE
            "Geçersiz doktor seçimi!" yaz
            DÖNDÜR YANLIŞ
        SON_EĞER
    DEĞİLSE
        "Geçersiz poliklinik seçimi!" yaz
        DÖNDÜR YANLIŞ
    SON_EĞER
SON_MODÜL

// Tahlil Sonucu Görüntüleme Modülü
MODÜL TAHLİL_SONUCU_GÖR(TC_NO)
    EĞER TAHLİL_VAR_MI(TC_NO) İSE
        TAHLİL_LİSTESİ = TAHLİLLERİ_GETİR(TC_NO)
        
        "Tahlil listesi:" yaz
        i = 1
        TEKRAR
            i + ". " + TAHLİL_LİSTESİ[i].TARİH + " - " + TAHLİL_LİSTESİ[i].TÜR yaz
            i = i + 1
        i = TAHLİL_LİSTESİ.UZUNLUK olana kadar
        
        "Görüntülemek istediğiniz tahlilin numarasını girin:" yaz
        SEÇİLEN_TAHLİL'i al
        
        EĞER TAHLİL_HAZIR_MI(SEÇİLEN_TAHLİL) İSE
            SONUÇ = TAHLİL_SONUCUNU_GETİR(SEÇİLEN_TAHLİL)
            SONUÇ'u görüntüle
            
            "Sonucu PDF olarak indirmek ister misiniz? (E/H)" sor
            CEVAP'ı al
            
            EĞER CEVAP = "E" İSE
                PDF_OLUŞTUR(SONUÇ)
                "PDF dosyası oluşturuldu ve indirildi." yaz
            SON_EĞER
            
            DÖNDÜR DOĞRU
        DEĞİLSE
            "Tahlil sonucu henüz hazır değil. Lütfen daha sonra tekrar deneyiniz." yaz
            DÖNDÜR YANLIŞ
        SON_EĞER
    DEĞİLSE
        "Size ait tahlil bulunmamaktadır." yaz
        DÖNDÜR YANLIŞ
    SON_EĞER
SON_MODÜL

// Ana Program
BAŞLA
    TEKRAR
        "TC Kimlik Numaranızı giriniz:" yaz
        TC_NO'yu al
        
        EĞER TC_NO_DOĞRULA(TC_NO) İSE
            "1- Randevu Al" yaz
            "2- Tahlil Sonucu Gör" yaz
            "3- Çıkış" yaz
            SEÇİM'i al
            
            EĞER SEÇİM = 1 İSE
                RANDEVU_AL()
            YADA SEÇİM = 2 İSE
                TAHLİL_SONUCU_GÖR(TC_NO)
            YADA SEÇİM = 3 İSE
                ÇIKIŞ
            DEĞİLSE
                "Geçersiz seçim!" yaz
            SON_EĞER
            
            "Başka işlem yapmak istiyor musunuz? (E/H)" sor
            DEVAM_CEVAP'ı al
            
            EĞER DEVAM_CEVAP = "H" İSE
                ÇIKIŞ
            SON_EĞER
        DEĞİLSE
            "Geçersiz TC Kimlik Numarası!" yaz
        SON_EĞER
    SONSUZ TEKRAR
BİTİR
```
