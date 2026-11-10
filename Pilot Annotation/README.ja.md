<p align="right"><a href="README.md">English</a> | <a href="README.ja.md">日本語</a></p>

# パイロット用スライド・ナレーション関係アノテーションデータ

このパイロット用パッケージには、講義2本から選んだスライド15枚・NU（Narration Unit）136件と、記入済みの作業例（スライド1枚・NU 9件）が含まれます。スライド画像、ナレーション、NU を参照し、[アノテーションマニュアル](manual/ANNOTATOR_MANUAL_JA.md)に従ってラベルを付けます。英語版は[こちら](manual/ANNOTATOR_MANUAL_EN.md)です。

## パイロットの対象

| 講義 | 優先（`slide_index`） | 予備（`slide_index`） | スライド数 | NU数 |
|---|---|---|---:|---:|
| 心理学入門（PSY101/1） | 5–6 | 3、4、7 | 5 | 53 |
| 学術的文章作成（/23） | 3–5 | 6–12 | 10 | 83 |

`slide_index` は元の講義の値をそのまま使用しています。心理学入門の講義では0から始まります。予備のスライドは、必要に応じて追加で作業していただく分です。

## データ統計

以下はパイロット対象の2講義から再集計した値です（作業例の `example` は含みません）。英語の語数は空白区切りで数え、平均は小数第1位に丸めています。

| 分野・講義 | スライド数 | ナレーション平均語数／枚 | NU総数 | 平均NU数／枚 | NU平均語数／件 |
|---|---:|---:|---:|---:|---:|
| 心理学入門（PSY101/1） | 5 | 363.6 | 53 | 10.6 | 34.0 |
| 学術的文章作成（/23） | 10 | 276.3 | 83 | 8.3 | 32.7 |
| **合計** | **15** | **305.4** | **136** | **9.1** | **33.2** |

## ファイル構成

| パス | 内容 |
|---|---|
| `lectures/<name>.json` | 講義ごとの入力ファイル（`example.json` を含む） |
| `slide_images/<name>/` | 講義ごとのスライド画像 |
| `manual/` | 英語・日本語のアノテーションマニュアルと例示用画像 |
| `results/<name>.json` | 入力ファイルに対応するアノテーション結果。`example.json` は記入済み |

## データ構造

### 講義の入力データ（`lectures/<name>.json`）

以下は `lectures/example.json` の抜粋です。このスライドのナレーション全文と、9件の NU から選んだ4件を示します。実際のファイルには9件すべてが含まれています。`image_path` はパッケージのルートからの相対パスです。

```json
{
  "lecture_id": "example",
  "source_dataset": "lpm",
  "video_url": "https://www.youtube.com/watch?v=uNrB2uG_9gs",
  "slides": [
    {
      "slide_index": 11,
      "image_path": "slide_images/example/slide_0011.jpg",
      "narration": "when it comes to diabetes most of us know there are two types type 1 type 2 the way i always remember type 2 is that you're too fat and it's more than just simply being too fat but that's what we tend to talk about and as you can see in the chart there's a lot more type 2 diabetes than there is type 1 now there is a third type of diabetes which is basically women who are pregnant who get elevated glucose levels during pregnancy but for most of us we tend to you've only type 1 and type 2 those of you who are going into the allied health fields you'll might even discuss up to five different types of diabetes but for us for this class type 1 type 2 and remember type 2 is because you're too fat as i always like to do give you a little hints to help you remember things",
      "narration_units": [
        {
          "unit_id": "example_s011_u02",
          "text": "The way I always remember type 2 is that you're too fat.",
          "evidence": [
            {
              "quote": "the way i always remember type 2 is that you're too fat"
            }
          ]
        },
        {
          "unit_id": "example_s011_u03",
          "text": "And it's more than just simply being too fat, but that's what we tend to talk about.",
          "evidence": [
            {
              "quote": "and it's more than just simply being too fat but that's what we tend to talk about"
            }
          ]
        },
        {
          "unit_id": "example_s011_u04",
          "text": "As you can see in the chart, there's a lot more type 2 diabetes than there is type 1.",
          "evidence": [
            {
              "quote": "as you can see in the chart there's a lot more type 2 diabetes than there is type 1"
            }
          ]
        },
        {
          "unit_id": "example_s011_u08",
          "text": "But for us, for this class, type 1, type 2, and remember type 2 is because you're too fat.",
          "evidence": [
            {
              "quote": "but for us for this class type 1 type 2 and remember type 2 is because you're too fat"
            }
          ]
        }
      ]
    }
  ]
}
```

### アノテーション結果（`results/<name>.json`）

`annotations` のキーは `unit_id` です。各項目には主ラベルを `label` に記入し、必要に応じて `sublabel`、`not_on_slide_span`、`remainder_label`、`note` を追加します。文字起こしの修正内容は、`note` に `{{FIX: 誤った表記 => 正しい表記}}` の形式で記入します。判断の前提に問題がある場合は、`label` を空欄（`""`）にし、該当箇所と理由を `note` に記入します。パイロット対象の講義2本分の結果ファイルは `annotations` が空の状態で配布しており、`results/example.json` には記入済みの結果が入っています。以下は上の入力例と同じ4件の結果です。

```json
{
  "lecture_id": "example",
  "annotations": {
    "example_s011_u02": {
      "label": "on_slide_textual_content"
    },
    "example_s011_u03": {
      "label": "implicit_lecture_content",
      "sublabel": "concept_clarification",
      "not_on_slide_span": "more than just simply being too fat",
      "remainder_label": "metadiscourse"
    },
    "example_s011_u04": {
      "label": "on_slide_visual_content"
    },
    "example_s011_u08": {
      "label": "metadiscourse",
      "sublabel": "organization_management"
    }
  }
}
```
