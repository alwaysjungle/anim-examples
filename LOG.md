# AI video-to-animation pipeline log

## Setup (2026-11-18)
- PC: RTX 4090 24GB, 64GB RAM, Py3.12, Blender 5.2. Tools venv: D:\AI_Anim_Pipeline\venv_tools
- Test clip: clips\backstep_3s.mp4 (backstep clip.mp4 0.5-3.5s, 30fps, 92 frames)

## Candidate 1: FlowHMR (HF Space fafsaf1/FlowHMR, anonymous gradio_client, no login)
- Ran OK in 42s, got NPZ+FBX in flowhmr_space\backstep\

- Backstep (moving-cam mode, VGGT 5): 2D limb cos 0.948, knee lag 0-1, FBX reimport 0.001mm. Needed cleanup: foot pitch fix, contact lock+IK, step arcs, swing clearance, pelvis drop. Remaining: 1 skim frame + 1 calf spike at L-foot re-plant (f61).
- BLOCKER: anonymous ZeroGPU quota hit after 3 runs ('exceeded your ZeroGPU runs limit'). Local FlowHMR needs gated SMPL/SAM3D/VGGT-Omega (login) -> skipped per rules.

## Candidate 2: MediaPipe Pose heavy 3D world landmarks (local, no login) + contact-integrated root

- Ran all 6 clips (backstep, roll_medium_f, curved_sword_heavy, great_hammer_heavy, hit_heavy, jump; 3-3.5 s windows picked by eye from 2 fps contact sheets, list in clips\set.csv). Per-clip table: RESULTS.md.
- MediaPipe: FAIL 6/6. Per-frame 3D is jittery (83-208 rotation spikes per clip, up to 113 flips), and root from foot contacts drifts (steps up to 43 cm/frame). The judge also uses MediaPipe 2D, so its pose scores lean in its favour, and it still failed.

## Candidate 3: NLF (isarandi/nlf v0.3.2 patch6 torchscript, local on the 4090, no login; NONCOMMERCIAL licence)
- Install: D:\AI_Anim_Pipeline\nlf (venv, torch cu124). Capture: scripts\nlf_capture.py (floor = torso-pitch normal, heights metric, root from contacts). Retarget smoothing sigma 2.5.
- FAIL 6/6 on the strict gates. Best: backstep (only foot skim failed) and jump (2 flips). Roll: NLF itself loses the curled body (source 2D cos 0.72). Hammer: source 0.88, arm flips. hit_heavy: no usable reference (smoke/occlusion), so it can't be judged.
- Gate hole found: the root gate checked only smoothness, not direction or size. By hand: NLF backstep root goes FORWARD 0.38 m (wrong) and curved_sword drifts 3.7 m in 3.5 s (wrong). So NLF root = FAIL. FlowHMR backstep root = 0.35 m backward, smooth (correct).

## Status
- No candidate passes most of the set. FlowHMR is clearly the best (only backstep could run: pose 0.948, timing 0-1 frames, FBX exact, correct root; 1 skim frame plus 1 calf spike left), but the anonymous HF ZeroGPU quota blocks the other 5 clips.
- Next: Michael signs into Hugging Face on his own PC (free account gets more ZeroGPU; PRO gets 40 min/day) and reruns:
  powershell -ExecutionPolicy Bypass -File D:\AI_Anim_Pipeline\scripts\run_set.ps1 -Method flowhmr
  Or install FlowHMR locally, which needs the gated SMPL-X, SAM 3D Body and VGGT-Omega licences accepted on his account.

## Roll v2 (11:50)
- FlowHMR still over the ZeroGPU quota. NLF with num_aug=5 + flip aug + implausible-pose filter off; fixed a capture bug (missed detections had frozen the last pose / dropped frames); smoothing 4; gravity cleanup (curled frames rest on the floor, no floor penetration); pelvis drop capped at 12 cm; render floor fixed at z=0.
- Result: pose cos 0.663 (v1 0.579), timing PASS (v1 FAIL), foot slide max 1.08 cm (v1 0.96, skim 2), 10 spikes/5 flips -> still FAIL. Staged grok_xfer\anim_prev\roll_medium_f_v2.mp4


## Batch (started 11:44)
- scripts\pick_window.py (MediaPipe energy @10fps + combo_hit_index), run_all.ps1 (resumable, progress runs_all_progress.json, log run_all.log), all_results.py -> ALL_RESULTS.md. Batch PID 77928. ~3.3 min/clip. FlowHMR quota still exhausted at start -> NLF (retries FlowHMR every 15 clips).
- Correction to roll v2 note: v1 slide max 0.96 cm skim 1, jitter 1 spike/0 flips; v2 jitter is worse (10/5).
