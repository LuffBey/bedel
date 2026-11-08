# Orkestrasyon: çok ajanlı çalışma düzeni

## Akış

```
Kullanıcı ──istek──▶ Ana planlayıcı (Claude Code)
                       │ 1. görevi böl → tasks/BOARD.md
                       │ 2. her dış ajan için prompt yaz → prompts/T-xxx-<ajan>.md
                       │ 3. prompt yolunu önce kullanıcıya söyle
                       │ 4. ajanları kendi worktree'lerinde arka planda başlat
                       ▼
          ┌────────────┼─────────────┐
       Codex          agy          Claude alt ajanı
          │            │             │
          └──── handoffs/T-xxx-<ajan>.md ────┘
                       ▼
          Ana planlayıcı: incele → kontrolleri çalıştır → birleştir → BOARD güncelle
                       ▼
          Kullanıcı: onay verirse commit
```

## Hangi işi kim yapar (başlangıç önerisi, esnek)

| Ajan | Güçlü olduğu iş |
|---|---|
| **Codex** | Saf mantık, durum makinesi, testler, veri katmanı ve şema |
| **agy (Gemini)** | İçerik üretimi (ikilem listesi, Türkçe metinler, betimleme araştırması), alternatif tasarım fikirleri |
| **Claude alt ajanı** | Arayüz bileşenleri, görselleştirme, entegrasyon |
| **Ana planlayıcı** | Sözleşme (`VERI-MODELI.md`), kararlar, inceleme, birleştirme |

## Worktree düzeni

İki ajan aynı dizinde çalışırsa birbirinin dosyasını ezer. Bu yüzden her görev ayrı bir worktree'de yürür:

```bash
# repo kökünden (ilk commit'ten sonra çalışır)
git worktree add ../bedel-wt/T-002-codex -b t/T-002-codex
```

Ajan işini commit atmadan bırakır. Ana planlayıcı worktree'deki diff'i inceler ve ana ağaca taşır.

## Ajanları çalıştırma

```bash
# Codex: stdin'i mutlaka kapat, yoksa sonsuza kadar bekler
cd ../bedel-wt/T-002-codex && timeout 900 codex exec "$(cat /root/projects/bedel/prompts/T-002-codex.md)" < /dev/null > /root/projects/bedel/handoffs/T-002-codex.log 2>&1

# agy (Gemini)
cd ../bedel-wt/T-003-agy && timeout 900 agy -p "$(cat /root/projects/bedel/prompts/T-003-agy.md)" --model gemini-4-argon-high --mode auto > /root/projects/bedel/handoffs/T-003-agy.log 2>&1
```

- `--dangerously-skip-permissions` ya da benzeri bayraklar kullanıcı açıkça istemedikçe kullanılmaz.
- Prompt dosyası tek başına yeterli olmalı: görev, izin verilen dosyalar, kabul ölçütleri, çalıştırılacak kontroller, handoff yolu. Şablon: `prompts/_SABLON.md`.

## İnceleme ölçütleri (ana planlayıcı)

1. Ajan izin verilen dosyaların dışına çıktı mı?
2. `VERI-MODELI.md` ile uyumlu mu?
3. Kontroller gerçekten geçiyor mu? (Handoff'a güvenme, kendin çalıştır.)
4. `KARAR-BEKLIYOR` işaretleri `KARARLAR.md`'ye yansıtıldı mı?
5. İçerik görevlerinde ton kuralları ve "gerçek felaket yasağı" çiğnendi mi?
