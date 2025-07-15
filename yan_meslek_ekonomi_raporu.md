# 🏢 Yan Meslekler Ekonomi Raporu

## 📋 İçindekiler
- [Genel Bakış](#genel-bakış)
- [Para Sistemi](#para-sistemi)
- [Mevcut Yan Meslekler](#mevcut-yan-meslekler)
- [Ekonomi Parametreleri](#ekonomi-parametreleri)
- [Bonus Sistemleri](#bonus-sistemleri)
- [Gecikme Mekanizmaları](#gecikme-mekanizmaları)
- [İstatistik Takibi](#istatistik-takibi)
- [Ekonomi Entegrasyonu](#ekonomi-entegrasyonu)
- [Önerilen Güncellemeler](#önerilen-güncellemeler)

---

## 🎯 Genel Bakış

Yan meslekler sistemi, oyuncuların ana mesleklerinin yanında ek gelir elde edebilecekleri geçici işlerdir. Bu sistem, gerçekçi bir ekonomi simülasyonu sağlayarak oyuncuların farklı gelir kaynaklarına sahip olmasını amaçlar.

### 🏗️ Sistem Mimarisi
- **Modüler Yapı**: Her yan meslek bağımsız bir modül
- **Dinamik Parametreler**: Dünya sabitleri ile ayarlanabilir
- **İstatistik Takibi**: Detaylı performans metrikleri
- **Gecikme Sistemi**: Spam koruması ve denge

---

## 💰 Para Sistemi

### 🪙 Cent Sistemi
Bu sistemde para **cent** cinsinden saklanır ve işlenir:
- **1 Dolar = 100 Cent**
- **$9.50 = 950 cent**
- **$25.00 = 2500 cent**

### 📊 Para Formatlaması
```javascript
// Economy.formatMoney() fonksiyonu
formatMoney(950) // "$9.50"
formatMoney(2500) // "$25.00"
formatMoney(47500) // "$475.00"

// Economy.unformatMoney() fonksiyonu
unformatMoney("$9.50") // 950
unformatMoney("$25.00") // 2500
```

---

## 🚛 Mevcut Yan Meslekler

### 1. 🚌 Otobüs Şoförü (Bus Driver)
- **Araç Sahibi ID**: 1
- **Rota Bazlı Sistem**: Dinamik mesafe ve ödeme
- **Özel Özellikler**: 
  - Çoklu rota seçenekleri
  - Mesafe bazlı ödeme
  - Tur tamamlama sistemi

### 2. 🗑️ Çöp Toplayıcısı (Trash Collector)
- **Araç Sahibi ID**: 2
- **Görev Sayısı**: 30 çöp kutusu
- **Ödeme**: 950 cent/görev ($9.50) + 2500 cent bonus ($25.00)
- **Toplam Kazanç**: 31,000 cent ($310.00)

### 3. 🧹 Cadde Süpürücüsü (Street Sweeper)
- **Araç Sahibi ID**: 3
- **Rota Bazlı**: Dinamik ödeme sistemi
- **Bonus**: 0 cent (bonus yok)
- **Özel Özellikler**: Mesafe bazlı ödeme

### 4. 🏊 Hazine Toplayıcısı (Treasure Collector)
- **Araç Sahibi ID**: 4
- **Görev Sayısı**: 20 nokta
- **Ödeme**: 1625 cent/görev ($16.25) + 2500 cent bonus ($25.00)
- **Toplam Kazanç**: 35,000 cent ($350.00)
- **Risk/Reward**: Yüksek risk, yüksek kazanç

### 5. 🌱 Çim Biçme (Lawn Mower)
- **Araç Sahibi ID**: 5
- **Maksimum Ödeme**: 22,500 cent ($225.00)
- **Bonus**: 2500 cent ($25.00)
- **Özel Özellikler**: Bölge bazlı sistem

### 6. 🚚 Kurye (Delivery Driver)
- **Araç Sahibi ID**: 6
- **Görev Sayısı**: 15 teslimat
- **Ödeme**: 3750 cent/görev ($37.50) + 2500 cent bonus ($25.00)
- **Toplam Kazanç**: 58,750 cent ($587.50)

### 7. 💰 Para Taşıyıcısı (Money Transporter)
- **Araç Sahibi ID**: 7
- **Görev Sayısı**: 10 ATM
- **Ödeme**: 4750 cent/görev ($47.50) + 2500 cent bonus ($25.00)
- **Toplam Kazanç**: 50,000 cent ($500.00)
- **Risk Seviyesi**: Yüksek

### 8. ⚡ Elektrikçi (Electrician)
- **Araç Sahibi ID**: 8
- **Görev Sayısı**: 12 arıza noktası
- **Ödeme**: 11250 cent/görev ($112.50) + 5000 cent bonus ($50.00)
- **Toplam Kazanç**: 140,000 cent ($1,400.00)

---

## 💰 Ekonomi Parametreleri

### 📊 Parametre Tablosu (Cent Cinsinden)

| Meslek | Görev Başına | Maksimum Görev | Tamamlama Bonusu | Toplam Kazanç | Gecikme/Görev | Standart Gecikme |
|--------|-------------|----------------|------------------|---------------|---------------|------------------|
| **Otobüs** | Route bazlı | Değişken | 2500 cent | Route bazlı | Route bazlı | 5 dakika |
| **Çöpçü** | 950 cent | 30 | 2500 cent | 31,000 cent | 30 dakika | 5 dakika |
| **Süpürgeci** | Route bazlı | 1 rota | 0 cent | Route bazlı | 720 dakika | 3 dakika |
| **Hazine** | 1625 cent | 20 | 2500 cent | 35,000 cent | 60 dakika | 5 dakika |
| **Çim Biçme** | Dinamik | 30+ | 2500 cent | 22,500 cent | 900 dakika | 5 dakika |
| **Kurye** | 3750 cent | 15 | 2500 cent | 58,750 cent | 15 dakika | 5 dakika |
| **Para Taşıyıcısı** | 4750 cent | 10 | 2500 cent | 50,000 cent | 360 dakika | 5 dakika |
| **Elektrikçi** | 11250 cent | 12 | 5000 cent | 140,000 cent | 30 dakika | 5 dakika |

### 🧮 Ödeme Hesaplama Formülü

```javascript
// Temel ödeme hesaplama (cent cinsinden)
const basePayout = PAY_PER_OBJECTIVE * completedObjectives;
const finishBonus = finished ? FINISH_BONUS : 0;
const totalPayout = basePayout + finishBonus;

// Ekonomi entegrasyonu
const amount = Economy.request(totalPayout);
player.character.money.putInSalary(amount, `Yan Meslek: ${jobName}`);

// Para formatlaması
const formattedAmount = Economy.formatMoney(amount); // "$XXX.XX"
```

---

## 🎁 Bonus Sistemleri

### 1. 🏆 Tamamlama Bonusu
- **Miktar**: 2500 cent ($25.00) - çoğu meslek için
- **Elektrikçi**: 5000 cent ($50.00) - özel bonus
- **Süpürgeci**: 0 cent - bonus yok
- **Şart**: Tüm görevleri tamamlama
- **Amaç**: Oyuncuları tamamlama için teşvik etme

### 2. 🚀 Çoklu Görev Bonusu
- **Sistem**: Bazı mesleklerde çoklu görev tamamlama
- **Bonus**: Ekstra ödeme veya deneyim puanı
- **Örnek**: Otobüs rotalarında tur tamamlama

### 3. ⚡ Hız Bonusu
- **Sistem**: Belirli sürede tamamlama
- **Bonus**: Zaman bazlı ek ödeme
- **Risk**: Hızlı tamamlama için acele etme

---

## ⏰ Gecikme Mekanizmaları

### 🔒 Gecikme Hesaplama
```javascript
const delay = STANDARD_DELAY + (DELAY_PER_OBJECTIVE * completedObjectives);
player.character.stats[sidejob.delayKey] = player.character.data.playTime + delay;
```

### 📊 Gecikme Tablosu

| Meslek | Standart Gecikme | Görev Başına Gecikme | Maksimum Gecikme |
|--------|------------------|---------------------|-------------------|
| **Otobüs** | 5 dakika | Route bazlı | Route bazlı |
| **Çöpçü** | 5 dakika | 30 dakika | 15 saat |
| **Süpürgeci** | 3 dakika | 720 dakika | 12 saat |
| **Hazine** | 5 dakika | 60 dakika | 20 saat |
| **Çim Biçme** | 5 dakika | 900 dakika | 15 saat |
| **Kurye** | 5 dakika | 15 dakika | 4.25 saat |
| **Para Taşıyıcısı** | 5 dakika | 360 dakika | 60 saat |
| **Elektrikçi** | 5 dakika | 30 dakika | 6 saat |

### 🛡️ Spam Koruması
- **Amaç**: Sürekli yan meslek yapmayı engelleme
- **Mekanizma**: Gecikme süresi boyunca tekrar yapamama
- **Kontrol**: `player.character.stats[sidejob.delayKey] > player.character.data.playTime`

---

## 📈 İstatistik Takibi

### 📊 Takip Edilen Metrikler

#### **Zaman İstatistikleri**
- `SIDEJOB_[JOB]_TIME`: Toplam çalışma süresi
- `SIDEJOB_[JOB]_DELAY`: Son gecikme zamanı

#### **Performans İstatistikleri**
- `SIDEJOB_[JOB]_LOADED/DELIVERED`: Tamamlanan görev sayısı
- `SIDEJOB_[JOB]_EARNED`: Toplam kazanç (cent cinsinden)
- `SIDEJOB_[JOB]_TODAY`: Bugün yapılan meslek sayısı
- `SIDEJOB_[JOB]_DONE`: Tamamlanan meslek sayısı

### 📋 İstatistik Örneği (Çöpçü)
```javascript
// Zaman takibi
player.character.stats.SIDEJOB_TRASH_TIME += Math.ceil((now.getTime() - this.startTime.getTime()) / 1000);

// Performans takibi (cent cinsinden)
player.character.stats.SIDEJOB_TRASH_LOADED += this.objective;
player.character.stats.SIDEJOB_TRASH_EARNED += payout; // 950 * objective + 2500
player.character.stats.SIDEJOB_TRASH_TODAY++;
if(finished) player.character.stats.SIDEJOB_TRASH_DONE++;
```

---

## 🏦 Ekonomi Entegrasyonu

### 💸 Para Sistemi
```javascript
// Ekonomi sisteminden para çekme (cent cinsinden)
const amount = Economy.request(payout);

// Maaş hesabına yatırma
player.character.money.putInSalary(amount, `Yan Meslek: ${jobName} - ${description}`);

// Para formatlaması
const formattedAmount = Economy.formatMoney(amount); // "$XXX.XX"
```

### 📊 Ekonomi Etkisi
- **Para Üretimi**: Ekonomi sistemine para ekleme
- **Enflasyon Kontrolü**: Dinamik fiyatlandırma
- **Denge**: Arz/talep dengesi

---

## 🔄 Önerilen Güncellemeler

### 1. 🎯 Dinamik Fiyatlandırma
```javascript
// Önerilen sistem (cent cinsinden)
static calculatePayPerObjective(player, basePay) {
    const level = player.character.data.level;
    const skill = player.character.skill.getJobSkill(jobName);
    const economy = Economy.getInflationRate();
    
    return Math.floor(basePay * (1 + (level * 0.01) + (skill * 0.005) + economy));
}
```

### 2. 🌟 VIP Bonus Sistemi
```javascript
// VIP bonus entegrasyonu (cent cinsinden)
const vipBonus = Economy.calculateVIPBonus(player, payout);
const totalPayout = payout + vipBonus;
```

### 3. ⚖️ Risk/Reward Sistemi
```javascript
// Para taşıyıcısı için risk sistemi (cent cinsinden)
static calculateRiskReward(player, basePay) {
    const successRate = player.character.stats.SIDEJOB_MONEY_TRANSPORTER_SUCCESS_RATE;
    const riskMultiplier = 1 + (successRate * 0.1);
    return Math.floor(basePay * riskMultiplier);
}
```

### 4. 📊 Skill Sistemi
```javascript
// Deneyim bazlı ödeme (cent cinsinden)
const skillLevel = player.character.skill.getJobSkill(jobName);
const skillBonus = skillLevel * 0.02; // %2 per level
return Math.floor(basePay * (1 + skillBonus));
```

### 5. 🎮 Gamification
```javascript
// Başarı sistemi
const achievements = {
    'SPEED_DEMON': 'Hızlı tamamlama',
    'PERFECTIONIST': 'Hata yapmadan tamamlama',
    'MARATHON_RUNNER': 'Uzun süre çalışma'
};
```

---

## 📋 Sonuç

Mevcut yan meslekler sistemi, cent bazlı para sistemi ile çalışmaktadır. Bu sistem, hassas para hesaplamaları için idealdir ve enflasyon kontrolü sağlar.

### 🎯 Ana Hedefler
1. **Dinamik Fiyatlandırma**: Piyasa koşullarına göre değişen fiyatlar
2. **Skill Entegrasyonu**: Deneyim bazlı ödeme artışı
3. **Risk/Reward**: Daha yüksek riskli meslekler için daha yüksek ödeme
4. **Gamification**: Başarı sistemi ve ödüller
5. **Ekonomi Dengesi**: Enflasyon ve deflasyon kontrolü

### 💡 Cent Sistemi Avantajları
- **Hassasiyet**: Kuruş hassasiyetinde hesaplama
- **Performans**: Tam sayı işlemleri
- **Tutarlılık**: Tüm sistemde aynı para birimi
- **Enflasyon Kontrolü**: Hassas fiyat ayarlamaları

---

*Bu rapor, yan meslekler sisteminin mevcut durumunu cent bazlı para sistemi ile analiz eder ve gelecekteki geliştirmeler için yol haritası sunar.* 
