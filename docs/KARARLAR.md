# Kararlar

Durumlar: **Alındı** (uygulanır) · **Açık** (karar bekliyor; ajanlar varsayılanı kullanıp `KARAR-BEKLIYOR: K-xx` diye işaretler).

## Alınanlar

### K-01 · Soru çerçevesi ve "hayır" davranışı (Alındı, 2026-11-08)
Soru şöyle sorulur: "{n} kişi ölecek, karşılığında {şey}'i kullanmaya devam edeceksin. Kabul mü?" **Evet** derse n bir sonraki basamağa çıkar. **Hayır** derse o şeyin sınırı kaydedilir ve kullanıcı **başka bir şeyle** sınanır. 1 kişide hayır demek oyunu bitirmez.
> Not: Kullanıcının ilk anlatımında "hayır → sayı artar" geçiyordu. Sonraki açıklamasına göre yukarıdaki şekilde yorumlandı. Yanlış anlaşıldıysa bu karar güncellenecek.

### K-03 · Gerçeklik aynası = gündelik birimler (Alındı, 2026-11-08)
Ölçek yalnızca gündelik birimlerle hissettirilir: stadyum, AVM, otobüs vb. Bağış ya da "X dolar bir hayat kurtarır" türü karşılaştırmalar **yok**. Gerçek felaketler birim olarak kullanılmaz.

### K-07 · Çok ajanlı çalışma (Alındı, 2026-11-08)
Ana planlayıcı Claude Code'dur. Uygulayıcılar Claude, Codex ve agy (Gemini). Düzen `ORKESTRASYON.md`'de anlatılıyor.

## Açıklar

### K-02 · Sınırın hassasiyeti
- **a)** Sınır = kabul edilen son basamak; sonuç "100 ile 300 arası" diye gösterilir. Basit, az soru gerektirir.
- **b)** Hayır gelince iki basamak arasında 2–3 soruluk ikili arama yapılır. Daha net sayı çıkar ama soru sayısı artar.
- *Önerim:* MVP'de **a**.

### K-04 · İkilem sırası ve sayısı
Önemsizden temele mi gidilsin (Instagram → kahve → araba → internet), rastgele mi, yoksa kullanıcı mı seçsin? Oturum başına kaç ikilem olsun?
- *Önerim:* 5–7 ikilem, ağırlık sırasıyla artan, her ağırlık grubu kendi içinde karışık.

### K-05 · Teknik yığın
Next.js + TS + Tailwind + pnpm, Canvas ile nokta görselleştirme, Supabase ile anonim istatistik, Vercel'de yayın.
- *Önerim:* bu yığın, çünkü ekip metu-proto'dan aynı yığını tanıyor.

### K-06 · Deney modu (anchoring)
Kullanıcıların bir kısmı 1 yerine yüksek bir sayıdan mı başlasın? Başlarsa aynı soruya farklı sınırlar çıkar ve bu ölçülebilir; ama ilk sürümü karmaşıklaştırır.
- *Önerim:* MVP'de yok. Veri modeli `deneyKolu` alanıyla buna hazır.

### K-08 · Ton
Ciddi ve sessiz mi, kara mizah mı, yoksa sona doğru ciddileşen bir akış mı?

### K-09 · İsim ve alan adı
"Bedel" çalışma adı.

### K-10 · Veri ve gizlilik
Anonim oturum. IP ve cihaz kimliği saklanmaz (KVKK). Girişte kısa bir içerik uyarısı gösterilsin mi?
- *Önerim:* evet, tek satırlık bir uyarı olsun.
