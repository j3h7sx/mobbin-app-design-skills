# Playbook: build from scratch

Use this playbook when the user asks for a new product, feature, or complete
mobile flow.

## 1. Define the research map

Translate the brief into the journeys and screens that determine the product
experience. A habit product might need first launch, habit creation, daily
check-in, progress, reminders, and a paywall. A health product might need
logging, severity entry, history, report creation, and permissions.

Write the design question for each important surface. The question should be
specific enough to change a design decision.

## 2. Search Mobbin flows

Use `search_flows` for each important journey. Keep each query focused on one
sequence. Start with one flow result because a single flow can contain many
screens. Set `platform="ios"` for iOS product work.

Examples:

```text
onboarding that collects goals and shows progress before account creation
health symptom logging from symptom selection through severity and save
subscription paywall shown after personalized onboarding results
```

Inspect the returned images and ordered positions. Record the flow name, app
name, screen count, canonical Mobbin URL, and one useful decision note.

When inline previews sample a long flow, inspect the steps needed for the
research question before describing the whole journey.

## 3. Search decisive screens

Use `search_screens` for important surfaces that need deeper comparison. Run a
`standard` query for a broad reference set. Follow with a `deep` query that
describes the intended hierarchy and interaction in detail. Pass previously
reviewed IDs through `exclude_screen_ids` when useful.

Inspect the images. Shortlist references based on their fit to the product
brief, clarity of interaction, and usefulness to the current decision.

Group the shortlist by product. Several strong results from one app can reveal
its visual language. Results across several apps reveal category conventions.

## 4. Synthesize the pattern

Write `patterns.md` with:

- The repeated structure that users are likely to recognize.
- Meaningful differences between products.
- The pattern selected for this product.
- The product-specific change that makes the pattern fit the user's brief.
- The Mobbin links that support each decision.

Extract structure instead of pixels. Record hierarchy, control choice,
spacing, action placement, progress treatment, and flow order. Preserve the
product's own brand and content.

## 5. Define the product flow

Turn the research into a screen and state list. Include entry points, main
actions, transitions, success states, empty states, loading, errors, and exits.

When the user is present, show the references and design decisions before a
large implementation. Continue after the direction is clear.

## 6. Build and verify

For each screen:

1. Reopen the selected Mobbin references and their decision notes.
2. Build with `mobbin-app-design-skill`.
3. Run the screen in the simulator.
4. Inspect layout, content range, safe areas, themes, accessibility, and
   motion.
5. Compare the result with the selected structural pattern.
6. Fix observed defects and repeat the verification.

After the screens pass individually, run the whole journey. Exercise the main
path, optional actions, invalid input, interruption, and recovery. The final
result should form one coherent product flow.
