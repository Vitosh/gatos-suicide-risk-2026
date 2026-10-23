# Task Description

This challenge consists of **two subtasks**. Participants may compete in both subtasks. The final composite score is weighted **70% on Subtask 1** and **30% on Subtask 2**.

**Subtask 1: Suicide Risk Detection (Weight: 70%)**  
Given a Reddit post, identify the author's suicide risk level into one of four categories:

- **Indicator**: The post contains no explicit mentions of suicide.
- **Ideation**: The post contains explicit suicidal expressions but no suicidal plan.
- **Behavior**: The post contains explicit suicidal expressions and self-harm/suicidal plan.
- **Attempt**: The post contains explicit mentions of recent/past suicidal attempts.

**Evaluation on Subtask 1:** 1) identify the suicide risk level of a social media post: Weighted F1. 2) The evidence extraction task is evaluated using Phrase F1. After case-insensitive normalization, a predicted phrase is considered correct if it either contains a ground-truth phrase or is contained by a ground-truth phrase. This allows partial but faithful extraction, such as matching "kill myself" with "I want to kill myself".

Phrase precision measures how many predicted phrases match the ground truth, while phrase recall measures how many ground-truth phrases are covered by the prediction. The final Phrase F1 is averaged over all posts. To prevent participants from submitting the entire post or excessively long text as evidence, a predicted evidence span will only be considered correct if its token length does not exceed three times the token length of the matched ground-truth evidence span.

In addition, each predicted evidence span can be matched to at most one ground-truth evidence span, and each ground-truth evidence span can be matched to at most one predicted span.

**Subtask 2: Suicide Factors Identification (Weight: 30%)**  
Given the same post, identify all suicide-related factors that are present in the post. This subtask is formulated as a multi-label classification problem: each post may be assigned zero, one, or multiple factor labels. The factor taxonomy is adapted from Li, J., Wang, X., Li, H., Yan, Y., Leong, H. V., Feng, L., et al. (2025), *Protective factor-aware dynamic influence learning for suicide risk prediction on social media*, arXiv:2507.10008.

The factor taxonomy includes the following categories:

- mental health issues
- physical health/characteristic
- substance use
- hopelessness
- emotion dysregulation
- low self-esteem
- poor school performance
- low socio-economic status
- interpersonal violence
- prior self-harm or suicidal thought/attempt
- poor social support
- interpersonal difficulty
- dysfunctional family
- exposure to others' suicide
- stressful life event
- traumatic experience
- cognitive deficits
- suicide means (with access)
- sexual orientation related issues
- social support
- coping strategy
- psychological capital
- sense of responsibility
- meaning in life

Participants are expected to predict all applicable factor labels for each post according to the predefined factor taxonomy. This subtask will be evaluated using the Macro F1 score across all factor categories.

**Composite Scoring:** The leaderboard score is computed as:

`Score = Subtask1 (0.4*suicide risk detection + 0.3*evidence support for detection) + Subtask2 (0.3*suicide factors identification)`

Teams that participate in Subtask 1 only will be scored on Subtask 1 alone (no penalty for skipping Subtask 2).

**Submission format:** Please submit your detections as a `.csv` file with the following structure. The file name must be `YourTeamName.csv`.

| Field | Type | Description |
| --- | --- | --- |
| row_id | string | The post identifier from the dataset |
| risk_level | string | One of: Indicator, Ideation, Behavior, Attempt |
| evidence | string | Semicolon-separated evidence text spans that support the predicted suicide risk level (e.g., want to kill myself; feel hopeless). Each span should be copied verbatim from the original post. |
| factors | list | List of factor categories |

**Final evaluation:** The final evaluation will be conducted after the submission deadline using a held-out test set. Only teams that submit both their source code and a report by the deadline will qualify for the final evaluation. Code and reports will be submitted via Google Drive; instructions will be sent by email in advance.

Source: [Explainable Suicide Risk Detection challenge](https://www.bigdatacompetition.cn/), accessed on 23 October 2026.
