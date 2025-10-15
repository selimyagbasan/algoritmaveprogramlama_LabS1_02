digraph OnlineShopping {
    Start -> "Ürünleri İncele";
    "Ürünleri İncele" -> Select [label="Ürün Seç"];
    AddToCart [label="Sepete Ekle"];
    ViewCart [label="Sepeti Görüntüle"];
    Checkout [label="Ödeme Sayfasına Geç"];
    EnterDetails [label="Teslimat Bilgilerini Gir"];
    Payment [label="Ödeme Yap"];
    Confirm [label="Siparişi Onayla"];
    End [label="Bitiş"];

    Start -> Browse;
    Browse -> Select;
    Select -> AddToCart;
    AddToCart -> ViewCart;
    ViewCart -> Checkout;
    Checkout -> EnterDetails;
    EnterDetails -> Payment;
    Payment -> Confirm;
    Confirm -> End;
}
