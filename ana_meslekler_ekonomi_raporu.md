# 🏢 Ana Meslekler Ekonomi Raporu

## 📋 İçindekiler
- [Genel Bakış](#genel-bakış)
- [Para Sistemi](#para-sistemi)
- [Mevcut Ana Meslekler](#mevcut-ana-meslekler)
- [Ekonomi Parametreleri](#ekonomi-parametreleri)
- [Maaş Sistemleri](#maaş-sistemleri)
- [İşbaşı (Duty) Sistemi](#işbaşı-duty-sistemi)
- [Servis Çağrı Sistemi](#servis-çağrı-sistemi)
- [İstatistik Takibi](#istatistik-takibi)
- [Ekonomi Entegrasyonu](#ekonomi-entegrasyonu)
- [Önerilen Güncellemeler](#önerilen-güncellemeler)

---

## 🎯 Genel Bakış

Ana meslekler sistemi, oyuncuların tam zamanlı olarak çalışabileceği ve düzenli gelir elde edebileceği mesleklerdir. Bu sistem, yan mesleklerden farklı olarak daha karmaşık ekonomi mekanizmaları ve sürdürülebilir gelir kaynakları sunar.

### 🏗️ Sistem Mimarisi
- **Flag Tabanlı**: Her meslek bir flag ile temsil edilir
- **İşbaşı Sistemi**: Duty durumunda çalışma
- **Servis Çağrıları**: Müşteri talepleri
- **Skill Sistemi**: Deneyim bazlı bonuslar
- **Kontrat Sistemi**: Meslek değiştirme kısıtlamaları

---

## 💰 Para Sistemi

### 🪙 Cent Sistemi
Bu sistemde para **cent** cinsinden saklanır ve işlenir:
- **1 Dolar = 100 Cent**
- **$10.00 = 1000 cent**
- **$15.00 = 1500 cent**

### 📊 Para Formatlaması
```javascript
// Economy.formatMoney() fonksiyonu
formatMoney(1000) // "$10.00"
formatMoney(1500) // "$15.00"
formatMoney(5000) // "$50.00"

// Economy.unformatMoney() fonksiyonu
unformatMoney("$10.00") // 1000
unformatMoney("$15.00") // 1500
```

---

## 🚛 Mevcut Ana Meslekler

### 1. 🚕 Taksi Şoförü (Taxi Driver)
- **Flag**: `JOB_TAXI_DRIVER`
- **İşbaşı Ücreti**: 1500 cent ($15.00)
- **Taksimetre Sistemi**: Dinamik ücretlendirme
- **Özel Özellikler**: 
  - Müşteri çağrı sistemi
  - Taksimetre kontrolü
  - Mesafe bazlı ücretlendirme
  - Minimum/Maksimum ücret limitleri

### 2. 🔧 Mekanik (Mechanic)
- **Flag**: `JOB_MECHANIC`
- **İşbaşı Ücreti**: 1000 cent ($10.00) + Skill bonusu
- **Servis Çağrıları**: Müşteri talepleri
- **Özel Özellikler**:
  - Araç tamir sistemi
  - Parça satışı
  - Modifikasyon hizmetleri
  - Skill bazlı bonus sistemi

### 3. 🚛 Tır Şoförü (Trucker)
- **Flag**: `JOB_TRUCKER`
- **Görev Bazlı**: Sefer başına ödeme
- **Kontrat Sistemi**: Sözleşme bazlı çalışma
- **Özel Özellikler**:
  - Dorse sistemi
  - Yük taşıma
  - Rota bazlı görevler
  - Farklı yük türleri

### 4. 📦 Kargo Taşıyıcısı (Cargo)
- **Flag**: `JOB_CARGO`
- **Şehir İçi**: Teslimat odaklı
- **Paket Bazlı**: Parça başına ödeme
- **Özel Özellikler**:
  - Paket teslimatı
  - Zaman bazlı görevler
  - Adres sistemi

### 5. 🌾 Çiftçi (Farmer)
- **Flag**: `JOB_FARMER`
- **Üretim Bazlı**: Hasat odaklı
- **Günlük Limit**: Tohum satın alma limiti
- **Özel Özellikler**:
  - Tohum ekme
  - Hasat sistemi
  - Ürün satışı
  - Mevsimsel üretim

### 6. 🪓 Oduncu (Lumberjack)
- **Flag**: `JOB_LUMBERJACK`
- **Kereste Üretimi**: Ağaç kesimi
- **Hammadde**: Doğal kaynak kullanımı
- **Özel Özellikler**:
  - Ağaç kesme
  - Kereste işleme
  - Satış sistemi

### 7. 🎣 Balıkçı (Fishing)
- **Flag**: `JOB_FISHER`
- **Balık Tutma**: Dinamik balıkçılık
- **Balık Türleri**: Farklı balık çeşitleri
- **Özel Özellikler**:
  - Balık tutma sistemi
  - Balık satışı
  - Balık türü çeşitliliği

### 8. 🔫 Silah Tüccarı (Arms Dealer)
- **Flag**: `JOB_ARMS_DEALER`
- **Silah Satışı**: Yasal silah ticareti
- **Lisans Sistemi**: Yetki kontrolü
- **Özel Özellikler**:
  - Silah satışı
  - Mühimmat ticareti
  - Lisans kontrolü

### 9. 🚗 Chop Shop (Hurda)
- **Flag**: `JOB_CHOPSHOP`
- **Araç Parçalama**: Hurda işleme
- **Parça Satışı**: İkinci el parçalar
- **Özel Özellikler**:
  - Araç parçalama
  - Parça satışı
  - Hurda işleme

---

## 💰 Ekonomi Parametreleri

### 📊 Parametre Tablosu (Cent Cinsinden)

| Meslek | İşbaşı Ücreti | Ödeme Sistemi | Skill Bonusu | Kontrat Süresi |
|--------|---------------|---------------|--------------|----------------|
| **Taksi** | 1500 cent | Taksimetre + İşbaşı | Yok | 5 payday |
| **Mekanik** | 1000 cent + Skill | Servis + İşbaşı | Var | 5 payday |
| **Tır Şoförü** | Görev bazlı | Sefer başına | Yok | 5 payday |
| **Kargo** | Görev bazlı | Teslimat başına | Yok | 5 payday |
| **Çiftçi** | Üretim bazlı | Hasat başına | Yok | 5 payday |
| **Oduncu** | Üretim bazlı | Kereste başına | Yok | 5 payday |
| **Balıkçı** | Balık bazlı | Balık başına | Yok | 5 payday |
| **Silah Tüccarı** | Satış bazlı | Komisyon | Yok | 5 payday |
| **Chop Shop** | Parça bazlı | Parça başına | Yok | 5 payday |

### 🧮 Ödeme Hesaplama Formülü

```javascript
// Taksi örneği
const dutyPayout = 1500; // cent
const fareMeterPayout = calculateFareMeter(); // cent
const totalPayout = dutyPayout + fareMeterPayout;

// Mekanik örneği
const basePayout = 1000; // cent
const skillBonus = player.character.skill.getJobBonuses('Mechanic', basePayout);
const servicePayout = calculateServiceCost(); // cent
const totalPayout = basePayout + skillBonus + servicePayout;

// Ekonomi entegrasyonu
const amount = Economy.request(totalPayout);
player.character.money.putInSalary(amount, `${jobName} Maaşı`);
```

---

## 💼 Maaş Sistemleri

### 1. 🕐 İşbaşı (Duty) Maaşı
```javascript
// Taksi şoförü
case 'Taxi Driver': {
    salaryAmount = mp.world.constants.JOB_TAXI_DUTY_PAYOUT; // 1500 cent
    break;
}

// Mekanik
case 'Mechanic': {
    salaryAmount = mp.world.constants.JOB_MECHANIC_DUTY_PAYOUT + 
                   player.character.skill.getJobBonuses('Mechanic', basePayout);
    break;
}
```

### 2. 🎯 Servis Çağrı Maaşı
- **Taksi**: Müşteri çağrıları
- **Mekanik**: Araç tamir talepleri
- **Dinamik Ücretlendirme**: Hizmet kalitesine göre

### 3. 📊 Skill Bonus Sistemi
```javascript
// Mekanik skill bonusu
const skillBonus = player.character.skill.getJobBonuses('Mechanic', basePayout);
const totalSalary = basePayout + skillBonus;
```

---

## 🕐 İşbaşı (Duty) Sistemi

### 🔄 Duty Kontrolü
```javascript
// Duty durumu kontrolü
if(player.data.jobDuty) {
    player.character.data.jobDutyTime++;
    
    // Belirli sürelerde maaş ödeme
    if(player.character.data.jobDutyTime >= DUTY_PAYOUT_TIME) {
        mp.events.call('triggerSalary', player, playerJob);
    }
}
```

### 📊 Duty İstatistikleri
- **Çalışma Süresi**: `jobDutyTime`
- **Kazanç**: `JOB_[JOB]_DUTY_EARNED`
- **Zaman**: `JOB_[JOB]_DUTY_TIME`

---

## 📞 Servis Çağrı Sistemi

### 🎯 Çağrı Yönetimi
```javascript
// Çağrı gönderme
jobReport.submit(flags.JOB_TAXI_DRIVER, player);

// Çağrı kabul etme
jobReport.resolve(player, counterId);

// Çağrı listesi
const serviceList = jobReport.getData(player.character.data.job);
```

### 📊 Çağrı Parametreleri
- **Arayan**: Müşteri bilgileri
- **Konum**: Hizmet noktası
- **Telefon**: İletişim bilgisi
- **Durum**: Aktif/Beklemede/Tamamlandı

---

## 📈 İstatistik Takibi

### 📊 Takip Edilen Metrikler

#### **Zaman İstatistikleri**
- `JOB_[JOB]_DUTY_TIME`: Toplam işbaşı süresi
- `JOB_[JOB]_DELAY`: Son gecikme zamanı

#### **Performans İstatistikleri**
- `JOB_[JOB]_DUTY_EARNED`: Toplam kazanç (cent cinsinden)
- `JOB_[JOB]_DUTY_TIME`: Toplam çalışma süresi
- `JOB_[JOB]_MISSIONS_COMPLETED`: Tamamlanan görev sayısı

#### **Özel İstatistikler**
- **Mekanik**: `JOB_MECHANIC_BUY_COMPONENT`, `JOB_MECHANIC_BUY_COMPONENT_SPENT`
- **Taksi**: `JOB_TAXI_FARE_EARNED`, `JOB_TAXI_MISSIONS_COMPLETED`
- **Tır Şoförü**: `JOB_TRUCKER_DELIVERIES`, `JOB_TRUCKER_EARNED`

### 📋 İstatistik Örneği (Mekanik)
```javascript
// Zaman takibi
player.character.stats.JOB_MECHANIC_DUTY_TIME += jobDutyTime;

// Performans takibi (cent cinsinden)
player.character.stats.JOB_MECHANIC_DUTY_EARNED += salaryAmount;
player.character.stats.JOB_MECHANIC_BUY_COMPONENT += componentQuantity;
player.character.stats.JOB_MECHANIC_BUY_COMPONENT_SPENT += componentCost;
```

---

## 🏦 Ekonomi Entegrasyonu

### 💸 Para Sistemi
```javascript
// Ekonomi sisteminden para çekme (cent cinsinden)
const amount = Economy.request(salaryAmount);

// Maaş hesabına yatırma
player.character.money.putInSalary(amount, `${playerJob} Mesai Ücreti`);

// Para formatlaması
const formattedAmount = Economy.formatMoney(amount); // "$XXX.XX"
```

### 📊 Ekonomi Etkisi
- **Para Üretimi**: Ekonomi sistemine para ekleme
- **Enflasyon Kontrolü**: Dinamik fiyatlandırma
- **Denge**: Arz/talep dengesi

---

## 🔄 Önerilen Güncellemeler

### 1. 🎯 Dinamik Maaş Sistemi
```javascript
// Önerilen sistem (cent cinsinden)
static calculateDutySalary(player, baseSalary) {
    const level = player.character.data.level;
    const skill = player.character.skill.getJobSkill(jobName);
    const economy = Economy.getInflationRate();
    const dutyTime = player.character.data.jobDutyTime;
    
    return Math.floor(baseSalary * (1 + (level * 0.01) + (skill * 0.005) + economy + (dutyTime * 0.001)));
}
```

### 2. 🌟 VIP Bonus Sistemi
```javascript
// VIP bonus entegrasyonu (cent cinsinden)
const vipBonus = Economy.calculateVIPBonus(player, salaryAmount);
const totalSalary = salaryAmount + vipBonus;
```

### 3. ⚖️ Performans Bazlı Maaş
```javascript
// Performans bazlı maaş (cent cinsinden)
static calculatePerformanceSalary(player, baseSalary) {
    const completedMissions = player.character.stats.JOB_[JOB]_MISSIONS_COMPLETED;
    const performanceBonus = completedMissions * 50; // 50 cent per mission
    return Math.floor(baseSalary + performanceBonus);
}
```

### 4. 📊 Skill Sistemi Geliştirmeleri
```javascript
// Gelişmiş skill sistemi (cent cinsinden)
const skillLevel = player.character.skill.getJobSkill(jobName);
const skillBonus = skillLevel * 0.02; // %2 per level
const experienceBonus = player.character.stats.JOB_[JOB]_DUTY_TIME * 0.001; // 0.1% per hour
return Math.floor(baseSalary * (1 + skillBonus + experienceBonus));
```

### 5. 🎮 Gamification
```javascript
// Başarı sistemi
const achievements = {
    'SPEED_DEMON': 'Hızlı hizmet',
    'CUSTOMER_SATISFACTION': 'Yüksek müşteri memnuniyeti',
    'LONG_TERM_EMPLOYEE': 'Uzun süreli çalışan',
    'TOP_PERFORMER': 'En iyi performans'
};
```

---

## 📋 Sonuç

Ana meslekler sistemi, yan mesleklerden daha karmaşık ve sürdürülebilir bir ekonomi simülasyonu sağlar. İşbaşı sistemi, skill bonusları ve servis çağrıları ile gerçekçi bir çalışma deneyimi sunar.

### 🎯 Ana Hedefler
1. **Dinamik Maaş**: Performans bazlı ödeme sistemi
2. **Skill Entegrasyonu**: Deneyim bazlı maaş artışı
3. **Servis Kalitesi**: Müşteri memnuniyeti bazlı bonus
4. **Gamification**: Başarı sistemi ve ödüller
5. **Ekonomi Dengesi**: Enflasyon ve deflasyon kontrolü

### 💡 Ana Meslek Avantajları
- **Sürdürülebilir Gelir**: Düzenli maaş sistemi
- **Skill Gelişimi**: Deneyim bazlı ilerleme
- **Servis Çağrıları**: Müşteri talepleri
- **İşbaşı Sistemi**: Gerçekçi çalışma deneyimi
- **Kontrat Sistemi**: Meslek değiştirme kısıtlamaları

---

*Bu rapor, ana meslekler sisteminin mevcut durumunu cent bazlı para sistemi ile analiz eder ve gelecekteki geliştirmeler için yol haritası sunar.* 
