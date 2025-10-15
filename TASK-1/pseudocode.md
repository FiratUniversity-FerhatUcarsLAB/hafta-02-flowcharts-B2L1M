# ATM Para Çekme Algoritması

```
BAŞLA
    TANIMLA pin_deneme = 0
    TANIMLA gunluk_cekim = 0
    TANIMLA gunluk_limit = 5000
    TANIMLA bakiye = 10000  // Örnek başlangıç bakiyesi
    TANIMLA islem_devam = DOĞRU

    GİRİŞ "Lütfen kartınızı takınız"
    
    İKEN islem_devam = DOĞRU YAP
        EĞER pin_deneme >= 3 İSE
            YAZDIR "Kartınız bloke olmuştur. Lütfen bankanızla iletişime geçiniz."
            ÇIK
        BİTTİ

        GİRİŞ "PIN kodunuzu giriniz"
        EĞER pin doğru İSE
            TEKRARLA
                YAZDIR "Mevcut bakiyeniz: " + bakiye + " TL"
                YAZDIR "1. Para Çek"
                YAZDIR "2. Çıkış"
                GİRİŞ secim

                EĞER secim = 1 İSE
                    GİRİŞ "Çekmek istediğiniz tutarı giriniz: "
                    tutar = OKU

                    EĞER tutar MOD 20 != 0 İSE
                        YAZDIR "Tutar 20 TL'nin katları olmalıdır"
                    DEĞİLSE EĞER tutar > bakiye İSE
                        YAZDIR "Yetersiz bakiye"
                    DEĞİLSE EĞER gunluk_cekim + tutar > gunluk_limit İSE
                        YAZDIR "Günlük çekim limiti aşıldı"
                    DEĞİLSE
                        bakiye = bakiye - tutar
                        gunluk_cekim = gunluk_cekim + tutar
                        YAZDIR "Paranızı alınız"
                        YAZDIR "Güncel bakiyeniz: " + bakiye + " TL"
                        YAZDIR_FİŞ
                    BİTTİ

                    YAZDIR "Başka işlem yapmak istiyor musunuz? (E/H)"
                    GİRİŞ devam_secim
                    EĞER devam_secim = "H" İSE
                        islem_devam = YANLIŞ
                    BİTTİ
                DEĞİLSE
                    islem_devam = YANLIŞ
                BİTTİ

            TA Kİ islem_devam = YANLIŞ OLANA KADAR

        DEĞİLSE
            pin_deneme = pin_deneme + 1
            YAZDIR "Hatalı PIN. Kalan deneme hakkı: " + (3 - pin_deneme)
        BİTTİ
    BİTTİ

    YAZDIR "ATM'mizi kullandığınız için teşekkür ederiz"
    YAZDIR "Lütfen kartınızı alınız"
BİTİR
```
