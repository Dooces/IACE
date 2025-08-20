Resource-Priced Predictive Control: A Unified Framework

Abstract
We formalize cognition as resource-rational predictive control: an agent with a hierarchical generative model chooses how much computation to do and which actions to take by trading expected benefit against energetic and computational cost. Behavior defaults to model-free (habitual) control; model-based (generative) control is gradedly engaged when (i) precision-weighted residual prediction error remains after fast local updates and (ii) physiological surplus permits expensive planning. Internally generated simulations (hippocampus–prefrontal) are allowed to influence behavior only when their marginal benefit per unit energy exceeds a state-dependent access threshold shaped by neuromodulators (NE, ACh, DA, 5-HT). Memory change follows use-weighted Hebbian plasticity during wake and synaptic down-selection during sleep. We build on established action-first architectures (affordance competition/urgency: Cisek/Kalaska) and BG‑gated prefrontal control (PBWM: O’Reilly/Frank), adding a physiological price signal (S) and a benefit‑per‑energy access rule. The framework yields concise equations, implementation-level circuit mapping (ACC/BG gating; HPC↔PFC simulation; fronto‑parietal broadcast), and preregisterable predictions (energy‑ordered failure; ACh×SNR and NE×volatility interactions; controller‑specific sleep effects).

Foundations of Adaptive Control
1.1 Evolutionary and physical constraints (no teleology)
Cognitive mechanisms persist insofar as they improve inclusive fitness under ecological and energetic constraints. The brain is metabolically costly, so neural computation must trade expected benefit against limited energy and time. We treat cognition as resource‑rational control: selecting computations and actions that maximize task performance per unit cost.

1.2 Predictive processing and active inference
The nervous system can be modeled as a hierarchical generative model. Higher areas send predictions; lower areas return precision‑weighted prediction errors (PEs). Perception reduces current PEs; learning updates parameters to reduce future PEs. Action is chosen to minimize expected free energy (EFE) of policies, combining pragmatic value (approach preferred states) and epistemic value (reduce uncertainty).

1.3 Resource rationality: pricing computation
Control is bounded and priced. Introduce a latent metabolic surplus S ∈ [0, 1] (inferred from proxies such as glucose, SpO₂, frontal CBF/fNIRS, baseline pupil; seconds–minutes timescale) that reduces the effective price of computation. Let m ∈ {MF, MB} denote model‑free (habit) versus model‑based (generative) control and π a policy. Choose m, π to minimize:
J(m, π) = EFE(π | m) + λ(m)·Ccomp(π | m) + μ(S)·Cmet(π | m), with μ′(S) < 0.
Higher S lowers the energy price μ(S). Define εres as the residual, precision‑weighted PE that remains after fast local predictive‑coding updates and habitual corrections—i.e., what the current cached policy cannot cheaply fix.

1.4 Two operational laws
A) Graded engagement (MB gate)
gMB = σ(α·εres + β·S − θ), with σ logistic and θ a context‑dependent threshold tuned by neuromodulators and task context. gMB ∈ [0, 1] is the degree of MB recruitment.

B) Priced access (promotion of internal simulation)
Let Benefit ≡ −ΔEFE (expected free‑energy reduction). Promote internally generated (hippocampus–PFC) simulations to influence behavior only if:
ΔBenefit/ΔEnergy > θ(S, sensory SNR, volatility).
Planning budget scales with need and capacity:
Bplan = Bmax · gMB · S.
Scheduler: iteratively expand the branch (depth or breadth) with maximal marginal ΔBenefit/ΔEnergy until the threshold is reached or the budget is exhausted.

Retention (wake + sleep)
Δw ∝ Hebbian co‑activity × (recruitment into control × precision‑weighted surprise × salience/valence) − β↓, with βsleep > βwake.
Used, high‑precision, behavior‑relevant traces potentiate; global sleep down‑selection (synaptic homeostasis) renormalizes and prunes unused hypotheses. Net: validated routines migrate toward model‑free circuits; speculative routines are trimmed unless repeatedly useful.

