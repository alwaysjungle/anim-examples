# Per-clip results (gates fixed before runs)
| clip | method | pose | timing | foot slide | jitter/pops | root | FBX | ALL |
|---|---|---|---|---|---|---|---|---|
| backstep | flowhmr | PASS cos 0.948 (src 0.956), frames>=0.8 0.957 | PASS knee lag [0, 1] | FAIL max 0.40cm mean 0.01cm skim 1 | FAIL spikes 1 flips 0 maxw 25.5 | PASS net [-0.055, 0.348] maxstep 2.37cm spikes 0 | PASS err 0.001mm off 0 | FAIL |
| backstep | nlf | PASS cos 0.957 (src 0.974), frames>=0.8 0.967 | PASS knee lag [0, 1] | FAIL max 0.68cm mean 0.27cm skim 1 | PASS spikes 0 flips 0 maxw 18.3 | PASS net [0.098, -0.377] maxstep 1.85cm spikes 0 | PASS err 0.001mm off 0 | FAIL |
| backstep | mediapipe | FAIL cos 0.902 (src 0.975), frames>=0.8 0.891 | PASS knee lag [1, 0] | FAIL max 0.63cm mean 0.10cm skim 3 | FAIL spikes 83 flips 21 maxw 156.6 | FAIL net [0.168, 0.165] maxstep 6.58cm spikes 12 | PASS err 0.001mm off 0 | FAIL |
| roll_medium_f | flowhmr | not run: ZeroGPU quota | | | | | | n/a |
| roll_medium_f | nlf | FAIL cos 0.579 (src 0.724), frames>=0.8 0.093 | FAIL knee lag [2, 3] | FAIL max 0.96cm mean 0.07cm skim 1 | FAIL spikes 1 flips 0 maxw 58.4 | PASS net [0.827, -1.888] maxstep 6.28cm spikes 0 | PASS err 0.001mm off 0 | FAIL |
| roll_medium_f | mediapipe | FAIL cos 0.65 (src 0.978), frames>=0.8 0.43 | FAIL knee lag [5, 6] | FAIL max 46.96cm mean 3.27cm skim 53 | FAIL spikes 202 flips 100 maxw 180.0 | FAIL net [0.596, -0.276] maxstep 42.87cm spikes 47 | PASS err 0.015mm off 0 | FAIL |
| curved_sword_heavy | flowhmr | not run: ZeroGPU quota | | | | | | n/a |
| curved_sword_heavy | nlf | FAIL cos 0.889 (src 0.959), frames>=0.8 0.935 | PASS knee lag [1, 1] | FAIL max 0.87cm mean 0.05cm skim 1 | PASS spikes 0 flips 0 maxw 77.4 | PASS net [2.822, -2.347] maxstep 13.12cm spikes 0 | PASS err 0.002mm off 0 | FAIL |
| curved_sword_heavy | mediapipe | FAIL cos 0.841 (src 0.983), frames>=0.8 0.785 | PASS knee lag [0, 1] | FAIL max 0.60cm mean 0.05cm skim 2 | FAIL spikes 128 flips 29 maxw 179.9 | FAIL net [0.274, -0.158] maxstep 12.85cm spikes 36 | PASS err 0.001mm off 0 | FAIL |
| great_hammer_heavy | flowhmr | not run: ZeroGPU quota | | | | | | n/a |
| great_hammer_heavy | nlf | FAIL cos 0.745 (src 0.878), frames>=0.8 0.43 | FAIL knee lag [0, 5] | PASS max 0.89cm mean 0.06cm skim 0 | FAIL spikes 3 flips 3 maxw 178.7 | PASS net [0.393, -0.088] maxstep 2.1cm spikes 0 | PASS err 0.001mm off 0 | FAIL |
| great_hammer_heavy | mediapipe | FAIL cos 0.66 (src 0.953), frames>=0.8 0.486 | FAIL knee lag [2, 3] | FAIL max 49.95cm mean 10.94cm skim 29 | FAIL spikes 208 flips 113 maxw 179.8 | FAIL net [0.042, 0.435] maxstep 41.2cm spikes 53 | PASS err 0.047mm off 0 | FAIL |
| hit_heavy | flowhmr | not run: ZeroGPU quota | | | | | | n/a |
| hit_heavy | nlf | JUDGE FAILED (MediaPipe found no usable 2D reference) | | | | | | FAIL |
| hit_heavy | mediapipe | JUDGE FAILED (MediaPipe found no usable 2D reference) | | | | | | FAIL |
| jump | flowhmr | not run: ZeroGPU quota | | | | | | n/a |
| jump | nlf | PASS cos 0.943 (src 0.974), frames>=0.8 0.972 | PASS knee lag [1, 0] | PASS max 0.64cm mean 0.16cm skim 0 | FAIL spikes 2 flips 2 maxw 87.0 | PASS net [-0.819, -0.139] maxstep 2.06cm spikes 0 | PASS err 0.001mm off 0 | FAIL |
| jump | mediapipe | PASS cos 0.926 (src 0.989), frames>=0.8 0.935 | PASS knee lag [1, 1] | FAIL max 0.75cm mean 0.07cm skim 1 | FAIL spikes 107 flips 20 maxw 162.7 | FAIL net [-0.066, -0.082] maxstep 9.9cm spikes 24 | PASS err 0.001mm off 0 | FAIL |
