# SSB Contest Runner Birinci Sürüm

Morse Runner'dan esinlenerek en temel işlevleri uygular

## Gereksinimler

- Mevcut yarışma kaydının tüm iletişim bilgilerini görüntüle
  - Kayıtlı çağrı işareti
  - RST
  - Takasiye (Exchange)
  - Doğruluk durumu

- Mevcut yarışma simülasyonunun çalışma süresini görüntüle

- Mevcut yarışma simülasyonunun iletişim istatistiklerini görüntüle
  - Ham
    - İletişim sayısı
    - Çarpan sayısı
    - Elde edilen puan
  - Doğrulanmış
    - İletişim sayısı
    - Çarpan sayısı
    - Elde edilen puan

- Mevcut QSO hızını görüntüle
  - Birim QSO/saat

- Temel yapılandırma
  - Ana çağrı işaretini yapılandır
  - Ses oynatma hızını yapılandır (seviye bazında yapılandırma, yapılandırma ne kadar yüksekse hız o kadar hızlı)
  - Bir yarışmanın toplam süresini yapılandır (dakika)
  - Şu anda yalnızca CQ WPX destekleniyor, gelecekte desteklenen yarışma türleri artırılacak

- Yarışma kontrolü
  - Yarışmayı başlat
  - Yarışmayı bitir

- İletişim kaydı
  - Çağrı işareti gir
  - RST gir (otomatik olarak 59 girer)
  - Takasiye gir
  - Kısayollar
    - N1MM+'a referans, F1-F8 sırasıyla farklı işlevlere karşılık gelir

- Pencere boyutu
  - Pencere boyutu 1280x720 dp olarak sabitlenmiştir

## Yarışma Akışı

![Yarışma Akışı Durum Makinesi](https://github.com/user-attachments/assets/c43f8fdc-fb66-4ef2-8dde-17385545a607)

Zaman aşımı süresi 10 saniye olarak belirlendi

F1-F8 tuşları durum geçişine ek olarak, ilgili ses oynatma işlevini de yürütmelidir

### Durum geçişi içermeyen tuş komutları

- Boşluk tuşu: Klavye imleci CALL ve Exchange giriş kutuları arasında geçiş yapar
- Tab tuşu: Klavye imleci bir sonraki giriş kutusuna atlar
- Shift+Tab tuşu: Klavye imleci bir önceki giriş kutusuna atlar
- Noktalı virgül tuşu: F5+F2 sesini oynatır


## Arayüz Prototipi

![Arayüz Prototipi](https://github.com/user-attachments/assets/eb906032-c1f8-464c-a883-cdda02f58c9b)

## Etkileşim Noktaları

### Mevcut yarışma kaydının tüm iletişim bilgilerini görüntüle

İletişim kayıt görüntüleme alanı Call, RST, Exchange içerir

- Yarışmanın başlama zamanını UTC 00:00:00 olarak al
- İletişim kaydı tamamen doğru olduğunda siyah renkte görüntüle, Corrections alanı boş
- İletişim kaydında hatalı kısımlar olduğunda, karşılık gelen hatalı kısımları kırmızı renkte görüntüle, Corrections alanında karşılık gelen doğru bilgileri göster
- Corrections alanı görüntüleme sırası
  1. Call
  2. RST
  3. Exchange

### Mevcut yarışma simülasyonunun çalışma süresini görüntüle

Mevcut yarışma simülasyonunun çalışma süresi `HH:MM:SS` formatında görüntülenir

### Mevcut yarışma simülasyonunun iletişim istatistiklerini görüntüle

Farklı yarışma kurallarına göre aşağıdaki içerikleri hesapla:

- İletişim sayısı
- Çarpan sayısı
- Puan istatistikleri

İletişim istatistikleri Ham ve Doğrulanmış olmak üzere iki bölüme ayrılır

Ham, kullanıcının iletişim kayıtlarının doğruluğunu dikkate almaz, kullanıcının iletişim kayıtlarının tamamının doğru olduğunu varsayarak yukarıdaki içeriklerin hesaplanmasını yapar

Doğrulanmış ise yarışma kurallarına sıkı sıkıya uyarak yukarıdaki bölüm içeriklerinin hesaplanmasını yapar

### Temel yapılandırma

- Ana çağrı işaretini yapılandır
  - Ana çağrı işareti giriş kutusu yalnızca çağrı işareti ile ilgili içeriği girebilir

- Ses oynatma hızını yapılandır (seviye bazında yapılandırma, yapılandırma ne kadar yüksekse hız o kadar hızlı)
  - Açılır seçim kutusu olarak yapılabilir

- Bir yarışmanın toplam süresini yapılandır (dakika)
  - Giriş kutusu, yalnızca sayı girebilir

- Ses oynatma modunu yapılandır
  - Açılır seçim kutusu, bu sürümde devre dışı
  - Şu anda yalnızca Single Call, yani tek çağrı işareti modu destekleniyor

- Mevcut simüle edilecek yarışmayı yapılandır
  - Açılır seçim kutusu, bu sürümde devre dışı
  - Şu anda yalnızca CQ WPX destekleniyor, gelecekte desteklenen yarışma türleri artırılacak

### Yarışma kontrolü

- Yarışmayı başlat
  - `BAŞLAT` düğmesine tıklayarak yarışmayı başlat
  - Bu sırada `BAŞLAT` düğmesi `DURDUR` olur

- Yarışmayı bitir
  - `DURDUR` düğmesine tıklayarak yarışmayı bitir
  - Bu sırada `DURDUR` düğmesi `BAŞLAT` olur

- Yarışma süresi dolduğunda otomatik olarak biter
  - Yarışma süresi dolduğunda otomatik olarak yarışma biter

### İletişim kaydı

- Çağrı işareti gir
  - Çağrı işareti giriş kutusu yalnızca çağrı işareti ile ilgili içeriği girebilir

```
Çağrı işareti ile ilgili içerik aşağıdaki bölümleri içerir: [harf, sayı, /]
Bunlar içinde harfler otomatik olarak büyük harfe dönüştürülür
```

- RST gir (otomatik olarak 59 girer)
  - SSB olduğu için yalnızca iki haneli sayı girebilir

- Takasiye gir
  - Farklı yarışmalara göre Exchange'in girebileceği içeriği sınırla
  - Şu anda yalnızca CQ WPX destekleniyor, yalnızca sayı girişi destekleniyor

- Kısayollar
  - N1MM+'a referans, F1-F8 sırasıyla farklı işlevlere karşılık gelir
  - Fare tıklayarak işlevi tetikleyebilir, aynı zamanda F1-F8 tuşlarına basarak da işlevi tetikleyebilir

### Pencere boyutu

- Şu anda bilgisayar ucu pencere boyutu 1280x720 px olarak sabitlenmiştir
- Pencere boyutunu değiştirmeye izin verilmez

### QSO hızı

En son 5 QSO'nun ortalama hızına göre mevcut QSO hızı olarak hesapla

Toplam QSO sayısı 5'ten az ise, toplam QSO'nun ortalama hızına göre mevcut QSO hızı olarak hesapla

```
Ortalama hız = QSO'nun harcadığı toplam süre / QSO sayısı, birim QSO sayısı/dakika

Görüntüleme hızı = Ortalama hız * 60
```