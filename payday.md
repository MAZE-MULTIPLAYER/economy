### PayDay Sistemi — Yönetici Rehberi

Bu rehber, PayDay sırasında oyuncuların hesabına yatan tutarın hangi kalemlerden oluştuğunu ve hangi durumlarda nasıl değiştiğini net, teknik olmayan bir dille özetler. Örnekler dolar cinsinden verilmiştir ve iki ondalık basamakla gösterilir (1 birim = 100 cent = 1.00$).

### Nasıl Çalışır?
- Ücretsiz Destek (Yeni Oyuncu): İlk 50 PayDay boyunca oyuncuya 3,000.00$ destek eklenir. Normalde bu dönemde vergi uygulanmaz; ancak evli oyuncularda en az %1 vergi kesintisi görülebilir.
- Maaş Hesabı: Oyuncunun birikmiş maaşı PayDay’de bankaya aktarılır ve sıfırlanır.
- Mesai Kazancı: O dönemki aktif çalışma süresine göre, saatlik 5.000 birim üzerinden hesaplanır.
- Banka Faizi: PayDay öncesi banka bakiyesine göre faiz eklenir. Toplam varlık arttıkça faiz oranı kademeli olarak düşer (yaklaşık %0.5’ten %0.1’e).
- Gelir Vergisi: Brüt toplam gelir üzerinden %1 ile %10 arasında vergi alınır. Toplam varlık arttıkça vergi oranı yükselir. Evli oyuncularda oran %10 indirimli uygulanır; fakat pratikte hiçbir zaman %1’in altına inmez.
- Net Yatırım: Brüt gelirden vergi düşülür ve net tutar bankaya yatırılır.
- Kademe Bilgisi: Uygulanan vergi oranına göre bilgilendirici bir kademe adı atanır (Düşük, Orta, vb.). Bu sadece raporlama/etiket amaçlıdır.

### Sistem Sabitleri ve Etkileri
- Ücretsiz Destek: Varsayılan sistemde konfigüre edilebilir. Bu rehberde 3,000.00$ kullanılmıştır (ilk 50 PayDay).
- BANK_INTEREST_MIN / MAX: Banka faizi oranının alt ve üst sınırı (%0.1 – %0.5 aralığı). Varlık arttıkça oran üst sınıra göre aşağı doğru yaklaşır.
- BANK_INTEREST_DEC_RATE / DEC_VALUE: Toplam varlık her belirli eşiği aştığında faiz oranının ne kadar azalacağını belirler.
- INCOME_TAX_MIN / MAX: Gelir vergisi oranının alt ve üst sınırı (%1 – %10 aralığı). Varlık arttıkça oran alt sınıra göre yukarı doğru yaklaşır.
- INCOME_TAX_INC_RATE / INC_VALUE: Toplam varlık her belirli eşiği aştığında vergi oranının ne kadar artacağını belirler.
- INCOME_TAX_MARRIED_DISCOUNT: Evli oyuncular için vergi oranına uygulanan indirim (%10). Ancak oran hiçbir zaman alt sınırın (genelde %1) altına inmez.
- Saatlik Ücret (Mesai): 5,000 birim/saat. Ödemeye yansıması dolar cinsinden hesaplanır.

### Matematiksel Hesap (Özet)
- Toplam Varlık: V = nakit + banka + ev değeri + araç değeri
- Faiz Oranı: r = max(min_faiz, max_faiz − azalış_adımı × floor(V / azalış_eşiği))
- Vergi Oranı: t = min(max_vergi, min_vergi + artış_adımı × floor(V / artış_eşiği))
- Evlilik İndirimi: t := max(min_vergi, t − t × evlilik_indirimi)
- Mesai Geliri: A_mesai = floor(jobDutyTime × saatlik_ücret / 3600)
- Banka Faizi: B = floor(banka_bakiyesi × r)
- Brüt Gelir: G = (maaş + ücretsiz_destek + A_mesai) + B
- Vergi: Tax = G × t
- Net: Net = G − Tax

### Vergi Kademeleri (Bilgilendirme)
| Kademe Adı | Vergi Oranı Eşiği |
|---|---|
| Düşük Klasman | %0 |
| Düşük Orta Klasman | %2 |
| Orta Klasman | %3.5 |
| Üst Orta Klasman | %5 |
| Düşük Elit Klasman | %6.5 |
| Orta Elit Klasman | %8 |
| En Üst Klasman | %10 |

### Kademelere Giriş Eşikleri (Toplam Varlık Bazında)
Aşağıdaki aralıklar “bekar” oyuncu ve ücretsiz destek dışı durum baz alınarak hesaplanmıştır. Formül: t = %1 + %0.1 × floor(Toplam Varlık / 1,000,000$), t üst sınırı %10’dur.

| Kademe | Uygulanan Vergi Oranı | Toplam Varlık Aralığı (bekar) |
|---|---:|---|
| Düşük Klasman | < %2.00 | 0$ – 9,999,999.99$ |
| Düşük Orta Klasman | ≥ %2.00 ve < %3.50 | 10,000,000.00$ – 24,999,999.99$ |
| Orta Klasman | ≥ %3.50 ve < %5.00 | 25,000,000.00$ – 39,999,999.99$ |
| Üst Orta Klasman | ≥ %5.00 ve < %6.50 | 40,000,000.00$ – 54,999,999.99$ |
| Düşük Elit Klasman | ≥ %6.50 ve < %8.00 | 55,000,000.00$ – 69,999,999.99$ |
| Orta Elit Klasman | ≥ %8.00 ve < %10.00 | 70,000,000.00$ – 89,999,999.99$ |
| En Üst Klasman | ≥ %10.00 | 90,000,000.00$ ve üzeri |