Metacontrol: Arbitrating Habitual vs Generative Control
2.1 Defaults and substrates

Model‑free (habitual): cached state–action values; fast/cheap; cortico–dorsolateral striatal loops (cerebellum for skills).
Model‑based (generative): counterfactual rollouts via hippocampus ↔ prefrontal circuits; flexible but costly.
Behavior defaults to MF; MB is recruited when needed and affordable.
2.2 Triggers: residual error and surplus

Informational trigger: εres (residual precision‑weighted PE) signals model misfit after local/MF correction.
Capacity gate: surplus S indexes energetic headroom. Low S biases toward MF even when εres is high; high S permits deeper MB search.
Measurement notes: estimate S as a time‑stamped latent scalar from proxies with known time constants—glucose/SpO₂ (slow), frontal CBF/fNIRS (10–60 s), baseline pupil (arousal/resource mobilization; interpret with care), EEG alpha attenuation (seconds); report confidence intervals.
2.3 Arbiter circuit and broadcast
ACC estimates expected value of control from εres, S, and context; basal ganglia implement Go/NoGo gating of PFC working‑memory states (PBWM‑style). When gated, PFC maintains task‑relevant representations and coordinates hippocampal rollouts. Internal content reaches global broadcast via fronto‑parietal/thalamo‑cortical loops only if the access law is satisfied. Operationalize “broadcast” with a panel: P3b amplitude/latency, long‑range phase‑locking, and TMS‑EEG effective connectivity (avoid P3 alone).

2.4 Graded engagement with neuromodulatory tuning
gMB = σ(α·εres + β·S − θ), with context‑dependent θ.

LC–noradrenaline (NE): signals volatility/unexpected uncertainty; lowers θ (easier MB engagement) under uncertainty; inverted‑U effects on planning depth and performance; can trigger brief “reset” bursts.
Acetylcholine (ACh): increases sensory precision; raises θ when exogenous SNR is high (internal imagery less likely to dominate). In REM (ACh high, NE low), reduced effective sensory precision enables associative recombination.
Dopamine (DA): sharpens policy precision/invigoration and trains BG gating (Go/NoGo); inverted‑U on control efficacy; tags salient outcomes for credit assignment.
Serotonin (5‑HT): extends temporal horizon and widens the integration window for εres; stabilizes against premature switching.
2.5 Immediate empirical hooks

