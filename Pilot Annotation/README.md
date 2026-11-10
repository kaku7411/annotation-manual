<p align="right"><a href="README.md">English</a> | <a href="README.ja.md">日本語</a></p>

# Pilot Slide–Narration Annotation Data

This pilot package contains 15 slides and 136 Narration Units (NUs) from two lectures, plus one completed example slide with 9 NUs. Compare each NU with its slide image and narration, then assign labels using the [English manual](manual/ANNOTATOR_MANUAL_EN.md) or [Japanese manual](manual/ANNOTATOR_MANUAL_JA.md).

## Pilot scope

| Lecture | Priority `slide_index` | Reserve `slide_index` | Slides | NUs |
|---|---|---|---:|---:|
| Introduction to Psychology (PSY101/1) | 5–6 | 3, 4, 7 | 5 | 53 |
| Essay Writing and Presentation Skills (/23) | 3–5 | 6–12 | 10 | 83 |

The original `slide_index` values are preserved. They start at 0 in the psychology lecture. Reserve slides are for additional work if needed.

## Data statistics

These figures are recalculated from the two pilot lecture files; the completed `example` is excluded. English words are counted by splitting on whitespace, and averages are rounded to one decimal place.

| Field and lecture | Slides | Avg. narration words/slide | NUs | Avg. NUs/slide | Avg. words/NU |
|---|---:|---:|---:|---:|---:|
| Introduction to Psychology (PSY101/1) | 5 | 363.6 | 53 | 10.6 | 34.0 |
| Essay Writing and Presentation Skills (/23) | 10 | 276.3 | 83 | 8.3 | 32.7 |
| **Total** | **15** | **305.4** | **136** | **9.1** | **33.2** |

## Files

| Path | Contents |
|---|---|
| `lectures/<name>.json` | One input file per lecture, plus `example.json` |
| `slide_images/<name>/` | Slide images grouped by lecture |
| `manual/` | Annotation manuals and example images |
| `results/<name>.json` | One annotation file per input file; `example.json` is filled in |

## Data structure

### Lecture input (`lectures/<name>.json`)

The following excerpt of `lectures/example.json` shows the complete narration for the example slide and four selected NUs. The actual file contains all nine NUs for this slide. `image_path` is relative to the package root.

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

### Annotation result (`results/<name>.json`)

`annotations` is keyed by `unit_id`. Each annotation has a primary `label`; `sublabel`, `not_on_slide_span`, `remainder_label`, and `note` are added when applicable. Transcription corrections are recorded in `note` in the format `{{FIX: incorrect text => correct text}}`. If the basis for a judgment is problematic, leave `label` empty (`""`) and describe the affected passage and the reason in `note`. The two pilot lecture result files start with empty `annotations`; `results/example.json` contains completed annotations. The excerpt below shows the results for the same four NUs shown above.

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
