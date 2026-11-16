# Research protocol

The project currently has a formally specified gauge and a set of author examples. A reproducible evaluation should preserve the examples as the origin of the questions and use newly collected data to test them. This page is a proposed design. It contains no participant data and reports no study results.

## Questions and predictions

| Question | Comparison | Primary outcome for that question | What would weaken the hypothesis |
| --- | --- | --- | --- |
| Does explicit provenance improve reading? | Explicit observed/inferred labels versus the same records unlabelled | Correct discrimination between transcript statements and inferred interpretations | Equivalent or worse discrimination, or gains confined to obviously labelled items |
| Does local closure help? | A scope-specific closure marker versus the same result without that marker | Correct identification of what was settled and what stayed open in a new item | More premature commitment or no improvement in scope accuracy |
| Does presentation shape `sz`? | Presentation changes with meaning, length, and task held constant where possible | Self-reported residual intensity at a fixed delay | No difference within an interval defined in advance, or a difference explained by legibility, familiarity, or baseline preferences |
| Does the order matter? | Choice before cue versus cue before choice, with matched exposure | Accuracy about available options and perceived freedom to disregard a cue | Effects attributable to unequal exposure or a first-screen advantage |
| Can readers carry the method away? | Transfer trial without the gauge or AI interface | Independent identification of evidence, a plausible inference, and an open question | Comfort with the display rises while unaided transfer stays the same or declines |

The alternatives in these rows use the same vocabulary and access to the same evidence. In a first confirmatory study, nominate one primary outcome, contrast, and analysis before collecting the confirmation sample. The other questions can remain exploratory or run in follow-up studies. [Preregistration and sample size](06-references.md#study-design-and-measurement) covers the methodological basis.

## Stimuli and randomization

Use brief synthetic chat pairs. Include a directly supported statement, an inference supported but left uncertain, and a plausible claim with insufficient evidence. For example, one synthetic case can contain two observations compatible with either a delayed reply or an unsent draft. Add a third case with a later delivery receipt that resolves that specific ambiguity. A separate group of coders should build the answer key from all available context before the experiment. Mark ambiguous items as such rather than forcing a single answer.

Use several items per condition and distribute equivalent item families across conditions. Assign each participant one version of a given family so seeing its twin cannot reveal the answer. Counterbalance order for within-participant manipulations. For unaided transfer, present fresh items with no visual labels, and consider between-participant assignment for training when the control group could otherwise learn the technique from earlier trials.

For the greeting experiment, treat spacing, casing, punctuation, and color as controllable features. The two conversation originals can appear as exploratory examples. Balanced variants can then test one feature at a time, or a factorial design can estimate preselected interactions. Keep message meaning, exposure duration, typography, and layout comparable. Record display and accessibility settings where feasible. Color can run with visible text labels so the task remains possible when hue cannot be distinguished.

A comparison of adults already familiar with the notation and adults new to it can estimate whether effects depend on familiarity. Measure familiarity before exposure. A difference between those groups is observational unless the learning step itself is randomized.

## Procedure and measures

1. Explain that participants can skip a prompt. Capture the stimulus version and planned assignment.
2. Show the chat pair. Ask participants to identify directly observable statements and proposed interpretations. Provide an explicit “insufficient evidence” response.
3. Present the choice or closure cue under the assigned condition. Record any voluntary revision and the final choice. For trials that test ambiguity, distinguish choosing an option from committing to its truth.
4. Prompt at a fixed, piloted delay. Collect perceived closure and `sz` separately. Use anchors that permit no sensation or no residual effect. For optional free text, ask what, if anything, the participant noticed.
5. Run the fresh unaided transfer task. Measure voluntary use of the same distinctions in a new problem.

Record decision time from stimulus readiness to submitted response. Keep prompt loading and rendering latency outside that interval or measure them separately. The feeling that the answer arrived instantly is its own rating. For optional pause durations, account for motor and device variance before interpreting timing effects.

Measure perceived closure with a pretested question on whether the specific numbered decision feels settled. Measure residual intensity with a separate item on what remains after the cue. Measure pleasantness independently. A strong residual can be unpleasant, and low residual intensity can accompany accurate comprehension. Record unsupported claims as a performance outcome even if the participant enjoyed the experience.

For provenance discrimination, report hit rate and false-alarm rate. Under the equal-variance signal-detection model, report `d′ = Φ⁻¹(hit rate) − Φ⁻¹(false-alarm rate)` if the item design supports that interpretation. Specify the correction for empirical rates of zero or one. A lower willingness to mark anything observed can reduce false alarms and hits together. Report response bias and uncertainty alongside sensitivity.

For explicitly resolvable binary claims, participants can report a probability and receive a Brier score `(p − y)²`. Exclude genuinely unresolved cases from outcome-based scoring by design. Use them to measure awareness of insufficient evidence. Keep a participant's confidence estimate independent of what the transcript proves.

## Analysis and decision criteria

Estimate the contrast on the primary outcome with an interval, plus trial and participant counts. For repeated observations and multiple texts, use a model that accounts for both participant and item variation. A logistic mixed model suits binary correctness when the design, sample size, and fit support it. An ordinal model suits anchored ratings if its assumptions are reasonable. Specify any transformations, handling of extreme reaction times, missing responses, and conditions for changing the planned model. Retain raw denominators and summarize exclusions by condition. Avoid recoding a skipped `sz` item as a zero.

A feasibility pilot can estimate comprehension of the marks, task variance, item ambiguity, and missingness. Use those estimates, a practical effect size, and the target precision or power to justify the confirmation sample. Report uncertainty even when a contrast crosses a decision threshold. Analyze manipulation checks as checks, with any exclusions or subgroup analyses declared in advance. Clarify which interactions and qualitative findings arose after looking at the data.

A favorable result would be improved evidence discrimination and preserved or improved transfer, even if participants disagree on how the presentation feels. A result in which perceived closure increases alongside more high-confidence unsupported claims would count against the interaction as designed.

## Reproducible materials

A research handoff can include the preregistration, versioned synthetic stimulus set, codebook, exclusion rules, analysis scripts, and de-identified aggregate results. A sample record shape follows.

```text
participant_code | item_version | assigned_condition | response_order
observed_choice | inferred_choice | insufficient_evidence | confidence
closure_rating | residual_intensity | pleasantness | response_ms
transfer_result | missing_reason
```

Publish synthetic materials and enough information to reproduce the analysis. Keep participation, data retention, and free-text publication within the consent given. A successful study should make it possible for another group to rerun the procedure, compare estimates, and improve the design.
