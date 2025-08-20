Resource-Priced Predictive Control: A Unified Framework
Abstract

We formalize cognition as resource-rational predictive control: an agent with a hierarchical generative model chooses how much computation to do and which actions to take by trading expected benefit against energetic and computational cost. Behavior defaults to model-free (habitual) control; model-based (generative) control is gradedly engaged when (i) precision-weighted residual prediction error remains after fast local updates and (ii) physiological surplus permits expensive planning. Internally generated simulations (hippocampus–prefrontal) are allowed to influence behavior only when their marginal benefit per unit energy exceeds a state-dependent access threshold shaped by neuromodulators (NE, ACh, DA, 5-HT). Memory change follows use-weighted Hebbian plasticity during wake and synaptic down-selection during sleep. The framework yields concise equations, implementation-level circuit mapping (ACC/BG gating; HPC↔PFC simulation; fronto-parietal broadcast), and preregisterable predictions (energy-ordered failure; ACh×SNR and NE×volatility interactions; controller-specific sleep effects).

1) Core assumptions (minimal commitments)

Predictive brain: hierarchical generative models minimize precision-weighted prediction error (PE) online; expected free energy (EFE) organizes policy selection over time.

Bounded resources: computation and information have costs; surplus energy (indexed by glucose, SpO₂, CBF/fNIRS, tonic pupil) changes the effective price of computation on second–minute timescales.

Two control modes: model-free (MF) cached policies (cheap, inflexible) vs model-based (MB) counterfactual rollouts (costly, flexible). MF is the default; MB is recruited as needed and affordable.

2) Control law (what flips planning on)

Let 
𝜀
res
ε
res
	​

 be residual PE after fast MF/local updates (precision-weighted). Let 
𝑆
∈
[
0
,
1
]
S∈[0,1] be physiological surplus (higher = cheaper energy).

Engagement (metacontrol)

𝑔
MB
=
𝜎
 ⁣
(
𝛼
 
𝜀
res
+
𝛽
 
𝑆
−
𝜃
)
g
MB
	​

=σ(αε
res
	​

+βS−θ)

where 
𝜃
θ is a context-dependent access threshold; 
𝜎
σ is logistic. 
𝑔
MB
∈
[
0
,
1
]
g
MB
	​

∈[0,1] is the degree of MB recruitment.

Access (promotion of internal simulation to influence behavior)

Δ
Benefit
Δ
Energy
  
>
  
𝜃
 ⁣
(
𝑆
,
 sensory SNR
,
 volatility
)
ΔEnergy
ΔBenefit
	​

>θ(S, sensory SNR, volatility)

Only simulations whose marginal benefit-per-energy clears 
𝜃
θ gain global access (fronto-parietal/thalamo-cortical broadcast).

Planning budget

𝐵
plan
=
𝐵
max
⁡
⋅
𝑔
MB
⋅
𝑆
B
plan
	​

=B
max
	​

⋅g
MB
	​

⋅S

Depth/length of hippocampal–PFC rollouts scales with both need (
𝜀
res
ε
res
	​

) and capacity (
𝑆
S).

Priced objective (unifying value, compute, and energy)

𝐽
(
𝑚
,
𝜋
)
=
E
F
E
(
𝜋
∣
𝑚
)
+
𝜆
(
𝑚
)
 
𝐶
comp
(
𝜋
)
+
𝜇
(
𝑆
)
 
𝐶
met
(
𝜋
)
,
𝜇
′
(
𝑆
)
<
0
J(m,π)=EFE(π∣m)+λ(m)C
comp
	​

(π)+μ(S)C
met
	​

(π),μ
′
(S)<0

𝑚
∈
{
MF, MB
}
m∈{MF, MB}. Higher 
𝑆
S lowers the multiplier on metabolic cost.

3) Implementation sketch (who does what)

Arbiter (metacontrol): ACC estimates expected value of control from 
𝜀
res
ε
res
	​

, 
𝑆
S, volatility; basal ganglia (BG) implement Go/NoGo gating of PFC working-memory states (PBWM-style).

Generative engine: hippocampus ↔ medial/lateral PFC run counterfactual rollouts (replay/preplay, scene construction), reusing sensory hierarchies via top-down drive.

Broadcast: fronto-parietal + thalamo-cortical loops; P3b/long-range phase-locking/TMS-EEG reactivity are candidate signatures.

Habitual substrate: dorsolateral striatum (and cerebellum for skills) supports cached, low-cost policies.

Sleep renormalization: hippocampo-cortical replay + synaptic homeostasis (slow-wave “down-selection”).

4) Neuromodulatory tuning (how 
𝜃
θ, precision, and horizon shift)

LC-Noradrenaline (NE): signals volatility/unexpected uncertainty; lowers 
𝜃
θ (easier MB engagement) and increases learning rate; expect inverted-U with planning depth.

Basal-forebrain Acetylcholine (ACh): increases sensory precision; raises 
𝜃
θ when exogenous SNR is high (internal simulations less likely to dominate).

Dopamine (DA): policy precision/invigoration and BG gate learning (Go/NoGo); sharpens credit assignment for salient outcomes.

Serotonin (5-HT): extends temporal horizon, widens integration window for 
𝜀
res
ε
res
	​

; stabilizes against premature switching.

5) Learning, consolidation, forgetting

Wake rule (use-weighted Hebbian)

Δ
𝑤
  
∝
  
Hebb
×
(
recruitment into control
×
precision
×
salience
)
  
−
  
