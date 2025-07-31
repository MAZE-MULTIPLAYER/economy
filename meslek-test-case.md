# Meslek Test Dokümantasyonu

Bu dokümantasyon, RAGE-MP sunucusundaki tüm ana meslekler ve yan mesleklerin test edilmesi için hazırlanmıştır. Her meslek için gereken araçlar, sistem açıklamaları ve location ekleme parametreleri detaylanmıştır.

## İçindekiler

1. [Ana Meslekler](#ana-meslekler)
   - [Taxi Driver (Taksi Şoförü)](#taxi-driver-taksi-şoförü)
   - [Mechanic (Mekanik)](#mechanic-mekanik)
   - [Trucker (Tırci)](#trucker-tırci)
   - [Farmer (Çiftçi)](#farmer-çiftçi)
   - [Fishing (Balıkçı)](#fishing-balıkçı)
   - [Cargo (Kargo)](#cargo-kargo)
   - [Chopshop (Araç Çalma)](#chopshop-araç-çalma)

2. [Yan Meslekler](#yan-meslekler)
   - [Bus Driver (Otobüs Şoförü)](#bus-driver-otobüs-şoförü)
   - [Trash Collector (Çöpçü)](#trash-collector-çöpçü)
   - [Lumberjack (Oduncu)](#lumberjack-oduncu)
   - [Miner (Madenci)](#miner-madenci)
   - [Street Sweeper (Sokak Temizleyicisi)](#street-sweeper-sokak-temizleyicisi)
   - [Treasure Collector (Hazine Avcısı)](#treasure-collector-hazine-avcısı)
   - [Lawn Mower (Çim Biçme)](#lawn-mower-çim-biçme)
   - [Delivery Driver (Teslimatçı)](#delivery-driver-teslimatçı)
   - [Money Transporter (Para Taşıyıcısı)](#money-transporter-para-taşıyıcısı)
   - [Electrician (Elektrikçi)](#electrician-elektrikçi)

3. [Location Ekleme Sistemi](#location-ekleme-sistemi)

---

## Ana Meslekler

### Taxi Driver (Taksi Şoförü)

**Sistem Açıklaması:**
- Müşteri taşıma ve taksimetre sistemi
- NPC'li görevler ve oyuncu çağrıları
- Maaş + mesai ücreti sistemi
- Taksi satın alma imkanı

**Gerekli Araç:**
- Model: `taxi` (Taxi)
- Araç sahibi: Oyuncu (satın alınmalı)

**Test Komutları:**
- `/meslekgir` - Mesleğe katılma
- `/meslekisbasi` - Mesaiye başlama/bitirme
- `/taksimetre [aç|kapat|başlat|durdur|sıfırla|belirle]` - Taksimetre kontrolü
- `/taksigorevi` - NPC görevleri
- `/taksial` - Taksi satın alma
- `/meslekayril` - Meslekten ayrılma

**Location Parametreleri:**
```
/location add Job Taxi Driver
```

**Test Senaryosu:**
1. Location'u taxi noktasına ekle
2. Taksi satın al (level 3+ gerekli)
3. Mesaiye başla (taksi içinde)
4. Taksimetre testleri
5. NPC görevlerini test et
6. Müşteri taşıma simülasyonu

---

### Mechanic (Mekanik)

**Sistem Açıklaması:**
- Araç tamir sistemi (motor, gövde, lastik)
- Modifiye sistemi
- Component (parça) sistemi
- Workshop entegrasyonu
- Müşteri çağrı sistemi

**Gerekli Araç:**
- Model: `towtruck` (Çekici) - işbaşı için
- Component parçaları gerekli

**Test Komutları:**
- `/meslekgir` - Mesleğe katılma
- `/meslekisbasi` - Mesaiye başlama/bitirme
- `/mekanik` - Tamir menüsü
- `/modonizleme` - Modifiye menüsü
- `/parcaal` - Component satın alma

**Location Parametreleri:**
```
/location add Job Mechanic
/location add MechanicArea (mesai alanı)
/location add ModShop (modifiye dükkanı)
/location add ModArea (modifiye alanı)
/location add Warehouse Component (parça deposu)
```

**Test Senaryosu:**
1. Location'ları ekle
2. Mekanik mesleğine katıl
3. Çekici araç spawn et
4. Mesaiye başla
5. Hasarlı araç getir ve tamir et
6. Modifiye sistemini test et
7. Component satın alma

---

### Trucker (Tırci)

**Sistem Açıklaması:**
- Tır ile kargo taşıma
- Dorse sistemi
- Mission tabanlı görevler
- Sözleşme sistemi
- Çeşitli dorse tipleri

**Gerekli Araç:**
- Tır modelleri (örn: `phantom`, `hauler`)
- Dorse (trailer) sistemi

**Test Komutları:**
- `/meslekgir` - Mesleğe katılma
- `/gorevler` - Görev listesi
- `/kontratlar` - Sözleşme listesi
- `/dorse` - Dorse bulma/sıfırlama
- `/goreviptal` - Görev iptal
- `/kontratiptal` - Kontrat iptal

**Location Parametreleri:**
```
/location add Job Trucker
```

**Test Senaryosu:**
1. Location'u ekle
2. Tır spawn et
3. Mesleğe katıl
4. Görev al veya kontrat seç
5. Dorseyi al
6. Teslimat yap
7. Görev bitirme

---

### Farmer (Çiftçi)

**Sistem Açıklaması:**
- Basit meslek sistemi
- Sadece mesleğe katılma
- Çiftlik sistemi ile entegre

**Test Komutları:**
- `/meslekgir` - Mesleğe katılma
- `/meslekayril` - Meslekten ayrılma

**Location Parametreleri:**
```
/location add Job Farmer
```

**Test Senaryosu:**
1. Location'u ekle
2. Mesleğe katıl
3. Çiftlik sistemi ile birlikte test et

---

### Fishing (Balıkçı)

**Sistem Açıklaması:**
- Balık tutma aktivitesi
- Farklı balık türleri ve nadirlikleri
- Fishing rod gerekli
- Su yönünde olma kontrolü
- Minigame sistemi

**Gerekli Eşya:**
- Fishing Rod (Olta)

**Test Komutları:**
- `/baliktut` - Balık tutmaya başla
- `/balikdurdur` - Balık tutmayı durdur

**Location Parametreleri:**
```
/location add FishArea (özel balık alanı)
/location add FishingSpot (balık noktası)
```

**Test Senaryosu:**
1. Location'ları ekle
2. Fishing rod edin
3. Su kenarına git
4. Balık tutmayı test et
5. Minigame'i tamamla

---

### Cargo (Kargo)

**Sistem Açıklaması:**
- Koli taşıma sistemi
- Warehouse ve çiftlik entegrasyonu
- Depozit sistemi
- Koli bırakma streaki

**Gerekli Araç:**
- Kamyonet (van tipi araç)

**Test Komutları:**
- `/kolial` - Koli alma

**Location Parametreleri:**
```
/location add Job Cargo
/location add Warehouse [Plant|Fish Factory|Ore Refinery|Lumber Mill|Meat Factory|Seed Warehouse|Component]
```

**Test Senaryosu:**
1. Location'ları ekle
2. Mesleğe katıl
3. Warehouse'dan koli al
4. Teslimat yap
5. Koli bırakma test et

---

### Chopshop (Araç Çalma)

**Sistem Açıklaması:**
- Yasadışı meslek (level 6+ gerekli)
- Araç parçalama sistemi
- Dinamik lokasyon sistemi (her saat değişir)
- Minimum polis gereksinimi
- Oyuncu araçları hedefleme

**Test Komutları:**
- `/chopshop` - Araç parçalama
- `/chopshopdurdur` - İşlemi durdur

**Location Parametreleri:**
```
/location add IllegalJob Vehicle Stealer
```

**Not:** Chopshop lokasyonları otomatik olarak değişir, manuel ekleme gerekmez.

**Test Senaryosu:**
1. Level 6+ karakter
2. Mesleğe katıl
3. Oyuncu aracı bul
4. Chopshop lokasyonunu bul
5. Araç parçalama işlemi
6. Minimum polis kontrolü

---

## Yan Meslekler

### Bus Driver (Otobüs Şoförü)

**Sistem Açıklaması:**
- Rota tabanlı otobüs sürüş sistemi
- Durak sistemi
- Tur bazında ödeme
- Maksimum tur limiti

**Gerekli Araç:**
- Bus modelleri (`airbus`, `bus`, `coach`, `rentalbus`, `tourbus`)
- Owner: Sidejob

**Test Komutları:**
- `/yanmeslek` - Yan meslek seçimi
- `/busroute` - Rota yönetimi

**Location Parametreleri:**
```
/location add Sidejob Bus Driver
```

**Bus Route Oluşturma:**
```
/busroute add [rota adı]
/busroute addstop [rota id] [durak adı]
/busroute model [rota id] [araç modeli]
/busroute payout [rota id] [mil başına ücret]
/busroute maxlaps [rota id] [maksimum tur]
```

---

### Trash Collector (Çöpçü)

**Sistem Açıklaması:**
- Çöp toplama sistemi
- TrashDump location'ları gerekli
- Objektif bazında ödeme
- Tamamlama bonusu

**Gerekli Araç:**
- Trash truck (çöp kamyonu)
- Owner: Sidejob

**Test Komutları:**
- `/yanmeslek` - Yan meslek seçimi

**Location Parametreleri:**
```
/location add Sidejob Trash Collector
/location add TrashDump (çöp konumları)
```

---

### Lumberjack (Oduncu)

**Sistem Açıklaması:**
- Ağaç kesme sistemi
- Balta gerekli
- Farklı ağaç türleri

**Gerekli Eşya:**
- Balta (Hatchet)

**Test Komutları:**
- `/trees` - Ağaç yönetimi

**Location Parametreleri:**
```
/location add Job Lumberjack
```

**Ağaç Ekleme:**
```
/trees add [model] [tür] [miktar]
```

---

### Miner (Madenci)

**Sistem Açıklaması:**
- Maden çıkarma sistemi
- Delici gerekli
- Farklı maden türleri

**Gerekli Eşya:**
- Driller (Delici)

**Test Komutları:**
- `/ores` - Maden yönetimi
- `/madencilikdurdur` - Madenciliği durdur

**Maden Ekleme:**
```
/ores add [Iron|Silver|Gold|Diamond] [miktar] [model]
```

---

### Street Sweeper (Sokak Temizleyicisi)

**Sistem Açıklaması:**
- Sokak temizleme sistemi
- Özel araç gerekli

**Gerekli Araç:**
- Street sweeper araç
- Owner: Sidejob

**Location Parametreleri:**
```
/location add Sidejob Street Sweeper
```

---

### Treasure Collector (Hazine Avcısı)

**Sistem Açıklaması:**
- Denizaltı ile hazine toplama
- Submersible araç gerekli

**Gerekli Araç:**
- Submersible
- Owner: Sidejob

**Location Parametreleri:**
```
/location add Sidejob Treasure Collector
```

---

### Lawn Mower (Çim Biçme)

**Sistem Açıklaması:**
- Çim biçme sistemi
- Özel araç gerekli

**Gerekli Araç:**
- Lawn mower araç
- Owner: Sidejob

**Location Parametreleri:**
```
/location add Sidejob Lawn Mower
```

---

### Delivery Driver (Teslimatçı)

**Sistem Açıklaması:**
- Teslimat sistemi
- Delivery araç gerekli

**Gerekli Araç:**
- Delivery vehicle
- Owner: Sidejob

**Location Parametreleri:**
```
/location add Sidejob Delivery Driver
```

---

### Money Transporter (Para Taşıyıcısı)

**Sistem Açıklaması:**
- Para taşıma sistemi
- Zırhlı araç gerekli

**Gerekli Araç:**
- Armored vehicle
- Owner: Sidejob

**Location Parametreleri:**
```
/location add Sidejob Money Transporter
```

---

### Electrician (Elektrikçi)

**Sistem Açıklaması:**
- Elektrik işleri sistemi
- Utility araç gerekli

**Gerekli Araç:**
- Utility vehicle
- Owner: Sidejob

**Location Parametreleri:**
```
/location add Sidejob Electrician
```

---

## Location Ekleme Sistemi

### Temel Komutlar

```bash
# Location ekleme
/location add [tip] [ekstra parametre]

# Location taşıma
/location move [location id]

# Location silme
/location remove [location id]

# Location listeleme
/location find [tip]

# Location ekstra bilgi
/location extra [location id] [ekstra]

# Location label
/location label [location id] [label metni]
```

### Location Tipleri

**Ana Meslekler:**
- `Job` - Ana meslek başvuru noktası
- `IllegalJob` - Yasadışı meslek başvuru noktası

**Yan Meslekler:**
- `Sidejob` - Yan meslek başvuru noktası

**Meslek Alanları:**
- `MechanicArea` - Mekanik çalışma alanı
- `ModShop` - Modifiye dükkanı
- `ModArea` - Modifiye alanı
- `FishArea` - Balıkçılık alanı
- `FishingSpot` - Balık tutma noktası

**Depo/Warehouse:**
- `Warehouse` - Genel depo
- `BlackmarketParts` - Kara borsa

**Diğer:**
- `TrashDump` - Çöp konumu
- `TaxiSpawnNPC` - Taksi NPC spawn noktası

### Polygon Location'lar

Bazı location'lar alan (polygon) gerektirir:
```bash
/location add [tip]
# Polygon çizme modu başlar
# Noktaları işaretle
/location done
```

### Örnek Location Komutları

```bash
# Taksi meslek noktası
/location add Job Taxi Driver

# Mekanik meslek noktası  
/location add Job Mechanic

# Component deposu
/location add Warehouse Component

# Yan meslek noktası (Çöpçü)
/location add Sidejob Trash Collector

# Çöp toplama noktası
/location add TrashDump

# Kara borsa
/location add BlackmarketParts
```

---

## Test Checklist

### Ana Meslekler Test Listesi
- [ ] Taxi Driver - Mesaiye başlama/bitirme, taksimetre, görevler
- [ ] Mechanic - Tamir sistemi, modifiye, component
- [ ] Trucker - Görevler, kontratlar, dorse sistemi
- [ ] Farmer - Mesleğe katılma
- [ ] Fishing - Balık tutma, minigame
- [ ] Cargo - Koli alma/bırakma
- [ ] Chopshop - Araç parçalama

### Yan Meslekler Test Listesi
- [ ] Bus Driver - Rota sistemi, duraklar
- [ ] Trash Collector - Çöp toplama
- [ ] Lumberjack - Ağaç kesme
- [ ] Miner - Maden çıkarma
- [ ] Street Sweeper - Sokak temizleme
- [ ] Treasure Collector - Hazine toplama
- [ ] Lawn Mower - Çim biçme
- [ ] Delivery Driver - Teslimat
- [ ] Money Transporter - Para taşıma
- [ ] Electrician - Elektrik işleri

### Genel Sistem Testleri
- [ ] Location ekleme/kaldırma
- [ ] Araç spawn sistemi
- [ ] Meslek geçiş kontrolleri
- [ ] Ödeme sistemleri
- [ ] Delay/cooldown sistemleri
- [ ] İstatistik takibi

---

## Notlar

1. **Araç Ownership:** Sidejob araçları otomatik spawn olur, ana meslek araçları genellikle oyuncu satın alır
2. **Level Gereksinimleri:** Chopshop için minimum level 6 gerekli
3. **Polis Gereksinimleri:** Chopshop için minimum polis sayısı gerekli
4. **Envanter:** Eşya gerektiren meslekler için envanterde uygun eşyalar olmalı
5. **Tutorial:** Tüm meslekler için tutorial bitirme şartı var
6. **Faction Duty:** Yan mesleklerde faction duty'de olunmaz
