# Veri modeli (sözleşme)

Paralel çalışan ajanların aynı yapıya göre iş çıkarması için tek kaynak burasıdır. Değişiklikleri yalnızca ana planlayıcı yapar.

## Tipler (taslak)

```ts
/** Kullanıcının sınandığı şey: Instagram, AI kullanımı, araba... */
type Ikilem = {
  id: string;              // "instagram", "ai", "araba" (kebab-case, kalıcı)
  baslik: string;          // "Instagram"
  soru: string;            // "{n} kişi ölecek. Karşılığında Instagram'ı kullanmaya devam edeceksin."
  kategori: "sosyal" | "teknoloji" | "ulasim" | "yeme-icme" | "konfor" | "eglence" | "kisisel";
  agirlik: 1 | 2 | 3;      // 1 = önemsiz alışkanlık, 3 = hayatın temeli (sıralama için, K-04)
};

/** Sayıyı somutlaştıran gündelik birim */
type Betimleme = {
  n: number;               // yaklaşık kişi sayısı
  metin: string;           // "bir futbol takımı"
  kaynak?: string;         // sayının dayanağı (kapasite verisi vs.)
};

type Cevap = "evet" | "hayir";

type IkilemSonucu = {
  ikilemId: string;
  sinir: number | null;    // kabul edilen son n; null = ilk basamakta hayır
  sinirsiz: boolean;       // son basamağa kadar hep evet
  adimlar: { n: number; cevap: Cevap; sureMs: number }[];
};

type Oturum = {
  id: string;              // anonim, rastgele
  baslangic: string;       // ISO tarih
  deneyKolu?: string;      // A/B ya da anchoring deneyi için (K-06)
  sonuclar: IkilemSonucu[];
};
```

## Sayı basamakları (varsayılan)

```
1, 2, 5, 11, 20, 50, 100, 300, 1.000, 5.000, 10.000, 50.000,
100.000, 1.000.000, 10.000.000, 85.000.000, 1.000.000.000, 8.000.000.000
```

- Basamaklar yaklaşık logaritmik artar. Bazıları bilerek betimleme tablosuyla eşleşir (11, 50, 50.000…).
- Sınırın tam olarak nerede olduğunu bulmak için iki basamak arasında ikili arama yapılsın mı? Açık karar: **K-02**.

## Betimleme kuralları

- **Betimleme eşiği: 11.** Bunun altında yalnızca sayı gösterilir.
- n için seçilen betimleme, `Betimleme.n ≤ n` koşulunu sağlayan en büyük kayıttır. Fark büyükse katı söylenir: "300 kişi: dolu bir uçaktan fazla".
  - Kat ifadesinin kuralı ("iki stadyum", "~6 otobüs") içerik görevi T-003'te netleşecek.
- **Yasak:** gerçek felaket, savaş, saldırı, deprem ve salgın kayıpları.
- Her sayının makul bir dayanağı olmalı (`kaynak`).

## Betimleme tablosu (taslak, T-003'te doğrulanacak)

| n (yaklaşık) | Betimleme |
|---|---|
| 11 | bir futbol takımı |
| 30 | bir sınıf |
| 50 | dolu bir şehirlerarası otobüs |
| 150 | tanıdığın herkes |
| 180 | dolu bir yolcu uçağı |
| 500 | bir düğün salonu |
| 1.500 | dolu bir metro treni |
| 5.000 | bir mahalle |
| 20.000 | dolu bir kapalı spor salonu / hafta sonu bir AVM |
| 50.000 | dolu bir stadyum |
| 100.000 | bir ilçe |
| 1.000.000 | büyük bir şehir |
| 15.700.000 | İstanbul |
| 85.000.000 | Türkiye |
| 8.000.000.000 | herkes (sen dahil) |
