# SC tipi iş dosyası bilgileri

[English](SC-Type-en.md)

Bu bölüm, TT425 kılavuzuna eklenen SC tipi kesim/iş dosyası başvurusudur. Alan açıklamaları `TT426 SC type cut file description -en.xlsx` dosyasının **Descriptions** sayfasından, örnek kayıtlar `TT426_SCType_Sample.CSV` dosyasından alınmıştır. Kaynak dosyalardaki TT426 adlandırması korunmuştur.

Özgün CSV yerine temsili müşteri, üretim, profil ve dosya yolu değerleri içeren bir örnek sunulmuştur.

> **Not:** Bu SC tipi iş dosyası, HMS_W arayüzünü kullanan makinelerde kullanılabilir. CSV dosyasında aşağıda listelenen alanların tamamının bulunması gerekmez. Dosyanın tanınması ve kesim için gerekli alanlar (`id`, `ksn`, `ksnbar`, `code`, `ktnbar`, `l`, `r`) ile uygulamanın veya seçilen FastReport etiket/barkod şablonunun kullandığı alanlar korunmalıdır. Yalnızca baskıda kullanılan alanlar, şablonda kullanılmıyorsa CSV'ye eklenmeyebilir. HMS_W, `nccode`, `isfix` ve `subcust` alanlarını okumaz; bu sütunlar tamamen kaldırılabilir. Makro desteği yoktur.
>
> `DATA1` her zaman yalnızca etiket alanı değildir: sayısal değer içerdiğinde HMS_W bu değeri profil yüksekliği olarak da kullanır. Makinenin çalışma biçimi bu değere ihtiyaç duyuyorsa sütun korunmalıdır.

## Dosya yapısı

Tam başvuru örneğinde alan ayırıcı noktalı virgüldür (`;`). İlk satır 29 alanın başlığını içerir; sonraki her satır bir parçayı tanımlar. Bu, 29 sütunun tamamının bulunmasını zorunlu kılan bir yapı değildir. HMS_W, SC alanlarını başlık adına göre okur; sütun sırası değişebilir. Başlık adları korunmalı ve her satırdaki değerler başlıklarıyla eşleşmelidir. Bir sütun kaldırıldığında hem başlığı hem de tüm parça satırlarındaki karşılık gelen değeri kaldırılmalıdır. Sütun korunup değeri boş bırakılıyorsa ayırıcı korunur. Tam örneğin başlığı aşağıdaki gibidir:

```text
id;ksn;ksnbar;ktn;ktnbar;l;r;code;info;width;height;trolley;box;orientation;reinf;reinfbar;pos;prono;offno;customer;date;nccode;isfix;colorcode;colorinfo;mainprofile;subcust;image;DATA1
```

[Temsili CSV örneğini indir](downloads/SCType_Example.csv)

## Alan açıklamaları

Kesim ve etiket sütunlarında **Evet**, kaynakta açıkça işaretlenen alanları gösterir. **—**, kaynakta işaret/açıklama olmadığını belirtir; alanın zorunlu olup olmadığını ifade etmez. `String(255)` metin, `Integer` tam sayı, `Double` ondalıklı sayıdır. `l` ve `r`, iki sayıyı `|` ile birleştirir.

| Alan | Tür | Kesim | Etiket | Açıklama |
| --- | --- | --- | --- | --- |
| `id` | String(255) | — | Evet | Parça kimliği. |
| `ksn` | Integer | — | Evet | Çubuk numarası. Aynı numarayı taşıyan satırlar aynı çubuğa aittir. Örnekte ilk dört parça 1 numaralı, sonraki beş parça 2 numaralı çubuktadır. |
| `ksnbar` | Double | — | Evet | Çubuk uzunluğu. Çubuk kimliği `ksn` alanındadır. `59800` değeri 5980,0 mm anlamına gelir; son hane ondalık basamaktır. |
| `ktn` | Integer | — | Evet | Aynı çubuk içindeki parça sırası. Örnekte 1 numaralı çubukta 1–4 arasında dört parça bulunur. |
| `ktnbar` | Double | Evet | Evet | Parça uzunluğu. `4710` değeri 471,0 mm anlamına gelir; son hane ondalık basamaktır. |
| `l` | Double &#124; Double | Evet | Evet | Parçanın başlangıcındaki kesim açısı. `&#124;` öncesi tilt, sonrası pivot açısıdır. Ondalık değer kullanılabilir: `45.55&#124;90.00`. |
| `r` | Double &#124; Double | Evet | Evet | Parçanın sonundaki kesim açısı. `&#124;` öncesi tilt, sonrası pivot açısıdır. Ondalık değer kullanılabilir: `45.55&#124;90.00`. |
| `code` | String(255) | — | Evet | Profil kodu. |
| `info` | String(255) | — | Evet | Çubuk hakkında ayrıntılı bilgi. |
| `width` | Double | — | Evet | Kasa genişliği. |
| `height` | Double | — | Evet | Kasa yüksekliği. |
| `trolley` | String(255) | — | Evet | Parçanın yerleştirileceği araba. |
| `box` | String(255) | — | Evet | Parçanın arabadaki yer/kutu numarası. |
| `orientation` | String(255) | — | Evet | Kesilen parçanın pencere üzerindeki konumu. Aşağıdaki yön kodları tablosuna bakın. Bazı işleme merkezleri bu veriyi kullanır. |
| `reinf` | String(255) | — | Evet | Destek sacı kodu. |
| `reinfbar` | Double | — | Evet | Destek sacı uzunluğu. |
| `pos` | String(255) | — | Evet | Pencere numarası (poz). Aynı pencereye ait tüm parçalar aynı değeri taşır; her pencerenin değeri farklıdır. |
| `prono` | String(255) | — | Evet | Üretim numarası. |
| `offno` | String(255) | — | Evet | Sözleşme numarası. |
| `customer` | String(255) | — | Evet | Müşteri bilgisi. |
| `date` | String(255) | — | Evet | Tarih. |
| `nccode` | String(255) | — | — | HMS_W bu alanı okumaz ve makro desteklemez. Sütun kaldırılabilir. |
| `isfix` | — | — | — | Kaynak dosyada tür ve açıklama belirtilmemiştir. Örnek CSV’de değer `0` olarak verilmiştir. HMS_W bu alanı okumaz; sütun kaldırılabilir. |
| `colorcode` | String(255) | — | — | Renk kodu. Aşağıdaki renk kodları tablosuna bakın. Haffner dört kafa köşe kaynak ve köşe temizleme makinelerinde kullanılır. |
| `colorinfo` | String(255) | — | Evet | Renk açıklaması. |
| `mainprofile` | String(255) | — | Evet | Ana profil kodu. Bazı işleme merkezleri bu veriyi kullanır. |
| `subcust` | — | — | — | Müşteri hakkında ayrıntılı bilgi. Kaynak dosyada veri türü belirtilmemiştir. HMS_W bu alanı okumaz; sütun kaldırılabilir. |
| `image` | String(255) | — | Evet | Etikete/barkoda görsel basılacaksa görsel dosyasının yolu. |
| `DATA1` | String(255) | — | Evet | Etikete/barkoda basılacak ek bilgi (isteğe bağlı). HMS_W, sayısal değeri profil yüksekliği olarak da kullanır; makinenin çalışma biçimi gerektiriyorsa korunmalıdır. |

