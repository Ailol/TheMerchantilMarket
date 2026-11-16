# Observation and closure

## The kår

Ailo called the minimum structure the `kår`. Once a previous chat and the current chat are available to the reader, each can be cited as an observed record. A third slot can hold what the two records suggest.

```text
weights = observed

[1] this chatg          quote, source, version
[2] the chatg before   quote, source, version
[3] inferred setz'     claim, cited slots, alternatives
```

Here “observed” means available and inspectable in the transcript. A message that says “the door was open” provides direct evidence that the sentence appeared. The claim about the door requires evidence about the door. An edited message and a recalled message are two further cases. A versioned quotation can mark the former, and a recollection can be recorded as a self-report. A missing source remains missing.

The author wrote “unobserved always leaves the observed partz behind.” One rigorous use of “always” is to scope the operator to hidden steps for which a trace was captured. Within that scope every selected step has at least one observable consequence by construction. The existence of a trace, its preservation, its observation, and the ability to reconstruct a unique cause are four different conditions. Suppose the same visible line can arise from two distinct editing histories. Without a further record or a discriminating prediction, the history is underdetermined even if the line is perfectly preserved. [Abduction and source monitoring](06-references.md#reasoning-and-conversation) supply nearby concepts.

### What counts as a weight

As an evidence rule, `weights = observed` anchors contributions in items the reader can inspect. An optional numeric model can still use confidence or likelihood, but its coefficients, assumptions, and calibration procedure need to be documented. If two messages repeat the same report, their agreement alone does not provide two independent observations. If a field is missing, it does not automatically contribute a zero or a prior. The model has to specify how missingness is handled.

Here is a schematic reduction with explicit provenance.

| Slot | Record | Scope |
| --- | --- | --- |
| `[1]` | “Could we leave this open?” | Observed request in the current passage |
| `[2]` | “I want to compare both options.” | Observed request in the prior passage |
| `[3]` | The reader may want more time to choose. | Plausible inference. They may also want both options preserved for somebody else. |

A one-pass answer could be “I’ll keep both options open.” A later reply can clarify who needs them. A short annotation can be both useful and strictly weaker than a claim to know the speaker's motives.

## Compacting labels

The discussion used this deliberately compact line.

```text
non ' semantikal
≡ the inferred ' doktor = observed ' doktor = observed doktor = observed'doktor = observed
```

One implementation reading is that successive boundary and spacing variants display a category called `observed`. Store provenance in the data before rendering that shorthand. In particular, if the string “the inferred” appears in an observed quotation, the quotation's provenance can be observed while any proposition asserted by the quotation keeps its own evidence status. A render-only `=` cannot establish evidential equivalence.

## What think'g ends

The end is local to one pass. Ailo's `mikro bullet` describes the moment at which a human feels that decision land. That wording is a report about the experience. Below is a proposed operational meaning for the software or prompt layer.

| Field | What to preserve |
| --- | --- |
| Scope | The question or decision this pass addressed |
| Inputs | The records actually considered, with their order and versions |
| Reduction | The chosen row and mask, or the XOR sum of a path |
| Local result | Terminal gauge state and, when relevant, the selected move |
| Open point | Any unresolved interpretation or missing record that would justify reopening |
| Human record | Optional `sz` report after the pass, with its own label and source |

For an undecidable reading, `unresolved` can be the local result. This lets the pass end with no invented certainty. A new message starts another pass, and can cite the old result and revise it. For a correction the prior line is useful evidence of what was believed at the time.

Commitment can be modeled as a stopping rule. Its thresholds depend on the purpose. A low-stakes greeting can be tried and changed in one turn. An inference that materially affects another person needs a stronger basis. Equating a short pause, a strong felt response, and a well-supported inference would erase the combinations the framework can study. [Metamemory, event segmentation, and grounding](06-references.md#attention-monitoring-and-boundaries) provide comparisons for monitoring, boundaries, and sufficiency for a current purpose.
