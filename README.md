# 99p

Finding out *what kind* of situation a policy is bad at, by reading the policy's own
internal activations, instead of guessing the categories in advance.

Status: scaffolding. Nothing is implemented yet.

## The problem

When a driving policy fails, the question that matters is what data to collect next.
The usual loop is to write down a list of things you think are hard (rain, night,
unprotected lefts, merges), test each one, and go collect more data wherever the
score is worst.

That loop can only find failure modes somebody thought to name. Whatever is not on
the list stays invisible, and for driving the real "hard" situations are often
compounds nobody writes down: a partially occluded pedestrian stepping out from
behind a stopped bus while the sun is low and behind them.

Mobileye's [Meteor and Genario pipeline](https://www.mobileye.com/blog/diagnosing-the-long-tail-how-mobileye-turns-edge-cases-into-targeted-training/)
automates most of this loop. Meteor mines logged driving for *reproducible* failures,
generates hypotheses about what causes them, turns those hypotheses into semantic
queries to pull similar scenarios, and validates them. Genario then synthesizes
matching scenarios for retraining.

The search there still happens in data space. A failure axis has to be expressible as
a query over scenario attributes before the pipeline can go looking for it.

## The idea

Collect activations from the policy across many rollouts, and look for structure in
that activation space that lines up with failures.

The claim under test: **the policy's internal representation already separates kinds
of situation that nobody has labeled, and those separations are the failure axes.**
If true, you get candidate axes without having to name them first.

The output is not a score per episode. It is a description of a class of situations,
specific enough that you can go generate more of them.

## What this is not

- **Not a failure detector.** Predicting "this episode is about to go wrong" is a
  crowded area and is a different task.
- **Not test-time action selection.** Runtime monitoring and fallback policies are
  also crowded, and also a different task.

The contribution is discovering the *axes*.

## Methodology

**Planted gaps.** Before training, deliberately hold out known subsets of the data.
Train the policy on what remains, so it has known, engineered blind spots. Then run
discovery and check whether it recovers the specific subsets that were held out.

That gives real precision and recall numbers on the discovery step itself, rather than
on downstream failure prediction:

- precision: of the axes the method proposes, how many are real planted gaps
- recall: of the planted gaps, how many the method recovers

**Closing the loop.** Take a discovered axis, generate matching scenarios in
simulation, fine-tune on them, and re-measure. If the failure goes away, the axis was
both real and actionable. Same shape as Genario, except the axis comes from
interpretability rather than from a hypothesis a person wrote down.

## Domain

The policy does not have to be a driving policy. Driving is the example used here
because it fits Honda and because the long tail is well documented there. Candidate
domains, including a mobility-adjacent one with a natural sparse grid, are in
[docs/domain-candidates.md](docs/domain-candidates.md).

## Open questions

- Which representation: which layer, and pooled across an episode or kept per-timestep?
- How do you get from a cluster in activation space to a sentence someone can act on?
- Planted gaps may be too easy. Holding out "night rain" might show up as a clean
  separation for trivial reasons (the pixel statistics differ) rather than because the
  policy struggles there. The planted gaps need to be ones that are hard to spot from
  the input alone.
- Scoring discoveries that were never planted. A real gap the method finds that nobody
  held out counts against precision under the naive metric, and is probably the most
  interesting result the method can produce.