𝛽
↓
Δw∝Hebb×(recruitment into control×precision×salience)−β
↓
	​


Plasticity favors synapses actually recruited by the controlling mode (MF or MB) and scaled by precision and valence (neuromodulators).

Sleep rule (down-selection)

𝛽
↓
sleep
>
𝛽
↓
wake
β
↓
sleep
	​

>β
↓
wake
	​


Global multiplicative down-scaling preserves relative strengths → unused hypotheses prune, used traces consolidate. Controller-specific signatures: hippocampo-cortical for structured/MB knowledge; striatal/cerebellar for habits.

6) Measurement model (practical definitions)

Surplus 
𝑆
S: composite latent variable. Proxies by design: glucose (capillary), SpO₂, frontal fNIRS/CBF, baseline pupil (arousal; report, don’t over-interpret), EEG alpha attenuation.

Residual error 
𝜀
res
ε
res
	​

: task-level model misfit after local corrections; operationalize via hybrid RL fits (two-step task) or prediction-error regressors in EEG/MEG/fMRI.

Access/broadcast: P3b amplitude, long-range phase-locking, TMS-EEG evoked connectivity; HPC–PFC coupling (MEG/fMRI).

7) Distinctive predictions (preregisterable, directional)

P1 — Energy-ordered failure (clamp 
𝑆
S down safely).
With mild hypoxia or hypoglycemia:

MB planning depth and HPC–PFC coupling drop first;

broadcast/executive markers (P3b, long-range coupling) next;

habits preserved longest;

possible transient NE “reset” (pupil-indexed) immediately before behavioral collapse.

P2 — Access interaction at matched 
𝑆
S.

ACh×SNR: donepezil/nicotine reduces imagery-driven bias only when sensory SNR is high (higher 
𝜃
θ).

NE×volatility: yohimbine increases MB engagement mainly under high volatility; clonidine reduces it.

P3 — Controller-specific sleep benefit.
After MB-heavy tasks: NREM SO–spindle–ripple coupling predicts next-day schema transfer. After MF-heavy training: striatal markers predict habit retention. Sleep restriction selectively harms the controller taxed.

P4 — DA precision & vigor.
DA agonism raises policy precision and vigor; excessive DA narrows exploration (failure to escalate MB at high 
𝜀
res
ε
res
	​

).

8) Minimal computational skeleton (for reproducible demos)

Loop per time step

Perception: predictive coding update; compute 
𝜀
res
ε
res
	​

.

Capacity: update 
𝑆
S from intake/use (and adenosine-like accumulation).

Metacontrol: 
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
−
𝜃
)
g
MB
	​

=σ(αε
res
	​

+βS−θ).

Budget: 
𝐵
plan
=
𝐵
max
⁡
𝑔
MB
𝑆
B
plan
	​

=B
max
	​

g
MB
	​

S.

Simulation: prioritized rollouts; stop when 
Δ
Benefit
/
Δ
Energy
<
𝜃
(
𝑆
,
SNR
,
volatility
)
ΔBenefit/ΔEnergy<θ(S,SNR,volatility).

Action: sample policy with DA-tuned precision; execute.

Plasticity: wake rule; tag controller; nightly sleep down-selection.

Neuromodulation: update 
𝜃
θ (NE/ACh) and horizons (5-HT) from volatility/SNR estimates.

9) Relation to prior work (positioning without overclaiming)

PBWM / BG gating (O’Reilly/Frank): supplies the mechanism for ACC/BG-gated PFC working memory; our addition is a physiological price signal 
𝑆
S and a benefit-per-energy access rule controlling promotion of internal simulations.

Expected Value of Control (ACC; Shenhav/Botvinick/Cohen): we bind EVC to measurable physiology via 
𝑆
S and predict energy-ordered failure.

Predictive processing/active inference (Friston et al.): we instantiate bounded control with explicit pricing and a broadcast criterion.

ACh/NE precision & gain (Yu & Dayan; Hasselmo; Bouret & Sara; Aston-Jones & Cohen): we predict ACh×SNR and NE×volatility interactions at matched 
𝑆
S, plus a transient NE reset at failure.

Sleep synaptic homeostasis (Tononi & Cirelli): provides the down-selection backbone; we add controller-specific consolidation via recruitment tags.

10) What would falsify key pieces (clean exits)

No energy ordering: if MB depth/broadcast do not degrade before habits under controlled 
𝑆
S clamps, P1 is false.

No access interactions: if ACh changes imagery bias regardless of SNR, or NE changes MB regardless of volatility at matched 
𝑆
S, P2 is false.

No controller specificity: if sleep benefits are indifferent to which controller was taxed (no differential replay signatures), P3 is false.

No pricing: if manipulating 
𝑆
S never shifts 
𝑔
MB
g
MB
	​

 or planning budget after accounting for nuisance arousal, the resource-pricing premise fails.

11) Practical starter experiments (tight, feasible)

Two-step task × (glucose/placebo or mild normobaric hypoxia) with EEG/MEG: fit MB weight; track P3b/phase-locking and HPC–PFC coupling; pupil for NE.

Binocular rivalry / degraded-SNR perception × (donepezil vs scopolamine) at matched 
𝑆
S: test ACh×SNR imagery-bias interaction.

Volatile bandit × (yohimbine vs clonidine) at matched 
𝑆
S: test NE×volatility effect on 
𝑔
MB
g
MB
	​

.

Sleep arm: MB-heavy vs MF-heavy training; overnight EEG (SO–spindle–ripple vs striatal indices); next-day transfer vs habit retention.