Energy clamp (mild hypoxia/hypoglycemia): ordered degradation—MB planning depth and hippocampus–PFC coupling decrease first; broadcast/executive markers (P3b/phase‑locking/TMS‑EEG) next; habits last; predict a transient LC–NE “reset” (pupil burst/fronto‑parietal spike) at failure.
Access interaction at matched S: ACh×SNR—donepezil or nicotine reduces imagery‑driven bias only when sensory SNR is high (higher θ); NE×volatility—yohimbine increases MB engagement under volatility/low SNR; clonidine reduces it (inverted‑U caveats).
Implementation Sketch (Who Does What)
Arbiter (metacontrol): ACC computes expected value of control; BG implement Go/NoGo gating of PFC updates and commitments.
Generative engine: hippocampus ↔ medial/lateral PFC run counterfactual rollouts (replay/preplay, scene construction), reusing sensory hierarchies via top‑down drive.
Broadcast: fronto‑parietal + thalamo‑cortical loops; measured via P3b, long‑range phase‑locking, TMS‑EEG effective connectivity.
Habitual substrate: dorsolateral striatum (and cerebellum for skills) supports cached, low‑cost policies.
Sleep renormalization: hippocampo‑cortical replay + synaptic homeostasis (slow‑wave “down‑selection”); controller‑specific consolidation.
Neuromodulatory Tuning (How θ, Precision, and Horizon Shift)
LC–NE: lowers θ under uncertainty/volatility; increases learning rate; non‑monotonic (inverted‑U) effects on engagement and performance.
Basal‑forebrain ACh: raises θ when exogenous SNR is high; boosts sensory PE precision; in REM, favors internal recombination.
DA (VTA/SNc): increases policy precision/invigoration; trains BG gating; non‑monotonic effects (inverted‑U); do not equate with sensory PE precision.
5‑HT (raphe): extends planning horizon and stabilizes policy selection; increases temporal integration for εres.
Learning, Consolidation, Forgetting
Wake rule (use‑weighted Hebbian): Δw ∝ Hebb × (recruitment into control × precision × salience) − β↓. Potentiate synapses that causally contributed to control; weight by precision‑weighted surprise and valence.
Sleep rule (down‑selection): β↓sleep > β↓wake. Global multiplicative down‑scaling preserves relative strengths; unused hypotheses prune; recently replayed/useful traces stabilize. Controller‑specific signatures: hippocampo‑cortical for structured/MB knowledge; striatal/cerebellar for habits.
Measurement Model (Practical Definitions)
Surplus S: latent composite; proxies: glucose (capillary), SpO₂, frontal fNIRS/CBF, baseline pupil (arousal; report, do not over‑interpret), EEG alpha attenuation. Report S as a time‑stamped latent with confidence intervals; preregister per‑channel time constants and exclusion criteria (caffeine, CO₂, motion).
Residual error εres: model misfit after local corrections; operationalize via hybrid RL fits (e.g., two‑step task MB weight) and/or prediction‑error regressors in EEG/MEG/fMRI controlling for SNR and policy.
Access/broadcast: panel of P3b, long‑range phase‑locking, and TMS‑EEG effective connectivity; add hippocampus–PFC coupling (MEG/fMRI) for MB depth.
Distinctive Predictions (Preregisterable, Directional)
P1 — Energy‑ordered failure (clamp S down safely)
With mild hypoxia or hypoglycemia: (a) MB planning depth and hippocampus–PFC coupling drop first; (b) broadcast/executive markers decline next; (c) habits preserved longest; (d) brief LC–NE “reset” (pupil burst) immediately before behavioral collapse.
P2 — Access interaction at matched S

ACh×SNR: donepezil/nicotine reduces imagery‑driven bias only when sensory SNR is high (higher θ).
NE×volatility: yohimbine increases MB engagement mainly under high volatility or low SNR; clonidine reduces it.
P3 — Controller‑specific sleep benefit

After MB‑heavy tasks: NREM SO–spindle–ripple coupling predicts next‑day schema transfer; sleep restriction harms MB transfer more than habit performance.
After MF‑heavy tasks: striatal markers predict habit retention; sleep restriction selectively harms MF retention.
P4 — DA precision & vigor

