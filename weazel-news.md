## Weazel News Sistem Rehberi

### Genel Bakış
Weazel News; sunucu içi reklam, duyuru ve canlı yayın akışlarını yöneten oluşumdur. Bu rehber; teknik detaylara girmeden, oyuncu ve Weazel personeli için sistemlerin nasıl kullanılacağını açıklar.

- Reklam Sistemi: Anlık reklam verme, teklif/kabul akışı, ücret ve bekleme süresi.
- Toplu Reklam: Belirli aralıklarla tekrarlayan reklamlar.
- Olay Bölgesi (Canlı Yayın Alanı): Saha yayınları için alan oluşturma, isimlendirme ve yayına başlama/bitirme.
- Weazel Fraksiyon Özellikleri: Ekipman (zırhlık), harita işaretleri (Weazel blip), çağrı ve telefon entegrasyonu.

---

### Roller ve Yetkiler
- Vatandaş
  - Reklam verebilir (ücret ve koşullar geçerlidir).
  - Telefon arayüzünde reklam akışını görebilir; Weazel çağırabilir.
- Weazel Personeli
  - Görevdeyken ücretsiz reklam yayınlayabilir.
  - Olay Bölgesi komutlarını kullanarak canlı yayınları yönetebilir, kişileri yayına davet edebilir/bitirebilir.
  - Zırhlık ve fraksiyon blip (geçici işaret) işlemlerini kullanabilir.

---

### Reklam Sistemi
Amaç: Duyuru veya reklam mesajını sunucuya iletmek ve iletişim numarasıyla paylaşmak.

- Görünüm: Reklamlar oyun içi sohbette “Reklam:” etiketiyle görünür; cep telefonundaki reklam listesi de güncellenir.

- Komutlar (Genel Kullanım)
  - `/reklam [yazı]`
    - VIP hesap: Her yerden kullanılabilir.
    - Normal hesap: Bir reklam noktasında (`AdvertisementPoint`) olmanız gerekir.
    - Ücret: Sunucu ekonomisindeki `Weazel Reklam Ücreti` (nakit veya banka).
    - Bekleme: 60 saniyelik bekleme (spam önleme).
  - Telefon: Reklam listesi cep telefonunda anlık güncellenir.

- Komutlar (Weazel Görevde)
  - `/reklam [yazı]` → Ücretsiz, anında yayına çıkar ve telefon listesine düşer.

- Reklam Teklifi/Kabul (Sahada Weazel hizmeti için)
  - `/offerads [oyuncu id] [fiyat] [yazı]` → Hedef oyuncuya ücretli reklam teklifi gönderir.
  - Hedef oyuncu `/acceptads` yazarak öder ve reklam yayınlanır.
    - Ödeme: Nakit veya bankadan otomatik düşer.
    - Yayında mesajla beraber ad ve aktif telefon numarası görünür.

- İletişim Bilgisi
  - Reklamda görünen telefon numarası, oyuncunun o an takılı olan cihazın (sağlayıcının) aktif numarasıdır.

- Kurallar/İpuçları
  - Metin net, kısa ve konuya uygun olmalıdır.
  - Spam ve uygunsuz/kurallara aykırı içerik yasaktır.
  - VIP olsanız bile her reklam arasında 60 saniye bekleme vardır.

---

### Toplu Reklam (Tekrarlayan)
Belirli aralıklarla önceden planlanan sayıda reklamı otomatik yayınlar.

- Komutlar
  - `/toplureklam [miktar] [aralık(dakika)] [yazı]`
    - Örnek: `/toplureklam 5 10 Açık artırma başlıyor!` → 10 dakikada bir, toplam 5 kez yayınlar.
  - `/reklamlistesi` → Aktif toplu reklamları listeler.
  - `/removeads [id]` veya `/reklamsil [id]` → Seçilen toplu reklamı kaldırır.

- Notlar
  - Toplu reklamlar veritabanında saklanır; kalan sayı ve süre otomatik takip edilir.
  - Yetkisiz/abuse tespitinde yönetim kuralları geçerlidir.

---

### Olay Bölgesi (Canlı Yayın Alanı)
Saha yayınlarının düzenli ve kontrollü biçimde yapılmasını sağlar. Olay bölgesine giren yetkili oyuncular bilgilendirilir; yayına başlanabilir veya yayına davet gönderilebilir.

- Alan Kuralları
  - Yarıçap (range) 5–50 arasında olmalıdır (varsayılan 10).

