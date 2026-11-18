# Animation examples

Private collection of doll side-by-side animation previews and Elden Ring reference clips, from work on 2026-11-18.

These files were copied from the PC. The originals on `D:\AI_Anim_Pipeline` and `E:\EldenRing_Animation_Ref` were left in place.

## Previews

Folder: `previews/`

Each finished pipeline run has:

- `<run>.mp4` — side-by-side video (Elden Ring reference on one side, the doll animation in Blender on the other)
- `<run>_contact_sheet.png` — frame contact sheet
- `<run>_framing_check.json` and `<run>_verdict.json` — framing and quality-gate notes, when present

`roll_medium_f_v2.mp4` is the later NLF roll redo (also present as `roll_medium_f_v2_nlf.mp4` from that run folder).

Pipeline logs and score tables are in the repo root: `LOG.md`, `RESULTS.md`, `ALL_RESULTS.md`.

### How the previews were made

A local video-to-animation pipeline on this PC (`D:\AI_Anim_Pipeline`, RTX 4090, Blender 5.2) estimated 3D pose from a short Elden Ring clip, retargeted it onto the doll, and rendered a side-by-side comparison.

Three methods were tried:

- **FlowHMR** (Hugging Face Space, anonymous). Best of the three on backstep, then blocked by the anonymous ZeroGPU quota, so most FlowHMR runs have no preview.
- **NLF** (isarandi/nlf, local, noncommercial licence). Used for the later batch and the roll v2 redo.
- **MediaPipe Pose** (local). Ran, but the 3D output was jittery.

None of the scored clips fully passed the quality gates. Details are in `LOG.md` and `RESULTS.md`. The later batch was stopped mid-run, so `ALL_RESULTS.md` is incomplete.

## Elden Ring clips

Folder: `elden_ring_clips/`

One reference clip per animation, cut from Elden Ring footage and stored as:

- `<clip>.mp4`
- `<clip>.meta.json`

Frame PNG folders from `E:\EldenRing_Animation_Ref\<clip>\frames` were not included.

`recoil_guard` and `recoil_wall` have metadata only; no `clip.mp4` existed on disk.

Clips that were over 95 MB were re-encoded with ffmpeg (H.264, slightly lower bitrate) so they stay under GitHub's 100 MB file limit. The originals on the E: drive were not changed. Those clips are listed in the commit or in notes below if any could not be shrunk.

## Layout

```
README.md
RESULTS.md
ALL_RESULTS.md
LOG.md
previews/
elden_ring_clips/
```
