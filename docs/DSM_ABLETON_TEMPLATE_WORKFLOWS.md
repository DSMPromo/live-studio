# DSM Music Studio: Ableton Live Starter Templates

This document accompanies three built-in presets in `src/modules/templates/tools.ts`:
`dsm_production` (12 tracks), `dsm_reverse_media` (11 tracks), and `mateo_adaptive` (7 tracks).

## 1. Install the extension

**Prerequisite:** Ableton Live 12 Suite Beta with Extensions support (12.4.5b+), per the official Ableton Extensions FAQ. On current beta builds use Settings > Extensions.

### Install a published package

1. Obtain `live-studio.ablx` from the repository's Releases page, if available.
2. In Live, open Settings > Extensions and install the `.ablx`.
3. Leave Developer Mode OFF for installed releases.
4. Fully quit and restart Live.
5. Right-click a track, clip, clip slot or scene > Extensions > Live Studio.

**Important:** A release built from `main` will not contain these new DSM presets until this branch has been merged and a new `.ablx` has been packaged.

### Build and run the source branch

1. Install Node.js 22.11+ and the beta Ableton Extensions SDK and CLI archives.
2. Clone this branch and enter the repository.
3. The existing `package.json` points to beta SDK/CLI tarballs under the original author's absolute macOS path (`/Users/imac/Documents/extensions-sdk-1.0.0-beta.0/...`). Change BOTH `file:` dependencies to the actual local tarball paths before `npm install`. Do not assume the public npm registry has these beta archives.
4. Run `npm install`, `npm run typecheck`, `npm test`, `npm run build`, and `npm run package`.
5. Install the resulting `live-studio.ablx` using the release instructions above, with Developer Mode OFF. For CLI development with `npm run start`, use the SDK's separate developer workflow.

Packaging uses Info-ZIP. Do not confuse the output `.ablx` extension package with an Ableton Set `.als` file.

## 2. Create DSM sets via the existing Project Templates module

**Start with a new, empty Live Set.** These commands *append* tracks and devices. Running a preset twice duplicates the tracks.

In Live Studio > Project Templates, select `apply_template` and specify one of:

| Preset | Tracks | Use |
| --- | ---: | --- |
| `dsm_production` | 12 | Daily music production, drums, synths, vocals, reference, prints |
| `dsm_reverse_media` | 11 | Reconstruct reference sounds and effects, dry/wet A-B comparison |
| `mateo_adaptive` | 7 | Five synchronized Mateo soundtrack stems + reference and review print |

Or ask the copilot: **"Use the Project Templates tool apply_template with genre mateo_adaptive in the current empty Set. List the tracks created and any skipped native devices."**

The template module inserts native devices on a best-effort basis. The result reports created tracks and inserted devices. Verify the result inside Live, especially any skipped devices. Audio source files, samples, routings, tempo, detailed device parameter values and color assignments are not constructed by these presets.

## 3. Finish and save genuine Ableton templates

1. Open the new Set and set BPM, time signature and key.
2. Set audio routing and returns, load instruments and samples, and optionally create groups.
3. Set reference tracks to a monitoring setup that avoids accidental inclusion in final prints.
4. Configure effect settings on each chain, then save reusable Audio Effect Racks / Instrument Racks in Live's browser.
5. Select File > Save Live Set as Template and name it for this workflow.
6. For portability, use File > Collect All and Save before moving a project with external audio references. Keep licensed/owned source files only.

The `.als` template is created by Ableton Live. A source-code preset is not the same as a finished `.als` Set.

## 4. DSM Production: starting routing

- Drum tracks (Kick, Snare Clap, Hats Perc) -> DRUM BUS.
- Bass -> BASS BUS, with sidechain ducking from kick when desired.
- Harmony + Lead -> MUSIC BUS.
- Texture + Vocal + FX -> AUDIO/FX BUS.
- Print tracks record the approved result; don't route the printed track back into the mix.
- Reference track is monitoring only, excluded from final renders.

Save an empty session as `DSM Production Base.als` through Ableton's Template command.

## 5. DSM Reverse Media: recreate an effect reproducibly

1. Add an audio reference you have the right to use to `REF | Original`. Mark the reference time range.
2. Note tempo (BPM), time signature, tonal center, groove, instrumentation, texture, stereo width, transition timing and apparent reverberation/delay.
3. Rebuild the DRY musical source with drums, bass, chords and lead tracks. Align transients.
4. Rebuild the WET effect in a separate Audio Effect Rack (e.g., EQ Eight -> Auto Filter -> Saturator -> Delay -> Reverb -> Utility). These are candidate devices, not a claim about any specific source.
5. Compare loudness-matched dry, wet and reference bounces, adjust and keep a dated revision history.
6. Save each successful chain as a native Live Rack and use Live Studio's FX Chain Presets > `save_fx_preset` for a *device-name-only* quick recall.
7. Use Project Templates > `extract_template` to save a named track/device structure for future Sessions.

**Limitation:** Current `extract_template` and `save_fx_preset` capture device **names**, not precise knob settings, mapping, third-party plugins, audio clips, or rack internals. Use native Ableton Racks and `.als` templates to preserve these.

### Reverse-engineering recipe log

For each source, record the following fields:

```yaml
recipe_id: DSM-FX-0001
source_url: "https://..."
source_time_range: "00:00-00:10"
permissions: "owned/licensed/reference-analysis-only"
bpm: null
key: null
dry_elements: []
fx_chain: []
parameter_notes: {}
automation: []
a_b_test: "loudness-matched reference vs dry vs wet"
rack_preset_name: "DSM FX - descriptive effect name"
quality_check: "transients, low-end, width, clipping, mono"
```

These recipe logs are documentation. The current Live Studio `apply_template` tool does **not** parse YAML.

## 6. Mateo Adaptive: 5 synchronized stems

Start at **84 BPM**, **4/4**, using an **8-bar loop** as an editable default (within the planned 83-86 BPM range). The first five tracks are the synchronized deliverable stems:

1. Ambience
2. Rhythm
3. Harmony
4. Mateo Melody
5. Emotion Action Cues

Use the two additional tracks for Guide Audio and Review Export.

Keep every stem aligned from bar 1 and render with identical start/end times. Create versions for Odyssey, Business, Nostalgia, Vacation, Osaka Night Drive, Mediterranean Trip and Singapore, adapting instrumentation and mood for each season. Export and verify 5 audio stems per section with consistent BPM, bar length, sample rate and tails. Test each stem alone and all five together for phase, timing, transition and overall level.

Suggested Copilot prompt:
> "Create the mateo_adaptive project template. Use 84 BPM and 4/4, write an 8-bar original loop plan with ambience, rhythm, harmony, Mateo melody and emotion cues. Show the plan before making any clips. Preserve exact loop boundaries for all five stems."

Only the track-creation portion is currently guaranteed by the template tool; transport/tempo and note generation depend on the separate Live Studio tools and SDK permissions available in the current build.

## 7. Daily reusable steps

1. Create a new Set.
2. Apply ONE preset.
3. Complete tracks, routing and effects in Live.
4. Save the native Live Template.
5. Store a recipe log and versioned reference notes for each effect.
6. Render a short A/B or stem-review export.
7. Reopen the saved template in a fresh session to verify all required devices and assets resolve.

## Links

- https://github.com/DSMPromo/live-studio
- https://ableton.github.io/extensions-sdk/
- https://help.ableton.com/hc/en-us/articles/27303428331420-Ableton-Extensions-FAQ
- https://help.ableton.com/hc/en-us/articles/209067189-Default-Set-and-Template-Sets
