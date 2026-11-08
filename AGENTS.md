# AGENTS.md: ortak kurallar

Bu dosya projede çalışan **tüm** ajanlar için geçerlidir: Claude Code, Codex, agy (Gemini). `CLAUDE.md` ve `GEMINI.md` buraya yönlendirir.

## Roller

- **Kullanıcı (LuffBey):** son karar verici. Commit/push yalnızca onun açık isteğiyle yapılır.
- **Ana planlayıcı (Claude Code, kullanıcının ana oturumu):** `docs/` ve `tasks/BOARD.md` dosyalarının sahibi. Görevleri böler, prompt yazar, sonuçları inceler ve birleştirir.
- **Uygulayıcılar (Claude alt ajanı, Codex, agy):** kendilerine verilen **tek** görevi yaparlar ve handoff raporu yazarlar.

## Kesin kurallar

1. **Commit ve push yok.** Değişiklikleri çalışma ağacında bırak. Branch açmak serbest; commit atmak, push etmek ve PR açmak yasak (kullanıcı açıkça istemedikçe).
2. **Sadece görevin dosyalarına dokun.** Her görev `tasks/BOARD.md` içinde hangi yollara yazabileceğini listeler. Listede olmayan bir dosyayı değiştirmen gerekiyorsa değiştirme, handoff'ta "Açık sorular" kısmına yaz.
3. **`docs/` ve `tasks/BOARD.md` dosyalarını yalnızca ana planlayıcı düzenler.** Uygulayıcılar bunları okur ama değiştirmez.
4. **Sözleşme `docs/VERI-MODELI.md`.** Tipler, basamaklar ve betimlemeler oradaki tanımla birebir uyumlu olmalı. Uyumsuzluk görürsen kendi başına çözme, raporla.
5. **Kararlar `docs/KARARLAR.md`'de.** "Açık" durumdaki bir konuda kendi başına karar verme. Makul bir varsayılan seç, kodda `// KARAR-BEKLIYOR: K-xx` diye işaretle ve handoff'ta belirt.
6. **İş bitince handoff yaz:** `handoffs/<görev-id>-<ajan>.md` (şablon: `handoffs/_SABLON.md`).
7. **Kontroller geçmeden "bitti" deme.** Uygulama iskeleti kurulduktan sonra: `pnpm lint`, `pnpm exec tsc --noEmit`, `pnpm test`. Çalıştırdığın komutları ve sonuçlarını handoff'a yaz. Başarısız olanı gizleme.
8. **Gizli bilgi yok.** `.env*` dosyalarını commit'leme, içeriklerini loglara ya da handoff'a yazma.

## İçerik ve ton kuralları (ürünün özü)

- Betimlemeler **gündelik birimlerle** yapılır: futbol takımı, sınıf, otobüs, uçak, AVM, stadyum, şehir.
- **Gerçek felaketler, savaşlar, saldırılar, depremler ve salgınlar asla birim olarak kullanılmaz.** ("6 Şubat kadar" yasak.)
- Kan, şiddet ya da ölüm görseli yok. İnsanlar nötr noktalarla temsil edilir.
- Kullanıcıyı yargılayan ya da vaaz veren metin yok. Site ayna tutar, hüküm vermez.
- Arayüz dili Türkçe. Metinler ileride i18n'e taşınabilecek şekilde tek yerde tutulur.

## Teknik (öneri, K-05 onaylanınca kesinleşir)

Next.js (App Router) + TypeScript + Tailwind, pnpm. Noktalar Canvas/WebGL ile çizilir (DOM ile çizilmez). Anonim istatistik için Supabase. Testler: oyun mantığı saf TS olarak yazılır ve birim testiyle doğrulanır.
