BAŞLA

Sepet ← Boş Liste
ToplamTutar ← 0

TEKRARLA
    ÜrünAdı ← Kullanıcıdan "Ürün adını girin (bitirmek için 'q' yazın): " al
    EĞER ÜrünAdı = "q" İSE
        ÇIK
    SON
    Fiyat ← Kullanıcıdan "Ürünün fiyatını girin: " al
    Adet ← Kullanıcıdan "Kaç adet almak istiyorsunuz?: " al

    ÜrünToplam ← Fiyat * Adet
    Sepete ÜrünAdı, Fiyat, Adet ve ÜrünToplam EKLE
    ToplamTutar ← ToplamTutar + ÜrünToplam

SON TEKRAR

YAZ "Sepetinizdeki ürünler: "
HER ürün İÇİN Sepet
    YAZ ürün.Adı, ürün.Adet, ürün.Fiyat, ürün.Toplam
SON

YAZ "Toplam Tutar: ", ToplamTutar, " TL"

KargoÜcreti ← 0
EĞER ToplamTutar < 500 İSE
    KargoÜcreti ← 50
    YAZ "Kargo Ücreti: 50 TL eklendi."
SON

GenelToplam ← ToplamTutar + KargoÜcreti
YAZ "Ödenecek Toplam Tutar: ", GenelToplam, " TL"

YAZ "Ödeme işlemi tamamlandı. Teşekkür ederiz!"

BİTİR