- Komutlar (Türkçe)
  - `/olaybolgesi ekle [yaricap]` → Mevcut konumda yeni Olay Bölgesi oluşturur.
  - `/olaybolgesi isim [yeni_isim]` → İçinde bulunduğunuz Olay Bölgesi adını değiştirir.
  - `/olaybolgesi bilgi` → İçinde bulunduğunuz Olay Bölgesi bilgilerini gösterir.
  - `/olaybolgesi liste` → Tüm Olay Bölgelerini listeler.
  - `/olaybolgesi sil onayla` → İçinde bulunduğunuz Olay Bölgesini siler (onay gerekir).
  - Not: Geriye dönük uyumluluk için eski komut `/livearea` da çalışır.

- Yayın Komutları
  - `/haberler baslat` → Bulunduğunuz Olay Bölgesinde yayını başlatır.
  - `/haberler davet [oyuncu]` → Aynı Olay Bölgesindeki hedef oyuncunun yayınını başlatır.
  - `/haberler durdur` veya `/haberler bitir` → Kendi yayınızı sonlandırır.
  - `/haberler durdur [oyuncu]` → Aynı Olay Bölgesindeki hedefin yayınını bitirir.
  - `/haberler hepsinidurdur` veya `/haberler hepsinibitir` → Aynı Olay Bölgesindeki tüm yayınları kapatır.

- Davranış
  - Bölgeye giriş: Yetkili oyuncular “Olay Bölgesi” bilgilendirmesi görür ve bölgeye bağlanır.
  - Bölgeden çıkış: Bölge bağlantısı kaldırılır; oyuncu yayındaysa otomatik biter.
  - Oyuncu oyundan çıkar: Mevcut yayını otomatik sonlandırılır, bağlantı temizlenir.

---

### Weazel Fraksiyon Özellikleri

- Ekipman (Zırhlık)
  - Olay yerindeki Weazel zırhlık noktalarında `/ekipman` ile menü açılır.
  - “Ekipmanları İade Et” fraksiyona ait eşyaları topluca iade eder.
  - “Ekipmanlar” menüsünden seçilen ekipman envantere eklenir.
  - Fraksiyon serili eşyalar: `WEAZEL-XXXX-XXXX` biçiminde seri atanır.

- Weazel Blip (Harita İşaretleri)
  - `/weazelblip add [sprite] [color] [süre] [isim]` → Geçici işaret ekler (örn. 15m, 1h).
  - `/weazelblip remove [id]` → İşareti siler.
  - `/weazelblip list` → Yakın çevredeki Weazel işaretlerini listeler.
  - Kullanım: Çekim noktası, etkinlik, haber lokasyonu işaretleme. Süre bitince otomatik kalkar.

- Telefon Entegrasyonu
  - Vatandaş: Telefon reklam listesini görür; “Weazel çağır” özelliğiyle çağrı atabilir (sık kullanıma karşı bekleme koruması vardır).
  - Weazel: Görevde olan Weazel sayısı telefon arayüzüne yansır.

- Görev (Duty)
  - Weazel üyesi `/isbasi` ile göreve girip çıkabilir.
  - Görevdeyken `/reklam` ücretsizdir; Weazel adına yayınlanır.

---

### Örnek Akışlar

- Vatandaş Reklam Verme
  1) VIP ise: `/reklam Satılık Sultan, pazarlık payı var.`
  2) VIP değilse: Reklam noktasına gidip aynı komutu kullanır.
  3) Ücret tahsil edilir, reklam yayınlanır, telefon akışı güncellenir.

- Weazel Görevde Anons
  1) `/isbasi` ile göreve gir.
  2) `/reklam Şu saatte canlı yayındayız, detaylar için arayın.` → Ücretsiz yayınlanır.

- Olay Bölgesi ve Yayın
  1) Editör `/olaybolgesi ekle 20` ile alanda bölge açar.
  2) Muhabir bölgeye girer, popup görür.
  3) Editör `/haberler davet [oyuncu]` ile muhabiri yayına başlatır.
  4) İş bitince `/haberler hepsinidurdur` ile yayını kapatır.

---

### Sık Sorulanlar
- Reklam ücreti ne kadar? → Weazel’ın belirlediği `Weazel Reklam Ücreti` geçerlidir; oyun ekonomisine bağlıdır.
- Neden bekleme süresi var? → Spamı önlemek ve adil bir görünürlük sağlamak için.
- Olay Bölgesi niye gerekli? → Saha yayınlarını toplu ve düzenli yönetmek, davet/bitirme kontrollerini kolaylaştırmak için.


