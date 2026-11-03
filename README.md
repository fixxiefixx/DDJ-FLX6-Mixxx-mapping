# Pioneer DDJ-FLX6 mapping for Mixxx

MIDI mapping and script for the Pioneer DDJ-FLX6, based on the DDJ-FLX4 mapping that ships with Mixxx. Forum thread: <https://mixxx.discourse.group/t/ddj-flx6-and-mixxx/24714>

The controller's manual has no MIDI table. MIDI notes were taken from the FLX4 mapping and checked or measured on a DDJ-FLX6 with `mixxx --controller-debug`.

## Installation
1. Copy `Pioneer-DDJ-FLX6.midi.xml` and `Pioneer-DDJ-FLX6-script.js` to your Mixxx controllers folder: `~/.mixxx/controllers/` on Linux, or `~/.var/app/org.mixxx.Mixxx/.mixxx/controllers/` for the Flatpak version.
2. Start Mixxx, open Preferences, then Controllers, select the DDJ-FLX6 and enable it with this mapping.
3. After editing the files, restart Mixxx or reload the mapping, otherwise the old version keeps running.

## What is mapped
- **Mixer:** trim, 3-band EQ, filter (Quick Effect `super1`), channel faders, crossfader, headphone CUE per channel, headphone mix, VU meters.
- **Transport and tempo:** play, cue, shift+cue, sync, master (sync leader), 14-bit tempo slider. Shift+master cycles the tempo range, shift+Beat Sync toggles quantize, shift+headphone CUE is tap tempo.
- **Jog wheel:** touch, scratch, bend, shift+search. If you lift your hand while the wheel is still moving (a back spin), scratching continues until the wheel has stopped. Shift+IN and shift+OUT adjust the loop points with the jog wheel; the lights show which point is being adjusted. A plain IN/OUT press during a loop sets new loop points, which differs from the manual.
- **Loops:** IN, OUT, reloop/exit, loop halve/double.
- **Pads:** Hot Cue (shift to clear), Beat Jump (shift to resize), Beat Loop, Sampler (shift to stop/eject, pads blink while a sample plays), Keyboard mode, Key Shift. Pad FX pads 1-8 trigger Quick Effect presets.
- **Browser:** rotary turn, rotary press (expands or collapses sidebar items and enters the track list; from the track list it moves back to the sidebar), BACK (moves focus backward), LOAD on all four decks, shift+LOAD sorting (deck 1 BPM, deck 2 title, deck 3 key, deck 4 artist), VIEW (maximized library), shift+rotary waveform zoom.
- **Merge FX:** select (shift reverses), press and turn, including the `mergeFxAsJogwheel` setting.
- **Decks 3 and 4:** all pad blocks mirror decks 1 and 2.

## Mixxx-specific mappings
Mixxx has no Merge FX, Release FX or Serato/rekordbox-only features, so these controls are used for Mixxx functions or are rebuilt on Mixxx equivalents.

| Control                                     | Mapping                                                                                 | Manual                                             |
|---------------------------------------------|-----------------------------------------------------------------------------------------|----------------------------------------------------|
| Merge FX (select, press, turn) and Pad FX   | Quick Effect chain presets; turn drives the Quick Effect knob                           | Merge FX / Pad FX effects                          |
| Merge FX knob turn (`mergeFxAsJogwheel` on) | Jog wheel and play/pause of the hidden deck (3/4)                                       | Changes the Merge FX effect                        |
| Shift + Merge FX knob, turn                 | Changes the deck's key (`pitch`, ±12 semitones)                                         | Sample/oscillator volume                           |
| Shift + Merge FX knob, press                | Resets `pitch` to 0                                                                     | Cancels Merge FX                                   |
| CUE/LOOP MEMORY                             | Toggles slip mode                                                                       | Saves a cue or loop                                |
| Shift + CUE/LOOP MEMORY                     | Toggles keylock                                                                         | Deletes a cue or loop                              |
| Shift + Beat Sync                           | Toggles quantize                                                                        | Cancels sync (Serato only)                         |
| Shift + PLAY/PAUSE                          | Reverse roll                                                                            | Stutter (Serato only)                              |
| Shift + RELOOP/EXIT                         | Reloop and stop                                                                         | Active-loop toggle (rekordbox)                     |
| BEAT ◄ / ►                                  | Steps the Beat FX effect selector                                                       | Beat fraction down / up                            |
| Beat FX slots and channel select            | Three slots on `EffectUnit1`/`EffectUnit2`, routed to channels                          | Beat FX slot and channel select                    |
| Beat FX LEVEL/DEPTH knob (per slot)         | Turn: `meta` (depth) of the slot's effect; shift + turn: `mix` (level) of effect unit 1 | Adjusts the Beat FX parameter (shift does nothing) |
| Shift + BEAT FX ON/OFF (Release FX)         | Spinback of the playing decks assigned to effect unit 1; releasing cancels it           | Turns Release FX on/off (rekordbox)                |

## Not mapped
- JOG CUTTER (Jog Cutter mode).
- Pad shift layers: Pad FX effects I-P, Keyboard mode shift (delete cue, semitone up/down) and Key Shift pad 7/8 (change pitch step).
- Beat FX: the beat-fraction buttons and shift+BEAT (Auto/Tap mode), which step the effect selector instead.
- Merge FX shift functions as described in the manual (shift+press to cancel, shift+turn for sample volume); the same inputs are used for the Mixxx-specific pitch controls above.
- Fader Start (shift + moving the channel fader or crossfader).
- CUE/LOOP MEMORY save and delete (the buttons are used for slip mode and keylock), 4-beat auto loop on long press of IN, secondary pad modes and Sample Scratch.
- Long press and shift+VIEW, shift+rotary press, shift+BACK.

## Handled by the controller itself
These work without any binding in the mapping:
- Shift+DECK SELECT (Dual Deck). The messages it sends in Dual Deck mode are not checked, so the Merge FX deck tracking may not follow it.
- Double-press LOAD (Instant Doubles). It presumably loads the same selected library track onto the second deck; whether it also copies the playback position, as Mixxx's `CloneFromDeck` would, is not checked.
- Vinyl mode (shift+JOG CUTTER). The controller switches it itself: with it on, touching the top of the platter scratches; with it off, the platter only bends the pitch. No light shows the mode.
- Master headphone CUE, probably because the FLX6 has a built-in audio interface and routes it itself.
- Lighting of the pad mode buttons (HOT CUE, PAD FX, BEAT JUMP, SAMPLER, KEYBOARD, KEY SHIFT, …) on all decks. The pad LEDs themselves (hot cue, beat loop and sampler state) are driven by the mapping.
