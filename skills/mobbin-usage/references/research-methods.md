# Research methods

Use this reference for focused screen, flow, component, and product-pattern
research with Mobbin.

## Screen research

Use `search_screens` when the question concerns one surface.

A strong query describes visible elements and their relationship:

```text
pain logging screen with symptom choices, a severity scale, and a fixed save action
paywall with annual and monthly plans, trial terms, and a restore action
empty activity history with an explanation and one primary logging action
```

Use `standard` mode for a broad pass. Use `deep` when the brief contains a
specific information hierarchy or interaction. Inspect the image for every
reference you keep.

## Flow research

Use `search_flows` when the question concerns sequence, timing, or state
changes. Search one journey at a time.

Record:

- The entry point.
- Screen count and ordered positions.
- What each step asks from the user.
- What each step gives back.
- Progress and exit behavior.
- The location of permissions, account creation, and payment when relevant.
- The canonical Mobbin flow URL.

Compare several products when the question concerns a category convention.
Name an app in the query when the task requires a specific product.

## Component research

Mobbin MCP does not expose a separate element taxonomy. Describe the component
inside a real screen context with `search_screens`.

Examples:

```text
iOS bottom tab bar with a raised central create action on a health dashboard
horizontal severity selector with text labels and a fixed bottom action
calendar day cells that communicate logged symptoms beyond color alone
```

Extract measurable properties where the image supports them. Include item
count, placement, label treatment, selected state, surrounding spacing, and
relationship to the primary task.

## Working with a supplied Mobbin link

Treat a user-supplied Mobbin screen, flow, or collection as the starting
reference. Record its canonical URL. Inspect the visible content before using
it. Use targeted searches to find supporting or alternative patterns when the
task needs comparison.

## Evidence discipline

Begin each pass with a question that can change the design. Inspect images
before writing conclusions. Use results across products to identify repeated
structure. Keep one product's branding separate from the shared interaction
pattern.

For every selected result, write one short decision note and its canonical
Mobbin URL. Mark a pattern as common only after several relevant products show
it. State when the reference set is too small to support a category claim.

Research reaches saturation when new relevant results stop changing the
decision. End the search at that point and move to implementation or review.
