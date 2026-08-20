# Playbook: improve an existing screen

Use this playbook when the user provides code, a screenshot, or a live screen
and asks for a better version.

## 1. Inspect the current screen

Run the current screen when a runnable project is available. Capture its
layout and interaction. Name the specific issues that the research must answer.

Useful issue statements describe visible behavior:

- The primary action has the same visual weight as secondary controls.
- The hierarchy does not explain which value matters first.
- The sheet appears without a clear relationship to the action that opened it.
- The error message shifts the layout and hides the recovery action.

## 2. Build a Mobbin reference set

Use `search_screens` with one query for the screen's function and visible
structure. Start with `mode="standard"`.

Run a second query with `mode="deep"`. Describe the hierarchy, interaction,
and product context that would address the observed problem. Exclude reviewed
screen IDs when the second pass should provide new material.

Inspect each returned image before selecting it. Keep the canonical Mobbin
link and a short note that states why the reference matters.

Continue until new results stop changing the intended screen structure. Select
the smallest set that explains the direction clearly.

## 3. Check the surrounding flow

When the screen belongs to a journey, use `search_flows` for that journey.
Study the step before the screen, the screen itself, and the next meaningful
state. This reveals transition, state-carrying, and exit requirements that one
screenshot cannot show.

## 4. Write the target

Turn the reference findings into checkable decisions:

- Layout skeleton and hierarchy order.
- Control types and action placement.
- Spacing and surface relationships.
- Content behavior for long and missing values.
- Entrance, response, and exit motion.
- Loading, empty, error, and success states.

Link each reference used for a decision.

## 5. Implement and compare

Build with `mobbin-app-design-skill`. Run the updated screen in the simulator.
Compare it with the target decisions and the selected Mobbin references.

Record the complete interaction when motion or keyboard behavior matters.
Inspect the recording at normal speed and frame by frame. Verify light and
dark appearance, safe areas, Dynamic Type, Reduce Motion, and relevant error
paths.

Repeat until the observed screen satisfies the target decisions and the
surrounding flow remains coherent.
