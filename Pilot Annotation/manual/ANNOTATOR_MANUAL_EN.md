# Slide–Narration Relation Annotation (SNRA) Manual

## Contents

- [1. Purpose of this annotation](#sec-1)
- [2. Overview of this annotation](#sec-2)
  - [2.1 Information shown](#sec-2-1)
  - [2.2 Summary of the work](#sec-2-2)
- [3. Detailed instructions](#sec-3)
  - [3.1 Annotation workflow](#sec-3-1)
  - [3.2 Labels and required entries](#sec-3-2)
    - [3.2.1 On-slide Content](#sec-3-2-1)
    - [3.2.2 Figure/Formula Explanation](#sec-3-2-2)
    - [3.2.3 Implicit Lecture Content](#sec-3-2-3)
    - [3.2.4 Metadiscourse](#sec-3-2-4)
    - [3.2.5 Unrelated Content](#sec-3-2-5)
    - [3.2.6 Invalid NU](#sec-3-2-6)
- [4. Worked example](#sec-4)

<a id="sec-1"></a>

## 1. Purpose of this annotation

Lecture slides usually present a concise outline. A lecturer may read or paraphrase the slide text, explain figures, add information that helps the audience understand the topic, and manage the lecture. The lecturer may also mention content unrelated to the current slide.

This annotation identifies how the lecturer's speech relates to slide content. The resulting data will support the analysis of **Implicit Lecture Content (ILC: information not directly shown on the current slide that helps the audience understand a topic on that slide)** and research on lecture-narration generation that adds information to support understanding.

<a id="sec-2"></a>

## 2. Overview of this annotation

<a id="sec-2-1"></a>

### 2.1 Information shown

Each **slide entry** in the lecture input file contains these three items:

1. the current slide image;
2. the full narration transcript segment associated with that slide; and
3. the list of NUs extracted from that narration.

**Example: `example` (source lecture `slide_index: 11`)**

![Example slide showing types of diabetes](example_images/example/slide_0011.jpg)

Figure 2.1: Example slide image

**Original narration for this slide (beginning and end; the middle is omitted with “…”):**

> when it comes to diabetes most of us know there are two types type 1 type 2 … as i always like to do give you a little hints to help you remember things

**NUs extracted from this narration:**

1. `example_s011_u01` — When it comes to diabetes, most of us know there are two types: type 1, type 2.
2. `example_s011_u02` — The way I always remember type 2 is that you're too fat.
3. `example_s011_u03` — And it's more than just simply being too fat, but that's what we tend to talk about.

…

An **NU (Narration Unit)** is a segment of the narration for one slide, produced by splitting that narration with an LLM. The extraction follows these principles:

- One NU is a coherent span of speech conveying one instructional point or discourse act.
- Keep clauses that develop the same point together. Start a new NU when the lecturer moves to a distinct, independently understandable point, example, question, or discourse act.
- Stay as close as possible to the lecturer's wording and perspective. Preserve substantive meaning, qualifications, degree of certainty, and meaningful emphasis.
- Lightly correct punctuation, disfluencies, and clear transcription errors without adding information.

<a id="sec-2-2"></a>

### 2.2 Summary of the work

Refer to the slide and narration and assign a label to each NU.

**Primary labels**

| Primary label | Summary |
|---|---|
| `on_slide_content` | The NU's content is expressed by text on the slide. |
| `figure_formula_explanation` | The NU's content can be read from a figure, table, formula, graph, or image on the slide. |
| `implicit_lecture_content` | Adds information that is not directly shown on the slide but helps the audience understand its topic. |
| `metadiscourse` | Speech about the lecture's progress, the speaker's stance, or interaction with the audience. |
| `unrelated_content` | Understandable speech whose relation to the current slide fits none of the categories above (e.g., “The weather is nice today”). |
| `invalid_nu` | An NU that remains unintelligible even after checking the context because of a cut-off utterance or a clear speech or transcription error. |

1. Refer to the slide and narration and select one primary label for each NU.
2. For `implicit_lecture_content`, copy the part of the NU that is not written on the slide into `not_on_slide_span`, and enter one ILC category in `sublabel`.
3. For `metadiscourse`, enter one metadiscourse function in `sublabel`.
4. If you select `other` as the `sublabel`, briefly describe in `note` the category you think is missing and why.

In this manual, the category entered in `label` is the primary label, the category entered in `sublabel` is the sublabel, and the items listed under each sublabel are subtypes. Subtypes are not recorded.

Section 3.1 summarizes the required entries; Section 3.2 explains each label.

<a id="sec-3"></a>

## 3. Detailed instructions

<a id="sec-3-1"></a>

### 3.1 Annotation workflow

First make sure you understand what each NU says. Then **start at step 1 and select only the first primary label that applies.** Fill in any additional fields required for that label, then move to the next NU.

1. **Is the content expressed by text on the slide?** If so, select `on_slide_content`.
2. **Can the content be read from a figure, table, formula, graph, or image?** If so, select `figure_formula_explanation`.
3. **Does the NU add information that helps explain a topic on the slide?** If so, select `implicit_lecture_content`.
4. **Is the NU about organizing or progressing through the lecture, expressing the speaker's stance, or interacting with the audience?** If so, select `metadiscourse`.
5. **Does none of the above apply?** If the NU is understandable, select `unrelated_content`.

*If an utterance is cut off or contains a clear speech or transcription error such that the NU itself remains unintelligible even after checking the context, select `invalid_nu`. If an unreadable image, a slide–narration mismatch, or a difference in meaning between the NU and narration undermines the basis for a judgment, leave `label` empty (`""`) and describe the affected passage and the reason in `note`.*

| Primary label | Additional entry |
|---|---|
| `on_slide_content` | None |
| `figure_formula_explanation` | None |
| `implicit_lecture_content` | `not_on_slide_span` (exact excerpt from the NU) + one `sublabel` (ILC category) |
| `metadiscourse` | One `sublabel` (metadiscourse function) |
| `unrelated_content` | None |
| `invalid_nu` | None |

<a id="sec-3-2"></a>

### 3.2 Labels and required entries

Assign one of the following primary labels to each NU.

<a id="sec-3-2-1"></a>

#### 3.2.1 `on_slide_content` — On-slide Content

Use this label when the NU's content is expressed by text on the slide, such as a title, bullet point, or explanatory sentence. This includes paraphrases that preserve the meaning.

<a id="sec-3-2-2"></a>

#### 3.2.2 `figure_formula_explanation` — Figure/Formula Explanation

Use this label when the NU's content can be read from a figure, table, formula, graph, or image on the slide.

<a id="sec-3-2-3"></a>

#### 3.2.3 `implicit_lecture_content` — Implicit Lecture Content

Use this label when the NU **adds information that helps explain a topic on the slide**, and that information is not directly shown on the slide.

**Also record:**

1. `not_on_slide_span`: the part of the NU that you judge is not written on the slide. Copy it exactly from the NU's `text` (do not paraphrase or summarize).
   - If the relevant content appears in separate places, copy the shortest continuous span that includes all of them.
   - If the entire NU is not written on the slide, copy the entire NU.
2. `sublabel`: the one ILC category that best describes the function of the added information. If none of the five categories fits, select `other` and briefly describe in `note` the category you think is missing and why.

##### Overview of ILC categories

The table lists the five ILC categories (sublabels) and their subtypes.

**Enter one ILC category in `sublabel` and copy the part not written on the slide into `not_on_slide_span`.** Subtypes are for reference only and do not need to be recorded.

| Category | Definition | Included subtypes |
| --- | --- | --- |
| Concept clarification<br>`concept_clarification` | Adds information that makes a term or concept easier to understand. | Definition<br>Attribute<br>Elaboration<br>Example<br>Analogy<br>Misconception correction |
| Explanation and reasoning<br>`explanation_reasoning` | Explains why or how something occurs, or what a result means. | Cause<br>Reason / Rationale<br>Mechanism<br>Process<br>Result / Consequence<br>Implication<br>Interpretation |
| Contextual knowledge<br>`contextual_knowledge` | Adds background or external knowledge that helps explain the current topic. | Background<br>Historical development<br>Evidence<br>Source / Attribution<br>Application / Use case |
| Qualification and relation<br>`qualification_relation` | Specifies the conditions, assumptions, relations, or limitations of a claim or method. | Condition<br>Assumption<br>Prerequisite<br>Comparison<br>Contrast<br>Limitation / Caveat<br>Exception |
| Method and action<br>`method_action` | Explains how a method is performed or how a problem can be solved. | Method / Approach<br>Procedure / Step<br>Practical strategy |
| Other (`other`) | The added content or function cannot be represented by the listed categories. | Free-text description |

##### Concept clarification — `concept_clarification`

What to look for: Ask what the audience learns about the meaning or characteristics of a concept. A definition, added detail, or concrete case belongs here when its main purpose is to make that concept easier to understand.

| Subtype | Detailed description |
|---|---|
| Definition | States what a term means. |
| Attribute | Describes a feature of the concept or object. |
| Elaboration | Develops a brief description with further detail. |
| Example | Gives a specific case of the concept. |
| Analogy | Explains a concept through a familiar comparison. |
| Misconception correction | Clarifies an incorrect understanding of a concept. |

##### Explanation and reasoning — `explanation_reasoning`

What to look for: Does the NU explain why or how something happens, or what a result means? This includes a cause, rationale, mechanism, consequence, or interpretation. Distinguish an NU that only states a result from one that explains why it occurred or what follows from it.

| Subtype | Detailed description |
|---|---|
| Cause | Identifies what produces an event or outcome. |
| Reason / Rationale | Explains why a claim, choice, or conclusion is justified. |
| Mechanism | Explains how interacting elements produce an outcome. |
| Process | Describes how a phenomenon unfolds over time. |
| Result / Consequence | Describes what follows from an event or action. |
| Implication | States what further conclusions can be drawn from a fact or result. |
| Interpretation | Explains how to understand the meaning of a result. |

##### Contextual knowledge — `contextual_knowledge`

What to look for: Look for background from outside the slide that places the topic in context or supports it. This can be historical context, a reported observation, an information source, or a setting in which an idea is used.

| Subtype | Detailed description |
|---|---|
| Background | Supplies surrounding facts needed to understand the topic. |
| Historical development | Describes how an idea or method originated, or how a situation developed. |
| Evidence | Reports observations or findings supporting a claim. |
| Source / Attribution | Identifies where information comes from or who proposed it. |
| Application / Use case | Describes where or for what purpose an idea or method is used. |

##### Qualification and relation — `qualification_relation`

What to look for: Focus on how the addition clarifies the scope of a claim or method, or its relationship to other matters. It may state when a claim applies, what must be assumed, how two options compare, or where a generalization has limits.

| Subtype | Detailed description |
|---|---|
| Condition | States when a claim or method applies. |
| Assumption | States what is taken as given in an explanation. |
| Prerequisite | States what must be available or satisfied beforehand. |
| Comparison | Relates objects along a shared criterion. |
| Contrast | Highlights a difference between objects or approaches. |
| Limitation / Caveat | Identifies a drawback or restriction in interpretation or use. |
| Exception | Identifies a case outside a stated generalization. |

##### Method and action — `method_action`

What to look for: Ask what someone would actually do to carry out a method or solve a problem. The addition may describe an overall approach, ordered actions, or a practical adjustment. If the NU describes how a natural or cognitive process unfolds, use `explanation_reasoning` (Process) instead.

| Subtype | Detailed description |
|---|---|
| Method / Approach | Describes a way of addressing a problem or objective. |
| Procedure / Step | Specifies actions and their order in carrying out a method. |
| Practical strategy | Describes a practical way to handle a situation or carry out an activity more effectively. |

<a id="sec-3-2-4"></a>

#### 3.2.4 `metadiscourse` — Metadiscourse

Use this label when the NU's main purpose is to indicate the lecture's structure or progression, express the speaker's stance or evaluation toward what is being said, or manage interaction with the audience.

**Also record:** one metadiscourse function in `sublabel`.

##### Overview of metadiscourse functions

The table lists the three metadiscourse functions (sublabels) and their subtypes. The rightmost column explains each subtype. Enter one function category in `sublabel`; subtypes are not recorded.

| Category | Definition | Included subtypes | Detailed description |
|---|---|---|---|
| Discourse organization<br>`organization_management` | Organizes the structure, sequence, transitions, or progress of the lecture or presentation. | Opening<br>Closing<br>Topic introduction<br>Goal announcement<br>Sequencing<br>Transition<br>Previewing<br>Reviewing<br>Summarizing<br>Concluding<br>Endophoric reference<br>Aside<br>Returning to topic<br>Task / Schedule management<br>Time management | Opening: Marks the start of the lecture or presentation.<br>Closing: Marks the end of the lecture or presentation.<br>Topic introduction: Introduces the topic to be discussed.<br>Goal announcement: States the purpose of the lecture or a section.<br>Sequencing: Organizes the order in which points are presented.<br>Transition: Moves from one point or section to another.<br>Previewing: Indicates what will be discussed later.<br>Reviewing: Directs attention back to material already covered.<br>Summarizing: Signals a recap of the discussion.<br>Concluding: Signals the completion of a topic or section.<br>Endophoric reference: Points to an earlier or later part of the lecture or materials.<br>Aside: Signals a temporary departure from the main discussion.<br>Returning to topic: Signals a return to the main discussion.<br>Task / Schedule management: Communicates assignments or scheduling information.<br>Time management: Adjusts the lecture to the available time. |
| Speaker stance<br>`speaker_stance` | Expresses the speaker's certainty, attitude, evaluation, or commitment toward the content. | Hedge / Uncertainty<br>Booster / Certainty<br>Attitude / Evaluation<br>Importance marking<br>Difficulty marking<br>Self-positioning<br>Limiting commitment | Hedge / Uncertainty: Expresses uncertainty or presents a position cautiously.<br>Booster / Certainty: Expresses strong confidence or emphasizes a claim.<br>Attitude / Evaluation: Expresses an attitude or evaluative judgment.<br>Importance marking: Marks a point as important.<br>Difficulty marking: Comments on how easy or difficult a point is.<br>Self-positioning: Indicates the perspective or role from which the speaker is speaking.<br>Limiting commitment: Indicates how far the speaker is prepared to commit to a claim. |
| Audience interaction<br>`audience_interaction` | Addresses the audience, guides attention, checks understanding, or encourages participation. | Direct address<br>Attention directing<br>Comprehension check<br>Channel check<br>Question / Invitation<br>Directive / Request<br>Shared knowledge<br>Anticipating response<br>Inclusive reference<br>Q&A management<br>Greeting / Thanks | Direct address: Addresses the audience explicitly.<br>Attention directing: Directs attention to a point or part of the material.<br>Comprehension check: Checks whether the audience understands.<br>Channel check: Checks whether the audience can hear or see the presentation.<br>Question / Invitation: Asks for an audience response or invites participation.<br>Directive / Request: Requests an action from the audience.<br>Shared knowledge: Appeals to knowledge assumed to be shared with the audience.<br>Anticipating response: Anticipates a likely question, concern, or reaction.<br>Inclusive reference: Uses inclusive wording to involve the audience.<br>Q&A management: Organizes questions and responses from the audience.<br>Greeting / Thanks: Greets or thanks the audience. |
| Other (`other`) | The function of the NU does not fit any of the listed categories. | Free-text description | Briefly describe in `note` the category you think is missing and why. |

<a id="sec-3-2-5"></a>

#### 3.2.5 `unrelated_content` — Unrelated Content

Use this label for an understandable NU that is neither directly shown on the current slide, nor an addition that helps explain its topic, nor metadiscourse.

**Additional entry:** none.

<a id="sec-3-2-6"></a>

#### 3.2.6 `invalid_nu` — Invalid NU

Use this label when an utterance is cut off or a clear speech or transcription error makes it impossible to understand what the NU itself says, even after checking the surrounding narration and slide. Interpret words such as "this", "that", or "it" from context; their presence alone is not a reason to choose this label.

**Additional entry:** none.

<a id="sec-4"></a>

## 4. Worked example

The slide (`slide_index: 11`) comes from `lectures/example.json`; its annotations are in `results/example.json`.

**Slide image**

![Slide showing types of diabetes](example_images/example/slide_0011.jpg)

**Original narration (full text)**

> when it comes to diabetes most of us know there are two types type 1 type 2 the way i always remember type 2 is that you're too fat and it's more than just simply being too fat but that's what we tend to talk about and as you can see in the chart there's a lot more type 2 diabetes than there is type 1 now there is a third type of diabetes which is basically women who are pregnant who get elevated glucose levels during pregnancy but for most of us we tend to you've only type 1 and type 2 those of you who are going into the allied health fields you'll might even discuss up to five different types of diabetes but for us for this class type 1 type 2 and remember type 2 is because you're too fat as i always like to do give you a little hints to help you remember things

**NUs and annotations (all 9)**

| NU ID | Full NU text | `label` | Additional entries |
|---|---|---|---|
| `example_s011_u01` | When it comes to diabetes, most of us know there are two types: type 1, type 2. | `on_slide_content` | None |
| `example_s011_u02` | The way I always remember type 2 is that you're too fat. | `on_slide_content` | None |
| `example_s011_u03` | And it's more than just simply being too fat, but that's what we tend to talk about. | `implicit_lecture_content` | `sublabel`: `concept_clarification`<br>`not_on_slide_span`: `more than just simply being too fat` |
| `example_s011_u04` | As you can see in the chart, there's a lot more type 2 diabetes than there is type 1. | `figure_formula_explanation` | None |
| `example_s011_u05` | Now, there is a third type of diabetes, which is basically women who are pregnant who get elevated glucose levels during pregnancy. | `on_slide_content` | None |
| `example_s011_u06` | But for most of us, we tend to you've only type 1 and type 2. | `metadiscourse` | `sublabel`: `audience_interaction` |
| `example_s011_u07` | Those of you who are going into the allied health fields, you'll might even discuss up to five different types of diabetes. | `implicit_lecture_content` | `sublabel`: `contextual_knowledge`<br>`not_on_slide_span`: `allied health fields, you'll might even discuss up to five different types of diabetes` |
| `example_s011_u08` | But for us, for this class, type 1, type 2, and remember type 2 is because you're too fat. | `metadiscourse` | `sublabel`: `organization_management` |
| `example_s011_u09` | As I always like to do, give you a little hints to help you remember things. | `metadiscourse` | `sublabel`: `speaker_stance` |

For `example_s011_u03`, the slide says “Too Fat,” but it does not say that type 2 diabetes involves more than simply being too fat, so that part of the NU is copied.
For `example_s011_u07`, the slide shows only three types of diabetes and does not say that allied-health fields may discuss up to five. Because “allied health fields” and “five different types” are separated in the NU, the shortest continuous span containing both is copied.
