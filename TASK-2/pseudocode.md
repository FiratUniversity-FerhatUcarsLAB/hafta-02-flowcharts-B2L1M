# E-Ticaret Sistemi Sözde Kodu

```
BAŞLA

// Kullanıcı girişi kontrolü
GİRİŞ_DURUMU = YANLIŞ
TEKRAR
    KULLANICI_ADI'nı al
    PAROLA'yı al
    
    EĞER KULLANICI_ADI ve PAROLA doğru İSE
        GİRİŞ_DURUMU = DOĞRU
        "Giriş başarılı!" yaz
    DEĞİLSE
        "Hatalı kullanıcı adı veya parola!" yaz
    SON_EĞER
GİRİŞ_DURUMU = DOĞRU olana kadar

// Ürün kategorileri ve sepet işlemleri
SEPET = BOŞ_DİZİ
SEPET_TOPLAMI = 0

TEKRAR
    "1. Kategorileri Görüntüle" yaz
    "2. Sepeti Görüntüle" yaz
    "3. Ödemeye Geç" yaz
    "4. Çıkış" yaz
    SEÇİM'i al

    EĞER SEÇİM = 1 İSE
        KATEGORİLERİ_GÖSTER()
        ÜRÜN_SEÇ()
        
        // Stok kontrolü
        EĞER SEÇİLEN_ÜRÜN.STOK > 0 İSE
            SEPET'e ÜRÜN ekle
            SEPET_TOPLAMI = SEPET_TOPLAMI + ÜRÜN.FİYAT
            SEÇİLEN_ÜRÜN.STOK = SEÇİLEN_ÜRÜN.STOK - 1
        DEĞİLSE
            "Ürün stokta yok!" yaz
        SON_EĞER
        
    YADA SEÇİM = 2 İSE
        // Sepet görüntüleme ve düzenleme
        EĞER SEPET boş İSE
            "Sepetiniz boş!" yaz
        DEĞİLSE
            SEPET'i görüntüle
            "Ürün çıkarmak istiyor musunuz? (E/H)" sor
            EĞER cevap = "E" İSE
                ÜRÜN_NO al
                SEPET'ten ÜRÜN_NO'lu ürünü çıkar
                SEPET_TOPLAMI'nı güncelle
            SON_EĞER
        SON_EĞER
        
    YADA SEÇİM = 3 İSE
        // Minimum tutar kontrolü
        EĞER SEPET_TOPLAMI < 50 İSE
            "Minimum sepet tutarı 50 TL olmalıdır!" yaz
            DEVAM
        SON_EĞER

        // İndirim kodu kontrolü
        "İndirim kodunuz var mı? (E/H)" sor
        EĞER cevap = "E" İSE
            İNDİRİM_KODU'nu al
            EĞER İNDİRİM_KODU geçerli İSE
                İNDİRİM uygula
                SEPET_TOPLAMI'nı güncelle
            SON_EĞER
        SON_EĞER

        // Kargo ücreti hesaplama
        EĞER SEPET_TOPLAMI >= 200 İSE
            KARGO_ÜCRETİ = 0
        DEĞİLSE
            KARGO_ÜCRETİ = 30
        SON_EĞER

        // Ödeme yöntemi seçimi
        "Ödeme yöntemi seçin:" yaz
        "1. Kredi Kartı" yaz
        "2. Havale/EFT" yaz
        "3. Kapıda Ödeme" yaz
        ÖDEME_YÖNTEMİ'ni al

        // Sipariş onayı
        TOPLAM = SEPET_TOPLAMI + KARGO_ÜCRETİ
        "Toplam Tutar: " + TOPLAM yaz
        "Siparişi onaylıyor musunuz? (E/H)" sor
        
        EĞER cevap = "E" İSE
            SİPARİŞ_NUMARASI = YENİ_SİPARİŞ_NUMARASI_ÜRET()
            "Siparişiniz alındı! Sipariş numaranız: " + SİPARİŞ_NUMARASI yaz
            ÇIKIŞ
        SON_EĞER
    SON_EĞER
    
SEÇİM = 4 olana kadar

BİTİR
```