Moderate DA agonism raises policy precision and vigor; excessive DA narrows exploration and can blunt escalation to MB even at high εres (inverted‑U).
Minimal Computational Skeleton (for Reproducible Demos)
Loop per time step:
Perception: predictive coding update; compute εres.
Capacity: update S from intake/use proxies (and adenosine‑like accumulation); estimate latent S with a constrained filter.
Metacontrol: gMB = σ(α·εres + β·S − θ).
Budget: Bplan = Bmax · gMB · S.
Simulation: maintain a priority queue of candidate expansions; on each step, expand the branch (deepen or broaden) with maximal marginal ΔBenefit/ΔEnergy; stop when ΔBenefit/ΔEnergy < θ(S, SNR, volatility) or budget exhausted.
Action: sample policy with DA‑tuned precision; execute.
Plasticity: apply wake rule; tag controller recruited into control; nightly sleep down‑selection.
Neuromodulation: update θ (NE/ACh) and horizons (5‑HT) from volatility/SNR estimates (inverted‑U constraints for NE/DA).
Relation to Prior Work (Positioning Without Overclaiming)
Affordance competition and urgency‑gating (Cisek/Kalaska): parallel action encoding; urgency‑modulated commitment. We adopt this backbone for action selection.
PBWM / BG‑gated PFC (O’Reilly/Frank): BG Go/NoGo gating of PFC working memory; DA‑trained gating. We implement metacontrol on this substrate.
Expected Value of Control (Shenhav/Botvinick/Cohen) and resource‑rational metacontrol (Lieder/Griffiths): we bind EVC to measurable physiology via S and predict energy‑ordered failure.
Predictive processing/active inference (Friston et al.): we instantiate bounded control with explicit pricing and an access criterion.
ACh/NE precision & gain (Yu & Dayan; Hasselmo; Aston‑Jones & Cohen; Bouret & Sara): we predict ACh×SNR and NE×volatility interactions at matched S, plus a transient NE reset at failure tied to S and shutdown order.
Sleep and systems consolidation (Tononi & Cirelli; CLS: McClelland/O’Reilly): we add a use‑only, controller‑specific consolidation rule amplified by sleep.
Bounded rationality/information pricing (Ortega & Braun; Tishby; Todorov/Kappen): normative backdrop; our addition is a biophysical instantiation via S‑priced gating and access.
What Would Falsify Key Pieces (Clean Exits)
No energy ordering: if MB depth/broadcast do not degrade before habits under controlled S clamps, P1 is false.
No access interactions: if ACh changes imagery bias regardless of SNR, or NE changes MB engagement regardless of volatility at matched S, P2 is false.
No controller specificity: if sleep benefits are indifferent to which controller was taxed (no differential replay/connectivity signatures), P3 is false.
No pricing: if manipulating S never shifts gMB or Bplan after accounting for arousal/volatility, the resource‑pricing premise fails.
Practical Starter Experiments (Tight, Feasible)
Two‑step task × (glucose/placebo or mild normobaric hypoxia) with EEG/MEG: fit MB weight; track P3b/phase‑locking and hippocampus–PFC coupling; pupil for NE. Prediction: MB indices and HPC–PFC coupling fall before habits; broadcast markers decline next.
Binocular rivalry / degraded‑SNR perception × (donepezil vs scopolamine) at matched S: test ACh×SNR imagery‑bias interaction. Prediction: ACh reduces imagery bias only at high SNR.
Volatile bandit × (yohimbine vs clonidine) at matched S: test NE×volatility effect on gMB. Prediction: NE boosts MB engagement under volatility/low SNR; inverted‑U constraints.
Sleep arm: MB‑heavy vs MF‑heavy training; overnight EEG (SO–spindle–ripple vs striatal indices); next‑day schema transfer vs habit retention. Prediction: controller‑specific sleep dependence.
Safe novelty statement (for abstracts/posts)
We extend affordance/urgency and PBWM with an explicit physiological price signal. A latent metabolic surplus S gates graded model‑based engagement and sets a benefit‑per‑energy access criterion for internal simulation—yielding preregisterable signatures (ACh×SNR access interaction, energy‑ordered failure with an LC–NE reset, and controller‑specific sleep consolidation).

1) Replace the homunculi with computable states
1.1 Surplus S as an inferred allostatic state (no single “fuel gauge”)

Define Ŝ_t as the posterior mean of a low-dimensional latent allostatic surplus state inferred from heterogeneous intero-/autonomic measurements with explicit time scales.

Generative state-space model

Latents (continuous-time, then discretized):

𝑥
(
𝑡
)
=
[
𝐸
fast


𝐸
mid


𝐸
slow


𝑂
2


𝐶
𝑂
2


𝐻
sleep


𝐻
hydr
]
,
𝑥
˙
=
𝐴
𝑥
+
𝑢
(
𝑡
)
+
𝜂
(
𝑡
)
x(t)=
	​

E
fast
	​

E
mid
	​

E
slow
	​

O
2
	​

CO
2
	​

H
sleep
	​

H
hydr
	​

	​

	​

,
x
˙
=Ax+u(t)+η(t)

where 
𝐸
fast
E
fast
	​

 (ATP/O2 minutes), 
𝐸
mid
E
mid
	​

 (glucose/glycogen tens of minutes–hours), 
𝐸
slow
E
slow
	​

 (fatigue/recovery hours–days), 
