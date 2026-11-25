# ZenithPeak

Peak-level multi-chair live step-grid desk.

Elevated from ApexZenith with:
- Expanded chairs: kick, snare, hat, crash, tom, bass, piano, guitar, violin pad, trumpet
- Per-chair BiquadFilter (lowpass/highpass)
- Master delay send
- Full hardware MIDI note-on/off + velocity; record mode writes into the step grid in real time
- Stronger sustain envelopes on pads and held notes (attack ramp + full-length hold + 10–30 ms release)
- Deterministic humanize (downbeats stay exact)
- Full WorkinWithAI Audio Engine compliance

**Free.**

## Audio Engine compliance
- Timing on AudioContext clock only (LOOKAHEAD_MS=25, SCHEDULE_AHEAD=0.12)
- Live mutable state — changes take effect within one bar
- OfflineAudioContext WAV: exact length Math.round(bars * 4 * 60 / bpm * sampleRate), first transient at sample 0, folded ring-out tail, 48 kHz 24-bit stereo, peak ≤ −1 dBFS
- Matching multi-track MIDI (one track per chair, tempo + time signature)
- Pinned FluidR3 samples `@d58301e4a494555f411a2afbc448b724136eee76` (never @main)
- User BPM (60–180) + key + 4-chord entry persist in localStorage and apply to playback + export
- Per-chair gains → master compressor (safety limiter)
- First tap creates/resumes AudioContext; hidden tab stops cleanly
- Hardware MIDI supported (on-screen is fallback)

## Acceptance checks (section 9)
1. Export 92 BPM / 8 bars / 48 kHz → exactly 1,001,739 samples, first transient ≤ 1 ms of sample 0.
2. Loop 4× in DAW: no seam clicks, no grid drift.
3. Tab hide 30 s → clean stop, no stacked notes.
4. Live recipe/mute/BPM/key/chord change heard within one bar.
5. Block sample host → UI names missing instruments.
6. Longest pad at slowest tempo sustains to note end.
7. No `@main`/`@gh-pages`, no `Math.random` in export path, voice names match samples.

Live: [zenithpeak.vercel.app](https://zenithpeak.vercel.app) (after deploy)
