# Ana sayfadaki telefon

Ana sayfanın başındaki telefonda görünen uygulamalar `uygulamalar.json`'dan gelir.
Kod değiştirmeye gerek yok: dosyayı düzenlemen yeterli.
Değişiklik GitHub'a kaydedildikten 1–2 dakika sonra sitede görünür.
Tarayıcı önbelleği yüzünden telefonunda en geç 10 dakika içinde yansır.

Bir uygulamaya dokunulunca telefonda şu ekran açılır: uygulama logosu, tek cümlelik bilgi
ve mağaza rozetleri (App Store / Google Play). Ekran görüntüsü gösterilmez; kimse dokunmazsa
telefon kendi kendine uygulama açmaz.

## Klasör düzeni

```
telefon/
  uygulamalar.json      ← telefondaki uygulamaların listesi ve sırası
  tirdas/
    ikon.jpg            ← uygulama ikonu (kare)
  kelimece/ ...
```

Ekran görüntüleri (`1.webp`, `2.webp`) artık telefonda kullanılmıyor. Ana sayfadaki
uygulama kartlarında ise `1.webp` hâlâ gösteriliyor (Tırdaş, Kelimece, Quadmate, Bocu,
Muhasebe, Koyun, Tırdaş.kz); kartlardaki görüntüyü güncellemek için aynı adla üzerine yükle.

## Yeni uygulama eklemek

1. `telefon/yeniuygulama/ikon.png` olarak ikonu yükle (GitHub: **Add file → Upload files**).
2. `uygulamalar.json`'u aç (kalem simgesi), listeye bir blok ekle:

```json
    {
      "ad": "Yeni Uygulama",
      "etiket": "Yeni",
      "alt": "Kısa tanım",
      "ikon": "yeniuygulama/ikon.png",
      "renk": "#101828",
      "bilgi": "Uygulamayı anlatan tek cümle.",
      "magaza": [
        { "ad": "App Store", "url": "https://apps.apple.com/...", "durum": "Yayında" },
        { "ad": "Google Play", "durum": "Kapalı test" }
      ]
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
| `renk`      | hayır   | Uygulama ekranının arka plan rengi, örn. `#0E1B33`. Açık renkte yazı otomatik koyu olur |
| `bilgi`     | hayır   | Logonun altındaki tek cümlelik açıklama |
| `magaza`    | hayır   | Mağaza rozetleri listesi (aşağıya bak) |
| `gizle`     | hayır   | `true` yazarsan silmeden gizler |

### Mağaza rozetleri

Her rozet: `ad` (`App Store` veya `Google Play`), `durum` (rozetin üstündeki küçük yazı:
`Yayında`, `Kapalı test`, `Yakında`…) ve `url`. **`url` yazarsan rozet tıklanır ve mağazaya
gider; `url` yoksa tıklanmayan, kesik çizgili bir rozet olur** (yayında olmayan mağaza için).
Uygulama mağazada yayına çıkınca o rozete `url` ekleyip `durum`'u `Yayında` yap.

## Sıra

- Telefondaki sıra, `uygulamalar.json`'daki sıradır. BeScript ikonu her zaman en sonda durur.
- Klasöre rahatça 11 uygulama sığar (BeScript ile 3 sıra). Daha fazlası olursa klasör kaydırılabilir olur.
