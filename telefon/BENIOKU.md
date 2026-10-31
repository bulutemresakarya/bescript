# Ana sayfadaki telefon

Ana sayfanın başındaki telefonda görünen uygulamalar bu klasörden gelir.
Kod değiştirmeye gerek yok: dosyaları ve `uygulamalar.json`'u düzenlemen yeterli.
Değişiklik GitHub'a kaydedildikten 1–2 dakika sonra sitede görünür.
Tarayıcı önbelleği yüzünden telefonunda en geç 10 dakika içinde yansır.

## Klasör düzeni

```
telefon/
  uygulamalar.json      ← telefondaki uygulamaların listesi ve sırası
  tirdas/
    ikon.jpg            ← uygulama ikonu (kare)
    1.webp              ← ilk ekran görüntüsü
    2.webp              ← ikinci ekran görüntüsü (dokununca geçer)
  kelimece/ ...
```

## Ekran görüntüsünü güncellemek

En kolayı, yeni görüntüyü **aynı adla** yüklemek. Örneğin Tırdaş'ın ilk ekranı için:

1. GitHub'da `telefon/tirdas/` klasörünü aç.
2. **Add file → Upload files** ile yeni görüntüyü yükle.
3. Adı `1.webp` olmalı; eski dosyanın üzerine yazılır.

Adı farklıysa (örneğin telefondan çektiğin `Screenshot_2026.png`) dosyayı yükle,
sonra `uygulamalar.json`'da o uygulamanın `ekranlar` satırına yeni adını yaz.

- Telefonun normal ekran görüntüsü (PNG veya JPG) olduğu gibi kullanılabilir.
  Görüntü telefon çerçevesine üstten hizalanarak sığdırılır.
- Dosya küçük olursa sayfa hızlı açılır. 1 MB'ın altı ideal; WebP veya JPG tercih et.
- 1., 2., 3. … istediğin kadar ekran ekleyebilirsin. Ziyaretçi ekrana dokundukça sırayla geçer.
- **Kişisel bilgi** (telefon numarası, isim, plaka vb.) görünen ekranları yüklemeden önce bulanıklaştır.

`1.webp` aynı zamanda aşağıdaki "Sahada çalışan uygulamalar" kartlarında da kullanılır
(Tırdaş, Kelimece, Quadmate, Bocu). Orayı da birlikte günceller.

## Yeni uygulama eklemek

1. Bilgisayarında `yeniuygulama` adlı bir klasör hazırla; içine `ikon.png` ve ekran
   görüntülerini (`1.png`, `2.png` …) koy.
2. GitHub'da `telefon/` klasörünü aç, **Add file → Upload files** sayfasına bu klasörü
   olduğu gibi sürükle bırak. GitHub klasörü içindekilerle birlikte oluşturur.
3. `uygulamalar.json`'u aç (kalem simgesi), listeye bir blok ekle:

```json
    {
      "ad": "Yeni Uygulama",
      "etiket": "Yeni",
      "alt": "Kısa tanım",
      "ikon": "yeniuygulama/ikon.png",
      "renk": "#101828",
      "ekranlar": ["yeniuygulama/1.png", "yeniuygulama/2.png"]
    }
```

Bloklar arasına **virgül** koymayı unutma. Son bloktan sonra virgül olmaz.
JSON bozulursa telefonda yalnızca BeScript ikonu görünür.
Şüphelendiğinde metni https://jsonlint.com adresine yapıştırıp kontrol edebilirsin.

### Alanlar

| alan        | zorunlu | ne işe yarar |
|-------------|---------|--------------|
| `ad`        | evet    | Uygulamanın adı (açılış ekranında ve alttaki etikette) |
| `ikon`      | evet    | İkon dosyası, `telefon/`'a göre yol |
| `etiket`    | hayır   | İkonun altındaki kısa ad. Yoksa `ad` kullanılır |
| `alt`       | hayır   | Telefonun altındaki etikette adın yanındaki kısa tanım |
| `renk`      | hayır   | Açılış ekranının arka plan rengi, örn. `#0E1B33`. Açık renkte yazı otomatik koyu olur |
| `ekranlar`  | hayır   | Ekran görüntüleri listesi. Yoksa yalnızca açılış ekranı görünür |
| `durum`     | hayır   | Açılış ekranında rozet: `Yakında`, `Kapalı test` gibi |
| `aciklama`  | hayır   | Açılış ekranında rozetin altındaki kısa cümle |
| `gizle`     | hayır   | `true` yazarsan silmeden gizler |

## Sıra ve otomatik tanıtım

- Telefondaki sıra, `uygulamalar.json`'daki sıradır. BeScript ikonu her zaman en sonda durur.
- Kimse dokunmadığında telefon, **ekran görüntüsü olan ilk 4 uygulamayı** sırayla açıp kapatır.
- Klasöre rahatça 11 uygulama sığar (BeScript ile 3 sıra). Daha fazlası olursa klasör kaydırılabilir olur.
