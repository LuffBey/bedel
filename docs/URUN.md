# Ürün: Bedel

## Tek cümle

"Instagram'ı kullanmaya devam etmek için kaç insanın ölmesine göz yumarsın?" sorusunu, sayıyı adım adım büyüterek ve büyük sayıları gündelik birimlerle hissettirerek soran bir site.

## Oyun akışı

Bir oturum birkaç **ikilemden** oluşur. Her ikilem bir **şeyle** ilgilidir (Instagram, AI kullanımı, araba kullanmak…).

```
ikilem başlar (n = basamak[0] = 1)
  │
  ▼
SORU: "{n} kişi ölecek. Karşılığında {şey}'i kullanmaya devam edeceksin. Kabul ediyor musun?"
  │                                   (n ≥ betimleme eşiği ise: "Bu, {betimleme}.")
  ├─ EVET → n bir sonraki basamağa çıkar → SORU
  │          (son basamakta da EVET → "sınırsız" sonucu → sıradaki ikilem)
  │
  └─ HAYIR → ikilemin sonucu kaydedilir → sıradaki ikilem
               • ilk basamakta HAYIR  → "bu şey için kimseyi feda etmedin"
               • sonraki basamakta    → sınır = kabul edilen son n

tüm ikilemler bitti (ya da kullanıcı bitirdi) → SONUÇ EKRANI
```

**Önemli:** Kullanıcı 1 kişide "hayır" derse oyun bitmez, **başka bir şeyle** sınanır. Asıl soru şu: bu kişiyi feda ettirecek bir şey var mı, varsa o ne?

## Betimlemeler (ölçek hissi)

- Eşiğin altında yalnızca sayı gösterilir. Eşikten itibaren sayının yanında **gündelik bir birim** çıkar: "11 kişi: bir futbol takımı", "50.000 kişi: dolu bir stadyum".
- Birimler insanların gözünde canlanabilen yer ve topluluklardır: takım, sınıf, otobüs, uçak, düğün salonu, AVM, stadyum, şehir, ülke.
- Tablo ve kurallar: `VERI-MODELI.md`.

## Görsel dil

- **Her insan bir nokta.** 1 kişide ekranın ortasında tek bir nokta durur. Sayı büyüdükçe noktalar çoğalır, kamera geri çekilir, noktalar kum tanesine döner. 8 milyarda ekran gri bir sise dönüşür.
- Sade ve sessiz bir arayüz. Kan, kırmızı alarm, ölüm ikonu yok.
- Mobil öncelikli, çünkü insanlar siteye Instagram story'den gelecek.

## Sonuç ekranı

- **Senin fiyat listen:** her şey için verdiğin sınır, betimlemesiyle birlikte ("Instagram: bir otobüs dolusu insan").
- **Başkalarıyla kıyas** (anonim istatistik): "İnsanların %62'si bundan önce durdu."
- **Paylaşım kartı:** story formatında görsel.

## Ton

Ayna tutar, hüküm vermez. Kullanıcıyı utandırmaya çalışmayız. Rakamlar ve birimler kendi kendine konuşur.

## Kapsam dışı (şimdilik)

- Hesap ve giriş sistemi
- Kullanıcıların kendi ikilemini eklemesi
- Bağış ya da "gerçek dünyada X dolar bir hayat kurtarır" türü yönlendirmeler (karar K-03)