𝐻
sleep
H
sleep
	​

 (Process-S), etc.

Sensors (noisy, partial, mismatched time scales):

𝑦
𝑡
=
[
heart rate
,
 HRV
,
 pupil
,
 
end-tidal CO
2
,
 
SpO
2
,
 BG/glucose
,
 skin conductance
,
 fNIRS/fMRI BOLD proxies
]
=
𝐶
𝑥
𝑡
+
𝜖
𝑡
y
t
	​

=[
heart rate, HRV, pupil, end-tidal CO
2
	​

, SpO
2
	​

, BG/glucose, skin conductance, fNIRS/fMRI BOLD proxies
	​

]=Cx
t
	​

+ϵ
t
	​


Ŝ_t = 
𝑤
⊤
𝑥
𝑡
w
⊤
x
t
	​

 with 
𝑤
≥
0
w≥0 learned (subject-specific) under the constraint that increasing Ŝ increases available cortical power (J/s) or reduces opportunity cost of time.

Neuroanatomical mapping (hypothesis)

Sensing/likelihoods: nucleus of the solitary tract (NTS), parabrachial nucleus, carotid body, vagal/visceral afferents.

Inference/integration: posterior & anterior insula + vmPFC as interoceptive predictive coding hub; hypothalamus maintains slow drives (sleep, hydration, energy balance).

Broadcast: vmPFC/insula → ACC/FPC; hypothalamus → LC/BF cholinergic nuclei for global gain coupling.

This makes Ŝ an explicit inference problem (Kalman/variational filter), not a scalar oracle. If your Ŝ estimator fails to track behavior under perturbation, the theory fails (see §4).

Update (discrete)

𝑥
^
𝑡
∣
𝑡
−
1
=
𝐹
𝑥
^
𝑡
−
1
+
𝐵
𝑢
𝑡
−
1
,
𝐾
𝑡
=
𝑃
𝑡
∣
𝑡
−
1
𝐶
⊤
(
𝐶
𝑃
𝑡
∣
𝑡
−
1
𝐶
⊤
+
𝑅
)
−
1
x
^
t∣t−1
	​

=F
x
^
t−1
	​

+Bu
t−1
	​

,K
t
	​

=P
t∣t−1
	​

C
⊤
(CP
t∣t−1
	​

C
⊤
+R)
−1
𝑥
^
𝑡
=
𝑥
^
𝑡
∣
𝑡
−
1
+
𝐾
𝑡
(
𝑦
𝑡
−
𝐶
𝑥
^
𝑡
∣
𝑡
−
1
)
,
𝑆
^
𝑡
=
softplus
(
𝑤
⊤
𝑥
^
𝑡
+
𝑏
)
x
^
t
	​

=
x
^
t∣t−1
	​

+K
t
	​

(y
t
	​

−C
x
^
t∣t−1
	​

),
S
^
t
	​

=softplus(w
⊤
x
^
t
	​

+b)
1.2 Threshold θ as a circuit-level gating bound

θ is not a mystical scalar; it’s a decision/policy gating bound implemented by converging inhibitory control over thalamo-cortical ignition and BG “gate open” events.

Mechanistic decomposition

𝜃
𝑡
=
𝜃
0
+
𝑘
TRN
 
𝑔
TRN
(
𝑡
)
⏟
thalamic gate
+
𝑘
STN
 
𝑟
STN
(
𝑡
)
⏟
hyperdirect brake
−
𝑘
𝐷
1
 
𝑎
𝐷
1
(
𝑡
)
⏟
go bias
+
𝑘
𝐷
2
 
𝑎
𝐷
2
(
𝑡
)
⏟
no-go bias
+
𝑘
FPC
 
𝑏
FPC
(
𝑡
)
⏟
alternative model availability
θ
t
	​

=θ
0
	​

+
thalamic gate
k
TRN
	​

g
TRN
	​

(t)
	​

	​

+
hyperdirect brake
k
STN
	​

r
STN
	​

