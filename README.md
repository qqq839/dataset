# Dataset classification

This dataset is a case-level, multi-view English narrative dataset for binary harassment recognition and diagnostic analysis.

## Dataset unit and task

- Each JSON object represents one case.
- Each case contains three matched narrative views: short, medium, and long.
- The three views describe the same case and share the same binary target.
- The binary target concerns the conduct described in the narrative:
  - 0: non-harassment
  - 1: harassment
- The dataset contains 9,725 cases and 29,175 narrative views.
- The positive class contains 4,758 cases and the negative class contains 4,967 cases.

## Dataset files

The files use UTF-8 JSON Lines format. Each line contains one JSON object.

| File | Cases | Positive | Negative |
|---|---:|---:|---:|
| HarassLens_train.jsonl | 5,835 | 2,855 | 2,980 |
| HarassLens_validation.jsonl | 1,945 | 952 | 993 |
| HarassLens_test.jsonl | 1,945 | 951 | 994 |
| Total | 9,725 | 4,758 | 4,967 |

## Annotation coverage

- All cases contain the fields case_id, short, medium, long, and label.
- Positive cases contain evidence_sentences, behavior, behavior_comparison, and scenes.
- Negative cases use null for evidence_sentences, behavior, behavior_comparison, and scenes.
- The evidence sentences in a positive case are retained verbatim in all three narrative views.
- behavior records one primary behavior under the S5 hierarchy.
- behavior_comparison records an independently annotated comparison behavior under the S3 hierarchy.
- scenes is a case-level multi-label annotation based on the reported setting or communication channel.

# Field description

## Top-level fields

| Field | Type | Nullable | Description |
|---|---|---|---|
| case_id | string | No | Unique case identifier. Treat this value as an identifier only. |
| short | string | No | Short narrative view of the case. |
| medium | string | No | Medium narrative view of the case. |
| long | string | No | Long narrative view of the case. |
| label | integer | No | Binary target: 0 for non-harassment and 1 for harassment. |
| evidence_sentences | array of strings | Yes | Evidence sentences for positive cases. Each supplied sentence occurs verbatim in short, medium, and long. Null for negative cases. |
| behavior | object | Yes | Primary behavior annotation under the S5 scheme. Null for negative cases. |
| behavior_comparison | object | Yes | Independent comparison behavior annotation under the S3 scheme. Null for negative cases. |
| scenes | array of objects | Yes | One or more scene annotations for positive cases. Null for negative cases. |

## behavior

The behavior object contains one primary behavior annotation.

| Field | Type | Nullable | Description |
|---|---|---|---|
| scheme | string | No | The value is S5. |
| coarse | string | No | Broad behavior category. |
| fine | string | No | Fine-grained behavior category. |

### S5 coarse categories

| Code | Category |
|---|---|
| S5_A | Verbal |
| S5_B | Visual |
| S5_C | Pursuit |
| S5_D | Contact |
| S5_E | Sexual |

### S5 fine categories

| Code | Category |
|---|---|
| S5_A1 | Gender hostility and sexual shaming |
| S5_A2 | Sexual comments and unwanted propositions |
| S5_A3 | Sexual quid pro quo |
| S5_A4 | Pressure, blackmail, and sexual-violence threats |
| S5_B1 | Sexual staring and gestures |
| S5_B2 | Exposure and imposed sexual content |
| S5_B3 | Sexual-privacy observation, capture, or fabrication |
| S5_B4 | Intimate-image distribution or threats |
| S5_C1 | Repeated unwanted contact |
| S5_C2 | Following, monitoring, or spatial intrusion |
| S5_D1 | Touching, rubbing, or forced undressing |
| S5_D2 | Unwanted kissing |
| S5_E1 | Forced nonpenetrative acts |
| S5_E2 | Non-consensual penetration |

The S5 annotation identifies the primary behavior selected for a case. It is not an exhaustive list of every behavior that may be mentioned in the narrative.

## behavior_comparison

The behavior_comparison object contains an independent comparison annotation.