Notlar:
- Evlilik indirimi (%10), vergi oranını düşürerek bir alt kademeye kaymanıza neden olabilir; fakat oran hiçbir zaman %1’in altına inmez.
- Ücretsiz destek döneminde vergi normalde %0’dır; evli oyuncularda minimum %1 uygulanır, bu durumda kademeniz “Düşük Klasman” kalır.
- Aralıklar sistem sabitlerine (INCOME_TAX_MIN/MAX, INC_RATE, INC_VALUE) bağlıdır; bu sabitler değiştirilirse tablo güncellenmelidir.

### Vergi Sınıfları (taxClasses) ve Limitler
Limit değerleri kodda cent cinsinden saklanır; aşağıdaki tabloda dolar karşılıkları verilmiştir.

| Kademe | Limit ($) | Konut Vergisi | Araç Vergisi | Banka Faizi | Gelir Vergisi |
|---|---:|---:|---:|---:|---:|
| Düşük Klasman | 200,000.00$ | %0.04 | %0.08 | %1.00 | %0 |
| Düşük Orta Klasman | 500,000.00$ | %0.08 | %0.12 | %0.85 | %2.00 |
| Orta Klasman | 1,000,000.00$ | %0.12 | %0.15 | %0.70 | %3.50 |
| Üst Orta Klasman | 2,500,000.00$ | %0.16 | %0.20 | %0.55 | %5.00 |
| Düşük Elit Klasman | 5,000,000.00$ | %0.20 | %0.25 | %0.40 | %6.50 |
| Orta Elit Klasman | 10,000,000.00$ | %0.25 | %0.30 | %0.25 | %8.00 |
| En Üst Klasman | Sınır yok | %0.30 | %0.40 | %0.10 | %10.00 |

Notlar:
- “Limit”, o kademeye kadar olan üst varlık sınırını ifade eder; sınırı aşanlar bir üst kademeye geçer. Son kademede sınır yoktur.
- Tablo, `taxClasses` yapılandırmasını yansıtır; bu değerler ekonomideki diğer hesaplamalarla birlikte yorumlanmalıdır.

### Senaryolar (dolar cinsinden)
Not: Aşağıdaki örneklerde dolar cinsinden değerler verilmiştir ve iki ondalık basamakla gösterilmiştir.

#### C-1: Yeni Oyuncu (Bekar, ilk PayDay)
- Nakit ve banka bakiyesi yok, varlık yok.
- Ücretsiz destek: 3,000.00$, vergi yok.
- Net: 3,000.00$
- Kademe: Düşük Klasman

#### C-2: Çalışan (Bekar, orta varlık, 2 saat mesai)
- Örnek: Banka 200,000 birim, nakit 50,000 birim, maaş 3,000 birim, 2 saat mesai.
- Banka faizi: 1,000.00$
- Mesai kazancı: 10,000.00$
- Maaş hesabı aktarımı: 3,000.00$
- Brüt: 14,000.00$
- Vergi (%1): 140.00$
- Net: 13,860.00$
- Kademe: Düşük Klasman

#### C-3: Varlıklı (Evli, yüksek varlık, 1 saat mesai)
- Örnek: Banka 5,000,000 birim, nakit 500,000 birim, toplam varlık yüksek (ev/araç), 1 saat mesai.
- Banka faizi: 21,500.00$ (oran varlığa bağlı olarak azalır)
- Mesai kazancı: 5,000.00$
- Brüt: 26,500.00$
- Vergi (yaklaşık %2.43, evlilik indirimi sonrası): 643.95$
- Net: 25,856.05$
- Kademe: Düşük Orta Klasman

#### C-4: Kenar Durum — Evli + Ücretsiz Destek
- Nakit ve banka bakiyesi yok, evli, ilk 50 PayDay içinde.
- Ücretsiz destek: 3,000.00$
- Vergi (en az %1 uygulanır): 30.00$
- Net: 2,970.00$
- Kademe: Düşük Klasman

### Özet Tablo
| Karakter | Brüt ($) | Vergi Oranı | Vergi ($) | Net ($) | Kademe |
|---|---:|---:|---:|---:|---|
| C-1 Yeni | 3,000.00 | 0% | 0.00 | 3,000.00 | Düşük Klasman |
| C-2 Çalışan | 14,000.00 | 1.0% | 140.00 | 13,860.00 | Düşük Klasman |
| C-3 Varlıklı | 26,500.00 | ~2.43% | 643.95 | 25,856.05 | Düşük Orta Klasman |
| C-4 Evli+Ücretsiz | 3,000.00 | 1.0% | 30.00 | 2,970.00 | Düşük Klasman |

### Saha Notları
- Banka faizi sadece PayDay öncesi bankadaki bakiyeye göre hesaplanır. PayDay’de eklenen tutarlar bir sonraki döneme faiz üretir.
- Birikmiş maaş, PayDay’de bankaya aktarılır ve sıfırlanır.
- Negatif net ödeme mevcut oranlarla ortaya çıkmaz; vergi oranı üst sınırı %10’dur.