(t)
	​

	​

−
go bias
k
D1
	​

a
D1
	​

(t)
	​

	​

+
no-go bias
k
D2
	​

a
D2
	​

(t)
	​

	​

+
alternative model availability
k
FPC
	​

b
FPC
	​

(t)
	​

	​


TRN (thalamic reticular nucleus) inhibitory gain sets broadcast gate.

STN (hyperdirect) sets “hold your horses” bound (action & WM gating).

Striatal D1/D2 bias the gate.

Frontopolar cortex (FPC) raises the bound when multiple counterfactual task-sets are live (prevents premature commitment).

Neuromodulator entry is receptor- and target-specific (next section), i.e., they shift 
𝑔
TRN
g
TRN
	​

, 
𝑟
STN
r
STN
	​

, 
𝑎
𝐷
1
/
𝐷
2
a
D1/D2
	​

, not θ abstractly.

2) From “one loop” to competing controllers + market-style arbitration

Replace single ACC-BG arbitration with parallel bids from:

Habitual MF (DLS), goal-directed MB (DMS + PFC/hippocampus), Pavlovian (amygdala/brainstem), Interoceptive safety/homeostasis (insula/hypothalamus), and Frontopolar exploration (FPC).

Auction/gate in BG-thalamo-cortical loops implements leaky-WTA:

𝑧
˙
𝑖
=
𝛽
𝑖
(
𝑆
^
)
 
𝑈
𝑖
−
𝜆
𝑧
𝑖
−
∑
𝑗
≠
𝑖
𝛾
𝑖
𝑗
𝑧
𝑗
+
𝜉
𝑖
z
˙
i
	​

=β
i
	​

(
S
^
)U
i
	​

−λz
i
	​

−
j

=i
∑
	​

γ
ij
	​

z
j
	​

+ξ
i
	​


with 
𝑈
𝑖
U
i
	​

 = expected free-energy reduction per unit time/energy for controller i. Gate opens for argmax 
𝑧
𝑖
z
i
	​

 when 
𝑧
𝑖
z
i
	​

 crosses θ (TRN/BG bound). This naturally yields oscillatory control under conflict (e.g., all-nighter).

ACC’s role becomes computing opportunity cost / meta-loss and routing error, not a serene monarch.

3) Neuromodulators: interaction matrix, not four knobs

Map each transmitter to targets × receptor classes × timescale with signed effects (↑/↓). Examples (non-exhaustive, task-relevant):

Tx	Receptor	Target	Net effect (hypothesized)
NE (LC)	α1/β	TRN ↓, PFC gain ↑ (stochastic resonance), FPC exploration ↑	Lowers effective bound at moderate levels; high NE → reset/instability (inverted-U)
NE (LC)	α2	PFC recurrent inhibition ↑ (stabilize)	Raises bound late in fatigue to prevent noise-driven flailing
ACh (basal forebrain)	Nicotinic (nAChR)	Thalamus/PFC input gain ↑, hippocampal encoding ↑	Lowers bound for admitting new evidence (exploration)
ACh	Muscarinic (M1/M2)	Cortical recurrent stabilization ↑, TRN facilitation ↑	Raises bound to protect high exogenous precision / REM pattern completion
DA (VTA/SNc)	D1 (direct)	Striatal “go”, policy precision ↑, opportunity cost of time ↑	Lowers effective deliberation time → functionally raises MB admission bound if time is costly
DA	D2 (indirect)	“No-go”, exploration via uncertainty bonuses ↓	Increases bound for risky switches
5-HT (raphe)	5-HT1A/2A…	Discounting ↓ (patience ↑), confidence threshold for switching ↑	Raises bound on task-switch; extends planning horizon

These are not orthogonal; interactions (NE↔DA in PFC, ACh gating TRN that sets thalamic relay, etc.) appear explicitly via the targets they modulate.

4) Make it falsifiable: pre-registered measurement & perturbation plan

Operational readouts