## Uzunluk ve açı gösterimi

Kaynakta `ksnbar` ve `ktnbar` için son hane ondalık basamak olarak açıklanır:

- `ksnbar = 59800` → 5980,0 mm.
- `ktnbar = 4710` → 471,0 mm.

`width`, `height` ve `reinfbar` için kaynakta bu ölçekleme kuralı ayrıca belirtilmemiştir.

Açı biçimi `tilt|pivot` şeklindedir. Örnek CSV’de `l = 45|90` ve `r = 135|90` kullanılır. Ondalık açı örneği: `45.55|90.00`.

## Yön kodları (`orientation`)

| Kod | Konum |
| --- | --- |
| 0 | Önemsiz |
| 1 | Alt taraf (SILL / Bottom) |
| 2 | Sol taraf (Left) |
| 3 | Üst taraf (HEAD / Top) |
| 4 | Sağ taraf (RIGHT) |

Örnek CSV, `HEAD (3)`, `RIGHT (4)` ve `SILL (1)` gibi metin ve kodu birlikte içerir.

## Renk kodları (`colorcode`)

| Kod | Açıklama |
| --- | --- |
| `00` | Contasız beyaz |
| `01` | Contasız, alt taraf renkli |
| `02` | Contasız, üst taraf renkli |
| `03` | Contasız, üst ve alt taraf renkli |
| `10` | Contalı beyaz |
| `11` | Contalı, alt taraf renkli |
| `12` | Contalı, üst taraf renkli |
| `13` | Contalı, üst ve alt taraf renkli |

Bu kodlar Haffner dört kafa köşe kaynak ve köşe temizleme makinelerinde kullanılır. `colorinfo`, ayrı bir renk açıklaması alanıdır.

## Makro/NC işlem alanı (`nccode`)

HMS_W arayüzünü kullanan makinelerde makro desteği yoktur ve `nccode` okunmaz. Bu sütun tamamen kaldırılabilir; boş bir yer tutucu olarak dosyada kalması gerekmez. HMS_W tarafından okunmayan `isfix` ve `subcust` sütunları da kaldırılabilir. Başka bir sistemle uyumluluk için bu sütunlar korunuyorsa `nccode` boş bırakılmalı ve boş değerlerin ayırıcıları korunmalıdır.

## Temsili parça örneği

```csv
id;ksn;ksnbar;ktn;ktnbar;l;r;code;info;width;height;trolley;box;orientation;reinf;reinfbar;pos;prono;offno;customer;date;nccode;isfix;colorcode;colorinfo;mainprofile;subcust;image;DATA1
1;1;59800;1;4710;45|90;135|90;PROFILE001;DEMO PROFILE;4650;4100;1;1;HEAD (3);REINF001;0;1;DEMO-PR001;DEMO-CT001;DEMO CUSTOMER;2026-01-01;;0;10;WHITE WITH GASKET;MAIN001;;images/part-001.wmf;
```

Bu kayıt, 1 numaralı çubuğun 1. parçasını tanımlar: çubuk uzunluğu 5980,0 mm, parça uzunluğu 471,0 mm, profil kodu `PROFILE001`, konum `HEAD (3)`, araba `1` ve kutu `1`. Müşteri, üretim, profil ve dosya yolu değerleri temsilidir. Görsel yolu yalnızca biçimi göstermek için verilmiştir.

[Türkçe kılavuza dön](Turkish.md)