| Field | Type | Nullable | Description |
|---|---|---|---|
| scheme | string | No | The value is S3. |
| coarse | string | No | Broad comparison category. |
| fine | string | No | Fine-grained comparison category. |

### S3 categories

| Coarse code | Coarse category | Fine code | Fine category |
|---|---|---|---|
| S3_A | Non-contact harassment | S3_A1 | Gender hostility and sexual shaming |
| S3_A | Non-contact harassment | S3_A2 | Sexual comments and unwanted propositions |
| S3_A | Non-contact harassment | S3_A3 | Sexual staring, gestures, and sexual display |
| S3_A | Non-contact harassment | S3_A4 | Repeated contact, following, and spatial intrusion |
| S3_A | Non-contact harassment | S3_A5 | Sexual quid pro quo, pressure, and threats |
| S3_A | Non-contact harassment | S3_A6 | Sexual-privacy observation, capture, and fabrication |
| S3_A | Non-contact harassment | S3_A7 | Intimate-image distribution and threats |
| S3_B | Non-consensual physical contact | S3_B1 | Touching, rubbing, and forced undressing |
| S3_B | Non-consensual physical contact | S3_B2 | Unwanted kissing |
| S3_C | Non-consensual sexual acts | S3_C1 | Forced nonpenetrative acts |
| S3_C | Non-consensual sexual acts | S3_C2 | Non-consensual penetration |

## scenes

The scenes field is a list because a case may contain conduct in more than one setting. The list can contain multiple scene objects.

| Field | Type | Nullable | Description |
|---|---|---|---|
| coarse | string | Yes | Broad scene code. It can be null when the broad setting cannot be identified. |
| fine | string | Yes | Fine scene code. It can be null when the narrative supports only a broad or local-space annotation. |
| status | string | No | Annotation status. |
| micro | string | Yes | Local-space description when applicable. Otherwise null. |

### Scene status values

| Value | Description |
|---|---|
| leaf | A fine scene category is identified. |
| broad_only | A broad category is supported, but the fine category is not sufficiently specified. |
| micro_only | A local space is identified, but its surrounding venue is not. |
| unknown | The narrative does not provide enough information to identify a scene. |
| other_explicit | An explicit setting falls outside the released scene tree. |

### Scene coarse categories

| Code | Category |
|---|---|
| SC01 | Education |
| SC02 | Work |
| SC03 | Housing |
| SC04 | Transport |
| SC05 | Outdoors |
| SC06 | Services |
| SC07 | Leisure |
| SC08 | Healthcare |
| SC09 | Community |
| SC10 | Online |

### Scene fine categories

| Code | Category |
|---|---|
| SC01_A | Teaching and study spaces |
| SC01_B | Educational offices and ancillary rooms |
| SC01_C | Campus circulation and outdoor spaces |
| SC01_D | Campus toilets and changing spaces |
| SC01_E | Campus sports facilities |
| SC01_F | Campus dining and student communal spaces |
| SC02_A | Work and occupational spaces |
| SC03_A | Homes and residential common areas |
| SC03_B | Student and employee accommodation |
| SC03_C | Short-term or temporary accommodation |
| SC04_A | Public or group ground transport, aircraft, and vessels |
| SC04_B | Taxis, ride-hailing, and private small vehicles |
| SC04_C | Waiting, interchange, and parking facilities |
| SC05_A | Streets, neighborhood roads, and standalone public facilities |
| SC05_B | Parks, squares, and natural open spaces |
| SC06_A | Retail and everyday service spaces |
| SC06_B | Restaurants, cafes, and dining spaces |
| SC07_A | Bars and nightlife venues |
| SC07_B | Cultural, sports, performance, and recreational facilities |
| SC08_A | Healthcare and care institutions |
| SC09_A | Public-affairs and community-organization spaces |
| SC10_A | One-to-one messages, texts, and email |
| SC10_B | Groups, content platforms, and virtual interaction |
| SC10_C | Live voice or video calls |
