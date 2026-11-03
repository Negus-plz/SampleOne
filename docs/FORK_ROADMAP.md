# SampleOne roadmap (Negus fork of AM Mod)

This fork adds workflow features on top of AM Mod for **chopping, drum sequencing,
stems and live playing**. AM Mod is MIT-licensed and does the hard part: it runs a
patched copy of the stock app in RAM, without flashing anything.

**Upstream first.** Each feature is proposed to AM Mod as an issue before work starts,
so it can land there instead of splitting the community. This fork stays close to
`AlekseyMalykh/am-mod` main.

## Ground rules

- Keep AM Mod's `LICENSE`, `NOTICE.md` and credits.
- Follow [CONTRIBUTING.md](../CONTRIBUTING.md): **never commit firmware**, rootfs files, release zips,
  SD-card contents or device identifiers.
- **Clean room.** Every feature is written from scratch. Don't copy code, screens,
  layouts or text from closed-source mods. Describe the behaviour you want, then
  build it your own way.
- **Test in three levels**, and say which ones passed:
  1. ARM/QEMU checks (`verify_*.py`, `check_*.c`)
  2. The Virtual MPC Sample emulator (`orrpunk-art/virtual-mpc-sample`)
  3. A real MPC Sample on firmware 1.3.0.12
  Use AM Mod's labels: **trial** (checks passed, hardware pending) and **confirmed** (worked on hardware).
- Every feature must keep projects **loadable on a stock MPC Sample** and support **Undo**.

## One-time setup

- [ ] A Linux or Windows (WSL) computer, linked to Claude through the desktop app
- [ ] Python 3 and AArch64 GCC/binutils
- [ ] Your own copy of firmware 1.3.0.12. The app's SHA-256 must be
      `b6584cba76e416e432ad202509099d34373dc2c3d6a8fb625f5678bf0193b508`
- [ ] Rebuild the current AM Mod release from source and match its package
      before changing anything (see "Build from source" in [README.md](../README.md))
- [ ] The Virtual MPC Sample emulator running the stock firmware
- [ ] A spare exFAT SD card, and backups of every project you care about

## Already in AM Mod (no work needed)

Step sequencer on the pads · events editor · chords with inversions, latch and arp ·
scale lighting · per-pad EQ · resampling a single pad · batch extract of chops to WAVs ·
sample and project search · typing names with the pads · batch copy ·
16 Levels types including Probability and Ratchet.

## New features, in priority order

### Phase 1: foundations

| # | Feature | Why I want it | Notes |
| --- | --- | --- | --- |
| F1 | **Multiple drum tracks** (up to 16), each with its own pad banks. Pick a track with PAD BANK + encoder | Kit, chops, bass and keys on separate tracks | The biggest change. Check what the XPJ format already stores for tracks, and what a stock MPC loads |
| F2 | **Track View** in step editing: one row per track, 1–8 bars, copy, paste and duplicate across tracks | See and edit the whole beat at once | Depends on F1 |
| F3 | **Mixdown and stem export** to WAV: one file per track, tempo in the file name | Finish beats in a DAW, send stems | Already on AM Mod's ideas list ("Stem export") |

### Phase 2: performance

| # | Feature | Why I want it | Notes |
| --- | --- | --- | --- |
| F4 | **Per-sequence track mutes** and **recorded mutes** | Drops and breakdowns that play back by themselves | AM Mod already has step mutes, so build on those |
| F5 | **Record into the sequence** from Sample Record (one loop long, note on beat 1), plus a **looper** that stacks passes | Sample vinyl or keys straight into the beat | |
| F6 | **Sample tail**: a short ping-pong fade after a chop ends | Chops that don't cut off abruptly | |

### Phase 3: mixing

| # | Feature | Why I want it | Notes |
| --- | --- | --- | --- |
| F7 | **Mixer with inserts** on pads, tracks, submixes and master | Glue compression on drums, EQ on bass | Already on AM Mod's ideas list ("Mixer and effects") |
| F8 | **Explode**: split a drum track into one track per sound | Separate kick, snare and hat stems | Depends on F1 |
| F9 | **Fades**: write a volume or filter fade into a selection | Intros, outros, filter sweeps | |

### Phase 4: comfort

| # | Feature | Why I want it | Notes |
| --- | --- | --- | --- |
| F10 | **MIDI keyboard plays the selected pad** chromatically, with a root note per pad | Play chopped keys from a keyboard | Ties in with AM Mod's M01 MIDI audit |
| F11 | **Shortcut remapping** for SHIFT + pads and PAD FX | Your own button layout | |
| F12 | **Home folder** for Sample Select, and a **default template** for New Project | Faster start every session | |

## Done means

- [ ] Works in the emulator
- [ ] Confirmed on a real MPC Sample (note the firmware and build)
- [ ] The project still opens on a stock MPC Sample
- [ ] Undo restores the previous state
- [ ] Documented in [FEATURES.md](FEATURES.md), with status, and proposed upstream
