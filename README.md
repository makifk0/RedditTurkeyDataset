# 🗂️ Reddit Dataset — Türkçe/İngilizce Talimat-Yanıt Veri Seti

Kendi oluşturduğum veri toplama ağıyla (crawler) toplanan Reddit yorumlarından derlenen, talimat–yanıt (instruction–output) formatında yapılandırılmış bir veri seti. Türkiye'deki LLM ekosistemine katkı sağlamak amacıyla paylaşılmıştır.

## 📦 Dosya

| Dosya | Kayıt Sayısı | Açıklama |
|---|---|---|
| `133kReddit.jsonl` | ~133.333 | Kaliteye göre filtrelenmiş alt küme: %60 TR · %40 EN |

> Not: `reddit.jsonl` (tam veri seti, 530.536 kayıt) yayından kaldırılmıştır. Yalnızca `133kReddit.jsonl` yayınlanmaktadır.

## 📊 İstatistikler

**Mini set:** %60 Türkçe (80.000) · %40 İngilizce (53.333)

Mini set, her dil grubundan `quality_signal` skoruna göre en kaliteli örnekler seçilip `seed=42` ile karıştırılarak oluşturuldu.

## 🏆 Kapsanan Subredditler

- **İngilizce:** Sadece kaliteli, düşük-meme içerikli 20 subreddit (r/programming, r/Python, r/AskReddit, r/space, r/eu4 vb.) meme/shitposting subredditleri hariç tutuldu.
- **Türkçe:** r/Turkey, r/BiriyleKonus, r/LinuxTurkey, r/felsefe gibi 140+ subreddit.

## 🔍 Veri Alanları (özet)

`id`, `instruction`, `output`, `lang`, `is_duplicate`, `is_toxic`, `toxicity_score`, `quality_signal`, `topic_id`, `perspective_label` gibi alanlar içerir. Toksisite ve tekrar (duplicate) filtreleme yapılmıştır; kullanıcı adları (`author`) anonimleştirilmemiştir.

## 🚀 Kullanım

```python
import json
with open("133kReddit.jsonl", encoding="utf-8") as f:
    for line in f:
        s = json.loads(line)
        print(s["instruction"], "→", s["output"])
```

Hugging Face `datasets` ile de doğrudan yüklenebilir:

```python
from datasets import load_dataset
ds = load_dataset("json", data_files="133kReddit.jsonl", split="train")
```

## 🔒 Etik Notlar

- Sadece halka açık Reddit verisi kullanılmıştır.
- Toksik içerik etiketlenmiştir ama tamamen çıkarılmamıştır. kullanıcı ek filtreleme uygulamalıdır.
- Tekrar eden (duplicate) kayıtlar mini setten çıkarılmıştır.

## 📄 Lisans

Bu veri seti **Apache License 2.0** ile lisanslanmıştır. Ayrıca Reddit'in [Public Content Policy](https://www.redditinc.com/policies/content-policy) ve [Terms of Service](https://www.reddit.com/wiki/tos/) koşullarına da uyulmalıdır.

## 🎯 Amaç

Bu veri seti, kendi oluşturduğum veri toplama ağıyla derlenen daha büyük bir koleksiyonun küçük bir alt kümesidir ve Türkiye'deki LLM ekosistemine katkı sağlamak amacıyla açık şekilde paylaşılmıştır.
