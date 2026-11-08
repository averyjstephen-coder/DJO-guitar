# Psych Pedalboard

A guitar pedalboard plugin (AU / VST3 / Standalone) for pop-psych guitar tones in the direction of Djo's records.
Six pedals in a fixed order, each with an on/off switch, plus six starting presets.

    Drive > Top-boost amp (+ cab) > Chorus > Phaser > Delay > Reverb

| Pedal | Voiced after |
|---|---|
| Drive | Light overdrive for push or a fuzzier lead |
| Top-boost amp | Bright, chimey AC30-style top-boost amp with a speaker-style roll-off |
| Chorus | Boss CH-1-style stereo chorus (Rate, Depth, Level, EQ) |
| Phaser | 4-stage phase-90-style phaser with feedback |
| Delay | Dark, wobbly tape-style echo |
| Reverb | Freeverb-style room/hall |

## What this is based on
Public information about Djo's actual rig is thin. What I found: an Equipboard listing with a Boss CH-1 Super Chorus
(listed as a "closest match", unconfirmed) and a UAD Ruby '63 Top Boost amp plug-in; plus a third-party tutorial for
re-creating "End of Beginning" that uses an amp simulator, a chorus, reverb and palm muting. So the **chorus and
top-boost amp are the documented parts**. The drive, phaser, delay and reverb are common pop-psych pedals added so you
have options. They are not claimed to be Djo's gear. The presets are starting points, not copies of any song's sound.

## Hear it before you build it
`demo_presets.wav` is a synthesized plucked power chord through each preset in order (loudness-matched, stereo).
It shows the effects, but a real guitar will sound different.

## Build (macOS, for Logic)
    cmake -B build -G Xcode
    cmake --build build --config Release
JUCE 8.0.4 is fetched automatically. Or push to GitHub with `./push-to-github.sh` and download the build from the
Actions tab (`gh run download -n PsychPedalboard-macOS`), then install with
`sudo ./install-mac.sh ~/Downloads/PsychPedalboard-macOS.zip`. Run `auval -v aufx Psyb Pers` if Logic rejects it.

## Tests
    g++ -O2 -std=c++17 -ISource -Itests tests/test_engine.cpp -o engine_tests && ./engine_tests

## Status
Engine: unit-tested and rendered (all-pass level, chorus delay time, delay echo timing and decay, reverb tail decay and
stability, everything-off transparency, every preset finite and bounded). Plugin wrapper and editor are syntax-checked
against the real JUCE 8.0.4 headers, but never linked, run in a host, or listened to in real time.
Bypassing a pedal is a hard switch, so you may hear a small click.
