# bd_M_ABC — music module for ButterflyDreaming

Standalone deployment of the **bd_M_ABC** music module — plays an
[ABC-notation](https://abcnotation.com/) score through a
bass-recorder sampler with reverb, vibrato, and chorus effects,
driven by a compact `%%bd_…` directive script.

Live at: **https://wrcstewart.github.io/bd_M_ABC/preview.html**

## What this is

Two files serve directly from GitHub Pages:

- **`preview.html`** — the standalone harness. Script textarea,
  Edit toggle, Copy / Copy Link / Send↓ / Receive↑ buttons,
  BD-invite panel to jump back into the platform, and an inline
  media player at the bottom.
- **`music_module.html`** — the module itself, loaded as an
  iframe inside `preview.html`. Renders the current ABC score
  as audio via Tone.js + abcjs, plus a right-column stepper
  panel for the 8 effect / loop parameters and LH buttons for
  copy-script and bake-to-mp3.

Assets:

- **`bass-recorder/`** — 4 mp3 samples (F#2, C3, G#3, E4) used
  by Tone.js's `Sampler` to synthesise ABC pitches.

No server, no build step. Tone.js + abcjs load from CDN.

## Directive vocabulary

Every controllable parameter has a `%%bd_<name> <value>` directive.
Representative script (also the default when a visitor arrives
with no URL params):

```
%%bd_module bd_M_ABC
%%bd_reverb_wet 0.35
%%bd_reverb_decay 2.5
%%bd_vibrato_frequency 5.0
%%bd_vibrato_depth 0.2
%%bd_chorus_wet 0.3
%%bd_chorus_depth 0.4
%%bd_loop true
%%bd_loop_gap 6
%%bd_score [
X:1
T:Dream Fragment
M:4/4
L:1/8
Q:1/4=60
K:Amin
|A2 B2 [CEA]4 d2|e4 [EAc]4|
|A2 c2 e2 c2|A4 E4|
%%bd_]
```

`%%bd_score [ … %%bd_]` bracket-delimits the ABC block; everything
else is single-line `%%bd_key value` directives with the same
grammar as the rest of the ButterflyDreaming media modules.

## Deep links

Both directions supported:

- **Link into the standalone** — `preview.html?data=<base64>` where
  the payload carries `{ script, node_url, source_text, title, name }`.
  Used by the ButterflyDreaming platform's "Copy Link to External
  Website" button.
- **Link back to BD** — the "Jump to Butterfly Dreaming" and
  "Copy Link to Butterfly Dreaming" buttons in `preview.html`
  produce a URL of the same shape targeting the BD viewer, so
  the browser hands a user back to the graph at the node they
  came from.

## Relation to bd_V_Kolam

This is the musical counterpart to
[bd_V_Kolam](https://github.com/wrcstewart/bd_V_Kolam), which
covers the visual side. Same protocol, same deploy pattern,
same `%%bd_…` directive family.

Both modules are optional standalone deployments of media modules
that live inside the
[ButterflyDreaming graph viewer](https://github.com/wrcstewart/butterflydreaming-graphviewer1).
The main project provides the graph corpus, chat/pair system,
and the container that loads this module in its Player mode.

## License

Released under **CC0-1.0** (public domain dedication). Do what
you like with it, no attribution required.
