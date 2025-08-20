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
