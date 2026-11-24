# MOT_TbD_DeepSORT

**DeepSORT** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Wojke et al., ICIP 2017; official code: `nwojke/deep_sort`
- Principle: matching cascade on appearance + Mahalanobis gating, then IoU
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`deepsort`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (DeepSORT, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| libra_rcnn | 0.536 | 0.488 | 0.594 | 0.559 | 0.683 | 105 | 0.610 | 0.461 | 0.45 | 29.5 | 0.599 |
| cascade_rcnn | 0.513 | 0.464 | 0.571 | 0.543 | 0.655 | 89 | 0.586 | 0.439 | 0.35 | 37.8 | 0.625 |
| dynamic_rcnn | 0.503 | 0.454 | 0.561 | 0.527 | 0.658 | 89 | 0.588 | 0.418 | 0.39 | 28.3 | 0.579 |
| faster_rcnn | 0.501 | 0.449 | 0.564 | 0.525 | 0.659 | 94 | 0.601 | 0.400 | 0.44 | 28.2 | 0.582 |
| retinanet | 0.374 | 0.318 | 0.444 | 0.368 | 0.480 | 71 | 0.507 | 0.240 | 0.26 | 25.2 | 0.535 |
| v6 | 0.335 | 0.265 | 0.428 | 0.308 | 0.430 | 41 | 0.506 | 0.165 | 0.25 | 11.1 | 0.509 |
| ppyoloe | 0.317 | 0.255 | 0.410 | 0.295 | 0.384 | 59 | 0.513 | 0.120 | 0.25 | 12.0 | 0.487 |
| gfl | 0.309 | 0.230 | 0.422 | 0.261 | 0.363 | 39 | 0.455 | 0.164 | 0.19 | 24.3 | 0.522 |
| atss | 0.298 | 0.224 | 0.400 | 0.256 | 0.366 | 48 | 0.432 | 0.164 | 0.20 | 39.4 | 0.527 |
| x | 0.277 | 0.215 | 0.387 | 0.253 | 0.341 | 30 | 0.480 | 0.075 | 0.21 | 8.7 | 0.478 |
| tood | 0.267 | 0.197 | 0.368 | 0.222 | 0.307 | 38 | 0.401 | 0.133 | 0.18 | 29.1 | 0.506 |
| v11 | 0.262 | 0.189 | 0.419 | 0.216 | 0.300 | 26 | 0.464 | 0.060 | 0.17 | 9.1 | 0.435 |
| v9 | 0.254 | 0.178 | 0.403 | 0.201 | 0.279 | 42 | 0.441 | 0.067 | 0.17 | 14.1 | 0.460 |
| rtmdet | 0.240 | 0.178 | 0.339 | 0.207 | 0.292 | 20 | 0.437 | 0.044 | 0.16 | 10.0 | 0.465 |
| x2 | 0.235 | 0.173 | 0.330 | 0.199 | 0.284 | 28 | 0.409 | 0.061 | 0.18 | 11.0 | 0.452 |
| v8 | 0.233 | 0.175 | 0.326 | 0.198 | 0.272 | 46 | 0.420 | 0.046 | 0.16 | 8.1 | 0.443 |
| v10 | 0.229 | 0.161 | 0.348 | 0.183 | 0.265 | 39 | 0.399 | 0.060 | 0.16 | 10.7 | 0.455 |
| fcos | 0.229 | 0.159 | 0.337 | 0.177 | 0.251 | 66 | 0.341 | 0.118 | 0.15 | 33.9 | 0.493 |
| ssd | 0.218 | 0.190 | 0.251 | 0.216 | 0.273 | 68 | 0.435 | 0.000 | 0.18 | 32.1 | 0.288 |
| v1 | 0.218 | 0.182 | 0.268 | 0.198 | 0.266 | 139 | 0.293 | 0.142 | 0.21 | 8.6 | 0.374 |
| v13 | 0.212 | 0.159 | 0.318 | 0.182 | 0.251 | 35 | 0.417 | 0.007 | 0.16 | 13.4 | 0.372 |
| v12 | 0.198 | 0.148 | 0.265 | 0.167 | 0.235 | 29 | 0.395 | 0.000 | 0.14 | 11.4 | 0.424 |
| deformable_detr | 0.196 | 0.149 | 0.265 | 0.166 | 0.223 | 87 | 0.277 | 0.115 | 0.16 | 71.7 | 0.482 |
| v26 | 0.187 | 0.144 | 0.243 | 0.165 | 0.231 | 29 | 0.373 | 0.000 | 0.15 | 11.9 | 0.390 |
| fairmot | 0.156 | 0.098 | 0.295 | 0.115 | 0.180 | 23 | 0.287 | 0.026 | 0.05 | 8.3 | 0.387 |
| centernet | 0.075 | 0.051 | 0.111 | 0.057 | 0.080 | 23 | 0.150 | 0.000 | 0.03 | 12.1 | 0.395 |

### Score-threshold sensitivity (DeepSORT, HOTA with one common threshold)

| detector | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 |
|---|---|---|---|---|---|
| deformable_detr | 0.462 | 0.439 | 0.404 | 0.358 | 0.293 |
| faster_rcnn | 0.512 | 0.514 | 0.516 | 0.514 | 0.511 |
| fcos | 0.495 | 0.486 | 0.462 | 0.409 | 0.343 |
| libra_rcnn | 0.521 | 0.528 | 0.537 | 0.538 | 0.539 |
| ppyoloe | 0.459 | 0.460 | 0.439 | 0.416 | 0.373 |
| rtmdet | 0.476 | 0.461 | 0.435 | 0.393 | 0.324 |
| v10 | 0.462 | 0.447 | 0.424 | 0.396 | 0.339 |
| v11 | 0.441 | 0.422 | 0.397 | 0.363 | 0.324 |
| v12 | 0.448 | 0.430 | 0.406 | 0.362 | 0.264 |
| v13 | 0.371 | 0.352 | 0.338 | 0.315 | 0.279 |
| v26 | 0.411 | 0.389 | 0.352 | 0.296 | 0.251 |
| v6 | 0.502 | 0.487 | 0.472 | 0.448 | 0.413 |
| v8 | 0.437 | 0.424 | 0.402 | 0.361 | 0.323 |
| v9 | 0.461 | 0.446 | 0.423 | 0.386 | 0.330 |
| x | 0.438 | 0.436 | 0.426 | 0.410 | 0.370 |
| x2 | 0.436 | 0.440 | 0.413 | 0.376 | 0.322 |

Part of the *Physical AI MOT* comparison of the **Statera Working Group**: 10 trackers x 25 detectors (+ the detections of FairMOT), 3 joint
detection-and-tracking networks and 1 end-to-end tracker under one protocol. The full comparison (Pareto front,
tracker ranking, JDT / E2E against tracking-by-detection) is in `MOT_Detectors_KITTIMOTS` (`RESULTS.md`).

## Protocol (all MOT_* repositories)

- Online / causal only: every method sees the current frame and its own state; checked by re-running prefixes of
  every sequence (the output of frame t must not change when later frames are removed).
- Input 1216 x 384 (KITTI 1242 x 375 letterboxed), detectors trained from scratch on KITTI-MOTS train (12 sequences),
  30 epochs, Adam 1e-4, effective batch 8, seed 777 - the protocol of the *Physical AI Object Detection* series.
- Metrics: HOTA / DetA / AssA (TrackEval classes, car / pedestrian mean), MOTA, IDF1, IDSW.
- Latency: RTX 4070 Laptop GPU, batch 1, fp32, medians over val; pipeline = detector (forward + post-processing) +
  ReID (appearance trackers) + tracker (CPU); image decoding / letterboxing not included.
- Trackers run with their official default parameters; frame-based values given for 30 fps are scaled to 10 fps.
  A sensitivity table with one common score threshold for every tracker is reported separately (chosen on val, so it
  is analysis, not ranking).

## Data: KITTI-MOTS (box level, val = 9 sequences, 2,981 frames)

KITTI tracking images (21 training sequences) with instance / track annotations; boxes = tight boxes of the masks,
classes car and pedestrian, ignore regions (id 10000) neither rewarded nor penalised. The annotations are taken from
the **KITTI-STEP** panoptic maps (same sequences and split, car / person instances merged from KITTI-MOTS; frames,
track counts and pedestrian masks match the KITTI-MOTS paper, car masks differ by 39 of 26,899).

```bash
bash tools/mot/get_kitti_mots.sh            # KITTI tracking images + annotations (KITTI-STEP fallback)
python tools/mot/kittimots_to_voc.py        # VOC-layout copy with tracks + count report
UNIFIED_IMAGE_DATASET=kittimots python tools/mot/count_loader.py     # counts as the loaders read them
```

**Licence of the data and of every trained weight here: KITTI / KITTI-MOTS / KITTI-STEP are CC BY-NC-SA 3.0
(non-commercial).**

## Usage

```bash
pip install -r requirements.txt
pip install "git+https://github.com/JonathonLuiten/TrackEval.git@12c8791b303e0a0b50f753af204249e622d0281a"
# saved detections (+ ReID features) of the 25 detectors: Release of Statera-Workshop/MOT_Detectors_KITTIMOTS
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --trackers deepsort --causal
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --gt-as-pred      # evaluation self-test
python tools/mot/mot_table.py                                                             # tables of all runs
```

`run_tracker.py --trackers` accepts every tracker of the comparison (iou, sort, bytetrack, ocsort, hybridsort, botsort, botsort_reid, deepsort, tracktrack, fairmot), so other
trackers can be run on the same detections. Results of this repository: `results/` (JSON per detector).

## Files

```
common/mot/trackers.py    the trackers of the comparison (default here: deepsort)
common/mot/core.py        boxes, IoU, assignment, Kalman filters, camera-motion estimation
common/mot/evaluate.py    KITTI-MOTS ground truth and TrackEval metrics
tools/mot/run_tracker.py  run / time / evaluate trackers on saved detections (+ causality check)
tools/mot/*kitti*         data preparation
results/                  evaluation JSON of this repository's tracker(s)
THIRD_PARTY.md            sources and licences
```

## Global Collaboration

Hills Robotics is currently participating in multiple projects in Korea and internationally.

We are actively interested in building relationships with organizations that can complement our technology with global sales networks, distribution channels, system integration capabilities, manufacturing ecosystems, AI infrastructure, robotics technologies, research capabilities, or strategic investment.

Several technology and business collaborations are already underway. Some partners, projects, system architectures, and commercial programs cannot be publicly disclosed because they are subject to confidentiality and business agreements.

We believe that the emerging Physical AI ecosystem cannot be built by a single company.
It requires a global network connecting robotics companies, AI researchers, semiconductor and computing companies, sensor manufacturers, software developers, universities, system integrators, industrial customers, investors, and global distribution partners.

We have now begun our serious exploration of the Physical AI frontier, and we welcome connections with people and organizations who want to build this ecosystem together.

## Research, Contribution, and Donation

The repositories of the Statera Working Group are intended to contribute to the broader technical discussion around Physical AI.

Researchers, engineers, developers, companies, universities, and independent contributors interested in these subjects are welcome to connect with us.

If you would like to collaborate on Physical AI or autonomous robotics, participate in research or technology development, discuss international business cooperation, propose technology or platform integration, contribute technical knowledge, or support this GitHub knowledge initiative through sponsorship or donation, please contact us.

## Contact

**Richard Minsoo Go**
Head of AI, Hills Robotics
Statera Working Group

Personal / Research Contact:
[gominsoo888@gmail.com](mailto:gominsoo888@gmail.com)

Hills Robotics / Business Contact:
[minsoo.go@hillslogis.com](mailto:minsoo.go@hillslogis.com)

Hills Robotics:
https://hillslogis.com/

For inquiries regarding next-generation outdoor autonomous robotic platforms, Physical AI Spider Grid, Intelligence Cabinet, Edge AI, or On-Premise AI architectures that are not yet publicly presented on the company website, please contact us directly.