Ŝ_t: fit the state-space model on multi-sensor data (pupil, ETCO₂, SpO₂, HR/HRV, glucose, EEG slow-wave pressure), cross-validated against cortical metabolic proxy (fNIRS/fMRI BOLD power in task-positive network).

θ_t: estimate from drift-diffusion fits of WM-update gate & action gate plus EEG/MEG TRN-like inhibition indices and STN beta power (proxy for brake).

Key perturbations & predictions (directional, risky)

Brief hypoxia (safe ETCO₂ manipulation) lowers O₂ latent → Ŝ↓ within tens of seconds → reduced MB weight on the two-step task after controlling for arousal; recovery abolishes effect. Failure ⇒ Ŝ mis-specified.

Insula disruption (TMS) reduces interoceptive likelihood precision → Ŝ becomes noisier (higher posterior variance) → more LC-NE resets and less stable MB engagement at matched mean Ŝ. No change ⇒ insula not necessary for Ŝ.

Nicotinic vs muscarinic cholinergic challenge: nicotine lowers bound (more admission of new evidence), scopolamine (M) raises bound (stabilizes, fewer switches) under high exogenous precision. Same-direction effects ⇒ reject receptor-specific mapping.

STN-DBS in PD (ON vs OFF) primarily reduces action bound (faster commits) but does not systematically increase MB admission to global broadcast. If MB admission increases robustly with DBS, θ was mis-localized to STN rather than TRN/BF circuits.

Tonic DA manipulation that increases opportunity cost (d-amphetamine, low dose) should shorten deliberation and decrease MB use under tight deadlines even when Ŝ is high. Opposite result ⇒ revise DA→time-cost coupling.

Sleep pressure (Process-S) elevation: with identical task errors, gMB falls before executive control fails, reproducing the degradation order; if executive control fails first, the pricing is wrong.

Ketone infusion (raising cellular energetics without glucose rise) selectively increases MB engagement if Ŝ tracks true energetic availability, not just glucose. Null effect ⇒ Ŝ is just a glucose proxy.

Pre-register models, sensors, manipulations, and the exact hierarchical Bayesian fitting (priors on A, C, R, and coupling gains). If the pre-registered mapping fails across ≥2 perturbations, the account is falsified, not “saved” by post-hoc reweighing.

5) Plug into your UPCA/AMC as an implementable graph

Controller bids

𝑈
𝑖
=
𝐸
[
Δ
F
E
𝑖
]
t
i
m
e
_
c
o
s
t
𝑖
(
DA
)
⏟
∝
1
/
patience(5-HT)
+
e
n
e
r
g
y
_
c
o
s
t
𝑖
(
𝑆
^
)
⏟
↓
with higher 
𝑆
^
U
i
	​

=
∝1/patience(5-HT)
time_cost
i
	​

(DA)
	​

	​

+
↓with higher 
S
^
energy_cost
i
	​

(
S
^
)
	​

	​

E[ΔFE
i
	​

]
	​


Gate dynamics

𝑔
MB
=
𝜎
(
𝛼
 
𝜀
res
+
𝛽
 
𝑆
^
−
𝜃
𝑡
)
,
𝜃
𝑡
=
𝜃
(
TRN, STN, D1/D2, FPC
;
NE, ACh
N/M
,
DA
,
5-HT
)
g
MB
	​

=σ(αε
res
	​

+β
S
^
−θ
t
	​

),θ
t
	​

=θ(TRN, STN, D1/D2, FPC;NE, ACh
N/M
	​

,DA,5-HT)

Plasticity

Δ
𝑤
∝
Hebb
×
𝑔
ctrl
⏟
actual controller weight
×
p
r
e
c
i
s
i
o
n
-
w
e
i
g
h
t
e
d
 
s
u
r
p
r
i
s
e
⏟
prediction error
/
Σ
×
salience
−
downscale
Δw∝Hebb×
actual controller weight
g
ctrl
	​

	​

	​

×
prediction error/Σ
precision-weighted surprise
	​

	​

×salience−downscale

