### Envanter Geliştirmeleri: Eşya Görseli ve Değer/Piyasa (Aşınma) Sistemi

Bu doküman, iki yeni sistemi ve roleplay ortamına etkilerini açıklar:
- Eşyaya görsel atama, paylaşma ve inceleme
- Eşyaya değer atama ve aşınma (wear float) ile dinamik piyasa değeri

---

### 1) Eşya Görsel Sistemi

- Amaç: Oyuncuların bazı eşyalara URL ile görsel atayabilmesi, bu görseli yakın oyuncularla paylaşabilmesi ve CEF üzerinden inceleyebilmesi.
- Desteklenen türler: Outfit, Packaging, Drink, Food, Generic

#### Kullanım Akışı
- Görsel Ayarla: Envanterde sağ tık → Görsel Ayarla → URL girilir → Eşyaya atanır.
- Görseli İncele: Eşyada görsel varsa, CEF penceresinde açılır. ESC / Backspace ile kapanır.
- Görseli Paylaş: Eşyada görsel varsa, oyuncu ID girilerek (5m mesafe) hedef oyuncuya görsel gösterilir.

#### UI
- Context Menu seçenekleri:
  - Görsel Ayarla
  - Görseli Paylaş (görsel varsa)
  - Görseli İncele (görsel varsa)

#### Teknik Detaylar
- Veri saklama: `SpawnedItem.extra.imageUrl`
- Doğrulama:
  - HTTP/HTTPS zorunlu
  - Uzantı: .png, .jpg, .jpeg, .gif, .webp
  - Maksimum uzunluk: 300 karakter
- Yakınlık kontrolü: Paylaşım için 5m ve aynı dimension
- Görüntüleme: CEF HUD `CEFBrowser:openImage` ile

#### Roleplay Etkileri
- Ambalaj/gıda/icecek gibi ürünlerin marka, içerik, estetik sunumu
- Kanıt, afiş, broşür, ürün kataloğu gibi görsel aktarım rolleri
- Oyuncular arası görsel paylaşım ile sosyal etkileşim artışı

---

### 2) Değer ve Piyasa (Aşınma) Sistemi

- Amaç: Satın alınan ürünlere ödenen tutarın “değer” olarak yazılması; aşınma (float) ile dinamik “piyasa değeri aralığı” üretilmesi.

#### Sipariş Akışı ve Değer Atanması
- İşletmelerde yapılan siparişlerde (tekli/çoklu):
  - Müşterinin ödediği toplam tutar işletme kasasına girer.
  - Üretim maliyeti olarak ücretin %50’si işletme kasasından otomatik düşülür.
  - Ürün oyuncunun envanterine eklenirken şu metadata yazılır:
    - `extra.valueCents`: Birim fiyat (cent)
    - `extra.marketFloat`: Aşınma float (0.05–0.45 arası başlangıç)
- Not: Bu sayede her eşya “kişisel değer” kazanır; fiyat geçmişi RP’de önemlidir.

#### Aşınma (Wear Float) Katmanları
- Eşya aşınması 5 kademede gösterilir:
  - Üretimden Yeni Çıkmış: 0.00–0.07
  - Az Aşınmış: 0.07–0.15
  - Orta Aşınmış: 0.15–0.38
  - Ağır Aşınmış: 0.38–0.45
  - Eskimiş: 0.45–1.00

#### Piyasa Değeri Hesabı
- Gösterim: “Değer” + “Aşınma (float)” + “Piyasa Değeri” (min–max aralığı)
- Katsayılar (değerin çarpanı):
  - Üretimden Yeni Çıkmış: 0.95–1.20
  - Az Aşınmış: 0.85–1.05
  - Orta Aşınmış: 0.70–0.90
  - Ağır Aşınmış: 0.55–0.75
  - Eskimiş: 0.35–0.60

#### UI Entegrasyonu
- Envanter → Sağ tık → Bilgi:
  - Değer: ör. $300.00
  - Aşınma: ör. Orta Aşınmış (0.22)
  - Piyasa Değeri: ör. $210.00 – $270.00
- `SpawnedItem.basicData()` bu alanları `extra` içine ekler; React context menüsü otomatik gösterir.

#### Roleplay ve Ekonomi Etkileri
- Ürün Yaşlanması: Kullanım/süreçle genişletilebilir; ileriye dönük bakım/tamir sistemleri eklenebilir.
- Fiyat Çeşitliliği: Aynı item türü bile farklı değer/aşınma ile farklı piyasa aralıkları sunar.
- İşletme Dinamikleri:
  - Gelir: Ödeme anında kasaya girer
  - Gider: Üretim maliyeti (%50) otomatik düşer
  - Kar marjı, ürün seçimi ve pazarlama RP’sini zenginleştirir
- Koleksiyon/Premium: Düşük float (Üretimden Yeni Çıkmış) eşyalar “koleksiyon” mantığına evrilebilir.

---

### Genişletme Fikirleri
- Aşınma Güncellenmesi: Kullanım, hasar, çevresel etki, bakım/onarım ile float’ı dinamik güncelleme
- Pazar Yeri: Oyuncu-oyuncu satışta bu değerler UI’da vurgulanabilir
- Sertifikalar: Fatura/sertifika ile `valueCents` ve kaynağın doğrulanması
- Analitik: İşletme paneline ortalama satış değeri, aşınma dağılımı gibi metrikler

---

### Kısa Özet
- Görsel sistemi: Uygun türlere resim atanır; inceleme/şaretme yapılır; RP görselliği artar.
- Değer & Piyasa sistemi: Sipariş fiyatı değer olur; aşınma (float) → piyasa aralığı üretir; ekonomi ve RP çeşitlenir.
