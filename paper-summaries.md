# Acoustic & Vibration-Based Tactile Sensing — Literature Summary

Summaries of 26 references on tactile sensing for robots, with emphasis on
vibro-acoustic (contact-microphone / piezo) approaches. PDFs are in [papers/](papers/).

Every entry below is drawn from the downloaded PDF. Where a field does not apply
(e.g. a review with no model or no robot) it is marked **n/a**. Three references
could not be obtained automatically — see [Missing PDFs](#missing-pdfs).

---

## 1. Master comparison table

| # | Short name | Sensing technology | Model / algorithm | Robot platform | Headline result |
|---|---|---|---|---|---|
| 1 | Biomimetic Fingerprint | 3 contact mics (Harley Benton CM-1000) + 3D-printed beam-array "fingerprint" | None (analytic Euler–Bernoulli beam design + FFT/AUC analysis) | Seed Robotics RH8D hand | >11× spectral AUC vs. stock skin on rigid objects; 52-object public dataset |
| 2 | GTSP Survey | n/a (operations research) | n/a — survey of GTSP algorithms | n/a | **PDF not obtained** |
| 3 | Active Acoustic Sensing | Active: bone-conduction actuator + piezo contact mic on opposing gripper fingers | KNN / SVM(RBF) / MLP on 140-D FFT vector; KNN regressor for position | Franka Emika + Franka Hand | 82.9% object ID (7 objects), 84.3% single→multi-object transfer; 0.9 mm grasp-position RMSE |
| 4 | Active Haptic Perception | Review of tactile arrays, capacitive/FSR sensors | n/a — taxonomy of sensorimotor loops | n/a (surveys iCub, hands) | Proposes closed-loop state/process taxonomy linking EPs to features |
| 5 | AST | n/a (audio classification backbone) | Pure-attention ViT-style Transformer on log-Mel patches, ImageNet/DeiT pretrained | n/a | 0.485 mAP AudioSet, 95.6% ESC-50, 98.1% Speech Commands V2 |
| 6 | AU Dataset | 5 contact mics (CM-1000) + camera + RH8D motor current | n/a — dataset paper | NAO v5 + Seed Robotics RH8D | 63 objects; vision + kinesthetic + 400 kHz vibration; 3D "thimble" fingerprint raised signal up to 470% |
| 7 | SonicSkin | Active: 1 piezo TX + 1 piezo RX, 20–80 kHz chirp (Acoustic Surface Wave) | SVM(RBF) on OSPA-selected frequency bins; 1st-order Fourier curve fit for force | Kinova Jaco Gen2 7-DoF | <2 cm error for 96.4% of touches; 0.59 N force RMSE (static), 1.86 N (moving); 57,019 datapoints |
| 8 | Visuo-Haptic Integration | 4 contact mics (CM-1000) + NAO camera + joint angles/currents | GWR self-organizing networks in 3 fusion topologies; PCA + hyperopt | NAO T14 humanoid | Modality-based fusion best at 86.4% (11 objects) vs. 79.5% monolithic, 81.8% brain-inspired |
| 9 | GelSight | Vision-based optical: camera + illuminated elastomer with printed markers | Photometric-stereo lookup table for shape; VGG-16 CNN regression for force/torque | Baxter gripper (fingertip version) | 30–100 µm spatial resolution on robot fingers; R² > 0.9 for force on unseen shapes |
| 10 | Incipient Slip | Active: PZT motor injects 10–1100 Hz Gaussian noise into BioTac soft structure | Support Vector Regression on FFT spectrum (grid-searched kernel) | UR5 + SynTouch BioTac | Matches 19-electrode pressure array on mean RMSE, beats it on worst-case 10%; 100% stabilization success |
| 11 | MilliSonic | Airborne acoustic: smartphone speaker + 4-mic array, FMCW chirps | Analytic — band-pass filter + instantaneous FMCW phase | n/a (smartphones, Raspberry Pi 3B+) | 0.7 mm median 1D, 2.6 mm median 3D; 4 concurrent devices at 40 fps |
| 12 | EIT Soft Skin | Single-layer gelatin hydrogel skin + 32 perimeter electrodes (EIT) | PCA/F-test channel ranking + feedforward NN and weighted activation maps | Hollow cast hand (robot arm used to apply stimuli) | 863,040 electrode configs; ≥6 stimulus types; 24.7 mm touch localization over 38,000 mm² |
| 13 | Soft Pneumatic Acoustic | Active + passive: MEMS mic + balanced-armature speaker inside air chamber | KNN classifier/regressor; SVC for materials (grid-searched) | PneuFlex actuator on RBO Hand 2, Panda arm | 93% contact-location ACR, 3.7 mm regression RMSE, 98% force, 82% material, 100% inflation; unaffected by 90 dB noise |
| 14 | SonicBoom | 6 piezo contact mics in two rings inside a PVC end-effector tube | ResNet50 (mel-spec) + MLPs (GCC-PHAT, proprioception) fused by self-attention transformer | Franka | 0.43 cm in-distribution → 2.22 cm on novel objects/contacts; 18,000 collision events |
| 15 | SonicSense | 4 piezo contact mics, one per fingertip, 44.1 kHz | 3-layer CNN (material), PCN/PointNet (shape), CNN+PCN fusion (re-ID) | Custom 4-finger hand on Franka Emika Panda | 83 objects; 0.763 F1 material, 0.00876 m Chamfer-L1 shape, 92.5% re-identification |
| 16 | Routledge Handbook | n/a (book on bodily awareness) | n/a | n/a | **PDF not obtained** |
| 17 | TacTip Family | Vision-based optical: internal camera tracks 3D-printed biomimetic pins | Histogram likelihood model + maximum-likelihood classification | ABB IRB120 6-DOF arm | 0.16–0.24 mm localization on cylinder roll = 12–19× super-resolution over pin spacing |
| 18 | Touch & Activate | Active: vibration speaker + piezo mic on rigid objects | SVM on frequency response (per original abstract) | n/a (HCI, not robotics) | **PDF not obtained** — reported 99.6% gesture / 86.3% posture accuracy |
| 19 | MicCheck | Off-the-shelf Bluetooth pin microphone (BOYA mini-14) in 3D-printed gripper insert | Compact 3-block 2D CNN (classification); ACT transformer policy (ResNet-18 backbone) | LeRobot SO-101 (leader–follower teleop) | 92.9% on 10-class material task; pouring success 0.40 (vision) → 0.80 (vision+audio) |
| 20 | VibeAct | 2 piezo mics per fingertip (8 channels, 48 kHz) | CNN + temporal-conv/attention tactile estimator → PPO RL policy on contact/slip representation | xArm7 + LEAP hand, MuJoCo digital clone | Beats proprio+point-cloud baseline on all 5 tasks (e.g. Can Climb 60%→76%); real robot 19/20 vs 11/20 |
| 21 | VibeCheck | Active: identical Adafruit piezo discs as emitter and receiver on parallel gripper | Kernel PCA (cosine) + MLP (400,250,100); imitation-learned policy over classifier outputs | UR5 | 100% object & grasp-position classification; 0.95 contact type; 9/10 peg insertions in-distribution |
| 22 | Visuo-Haptic Overview | Review of visual + tactile transduction technologies | n/a — taxonomy over Baltrušaitis' 5 multimodal-ML challenges | n/a | Argues midst-mapping (intermediate) fusion is both best-performing and most brain-like |
| 23 | AuraSense | Active: 1 piezo TX + 1 piezo RX, 19 kHz CW ("Leaky Surface Wave") | Hilbert analytic signal + CUSUM; 7-layer 1D-CNN + 0.3 s sliding-window detector | Kinova Jaco Gen2 7-DoF | 100% TPR static / 95.3% moving objects, >99% TNR; >2000 trials, 24 objects |
| 24 | Vibro-Sense | 7 contact mics (Harley Benton CM-1000) on hand + forearm | Audio Spectrogram Transformer, patch-embedding widened to 7 channels | Seed Robotics RH8D, poked/drawn on by UR5e | 3.46 mm impulse localization (metal); 2.23 mm trajectory tracking (wood); <12 mm during self-motion |
| 25 | Panotti | 8 low-cost omni mics (~$10 ea.) along the arm, sound-deadener shielded | Analytic: LPF/HPF energy prorating + EMCL manifold multilateration (no learning) | Kinova Jaco (7-DOF) | ~100% TPR, ~0% FPR; 3.56 cm mean localization error (3.82 cm while moving) |
| 26 | Vibration Collision ID | 1 uniaxial + 1 triaxial industrial accelerometer (3.2 kHz) | Three BP neural networks (detect / localize / direction) on vibration modal features | STR6-05 6-DOF industrial arm | 0.95 detection accuracy; 0.87–0.94 link localization; 0.83–1.00 direction ID |

---

## 2. Detailed entries

### Group A — Active acoustic sensing (emit a probe signal, read the response)

#### [3] Lu & Culbertson, *Active Acoustic Sensing for Robot Manipulation* (IROS 2023)
- **Sensing technology.** A Dayton Audio BCE-1 bone-conduction actuator on one Franka Hand
  finger emits into the grasped object; an Adafruit piezo contact microphone on the opposing
  finger records it. Both route through a Sound Blaster Play! 3 sound card at 44.1 kHz.
  Sorbothane isolation pads decouple the sensors from gripper-borne vibration. Total cost ≈ $15.
- **Excitation.** Impulse (0.01 s), linear sweep and exponential sweep (20 Hz–10 kHz, 0.5 s),
  looped every 0.5 s.
- **Preprocessing.** 0.5 s windows → FFT → magnitude spectrum restricted to 3–10 kHz in 50 Hz
  steps, giving a **140-dimensional feature vector**. The 3 kHz floor deliberately excludes
  actuator-to-mic leakage through the gripper body and motor noise. Only the first second of each
  5 s recording is used.
- **Model.** Off-the-shelf scikit-learn: KNN (k=3, Euclidean), SVM (RBF), MLP (lr 1e-3, 1000
  iterations). KNN regressor (k=3) for grasp-position estimation, 3-fold CV.
- **Robot.** Franka Emika arm + Franka Hand, 40 N constant grasp force, Intel RealSense D435
  for coarse pose. Also a PyBullet + linear-modal-analysis **simulator** with viscous contact
  damping (Rayleigh α, β plus contact term γ).
- **Results.** 7 objects (2 shapes × 5 materials). Single-object scene: 80.0% (linear sweep, MLP),
  82.9% (exponential sweep, MLP), 5-fold stratified CV. Train-single → test-multi-object-with-contacts:
  84.3% (exponential sweep, MLP) vs. barely 50% for impulse. Grasp position over 13 points
  spaced 5 mm: best RMSE 0.9 mm (wood bar, linear sweep).
- **Caveats the authors state.** Modal simulation fails for thin shells, soft bodies, and the
  aluminium tube (near-singular eigenvalues); α/β/γ are hand-tuned.

#### [21] Zhang et al., *VibeCheck* (IROS 2025)
- **Sensing technology.** Two **identical** Adafruit piezo discs (ID 1740, 8 kHz resonance,
  0.2 mm × 6 mm radius with housing removed), one driven as speaker and one read as contact
  microphone — a deliberate simplification of [3]. Formlabs Clear V4 housings, sorbothane
  isolation pads, HDPE non-slip fingertip strips. Two Teensy 4.0 + audio adapter boards,
  inverting amp (gain 1.5), signal centred at 2.5 V ± 2.4 V, received unamplified at 44.1 kHz,
  micro-ROS to host.
- **Excitation.** 1 s linear sweep, 20 Hz–20 kHz (truncated in practice to 42,000 samples ≈ 19.029 kHz).
- **Preprocessing.** FFT → **kernel PCA with a cosine kernel**. Notably, 5–10 principal components
  (~90% explained variance) generalize best; more PCs overfit. Contact-type classification is the
  exception, needing 500 PCs.
- **Model.** MLP (400, 250, 100) per task. For manipulation: the classifier's **test-set confusion
  matrix** is used as an observation model in a discrete simulator (112 poses, 2 actions), and an
  imitation-learning policy is trained on 10-step observation histories via negative log-likelihood
  of the expert action.
- **Robot.** UR5 with the custom parallel gripper.
- **Results.** Object type (9 rods): 1.00 in-distribution, 1.00 on new surfaces and new orientations.
  Grasp position (3 classes): 1.00 / 0.99 / 0.90. Pose from internal structure: 20.0° RMSE over
  18 poses. Contact type (3 classes): 0.95 in-distribution, 0.73 interpolated. Peg insertion on
  the real UR5: 6/10 from the fixed training start pose, **9/10 from interpolated random starts**,
  6/10 from out-of-distribution starts; 95% in simulation. Contact-type model holds 87% with
  75 dB music playing.
- **Stated limits.** Models are object-set specific; response drifts with motor heating and minor
  hardware changes.

#### [7] Fan et al., *SonicSkin* — Low-Cost Full Surface Tactile Skin (RA-L 2022)
- **Sensing technology.** A **single pair** of CUI CPT-2065-L100 piezo elements (<$2 total),
  hot-glued 20 cm apart on one link and covered with sound deadener. RME Fireface UFX+ at
  192 kHz / 24-bit; Intel NUC7i7BNH for processing. The principle is the Acoustic Surface Wave:
  contact anywhere on the link changes damping/modes/impedance of the whole surface.
- **Excitation.** Chirp Spread Spectrum, 20–80 kHz, period T = 106.7 ms (which sets the response-time floor).
- **Preprocessing — three named algorithms.**
  1. Feature is the **chirp channel-response difference ΔH(f)**, which is far more force-invariant
     than raw amplitude or phase.
  2. **OSPA (Optimal Spectrum Prorating Algorithm):** matched-filter out <20 kHz mechanical noise
     and the 30/60/90 kHz motor-PWM harmonics, then rank frequency bins by
     VC(f) = MV(f)/TV(f) — moving-variance over touch-variance — and keep the γ = 300 lowest.
     Selected bins land mostly in **40–70 kHz**, not the piezo's most efficient 20–30 kHz band.
  3. **Online feature updating:** the robot warms 5.4 °C over 5 hours and localization collapses
     after ~30 min without correction. Every α = 20 min the system records β = 3 s of untouched
     chirps, averages the classifier score vector into S_c, and predicts on S − S_c.
- **Model.** SVM with RBF kernel, **one-shot training** (each location touched once). Force is a
  first-order Fourier fit P(t) = a·cos(ωE) + b·sin(ωE) + c on the OSPA-selected band energy,
  calibrated per location (R² rises from 0.46 to 0.92 when using selected bins).
- **Robot.** Kinova Jaco Gen2 7-DoF, 31 touch locations spaced **1.2 cm** apart around one linkage.
  SingleTact miniature force sensor supplies force ground truth.
- **Results.** 57,019 evaluation datapoints, 12 human subjects, three months. Stationary: 99.4%
  classification. Moving: 96.2% over 31 classes, 97.0% within 3 cm. Multi-person: 97.2%, 98.5%
  within 3 cm. Force RMSE 0.59 N stationary, 1.86 N moving, >96.7% cross-correlation with ground
  truth. Also validated on 15 other materials (100% classification, <0.5 N force error) — though
  each new surface needs its own OSPA calibration and retrained classifier.

#### [23] Fan et al., *AuraSense* (IROS 2021)
- **Sensing technology.** Same hardware family as SonicSkin (two CPT-2065-L100 piezos 20 cm apart,
  glued + sound deadener) but exploiting the **Leaky Surface Wave**: a small fraction of surface
  acoustic energy couples into the air, forming an "aura" that an approaching object perturbs via
  a standing wave. Zoom F8n field recorder at 96 kHz, SMSL M100 DAC, Cavalli Liquid Carbon X amp.
- **Excitation.** Continuous 19 kHz sinusoid — chosen because the motor noise sits below 15 kHz
  with an electrical spike at 30 kHz, and 18–19 kHz is the on-robot frequency-response sweet spot.
- **Preprocessing.** 19 kHz narrow band-pass → **Hilbert transform to the analytic signal** (every
  L = 300 samples) → CUSUM change detection. Wavelet scalograms reveal the proximity signature
  even when robot self-motion masks it in the analytic signal.
- **Model.** 7-layer fully-convolutional **1D-CNN**, kernel length 7, 256 hidden channels, stride 2,
  ReLU, batch norm, Adam at lr 1e-5, batch 32 (16 pos / 16 neg). Input = 960 samples (0.01 s at
  96 kHz), normalized over 0.3 s. Predictions are averaged over N = 30 windows (0.3 s sliding
  detector, 0.1 s hop) and thresholded at 0.717 (ROC inflection). Inference ≈ 2.5 ms on a 3090.
- **Robot.** Kinova Jaco Gen2 7-DoF (carbon-fibre surface).
- **Results.** >2000 on-robot trials with 24 objects over two days. Stationary arm: an SVM(RBF)
  suffices — 100% TPR/TNR. Moving arm, static object: SVM generalizes across days at only 75.8%,
  while the 1D-CNN reaches 96.7% window accuracy. Moving arm, moving object: 83.9% raw window
  accuracy, but the sliding-window detector lifts this to **95.3% TPR (moving) / 100% (static)
  with 99.1% TNR**; per-object TPR >91% for all 24 objects. Max detection range 18.3 cm
  (perpendicular) down to 10.9 cm (opposite side); fails entirely on thin foil, a stick, and a
  wooden plate. With 150 ms system response time this gives a 122 cm/s approach-speed ceiling.

#### [13] Wall, Zöller & Brock, *Passive and Active Acoustic Sensing for Soft Pneumatic Actuators* (IJRR 2023)
- **Sensing technology.** An Adafruit SPW2430 MEMS condenser microphone (100 Hz–10 kHz linear)
  and a Knowles RAB-32063-000 balanced-armature speaker embedded at **opposite ends of the air
  chamber** of a PneuFlex silicone continuum actuator, cast in during fabrication. MAYA44 USB+
  interface at 48 kHz / 32-bit.
- **Framing.** The "computational sensor" idea: one microphone + one speaker emulate contact,
  force, inflation, material and temperature sensors purely by swapping the trained model.
- **Preprocessing.** Trim to fixed length → DFT → **real-valued amplitude spectrum only**,
  1 Hz to 24 kHz (phase discarded). No downsampling was needed.
- **Model.** Deliberately simple: KNN (n = 5, Euclidean) classifier/regressor as a *lower bound*;
  SVC (linear, C = 100) for the harder material task. A grid search over KNN / SVC / random forest /
  MLP shows SVC best for materials (82% vs. KNN's near-chance).
- **Robot.** Actuator mounted as index finger of the RBO Hand 2; automated data collection on a
  7-DoF Panda arm (manual handle setup for the rest).
- **Results.** Contact location (6 classes): **93%** active, 52% dynamic-tap, 47% purely passive
  (chance = 17%). Contact-location regression over 30 points 3 mm apart: **3.7 mm RMSE** active vs.
  18.0 mm passive. Contact force (3 classes): 98%. Object material (3): 82%. Temperature: 4.5 °C
  RMSE active, 10.9 °C passive. Simultaneous location/force/inflation from one recording:
  95% / 97% / 100%.
- **Robustness findings that matter for design.** Background noise up to 90 dB has essentially no
  effect (the silicone hull insulates; SNR stays 43–47 dB). Four neighbouring actuators playing the
  same sweep simultaneously only drops accuracy to 96.7%. Sound *type* and *duration* barely matter
  (white noise ≥ 20 ms is enough; 25% volume suffices). **Models trained on one actuator transfer
  to another at only ~35–47% ACR** — the biggest practical limitation. Models also overfit
  pose-specific robot noise (100% same-pose vs. 82% transferred), fixed by training across ≥2 poses.

#### [10] Komeno & Matsubara, *Incipient Slip Detection by Vibration Injection* (RA-L 2024)
- **Sensing technology.** Inverts the usual approach: instead of observing the contact surface, a
  Cedrat APA50XS **PZT motor** injects Gaussian white noise (10–1100 Hz, 0 dB) into the soft
  structure of a SynTouch **BioTac**, and the BioTac's own internal AC-pressure hydrophone
  (P_AC) reads the propagated vibration. The soft body acts as a mechanical amplifier turning
  microscopic incipient slip into macroscopic deformation.
- **Preprocessing.** FFT magnitude spectrum over 10–1100 Hz, sampling window T = 500 ms.
  Ground truth is a **pseudo-stick-ratio** s = 1 − F_T/F_T^slip, linearly interpolated between
  full stick and gross slip (validated optically: R² = 0.97 between the 200 Hz spectral bin and
  tangential force measured through a transparent acrylic plate).
- **Model.** Support Vector Regression, kernel and hyperparameters grid-searched per dataset.
- **Robot.** UR5 arm holding the BioTac; object on a linear rail pulled by a linear actuator through
  a tension spring; OptiTrack Flex13 motion capture for object position. Five 3D-printed object
  materials (nylon, PA11, PLA, Agilus30, G1H) with different friction/elasticity.
- **Results.** Estimation RMSE is statistically indistinguishable from the 19-, 10- and 4-electrode
  pressure-distribution baselines, but **significantly better in the worst-case top-10% RMSE** —
  the baselines blow up above s = 0.7. Stabilization control at target s_d = 0.3: 1.0 success rate,
  1.38 mm object travel, 4.50 kPa normal force, all 450 steps — versus 0.3 success for the plain
  vibrotactile baseline and 0.0 for a single electrode. Results were consistent across all five
  object materials.

#### [18] Ono, Shizuki & Tanaka, *Touch & Activate* (UIST 2013)
The foundational HCI paper for active acoustic sensing: a vibration speaker and piezo microphone
pair attached to an everyday object turn it into a touch sensor. Reported per-user accuracies of
99.6% for five touch gestures on a plastic toy and 86.3% for six hand postures. **PDF not obtained**
(ACM DL paywall; the authors' Tsukuba server is offline and the Wayback copy 404s), so the method
and preprocessing details above are taken from the abstract and from citing papers [3], [13], [21],
not from the primary source.

---

### Group B — Passive vibro-acoustic sensing (listen to contact-generated vibration)

#### [24] Zai El Amri & Navarro-Guerrero, *Vibro-Sense* (arXiv 2601.20555, Jan 2026)
- **Sensing technology.** Seven Harley Benton CM-1000 contact microphones (±500 mV range) on
  a Seed Robotics RH8D hand and forearm, on custom mounts. Purely passive.
- **Two tasks.** (a) *Impulse response localization* — a UR5e with a solenoid and four
  interchangeable cylindrical indenters (soft plastic, hard plastic, wood, metal) pokes the hand
  from Back/Front/Right/Left. (b) *Trajectory tracking* — the UR5e draws Quick Draw sketches on
  the forearm; stroke ordering is solved as a **Generalized TSP** (hence reference [2]) with Google
  OR-Tools.
- **Preprocessing (parameter-swept, not assumed).** Raw capture at 50 kHz → downsample to **20 kHz**
  (content above 20 kHz is below −40 dB and adds nothing) → trim to a 200 ms window (125–325 ms of a
  500 ms recording triggered 200 ms pre-contact) → **STFT with n_fft = 128** → subtract steady-state
  background estimated from the discarded first 100 ms. The frequency × window-size sweep (10 seeds
  per config) gave 4.332 mm mean error at 20 kHz / 128.
- **Model.** **Audio Spectrogram Transformer** [5], with the patch-embedding layer widened to accept
  a 7-channel tensor (7 × T × F) so inter-microphone amplitude/phase differences are learned at
  tokenization. 12 transformer blocks, kernel 16, stride 10, batch 128, MSE loss, Adam at 7e-4,
  cosine schedule with 1% linear warmup.
- **Datasets.** ~65,000 impulse samples; 160,000 trajectory strokes (hand idle) + 80,000 (hand
  moving to random poses).
- **Results (leave-one-material-out, 10 seeds).** Impulse localization: **metal 3.46 mm** <
  soft plastic 4.94 < hard plastic 5.39 < wood 5.82 mm. Trajectory tracking **reverses the ranking**:
  wood 2.23 mm < hard plastic 2.69 < soft plastic 3.47 < metal 3.70 mm (fixed pose).
  Under random hand motion errors rise to 9.9–12.9 mm but remain usable.
- **The key physical insight.** Impulse localization is driven by *impact dynamics*, so stiff metal's
  sharp high-bandwidth transient wins. Trajectory tracking is driven by *friction*, so wood's surface
  roughness generates the richer continuous spectro-temporal texture. Any sensor design must pick which.

#### [1] Juiña Quilachamín & Navarro-Guerrero, *A Biomimetic Fingerprint for Robotic Tactile Sensing* (ISR Europe 2023)
- **Sensing technology.** Three Harley Benton CM-1000 contact microphones (two on the palm sides,
  one inside the palm) plus 3D-printed **fingerprint patterns** — arrays of solid square beams —
  covering the inner hand. Microphone characterized in-house (no public datasheet): noise floor
  −70 dB, useful bands [3.2, 26] kHz peaking at 9 kHz and [110, 280] kHz peaking at 150 kHz.
- **Design method (no ML).** Beam geometry is derived analytically from the Euler–Bernoulli free-vibration
  equation, ω₀ = (β₁l)²/2π · √(EI/ρAl⁴) with β₁l = 1.875104, to place the natural frequency inside the
  microphone's sensitive band. Square cross-sections give the lowest natural frequency (vs. hexagon,
  circle) without lengthening the beam. Final beams: 1.0 mm side × 2.6 mm length for PLA/ST 45B resin;
  3.2–4.0 mm side × 1.6–2.0 mm for TPU. Validated against 10 printed samples per size.
- **Preprocessing.** Recording at 500 kHz; frequency response averaged over 10 lateral-motion
  repetitions; quantified as **area under the spectral curve**, normalized per-microphone against the
  stock hand as baseline.
- **Robot.** Seed Robotics RH8D adult-size hand; index finger slid over objects at force setting 400
  (12-bit), object holder 20 cm from palm centre.
- **Results.** On a rigid wooden stick the optimized fingerprints give **>11× the baseline AUC**, with
  hard materials (ST 45B resin, PLA) beating flexible TPU. On a deformable sponge the gain vanishes —
  TPU is marginally better there. No single material won across all objects. Measured frequencies came
  out **lower than the single-beam theory predicts**, which the authors attribute to hand kinematics
  and multi-beam coupling.
- **Output.** A public dataset of 52 objects, 5 observations each, across four Lederman–Klatzky
  exploratory procedures (lateral motion, enclosure, pressure, unsupported holding), with vibration,
  motor position and current. DOI 10.6084/m9.figshare.21120982.

#### [14] Lee et al., *SonicBoom* (RA-L 2025)
- **Sensing technology.** Six piezo contact microphones in **two rings of three** at either end of a
  4″ × 12″ PVC pipe that replaces the robot's end-effector link. PVC was chosen over aluminium
  *because* its higher damping makes inter-microphone signals more distinct. 8-channel Behringer
  UMC1820 DAQ at 44.1 kHz.
- **Problem setup.** Predict contact point p(z, θ) in cylindrical coordinates (θ ∈ [−π, π],
  z ∈ [−10, +10] cm) from acoustics A and trajectory X. Restricted to impulsive, single-point contacts.
- **Preprocessing.** All six channels into one WAV for temporal alignment → **spectral gating** against
  a pre-recorded robot-motion-without-collision reference → trim to 1 s centred on the peak →
  mel spectrogram (STFT n_fft = 512, hop 128, **50 mel bins**) → **per-channel independent
  normalization** so inter-microphone relative differences survive. Augmentation: time/frequency
  masking and translation randomization (ablation shows background subtraction and time shifting
  help most; time-frequency masking barely matters).
- **Three input modalities.** (i) mel spectrograms; (ii) **GCC-PHAT** over all 15 microphone pairs,
  kept as the full correlation vector rather than the argmax lag (which was noisier); (iii) 1 s of
  end-effector pose and velocity.
- **Model.** ResNet50 spectrogram encoder (**empirically beat AST** [5] here — impulse signals favour
  local patterns over long-range dependencies), 3-layer MLPs for GCC-PHAT and proprioception, fused
  by a multi-sensory self-attention transformer encoder. Audio gets 2× the embedding dimension and
  lower dropout. MSE loss with θ decomposed into (sin θ, cos θ) to avoid wrap-around. 200 epochs,
  Adam, batch 64, lr 1e-3, ~4 h on an RTX 3090.
- **Data.** 18,000 collision events / 108,000 audio files over ~100 robot hours, striking rigidly
  mounted wooden rods. Ground truth from replaying joint states into a robot mesh against a FARO
  laser scan of the object, averaging near-zero-intersection points and projecting to the surface.
- **Robot.** Franka, in a mock tree canopy (agricultural motivation: pruning/apple picking under occlusion).
- **Results.** Mean Euclidean distance rises with difficulty: **0.43 cm** (validation) → 1.01 cm (novel
  rod geometries) → 2.01 cm (robot-active haptic mapping through leaves) → **2.22 cm** (zero-shot:
  stationary robot, human strikes, no useful proprioception). Chamfer distance 2.0 cm for the haptic map.
  Novel materials: wood 2.8, aluminium 3.4, PVC 4.4 cm.
- **Ablation worth noting.** Audio + proprioception is best in-distribution but **worst on test set 4**
  — the model overfits proprioception. **Phase (GCC-PHAT) is what carries generalization.**
  Proprioception alone predicts contact *angle* well (11.7°) but height poorly (4.3 cm).

#### [15] Liu & Chen, *SonicSense* (CoRL 2024)
- **Sensing technology.** A 3D-printed (PLA) four-finger hand, one DoF per finger, LX-224 servos
  (20 kg·cm, with position and voltage feedback). Each fingertip embeds a piezo contact microphone
  inside the shell with a **40 g counterweight** on the outside to raise tapping momentum — the
  authors found the counterweight essential for strong striking vibrations. 44.1 kHz, synchronized.
  Total cost **$215.26**.
- **Why contact mics.** Measured directly: as ambient Gaussian noise was raised, an external air
  microphone's amplitude climbed by thousands of units while the fingertip reading moved by a few.
- **Exploration policy.** Heuristic, not learned, but autonomous: top-down and side probes to find
  first contact, then a third-finger edge search to estimate height and radius, then grid-sampled
  tapping on top/left/back. Contact events are detected from **motor voltage feedback** (a 10 Ω
  series resistor) rather than acoustics, because the audio also contains motor noise.
- **Preprocessing.** From each 5 s recording, a 1000-sample sliding window finds the local amplitude
  peak; 20,000 samples (453.5 ms) are extracted around it → mel spectrogram 64 × 64, n_fft = 2048,
  64 mel bands, f_max 8192 Hz. For soft objects (foam) the extracted signal is mostly motor noise —
  treated as a feature of the material rather than a failure.
- **Models.** (a) Material: 3 conv + 2 MLP layers on one spectrogram, cross-entropy, plus an
  **iterative spatial refinement** step (filter low-occurrence labels, K-NN majority vote, repeat N times).
  (b) Shape: PCN-style — two stacked PointNet layers → 1024-D global feature → FC decoder → 2024-point
  cloud, Chamfer-distance loss, no folding decoder. (c) Re-identification: 15-channel spectrogram CNN
  + PCN contact-point encoder, fused by MLPs. All on one RTX 3090.
- **Dataset.** 83 real objects, 9 material categories, 22.9% multi-material, with 3D scans and
  per-point material annotations. Splits are **by object**, not by contact — an explicit fix for
  prior work that trained and tested on the same objects.
- **Results.** Material F1 0.523 → **0.763** after refinement (random 0.115, nearest-neighbour 0.371).
  Shape reconstruction Chamfer-L1 **0.00876 m** (NN baseline 0.01347, random 0.03653), aided by
  PyBullet synthetic pretraining with a blending schedule from 100% synthetic to 100% real.
  Re-identification over 82 objects: **92.52%** (audio only 84.11%, contact points only 48.89%,
  NN baseline 43.45%).
- **Negative result worth recording.** Pretraining on existing audio-material datasets (ObjectFolder
  etc.) **hurt** performance — those were recorded with air microphones under noise control, and the
  domain gap is large.

#### [25] Fan et al., *Panotti* — Acoustic Collision Detection and Localization (IROS 2020)
- **Sensing technology.** Eight Sujeetec miniature omnidirectional microphones (~$10 each) spaced
  evenly along a 1 m Kinova Jaco arm, each sealed in Noico 80 mil butyl/foil sound deadener
  (−20 dB on airborne sound). Zoom F8n recorder, 48 kHz, 24 V phantom power.
- **Why classical methods fail (stated and demonstrated).** Collision waves in robot plates are
  dispersive Lamb waves, so different frequencies travel at different speeds and each microphone
  receives a *different* waveform — correlation-based TDoA is unusable. Structural heterogeneity
  means a farther microphone can receive the impulse first. And microphone positions move as the
  arm moves, so triangulation is out.
- **Preprocessing / algorithm — no machine learning at all.**
  - *Detection:* an on-robot collision must pass **both** a low-pass filter (F_LC = 200 Hz; on-robot
    micro-vibrations put much more energy into infrasound than airborne sounds) **and** a high-pass
    filter (F_HC = 10 kHz; table/floor-borne sounds lose high frequencies to absorption). Both cut-offs
    were swept empirically against 311 over-the-air and 276 on-table/floor sound sources.
  - *Localization — EMCL (Epicenter Multilateration for Collision Localization):* onset times give a
    relative onset-time vector ROT = T − min(T), which lies on a **one-dimensional manifold** in the
    8-microphone space. Calibrate by striking 21 markers 5 cm apart; clean the manifold using fixed
    inter-microphone onset differences ΔT. At test time only the **strongest** microphone's onset is
    detected; virtual onsets for the rest are generated by shifting the manifold, scored by the
    **standard deviation within a 10-sample window** (the best of five scoring functions tested),
    and the peak of a quadratic fit gives the location.
  - *Motor noise:* a band-stop filter at the arm's fundamental (100 Hz for Jaco, 80 Hz for Gen3).
- **Results.** 527 on-robot collisions, 359 over-the-air and 224 on-table/floor sources in the field
  study: TPR and TNR both near 100%, FPR/FNR near 0; 96% TNR even for sounds within 0.3 m of the arm.
  Localization: **3.56 cm** mean (screwdriver), 3.82 cm with the arm moving, 95% of errors under
  ~11 cm across 16 different collision objects including a human.

#### [26] Min, Wang & Liu, *Collision Detection and Identification Based on Vibration Analysis* (Sensors 2019)
- **Sensing technology.** One 1A113E uniaxial accelerometer beside joint 2 and one 1A114A triaxial
  accelerometer beside the end-effector (Donghua Testing), NI-9232 DAQ, **3.2 kHz** sampling.
  Model-independent by design — no torque sensors needed.
- **Theory.** Elastodynamic modelling decomposes the transfer function from collision force to
  vibration into m + n modes. Because the stiffness/damping matrices are near-constant, the dominant
  collision natural frequencies (50–1500 Hz) are **independent of the robot's dynamic state**, while
  the active dynamics sit below 50 Hz. This is what lets training data be collected in simple static
  scenarios.
- **Preprocessing.** FFT in a 320-sample sliding window (0.1 s, 50% overlap → 0.05 s cycle) →
  a 9-step **peak-frequency algorithm** with an adaptive tolerance Δ that extracts exactly m local
  maxima per channel, groups them across channels, and averages to estimate the modal frequencies;
  the magnitudes at those frequencies form the modal matrix Φ̂.
- **Model.** Three back-propagation ANNs (Matlab NN toolbox, Levenberg–Marquardt) in cascade:
  BP1 detect → BP2 localize link → BP3 identify direction (input to BP3 depends on BP2's output).
- **Robot.** STR6-05 6-DOF heavy-load industrial arm, 8 contact points, 5 working patterns,
  800 samples (50% collisions), 85/15 train/test split.
- **Results.** Detection ~0.95 (e.g. 27-5-1: 0.962 collision / 0.949 non-collision). Localization
  into two link groups: best 0.913 / 0.871 with 27-10-5-1. Direction (X/Z/Y): best 0.833 / 0.900 /
  0.667 with 33-10-6-2. Errors concentrate on boundary samples near joint 3; the authors recommend
  a third accelerometer there. ~300 collision samples suffice to train a new arm in under an hour.

#### [19] Oh et al., *MicCheck* (arXiv 2511.18299, Nov 2025)
- **Sensing technology.** An unmodified **consumer Bluetooth pin microphone** (BOYA mini-14, 2.4 GHz),
  press-fit into a redesigned 3D-printed gripper so that its **stock foam pad is the contact surface** —
  providing both compliance for grasping and acoustic coupling. USB-C dongle enumerates as a standard
  audio input; no custom electronics or drivers. 48 kHz / 16-bit, built-in noise cancellation enabled.
- **Preprocessing — two different regimes, deliberately.**
  - *Material classification:* non-overlapping **1 s** windows → log-magnitude mel spectrogram.
    A "blank" no-contact class is included so the softmax can reject low-evidence windows.
  - *Imitation learning:* **0.2 s** frames at 30 Hz (0.04 s hop, **80% overlap**), n_mels = 32,
    with frequencies above 0.3× Nyquist amplified 2× to emphasize sharp impacts. Shorter, overlapping
    windows keep transients temporally aligned with proprioception and vision.
- **Models.** (a) Compact 2D CNN: three Conv–BN–ReLU blocks → global adaptive average pooling →
  linear classifier; 8:2 stratified split, cross-entropy, Adam 3e-4, batch 32, 2000 epochs.
  (b) **ACT (Action Chunking with Transformers)**: chunk size 100, ResNet-18 ImageNet backbone,
  d_model 512, 8 heads, FFN 3200, 4 encoder / 1 decoder layers, CVAE with latent dim 32, dropout 0.1,
  KL weight 10.0, lr 1e-5, 100k steps. Observations = RGB + latest audio spectrogram frame + proprioception.
- **Robot.** LeRobot SO-101, leader–follower teleoperation, 20 demonstrations per task, 50 Hz inference
  (camera-bound).
- **Results.** Material classification **92.9%** on 9 objects + blank across four interaction types
  (tap, knock, slow press, drag); perfect on blank, glass cup, ceramic mug, human skin, steel tumbler;
  confusions concentrate among soft/textured classes (plushie ↔ leather ↔ notebook). Manipulation:
  picking-and-pouring **0.40 (vision only) → 0.80 (vision + audio)** over 10 rollouts; unplugging a
  high-friction connector 1.00; sound-based sorting 0.70/0.60; material sorting 0.70/0.40.
- **Honest framing.** The authors position this as a cost/fidelity trade-off, not a replacement for
  high-resolution tactile sensors, and flag wireless compression artifacts and latency as limitations.

#### [20] Mao, Yoo et al., *VibeAct* (arXiv 2606.27344, Jun 2026)
- **Sensing technology.** **Two piezo microphones embedded in each fingertip** of a LEAP hand
  (8 channels total), synchronized through an audio mixer at 48 kHz. Sensors sit inside the finger
  body, so external contact geometry and surface texture are unchanged.
- **The core idea.** Raw vibro-acoustic signals cannot be simulated faithfully enough for sim-to-real
  RL, so VibeAct inserts an intermediate **physically-grounded representation** that is both estimable
  from real microphones and computable from a contact solver: per finger,
  z = [binary slip, slip magnitude, contact-onset pulse] → 12-D for four fingers. It deliberately
  excludes privileged simulator info (contact location, normals, forces, object identity).
- **Label generation without annotation.** Real teleoperated trajectories (with mocap or rigidly fixed
  object poses) are **replayed in a calibrated MuJoCo digital clone**; the contact solver emits contact
  onset, slip presence (threshold 5 mm/s tangential velocity) and slip magnitude per fingertip.
- **Preprocessing.** 200 ms windows → log-mel spectrograms, n_fft 2048, hop 512, 64 mel bins,
  f_min 500 Hz → shape (B, 1, 19, 64) per microphone. Absolute dB magnitudes with dataset-wide
  normalization (preserves amplitude while compensating mic gain differences). A **learnable
  microphone-gating layer** suppresses noisy channels.
- **Models.** *Tactile estimator:* four **independent per-finger subnetworks** — 3 Conv2d blocks with
  frequency-only pooling (preserving temporal resolution for transients) → temporal Conv1d + attention
  pooling → cross-microphone fusion → three heads (onset, slip presence, slip magnitude, the last
  conditioned on amplitude statistics). Class-weighted BCE (w₊ = 30 for sparse onsets, 0.5 for slip)
  plus masked Huber loss (δ = 5 mm/s). AdamW, cosine decay, pretrain 100 epochs on fixed-object data
  at 3e-4 then fine-tune 100 epochs on moving-object data at 3e-5.
  *Policy:* PPO in MuJoCo, PointNet branch for point clouds + MLPs for proprioception and tactile,
  symmetric actor/critic; 24 parallel envs, 5e6 steps, γ 0.99, GAE λ 0.95, clip 0.2, ~66.7 Hz control.
- **Robot.** xArm7 + LEAP hand; 5 tasks (Box Climb, Can Climb, Peg in Hole, Cube Rotation, Nut Rotation).
- **Results.** Estimator: contact-onset F1 0.597, slip-presence F1 0.913, slip-magnitude MAE
  4.74 mm/s. Ablations confirm sequential (pretrain→fine-tune) training and independent per-finger
  encoders/heads each help. Policies: full VibeAct wins on all five tasks — Cube Rotation +51 pts,
  Peg in Hole +24, Can Climb 60→76%, Nut Rotation 28.5→44%, Box Climb 46.7→50%.
  **Slip magnitude is the load-bearing channel**; contact onset alone sometimes *hurts*.
  Real hardware: Box Climb 4/20→12/20, Can Climb 11/20→19/20, Nut Rotation 1/20→8/20.

---

### Group C — Non-acoustic tactile sensors (baselines and comparison points)

#### [9] Yuan, Dong & Adelson, *GelSight* (Sensors 2017)
- **Sensing technology.** Vision-based optical. A camera images a soft elastomer coated with an
  opaque reflective skin (bronze/aluminium flake for semi-specular, matte for general shape) lit from
  multiple directions; printed markers (~1.1 mm spacing on the 25 × 25 × 2 mm fingertip version)
  track lateral displacement. Elastomer is near neo-Hookean, µ = 0.145 MPa, Shore 00-45.
- **Algorithms.** Shape comes from a **3D lookup table** mapping RGB pixel intensity to surface
  gradient, calibrated by pressing a sphere of known radius; gradients are integrated to depth.
  Force and in-plane torque come from a **VGG-16 CNN** pre-trained on ImageNet, last FC layer replaced
  by 4 outputs (Fx, Fy, Fz, Tz), input = difference image against the no-contact reference, MSE loss.
- **Robot.** The first fingertip version was built for a **Baxter** (Rethink Robotics) gripper.
- **Results.** Spatial resolution 1–2 µm in metrology configurations, **30–100 µm** on compact robot
  fingers. Minimum perceivable force typically <0.05 N (below the ATI Nano-17 reference's own floor).
  Force network: trained on 28,815 images of spheres/cylinders/planes, tested on 6,705 images of three
  *unseen* objects — **R² > 0.9** for forces. The authors are explicit that the CNN does not fully
  generalize force across contact geometry, and that per-sequence bias remains.
- **Demonstrated applications.** USB-plug in-hand localization for insertion, fabric/texture
  discrimination, hardness estimation from deformation sequences, slip and incipient-slip detection.

#### [17] Ward-Cherrier et al., *The TacTip Family* (Soft Robotics 2018)
- **Sensing technology.** Vision-based optical, but biomimetic in a different way from GelSight: an
  internal camera tracks **3D-printed pins** on the underside of a soft skin, analogous to intermediate
  ridges in the human fingertip, which mechanically amplify surface deformation into lateral pin motion.
  Dual-material 3D printing prints the skin and pin tips directly, removing the casting step.
  Four variants: TacTip (127 pins, 2.4 mm spacing, Microsoft LifeCam HD), TacTip-GR2 (44 mm form
  factor, Raspberry Pi spycam + fisheye), TacTip-M2 (3.5 mm spacing, for the M2 gripper), TacCylinder
  (4.3 mm spacing, catadioptric 360° mirror, for capsule endoscopy).
- **Preprocessing.** 640 × 480 frames at ~20 fps → OpenCV filter and threshold → contour detection for
  pin centres → each pin matched to its default position (within a 20 px radius; otherwise the previous
  frame is reused) → x and y deflections treated as independent taxels (N_dims = 254 for the TacTip).
- **Model.** Not a neural network: a **histogram-based measurement model**. For each of 72 location
  classes, sensor values per dimension are binned into 100 equal intervals; log-likelihoods are summed
  over 10 samples × 254 dimensions (normalized by the total count) and the maximum-likelihood location
  is returned. Bin counts are regularized by a small constant.
- **Robot.** ABB IRB120 6-DOF arm, rolling a 25 mm cylinder in 0.1 mm increments over 72 mm
  (720 locations), 10 frames each, with independent train and test sets.
- **Results.** Mean absolute error: TacTip 0.20 mm, TacTip-GR2 0.16 mm, TacTip-M2 0.24 mm,
  TacCylinder 0.22 mm — i.e. **12×, 15×, 15× and 19× super-resolution** relative to pin spacing.
  A useful data point for the acoustic papers: morphology dominates signal character, and sub-taxel
  accuracy comes from the statistical model, not from denser sensing.

#### [12] Hardman, Thuruthel & Iida, *Multimodal Information Structuring with Single-Layer Soft Skins and High-Density EIT* (Science Robotics 2025)
- **Sensing technology.** A **single layer** of piezoresistive gelatin hydrogel — no embedded
  components, no soft–rigid interfaces anywhere on the sensing surface, and thermoreversible so it
  can be cast into complex 3D shapes (demonstrated as a full-size hollow human hand). Electrodes sit
  only at the perimeter/wrist: 8 for the flat test membrane, 32 for the hand.
- **Why the numbers are large.** Choosing all four tetrapolar electrodes independently gives
  32 × 31 × 30 × 29 = **863,040 configurations**; measuring RMS amplitude *and* phase doubles this to
  **1,726,080 information channels**. All channels can be swept at 0.02 Hz; monitoring a selected
  subset scales the frame rate linearly up to 33 kHz.
- **Six stimulus modalities** with distinct conductivity mechanisms: insulated press and damage
  (local conductivity decrease), conductive touch and local melting (increase), single human touch
  (shunting to ground), multi-finger human touch (new current path). An insulated *touch* is the
  null baseline.
- **Preprocessing / "information structuring" — the actual contribution.** Rather than reconstructing
  a conductivity map, the paper ranks channels directly from physical measurements by three methods:
  PCA-based "fingerprints" per modality, an environment-correlation ranking, and a **statistical
  F-test** against ground-truth positions. F-test ranking converged fastest; its top 50 configurations
  outperformed 150 configurations of a standard adjacent/opposite sweep.
- **Models.** Feedforward neural networks for regression and environmental prediction; **weighted
  activation maps (WAMs)** for touch localization on the 3D hand.
- **Results.** Circular membrane: <10 mm localization from 1000 robot-placed steel-nut positions.
  3D hand: **24.7 mm** localization over a 38,000 mm² surface using 500 F-test-ranked channels
  (>40 mm with 500 unranked channels); below 40 mm with only 10 channels, enabling 3.3 kHz frame
  rates. Environmental temperature (19–25 °C) and humidity (38–72%) predicted from 50 ranked signals
  over 100 hours, with touch localization (26.3 mm) running concurrently. Response vectors transfer
  across modalities by sign: a model trained only on conductive touch predicts insulated-press
  locations because presses produce vectors in the opposite direction.

---

### Group D — Enabling techniques and background

#### [5] Gong, Chung & Glass, *AST: Audio Spectrogram Transformer* (Interspeech 2021)
The backbone that [24] adopts and [14] rejects. Input audio → 128-dim log-Mel filterbank (25 ms
Hamming window, 10 ms hop) → 128 × 100t spectrogram → split into 16 × 16 patches with **overlap 6**
in both axes → linear projection to 768-D + learnable positional embedding + [CLS] token →
standard 12-layer, 12-head Transformer encoder, no convolutions. The key trick is **cross-modality
transfer from ImageNet**: ViT/DeiT weights are reused by averaging the 3 input-channel weights into
one, and the positional embedding is **cut in one dimension and bilinearly interpolated in the other**
(e.g. 24 × 24 → 12 × 100). Results: 0.485 mAP AudioSet (ensemble), 0.459 single model;
95.6% ESC-50; 98.1% Speech Commands V2. Ablations: ImageNet pretraining lifts balanced-AudioSet mAP
from 0.148 to 0.347; more patch overlap monotonically helps; the same architecture handles 1 s to
10 s inputs unchanged. No robot involved.

#### [11] Wang & Gollakota, *MilliSonic* (CHI 2019)
Airborne (not contact) acoustic tracking, included as the accuracy ceiling for acoustic
localization. A smartphone speaker emits FMCW chirps; a 4-microphone array (15 × 15 cm and
6 × 5.35 cm versions) receives. The contribution is using the **instantaneous FMCW phase** rather
than the peak frequency bin: a dynamic narrow band-pass filter removes distant multipath, and the
residual error becomes sin⁻¹(A₂/A₁), independent of the path separation |f_t2 − f_t1| that limits
conventional FMCW. Real-time on a Raspberry Pi 3B+. Results: **0.7 mm median 1D** error to 1 m
(1.7 mm from 1–2 m), **2.6 mm median 3D** — ~5× better than prior work — and up to four concurrent
smartphones at 40 fps each via intentionally time-shifted chirps. [24] cites it to bound what
acoustic trajectory tracking can achieve, while noting it needs external microphone arrays.

#### [6] Bonner et al., *AU Dataset for Visuo-Haptic Object Recognition* (arXiv 2112.13761)
A dataset paper, and a direct methodological ancestor of [1] and [24]. **63 objects**, each recorded
three times with repositioning, spanning visual and haptic ambiguity (e.g. yellow ball vs. yellow
lemon; a velvet bag filled with salt, coffee beans or Play-Doh). Setup: NAO v5 + Seed Robotics RH8D
+ Olympus OM-D E-M10 III camera + PicoScope 4824. Five Harley Benton CM-1000 contact microphones
(2 on NAO, 3 on RH8D), placement chosen empirically by maximising the absolute average signal
difference between a soft rubber ball and a hard wooden box — two candidate positions were dropped.
Sampling at **400 kHz**, justified explicitly: sound travels ~2750 m/s in plastic and the microphones
are ≥2 cm apart, so ≥275 kHz is needed for time-of-arrival differences. A 3D-printed PLA **thimble**
with 2 mm protuberances on the NAO finger raised the signal by at least 166% (470% on the best
microphone). Modalities: 4 images per object, RH8D finger positions and wrist current, IR proximity,
and vibration for "feel" (lateral motion) and "pressure-poke", each with a matched background-noise
recording. No model is trained.

#### [8] Toprak, Navarro-Guerrero & Wermter, *Evaluating Integration Strategies for Visuo-Haptic Object Recognition* (Cognitive Computation 2018)
- **Sensing technology.** Four Harley Benton CM-1000 contact microphones (two on a custom table with
  a ridged "extra finger" stick, two on the robot's left arm) via an ALESIS iO4 interface, plus NAO's
  lower head camera and arm joint angles/currents. This is the paper that established contact
  microphones as a viable cheap tactile sensor in this line of work.
- **Preprocessing.** *Visual:* background subtraction → 7 Hu moments (shape), concatenated BGR
  histograms (768-D, colour), LBP histogram (26-D, texture). *Kinesthetic:* 12-D joint positions
  (shape), 36-D positions + currents (weight). *Tactile:* 1 s snippets at 44.1 kHz recorded before
  and during each exploratory movement → **spectral subtraction** to remove background → one-sided
  FFT magnitude spectrum, **22,050-D**. Total 44,949 dimensions → per-property PCA (fit on train,
  applied to test) → standardization to zero mean / unit variance.
- **Model.** Grow-When-Required (GWR) self-organizing networks used as classifiers (labels attached
  to best-matching nodes), arranged in three topologies: **monolithic** (concatenate everything),
  **modality-based** (visual stream + haptic stream), and **brain-inspired** (shape stream +
  material stream, matching the brain's organizational principles). Hyperparameters via hyperopt.
- **Robot.** NAO T14 humanoid, 11 objects, 10 observations each under controlled lighting (70:30
  train/test) plus 3 per object under uncontrolled conditions.
- **Results.** Microphone placement matters: channel 0 (closest to the exploration site) was best for
  both texture and hardness. Single properties: colour 88.6%, haptic shape 81.8%, visual texture 79.5%,
  weight 75.0%, haptic texture 68.2%, hardness 52.3%, visual shape 40.9% (chance ≈ 9%).
  **Integration strategies: modality-based 86.4% > brain-inspired 81.8% > monolithic 79.5%.**
  The brain-inspired strategy did *not* win, which the authors attribute to the quality of the
  haptic data rather than the principle.

#### [4] Seminara et al., *Active Haptic Perception in Robots: A Review* (Front. Neurorobot. 2019)
A conceptual review, not an experimental paper. It proposes a closed-loop sensorimotor taxonomy
splitting the problem into **the state** (features and their representation) and **the process**
(actions that change the state), and maps Lederman & Klatzky's exploratory procedures onto haptic
features. It contrasts **task-based** design (behaviour specified per task) with **structure-based**
design, and argues for probabilistic formulations in which each loop step maintains distributions
over features and poses. Reviewed use cases use tactile sensor arrays (8 FSRs; iCub's 12-element
capacitive arrays) — **no acoustic sensing**. Its relevance here is the vocabulary: exploratory
procedures, active vs. passive touch, and the sensor-binding/dimensionality-reduction problem that
whole-body acoustic sensing sidesteps by using few sensors.

#### [22] Navarro-Guerrero et al., *Visuo-Haptic Object Perception for Robots: An Overview* (Autonomous Robots 2023)
The broad survey for this area. Covers the neural basis of human multimodal object perception,
visual and tactile sensor technologies (with a table of transduction mechanisms), data collection
and datasets, then organizes computational work around Baltrušaitis' five multimodal-ML challenges:
**representation, translation, alignment, fusion, co-learning.** The fusion taxonomy is the part the
other papers here use: **pre-mapping** (early — concatenate features; each modality's influence is
set by vector length rather than statistical relevance), **midst-mapping** (intermediate — separate
streams integrated during mapping), and **post-mapping** (late — combine decisions). The authors
argue midst-mapping is both the most common and the best-performing, and the best match to the
brain's hierarchical converging substreams. Directly relevant note: optical tactile data and
**vibration data via spectrograms** can be fused early with vision, whereas kinesthetic data cannot.

#### [2] Pop et al., *A Comprehensive Survey on the Generalized Traveling Salesman Problem* (EJOR 2024)
Not a sensing paper. It appears in this bibliography because **Vibro-Sense [24] formulates its
stroke-ordering problem as a GTSP** to minimize UR5e travel time while drawing Quick Draw sketches,
solving it with Google OR-Tools. **PDF not obtained** — see below.

#### [16] Alsmith & Longo (eds.), *The Routledge Handbook of Bodily Awareness* (Routledge 2022)
An edited academic book on bodily awareness, cited by **Vibro-Sense [24]** for the Hoffmann & Longo
chapter "Body Models in Humans and Robots" — i.e. as background on body representation, not on
sensing hardware. **PDF not obtained** (commercial book).

---

## 3. Cross-cutting observations

**Active vs. passive is the primary design split.** Active systems ([3], [7], [10], [13], [21], [23])
inject a known probe and read its modulation; they get object-global state (material, internal
structure, extrinsic contact, inflation, even temperature) and work without any interaction event,
but need an emitter, are object/actuator-specific, and face cross-talk questions at scale. Passive
systems ([1], [14], [15], [19], [20], [24], [25], [26]) only need microphones and avoid cross-talk
entirely, but require an impact or sliding event to produce signal. [13] measures the gap directly on
identical hardware: 93% active vs. 47% passive on the same contact-location task, and 3.7 mm vs.
18.0 mm on regression.

**Contact microphones' decisive advantage is noise immunity.** [15] shows an air microphone's amplitude
rising by thousands of units under injected noise while a fingertip contact mic moves by a few.
[13] finds no degradation up to 90 dB (the silicone hull insulates). [21] keeps 87% accuracy with
75 dB music playing. The dominant noise is *internal* — motor PWM and mechanical noise — which is
why nearly every paper here spends its preprocessing budget on rejecting it: band-stop at the arm's
fundamental [25], matched-filtering PWM harmonics and variance-ratio bin selection [7], spectral
gating against a motion-only reference [14], spectral subtraction against a pre-recorded background
[8], [24].

**Feature choice clusters into three families.** (i) Plain FFT magnitude spectra with classical ML —
[3], [7], [8], [13], [21]; often with aggressive dimensionality reduction (kernel PCA to 5–10
components in [21], PCA in [8]). (ii) Mel spectrograms into CNNs or transformers — [14], [15], [19],
[20], [24]. (iii) No learning at all, using manifold or modal structure — [25], [26], and the shape
lookup table in [9]. Family (iii) generalizes to novel objects most cleanly; family (ii) scales best
with data.

**Phase carries generalization; magnitude carries identity.** [14]'s ablation is the clearest evidence:
audio + proprioception wins in-distribution but is *worst* on the out-of-distribution test set, while
models including GCC-PHAT phase hold up. [11] makes the same argument analytically for airborne
tracking — FMCW phase error is independent of path separation whereas peak-frequency error is not.
[13] explicitly discards phase and notes it as future work.

**Impact stiffness and surface friction pull in opposite directions.** [24] is the only paper that
isolates this: stiff metal gives the best impulse localization (3.46 mm) but the worst trajectory
tracking (3.70 mm), while textured wood reverses both rankings (5.82 mm / 2.23 mm). [1] finds the
complementary hardware result — rigid resin fingerprints give >11× signal on rigid objects but no
gain at all on a sponge, and no single material won everywhere.

**Calibration transfer is the shared unsolved problem.** [13] measures it directly: sensor models
transfer between nominally identical actuators at only 35–47% ACR (chance = 25%), and overfit
pose-specific robot noise unless trained across ≥2 poses. [7] needs one-shot recalibration plus
classifier retraining for every new surface material, and a 20-minute online update loop just to
survive a 5.4 °C thermal drift. [21] lists motor heating and minor hardware adjustments as sources of
drift. [20] states its estimator is tied to a fixed microphone placement and finger material.
This — not raw accuracy — is what currently blocks deployment.

**The field is moving from classification to closed-loop control.** [3], [8], [13], [15], [26] stop at
perception. [21] closes the loop on peg insertion by treating the classifier's confusion matrix as a
simulator observation model. [19] feeds spectrograms into an ACT policy. [20] goes furthest, defining
an intermediate contact/slip representation that is simultaneously estimable from real microphones and
computable from a contact solver, which is what makes sim-to-real RL possible without simulating audio.

**Sampling rates span three orders of magnitude and are rarely justified.** [26] uses 3.2 kHz,
[25] 48 kHz, [14]/[15]/[21] 44.1 kHz, [20] 48 kHz, [24] 50 kHz downsampled to 20 kHz, [7] 192 kHz,
[1] 500 kHz, [6] 400 kHz. Only three give a reason: [6] derives 400 kHz from the speed of sound in
plastic and 2 cm microphone spacing for time-of-arrival; [24] sweeps frequency × window size
empirically and finds nothing useful above 20 kHz; [26] derives 3.2 kHz from a measured 50–1500 Hz
collision band. If you are choosing a rate, [24]'s sweep is the most directly transferable evidence.

---

## Missing PDFs

Three references could not be downloaded automatically. All three are peripheral to the
vibro-acoustic core — [2] and [16] are cited by Vibro-Sense [24] for its stroke-ordering solver and
for body-representation background respectively, and [18] is the 2013 HCI origin of active acoustic
sensing.

| # | Reference | Why it failed | How to get it |
|---|---|---|---|
| 2 | Pop et al., GTSP survey, EJOR 314(3):819–835, 2024 | **Gold open access (CC-BY)** but Elsevier returns HTTP 403 to non-browser clients | Open <https://doi.org/10.1016/j.ejor.2023.07.022> in a browser and click "Download PDF" — no subscription needed |
| 16 | Alsmith & Longo, *The Routledge Handbook of Bodily Awareness*, 2022 | Commercial book, not open access | Library access or purchase via <https://doi.org/10.4324/9780429321542>. The chapter [24] actually cites is Hoffmann & Longo, "Body Models in Humans and Robots" |
| 18 | Ono, Shizuki & Tanaka, "Touch & Activate", UIST '13, pp. 31–40 | ACM DL paywall; no OA copy indexed; the authors' Tsukuba server is offline and the Wayback snapshot is a 404 | Institutional ACM DL access at <https://doi.org/10.1145/2501988.2501989>, or request from the authors |

**Obtained: 23 of 26.** Every other PDF is in [papers/](papers/), named `NN_short-name.pdf` where
`NN` is the reference number in this document.

Sources for the located PDFs: [arXiv](https://arxiv.org), [Unpaywall](https://unpaywall.org),
[Semantic Scholar](https://www.semanticscholar.org),
[Europe PMC / PMC](https://pmc.ncbi.nlm.nih.gov),
[Xiaoran Fan's publication page](https://ox5bc.github.io/) (for [7] SonicSkin and [25] Panotti),
[University of Hamburg WTM repository](https://www2.informatik.uni-hamburg.de/wtm/) (for [8]),
[Aberdeen AURA](https://aura.abdn.ac.uk) (for [17] TacTip), and the
[Cambridge repository](https://www.repository.cam.ac.uk) (for [12] EIT skin).