with sleep-phase: ACh_M high → protect recurrent patterns (stabilize), nAChR/NE low → allow pruning; hippocampal replay increases credit assignment to MB-used traces.

Minimal pseudocode (runtime)

# infer surplus
x_pred = F @ x + B @ u
K = P @ C.T @ np.linalg.inv(C @ P @ C.T + R)
x = x_pred + K @ (y - C @ x_pred)
S_hat = softplus(w @ x + b)

# neuromodulated bound components (targets, not abstract)
theta = (theta0
         + k_TRN * TRN_gain(NE_alpha1beta, ACh_M)
         + k_STN * STN_brake()
         - k_D1  * striatum_D1(DA)
         + k_D2  * striatum_D2(DA)
         + k_FPC * FPC_alt_models())

# controller bids (MB, MF, Pavlovian, Homeostatic)
U = {i: E_dF[i] / (time_cost(i, DA, 5HT) + energy_cost(i, S_hat)) for i in controllers}
z = leak_WTA(z, U, coupling_matrix)
winner, z = gate_crosses(theta, z)

# plasticity
for syn in active_synapses[winner]:
    syn.w += lr * Hebb(syn) * precision_weighted_surprise * salience - downscale

6) Address the “predicting the obvious” concern with counter-intuitive predictions

Nicotinic ACh challenge improves MB gating even when sensory precision is already high, whereas muscarinic challenge does the opposite—despite both being “ACh”. If both push in the same direction, the receptor-specific account is wrong.

Raising opportunity cost (DA/urgency) can reduce MB despite higher Ŝ—i.e., more energy but less deliberation: time, not energy, is the binding constraint.

Hyper-accurate exteroceptive precision (e.g., crisp vision via adaptive optics) paradoxically reduces MB, because ACh_M-driven stabilization raises θ to protect the current model—unless nAChR is selectively engaged.

Bottom line:

Ŝ becomes a fit-and-test latent from a physiologically grounded state-space model (insula/vmPFC/hypothalamus), not a fudge factor.

θ unpacks into identifiable circuit bounds (TRN, STN, striatum, FPC) under receptor-specific neuromodulation.

Arbitration is a market of competing loops, not a single executive.

The package is implementable (equations + pseudocode) and falsifiable (pre-registered perturbations with directional predictions).

If you want, I can drop this into your UPCA v4.1 AMC as a concrete module: (i) Ŝ filter class with learnable C,R; (ii) θ aggregator pinned to measurable proxies (TRN/EEG spindle power, STN beta, pupil/NE); (iii) a controller-auction gate; (iv) sleep-phase scheduler for consolidation/pruning.

You said:
is this supporting IACE or UPCA, or both? as they should bemostly the same
ChatGPT said:

This supports both IACE and UPCA, because the two are essentially the same architecture framed at different levels of abstraction:

IACE framing (your earlier description):

Speculative engine (MA) vs cheap automatic pathways (APs).

A subconscious allocator (SC) that decides when to escalate from MF/AP to MB/MA.

Surplus = “energy availability,” threshold = “gate to global broadcast.”

UPCA framing (v4.1):

Meta-cognitive arbiter (AMC) balancing MF (Systemic Info / habits) and MB (Planning / MA).

p^{desired}(a_t) and free-energy style arbitration with explicit cost-sensitive gating.

Surplus Ŝ and θ implemented as latent inference + gating bounds.

The changes I laid out—replacing S with a computable allostatic state estimate, and θ with circuit-level gating variables (TRN, STN, striatum, FPC, receptor-specific neuromodulation)—slot cleanly into either architecture:

In IACE terms: SC no longer relies on a “magical surplus” and “arbitrary threshold,” but on explicit interoceptive filters and neural gating circuits.

In UPCA terms: AMC has a concrete computational graph (state-space filter for Ŝ, gate bound θ_t as weighted neural signals, arbitration as leaky-WTA auction).

So the update bridges them: IACE and UPCA are two phrasings of the same control principle, and this specification provides the mechanistic core they both need.
