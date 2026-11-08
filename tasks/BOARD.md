# Görev panosu

Bu dosyayı yalnızca ana planlayıcı düzenler. Durumlar: `bekliyor` · `hazır` (başlatılabilir) · `sürüyor` · `inceleme` · `bitti`.

## Faz 0: Planlama

| ID | Görev | Ajan | Durum | Bağımlılık |
|---|---|---|---|---|
| T-000 | Repo, kurallar, ürün dokümanı, veri sözleşmesi | Ana planlayıcı | bitti | — |
| — | Açık kararlar: K-02, K-04, K-05, K-08 | Kullanıcı | bekliyor | — |

## Faz 1: Çekirdek (MVP)

| ID | Görev | Ajan | Durum | Bağımlılık |
|---|---|---|---|---|
| T-001 | Next.js iskeleti, lint/tsc/test komutları | Codex | bekliyor | K-05, ilk commit |
| T-002 | Oyun durum makinesi (saf TS + testler) | Codex | bekliyor | T-001 |
| T-003 | İçerik: ikilem listesi + doğrulanmış betimleme tablosu | agy | hazır | — |
| T-004 | Nokta görselleştirme prototipi (1 → 8 milyar) | Claude | bekliyor | T-001 |
| T-005 | Tasarım dili (`DESIGN.md`): tipografi, renk, hareket | Claude / agy | bekliyor | K-08 |

## Faz 2: Sonuç ve paylaşım

| ID | Görev | Ajan | Durum | Bağımlılık |
|---|---|---|---|---|
| T-006 | Anonim istatistik şeması + API (Supabase) | Codex | bekliyor | T-002, K-10 |
| T-007 | Sonuç ekranı + "fiyat listesi" | Claude | bekliyor | T-002, T-004 |
| T-008 | Paylaşım kartı (story görseli) | Claude | bekliyor | T-007 |

---

## Görev ayrıntıları

### T-001 · Next.js iskeleti
- **Yazabileceği yerler:** repo kökündeki yapılandırma dosyaları (`package.json`, `tsconfig.json`, `eslint.config.*`, `next.config.*`, `.gitignore`), `src/app/` (yalnızca boş bir giriş sayfası), `tests/`.
- **Kabul:** `pnpm lint`, `pnpm exec tsc --noEmit` ve `pnpm test` (en az bir örnek testle) geçiyor. README'ye çalıştırma komutları eklenmiş.

### T-002 · Oyun durum makinesi
- **Yazabileceği yerler:** `src/lib/oyun/**`, `tests/oyun*.test.ts`.
- **Kapsam:** `VERI-MODELI.md` tipleri; basamak ilerletme; hayır → sıradaki ikilem; son basamakta evet → sınırsız; betimleme seçimi (en büyük `n ≤ sayı` kaydı); oturum sonucu. React yok, yan etki yok.
- **Kabul:** K-01'deki her dal için test var (ilk basamakta hayır, ortada hayır, sonuna kadar evet, betimleme eşiğinin altı ve üstü).

### T-003 · İçerik
- **Yazabileceği yerler:** `content/ikilemler.json`, `content/betimlemeler.json`, `content/KAYNAKLAR.md`.
- **Kapsam:**
  - En az 20 ikilem, her kategoriden birkaç tane, ağırlıklarıyla birlikte (örnekler: Instagram, TikTok, AI kullanımı, araba kullanmak, uçağa binmek, kahve, internet, müzik, sıcak duş, klima).
  - Betimleme tablosundaki her sayının dayanağı (stadyum, uçak, metro, AVM kapasiteleri). Türkiye'den örnekler tercih edilir.
  - Kat ifadesi kuralı için öneri ("iki stadyum", "~6 otobüs").
- **Kabul:** JSON dosyaları `VERI-MODELI.md` tiplerine uyuyor. Gerçek felaket referansı yok. Her sayının kaynağı `KAYNAKLAR.md`'de.

### T-004 · Nokta görselleştirme
- **Yazabileceği yerler:** `src/components/noktalar/**`, `src/app/deneme/noktalar/page.tsx`.
- **Kapsam:** Canvas (gerekirse WebGL). n değişince geçiş animasyonu ve kamera uzaklaşması. 8 milyarda temsili yoğunluk; gerçekten 8 milyar nokta çizilmez, yöntem handoff'ta açıklanır. Orta segment bir telefonda 60 fps hedefi.
- **Kabul:** Deneme sayfasında basamaklar arasında gezilebiliyor. `prefers-reduced-motion` destekleniyor.
