# EQO/1 — Epistemic Quantization of Observables
**Specification · Version 1.0.0 · English Edition (canonical wire format)**

This specification is self-contained. It defines no migration path, no legacy resolution, and no compatibility layers: version 1.0.0 is the zero point of the standard. It is *constructed* as a standard — with conformance classes, normative language, reserved namespaces, and defined extension mechanisms; international standing arises through adoption, and the document is built precisely for that. The German edition (included in this package) is a language edition of identical structure; **this English edition is canonical for all machine-readable tokens.**

---

# Part I — Foundations

## §1 Purpose and Scope

EQO/1 classifies **documented observations of physical, chemical, and biological effects** — heterodox and orthodox alike — in a single vocabulary, and assigns every observation a **discrete epistemic coordinate**. The standard therefore does two things:

1. **Classification:** *What* was observed (Registry P), under which conditions (Registry K), which explanations are documented for it (Registry M), and in which typical compositions it occurs (Registry S).
2. **Quantization:** *How* the observation is documented (Registry E). Six ordered axes map every observation onto a cell of a finite epistemic lattice. Cells are clusterable, comparable, and trackable over time.

The corpus from which this standard emerged — free-energy, over-unity, Hutchison, Biefeld-Brown, and LENR claims — is also its hardest test case: a corpus in which documentation status and phenomenal claim can diverge radically. A standard that carries this corpus neutrally carries any.

## §2 Normative Language and Conformance

The key words **MUST**, **MUST NOT**, **SHALL**, **SHOULD**, and **MAY** are to be read normatively.

| Class | Requirement |
|-------|-------------|
| CL-1 *Minimal* | Every observation carries ≥ 1 P-leaf and `eqo_version` |
| CL-2 *Standard* | CL-1 + full K facets + raw E fields (unknown values as `x`) |
| CL-3 *Full* | CL-2 + M edges with role + derived E axes (C, T) + reference edges between observations |

## §3 Principles (normative)

1. **Primacy of the observable.** What is indexed is the documented observation as its own graph node — never the claimed mechanism, never the entity as a whole.
2. **Neutral labels.** P labels describe phenomena. Admissible baselines ("in excess of the accounted input", "without documented source") are statements about the documentation, not verdicts of truth.
3. **Unification.** Orthodox and heterodox cases use the same leaves. *Anomaly is not a property of a label but a property of the graph: the absence of a documented edge to an established mechanism* (operationally: axis T = 0, signature S-OFN).
4. **Status truth without claim judgment.** The research status of a *mechanism* (established/fringe/heterodox/historical) is documentable fact and lives in Registry M. The standard passes no judgment on individual *observations* — not even implicitly: EQO/1 **MUST NOT** be extended with a normative scalar "credibility score" (§Q.3).
5. **Exemplar principle.** Every family and every signature **SHALL** carry canonical prototype instances. Controlled vocabularies stabilize inter-tagger reliability through exemplars, not definitions alone; the instances in Part II and VI are normative registry content, not illustration.
6. **Closure guarantee.** Every class carries the residual family `SON`; every facet and every E axis admits `x` (unknown). Every observation is fully recordable. *Unknown is never the lowest grade* (§E.4).

## §4 Architecture

Five registries plus one computational module:

| Registry | Prefix | Content |
|----------|--------|---------|
| **P** Phenomena | `P-` | 10 classes → families → leaves (the observables) |
| **M** Mechanisms | `M-` | Explanatory models with status; incl. artifact classes |
| **K** Context | `K-` | Physical framing conditions (input, medium, vacuum …) |
| **E** Epistemics | `E-` | Six ordered axes D R C P T Q + raw fields |
| **S** Signatures | `S-` | Named compositions (co-occurrence patterns) |
| Module **Q** | — | Quantization, metric, clustering, epistemotypes |

Graph node types: `Entity` · `Observation` · `Source` · registry nodes. Edges: `Entity —hasObservation→ Observation —documentedIn→ Source`; `Observation —effectType→ P-leaf`; `Observation —[role]→ M-node`; `Observation —[reference]→ Observation` (`replicates` · `contradicts` · `confirms_per_source`).

## §5 Nomenclature and Syntax (normative)

**Design principle "dumb keys, smart labels":** IDs are semantically poor (registry prefix, mnemonic, running number) so that labels can sharpen without keys breaking. IDs are **never** recycled and **never** reinterpreted.

```
node_id   ::= REG "-" LOCAL
REG       ::= P | M | K | E | S
P-LOCAL   ::= CLASS "-" FAMILY "-" NN        # P-MEC-LEV-01
M-LOCAL   ::= ["ART-"] MNEMONIC3             # M-EHD, M-ART-PWR
K-LOCAL   ::= AXIS3                          # K-INP (values: snake_case tokens)
E-LOCAL   ::= AXIS1                          # E-D, E-R, E-C, E-P, E-T, E-Q
S-LOCAL   ::= MNEMONIC3                      # S-HUT
NN        ::= 01–89 gapless; 90–99 reserved for local extensions
```

**Validation regexes (MUST):**

```
P-leaf        ^P-[A-Z]{3}-[A-Z]{3}-[0-9]{2}$
M-node        ^M-(ART-)?[A-Z]{3}$
K/E values    ^[a-z][a-z0-9_]*$  and axis grades [A-Z][0-9]
E-signature   ^E1:D([0-7]|x)R([0-5]|x)C([0-5]|x)P([0-4]|x)T([0-4]|x)Q([0-3]|x)$
S-pattern     ^S-[A-Z]{3}$
```

**Further rules:**
- Uniqueness holds **per registry** (S-ORG and M-ORG coexist; the prefix disambiguates).
- All tokens are ASCII and IRI-safe; labels are multilingual (`prefLabel` per language). Canonical machine tokens are the English ones of this edition.
- **Reserved class codes** for future modules: `ENV` (environment/geophysics: weather-modification and seismic claims) and `PSI` (mental-influence claims). Deliberately unpopulated in 1.0.0: secure the namespace, normalize content only when needed.
- **Private extensions** use NN 90–99 or the registry prefix `X-`; they **MUST NOT** appear in interchange data without a namespace declaration. (The instance corpus of this package demonstrates the mechanism with one private mechanism node, `X-HYD`.)
- Every observation **MUST** carry `eqo_version` (here: `"1.0.0"`).

**Canonical wire tokens (English edition):**
- M-edge roles: `claimed` · `discussed` · `excluded_per_source`
- Observation references: `replicates` · `contradicts` · `confirms_per_source`
- K-INP: `hv_dc` `hv_ac` `lf_ac` `rf` `transient` `magnetostatic` `electrochemical` `mechanical` `acoustic` `optical` `thermal` `chemical` `passive` `x`
- K-MED: `air` `inert_gas` `vacuum` `water_electrolyte` `oil_dielectric` `solid` `plasma` `cryo` `x`
- K-VAC: `x` (default) `persists` `vanishes` `intensifies` `partial_only`
- K-SCL: `micro` `lab` `macro` `plant` `x` · K-PER: `transient` `decaying` `persistent` `permanent` `x`
- K-MOD: `temperature` `orientation` `astronomical` `time_of_day` `humidity` `geographic` `none_documented`

---

# Part II — Registry P: Phenomena

10 classes: **MEC** Mechanical/Kinematic · **THM** Thermal · **NUC** Nuclear/Material-analytic · **EMG** Electromagnetic · **GRA** Gravitational/Inertial (measurements) · **OPT** Optical/Radiative · **ACU** Acoustic/Vibrational · **CHM** Chemical/Phase · **BIO** Biological · **INS** Instrumental (reading as sole observable).

Every family lists its canonical instances (Principle 5); ⊕ marks orthodox anchors. A consolidated, machine-readable reference corpus built to this standard is published in its own repository (see README) — the standard itself ships no data.

## P-MEC

**P-MEC-LEV — Levitation & Hovering**
- P-MEC-LEV-01 Levitation of rigid bodies (free suspension)
- P-MEC-LEV-02 Levitation of liquids/droplets
- P-MEC-LEV-03 Near-ground hovering/gliding, or anomalously easy handling of heavy objects

*Instances:* Hutchison levitation footage, Vancouver 1979 ff. · Grebennikov's "cavity structural effect" platform, 1990s · Jarl account of Tibetan acoustic levitation (`K-INP: acoustic`) · Leedskalnin's Coral Castle megaliths 1923–51, anecdotal (LEV-03) · ⊕ Meissner demonstrations, acoustic traps (T4).

**P-MEC-KIN — Kinematics**
- P-MEC-KIN-01 Directed thrust on an apparatus (observed, or measured on balance/torsion balance)
- P-MEC-KIN-02 Self-propelled translation of objects
- P-MEC-KIN-03 Spontaneous spin-up/rotation of resting objects
- P-MEC-KIN-04 Precession behavior deviating from model (incl. Foucault pendulum plane)
- P-MEC-KIN-05 Abrupt stopping/reversal of moving objects
- P-MEC-KIN-06 Spontaneous alignment of objects
- P-MEC-KIN-07 Motion response deviating from the force/inertia budget
- P-MEC-KIN-08 Friction/drag change beyond material constants
- P-MEC-KIN-09 "Walking" of electrodes/contacts
- P-MEC-KIN-10 Continued motion without documented energy input (mechanical self-runners)

*Instances:* Brown gravitator 1929 and the lifter community (KIN-01, `hv_dc`) · EmDrive torsion-balance measurements, Eagleworks 2016 (KIN-01) · Searl SEG spin-up accounts (KIN-03) · ⊕ Crookes radiometer 1874 → today M-RAD/T4, paradigm of a migrated anomaly (KIN-03, `optical`) · Allais pendulum anomalies 1954/1959 (KIN-04, `K-MOD: astronomical`) · Dean Drive 1959 (KIN-07) · Bessler wheel 1712 (54-day sealed test, Kassel 1717) and the Finsrud sculpture (KIN-10).

**P-MEC-DEF — Deformation & Structure**
- P-MEC-DEF-01 Metal deformation without documented signs of heating
- P-MEC-DEF-02 Bursting/fragmentation
- P-MEC-DEF-03 Splitting/tearing
- P-MEC-DEF-04 Cold joining/fusing (visual/mechanical; analytic finding → P-NUC-ELM-03)
- P-MEC-DEF-05 Embedding of foreign bodies in solids
- P-MEC-DEF-06 Temporary softening/plastic state ("jellification")

*Instances:* Hutchison sample corpus: bent bolts (DEF-01), torn rods (DEF-03), wood-in-aluminum (DEF-05), "jelly" metal (DEF-06); delegation visits documented 1983.

**P-MEC-OSZ — Oscillation**
- P-MEC-OSZ-01 Visible vibration without documented excitation
- P-MEC-OSZ-02 Pendulum damping/amplitude anomalies

*Instances:* Object trembling in Hutchison footage (OSZ-01) · pendulum amplitude reports in eclipse contexts (OSZ-02, `astronomical`).

**P-MEC-FLU — Fluids & Particles**
- P-MEC-FLU-01 Fluid motion without documented drive (vortices, climbing)
- P-MEC-FLU-02 Self-organization/pattern formation of particles

*Instances:* Schauberger's vortex and trout observations (FLU-01) · water swirling in Hutchison footage (FLU-01).

**P-MEC-SON** — P-MEC-SON-01 Other mechanical observables

## P-THM

**P-THM-BIL — Heat Balance**
- P-THM-BIL-01 Heat output in excess of accounted input (calorimetry)
- P-THM-BIL-02 Heat generation spatially separated from the apparatus

*Instances:* Fleischmann–Pons, Utah, 23 March 1989 · Rossi E-Cat demonstrations 2011 ff. · Griggs hydrosonic cavitation pump, 1990s.

**P-THM-LOK — Local Heating**
- P-THM-LOK-01 Local heating/hotspots without accounted input
- P-THM-LOK-02 Metal melting at room ambient
- P-THM-LOK-03 Spontaneous ignition without ignition source
- P-THM-LOK-04 IR signature without corresponding contact/ambient measurement

*Instances:* Hutchison reports of glowing/molten metal directly beside unharmed combustible material (LOK-02).

**P-THM-KLT — Cooling**
- P-THM-KLT-01 Cooling without documented heat sink
- P-THM-KLT-02 Cooling of current-carrying conductors under load
- P-THM-KLT-03 Frost/condensation without corresponding ambient conditions

*Instances:* "Cold electricity" reports (Edwin Gray's EMA motor; Tesla reception) (KLT-02) · cooling reports around Schauberger implosion devices (KLT-01) · Roschin–Godin 2000: temperature drop around the rotor (KLT-01).

**P-THM-TRN — Transport & Dynamics**
- P-THM-TRN-01 Temperature gradient against expected heat flow
- P-THM-TRN-02 Heat conduction deviating from material constants
- P-THM-TRN-03 Thermal oscillation

*Instances:* Reich's orgone-accumulator ΔT and the Einstein examination of 1941 — Einstein's convection explanation is the model instance of an `M-ART-THK` edge with role `discussed` (TRN-01).

**P-THM-PHW — Phase Change**
- P-THM-PHW-01 Evaporation/phase change below equilibrium conditions

**P-THM-SON** — P-THM-SON-01 Other thermal observables

## P-NUC

**P-NUC-ELM — Elemental Analysis**
- P-NUC-ELM-01 Changed elemental inventory in before/after analyses
- P-NUC-ELM-02 Isotope-ratio shift
- P-NUC-ELM-03 Elemental intermixing in joint zones (analytic finding)
- P-NUC-ELM-04 Detection of fusion products above expectation (He-4, tritium)
- P-NUC-ELM-05 Elemental balance shift in organisms

*Instances:* Iwamura (Mitsubishi) Cs→Pr permeation findings, JJAP 2002 (ELM-01) · isotope shifts on Pd cathodes in the LENR literature (ELM-02) · analyses of Hutchison joint samples (ELM-03) · Miles/McKubre helium–heat correlation (ELM-04) · Kervran's chicken-calcium balances, 1960s (ELM-05).

**P-NUC-STR — Radiation**
- P-NUC-STR-01 Emission of ionizing radiation without documented source
- P-NUC-STR-02 Neutron emission
- P-NUC-STR-03 Residual radioactivity after experiment
- P-NUC-STR-04 Fission signatures under low-energy conditions

*Instances:* Jones's low-rate neutrons, BYU 1989 (STR-02) · Taleyarkhan's sonofusion, Science 2002, with the Purdue inquiries of 2008 (STR-02).

**P-NUC-MAT — Material Structure**
- P-NUC-MAT-01 New phases/nanoparticles (analytic finding)
- P-NUC-MAT-02 Microcraters/explosion traces on surfaces

*Instances:* SEM microcraters on LENR electrodes (MAT-02) · Keshe "GANS" material claims (MAT-01).

**P-NUC-SON** — P-NUC-SON-01 Other nuclear/material-analytic observables

## P-EMG

**P-EMG-FLD — Fields**
- P-EMG-FLD-01 Monopole-like/unipolar field signature
- P-EMG-FLD-02 Longitudinal/scalar propagation signatures
- P-EMG-FLD-03 Magnetic-field reversal without current reversal
- P-EMG-FLD-04 Field shielding/enhancement deviating from model
- P-EMG-FLD-05 Field focusing/local concentration

*Instances:* Ehrenhaft's "magnetolysis"/monopole reports, 1940s (FLD-01) · Meyl's scalar-wave experiment kits; Bearden's scalar reception (FLD-02).

**P-EMG-IND — Induction & Components**
- P-EMG-IND-01 Induction without relative motion/flux change
- P-EMG-IND-02 Capacitance/inductance values deviating from geometry and material
- P-EMG-IND-03 Permittivity values deviating
- P-EMG-IND-04 Negative differential resistance/anomalous characteristics

*Instances:* DePalma's N-machine measurements; Hooper's "motional field" apparatus (IND-01) · Moray's valve detector ("Swedish stone") (IND-04).

**P-EMG-BIL — Energy Balance & Conversion**
- P-EMG-BIL-01 Measured electrical excess power (COP > 1)
- P-EMG-BIL-02 Continued operation of electromagnetic systems without accounted input
- P-EMG-BIL-03 Self-recharging of storage devices
- P-EMG-BIL-04 Energy pickup via antenna/ground arrangements
- P-EMG-BIL-05 ⊕ Voltage/current generation under gradients or load (thermo-, piezo-, triboelectric, photovoltaic instances)

*Instances:* Steorn Orbo 2007/2009 (failed Kinetica demo; jury verdict 2009) · Bearden MEG patent 2002 · Lutec, QEG 2014, Kapanadze videos (BIL-01) · Methernitha's Testatika; Adams motor; Bedini SSG; Sweet's VTA (BIL-02) · Bedini battery "rejuvenation"; Joe Cell charging reports (BIL-03) · Moray receiver, 1920s/30s; Tesla patent US 685,957 (1901, `patent_flag`); Hendershot generator 1928 (BIL-04) · ⊕ Seebeck/PV demonstrations (BIL-05, T4).

**P-EMG-ENT — Discharge & Plasma**
- P-EMG-ENT-01 Plasma/discharge formation at atypically low voltage or with work output
- P-EMG-ENT-02 Electrostatic anomalies under AC
- P-EMG-ENT-03 RF bursts without identified source

*Instances:* Papp's noble-gas engine — Caltech demo 1968 with fatal explosion, Feynman's eyewitness account (ENT-01) · Correa PAGD patents (ENT-01) · Chernetsky's "self-generating discharge" (ENT-01) · RF-burst reports from the Hutchison milieu (ENT-03).

**P-EMG-KOR — Correlation**
- P-EMG-KOR-01 Correlated signals without documented transmission path

*Instances:* Kozyrev's telescope-detector claims toward true star positions (`astronomical`) · Montagnier's DNA-signal experiments 2009/2011.

**P-EMG-SON** — P-EMG-SON-01 Other electromagnetic observables

## P-GRA

**P-GRA-GEW — Weight**
- P-GRA-GEW-01 Weight change under influence (sign/magnitude as measured value)
- P-GRA-GEW-02 Reduced weight in the "field shadow" of an apparatus (static)
- P-GRA-GEW-03 Rotation-bound weight change
- P-GRA-GEW-04 Gyroscope weight anomalies
- P-GRA-GEW-05 Spatially bounded zone of deviant weight measurements

*Instances:* Brown's gravitator balance trials (GEW-01) · Podkletnov, Physica C 1992: 0.05–0.3 % above a rotating YBCO disc; NASA-MSFC rebuilds inconclusive (GEW-02/03) · Hayasaka–Takeuchi, PRL 1989, right-spinning gyro; Faller et al. 1990: null (GEW-04) · Oregon Vortex and related "mystery spots" (GEW-05, `M-ART-PER: discussed`).

**P-GRA-INR — Inertia & Free Fall**
- P-GRA-INR-01 Acceleration response deviating from applied force
- P-GRA-INR-02 Free-fall acceleration deviating from local g
- P-GRA-INR-03 Directional anisotropy of g/weight measurements

*Instances:* Woodward's MEGA force measurements in the µN range; Tajmar's adversarial test campaigns (INR-01) · DePalma's "spinning ball drop" 1977 (INR-02) · Saxl–Allen torsion pendulum during the 1970 solar eclipse, Phys. Rev. D (INR-03).

**P-GRA-SIG — Signals**
- P-GRA-SIG-01 Periodic/transient signals in gravimeters and balances

*Instances:* Gravimeter residuals during solar eclipses (campaigns 1997, published 2000) (`astronomical`).

**P-GRA-SON** — P-GRA-SON-01 Other gravitational observables

## P-OPT

**P-OPT-EMI — Emission**
- P-OPT-EMI-01 Visible glow/aura on apparatus or objects
- P-OPT-EMI-02 UV/IR emission without thermally corresponding source
- P-OPT-EMI-03 ⊕ Luminescence under mechanical, acoustic, or electrical action
- P-OPT-EMI-04 Cherenkov-like radiation
- P-OPT-EMI-05 Color shift/spectral anomaly

*Instances:* Glow reports from the Hutchison corpus; Searl SEG "halo" narratives; Roschin–Godin: pink glow (EMI-01) · glow reports from electrolysis cells (EMI-04) · ⊕ tribo-/sonoluminescence demonstrations (EMI-03, T4).

**P-OPT-PLS — Plasma Phenomena**
- P-OPT-PLS-01 Plasma balls/ball-lightning-like appearances
- P-OPT-PLS-02 Discharge action without visible glow

*Instances:* Laboratory ball-lightning attempts (incl. Golka's large coils) and plasma balls in Hutchison footage (PLS-01).

**P-OPT-MED — Medium & Imaging**
- P-OPT-MED-01 Refraction/propagation anomalies
- P-OPT-MED-02 Anomalies in the image content of recordings (device malfunction → P-INS-ELK-01)
- P-OPT-MED-03 Mist/haze formation around apparatus

*Instances:* The "orb" photography corpus (MED-02, `M-ART-CAM: discussed`) · mist reports at Hutchison and Schauberger setups (MED-03).

**P-OPT-SON** — P-OPT-SON-01 Other optical observables

## P-ACU

**P-ACU-EMI — Emission**
- P-ACU-EMI-01 Spontaneous tones/whistling
- P-ACU-EMI-02 Infra-/ultrasound without documented source
- P-ACU-EMI-03 Tonal emission from solids

*Instances:* The Taos Hum, investigations from the 1990s on (EMI-02, `geographic`) · metallic sounds in Hutchison footage (EMI-03).

**P-ACU-TRN — Transmission**
- P-ACU-TRN-01 Resonance/vibration transfer over distance

*Instances:* Tesla's oscillator lore (Houston Street) · Keely's "sympathetic vibratory" apparatus 1872–98; posthumous findings of concealed compressed-air lines 1899 = model instance of an `M-ART-AUF` edge.

**P-ACU-SON** — P-ACU-SON-01 Other acoustic observables

## P-CHM

**P-CHM-RKT — Reactions**
- P-CHM-RKT-01 Gas evolution deviating from the reaction budget
- P-CHM-RKT-02 Material decomposition without documented oxidizer/solvent
- P-CHM-RKT-03 Deviant corrosion behavior
- P-CHM-RKT-04 Formation of new compounds (analytic finding)
- P-CHM-RKT-05 Deviant electrochemical figures (cell voltage, yield)
- P-CHM-RKT-06 Deviant flame/combustion characteristics

*Instances:* Yull Brown's oxyhydrogen demonstrations; "cool flame that melts tungsten" (RKT-01/06) · Stanley Meyer's water fuel cell with claimed above-Faraday yield; Ohio court ruling 1996: fraud (RKT-05) · Garrett's water-carburetor patent 1935; Joe Cell (RKT-05) · Pantone's GEET reactor (RKT + ENT-01).

**P-CHM-PHS — Phases & Substance Properties**
- P-CHM-PHS-01 Phase transition under atypical conditions
- P-CHM-PHS-02 Property change of water without compositional change

*Instances:* Benveniste, Nature 1988, high dilution; supervised Maddox–Randi–Stewart recheck negative (PHS-02) · Grander water; Emoto crystal photographs (PHS-02) · Keshe GANS phase claims (PHS-01).

**P-CHM-SON** — P-CHM-SON-01 Other chemical observables

## P-BIO

**P-BIO-WRK — Effects**
- P-BIO-WRK-01 Growth inhibition/promotion
- P-BIO-WRK-02 Physiological sensations/symptoms in bystanders
- P-BIO-WRK-03 Cellular findings
- P-BIO-WRK-04 Effect on microorganisms

*Instances:* Pyramid germination trials of the 1970s; orgone plant studies (WRK-01) · warmth/tingling at orgone accumulators; bystander reports in the Hutchison milieu (WRK-02) · Rife's microscope findings (WRK-03) · Rife "beam ray" devitalization claims; Kervran's microbe trials (WRK-04).

**P-BIO-SON** — P-BIO-SON-01 Other biological observables

## P-INS

Applies only when the instrument reading is the sole observable, or the instrument itself is documented as affected; independently confirmed quantities → subject class.

**P-INS-MSS — Instruments**
- P-INS-MSS-01 Balance readings
- P-INS-MSS-02 Radiation-counter deflections
- P-INS-MSS-03 Readings of electrical instruments (oscilloscope, multimeter)
- P-INS-MSS-04 Clock-rate anomalies

*Instances:* Meter-only demonstrations of over-unity video culture (Kapanadze type) (MSS-01/03) · Geiger reports in the Hutchison milieu (MSS-02) · Kozyrev's and DePalma's clock claims (MSS-04).

**P-INS-ELK — Electronics**
- P-INS-ELK-01 Camera malfunctions/failures
- P-INS-ELK-02 Navigation/compass readings
- P-INS-ELK-03 Failures of digital electronics/data loggers

*Instances:* Camera failures and spinning compasses in Hutchison reports (ELK-01/02).

**P-INS-SON** — P-INS-SON-01 Other instrumental observables

---

# Part III — Registry M: Mechanisms

Explanatory models with `status` — a documentable, revisable statement about the state of research (Governance §G.3), **not** a verdict on individual observations. Status values: `established` · `fringe` (active, non-accepted research) · `heterodox` (outside accepted physics) · `historical` (superseded).

**Established:** M-EHD Electrohydrodynamics/ion wind · M-KOR Corona/gas discharge · M-MSN Superconductivity (Meissner, flux pinning) · M-DIA Diamagnetic levitation · M-ACL Acoustic levitation · M-AER Aerodynamics/convection · M-TEL Thermoelectrics · M-PIE Piezo-/electrostriction · M-TRB Triboelectrics · M-IND Induction/eddy currents · M-MST Magnetostriction · M-JOU Joule/induction heating · M-CHX Exothermic chemistry · M-ELY Electrolysis · M-KAV Cavitation & sonoluminescence · M-TLM Tribo-/electroluminescence · M-RAD Radiometric forces (thermal transpiration) · M-LFR Leidenfrost · M-CAS Casimir *(real effect; extraction claims → M-ZPE)* · M-RES Mechanical resonance/structure-borne sound

**Established artifact classes** *(conventional explanatory offers; central for this corpus):*
M-ART-PWR Power-measurement error (non-sinusoidal signals, power factor, RMS confusion) · M-ART-CAL Calorimetry/sensor placement · M-ART-STA Electrostatic force on balance/rig · M-ART-THK Thermal convection/draft *(instance: Einstein's account of the Reich ΔT, 1941)* · M-ART-VIB Vibration/footfall · M-ART-CAM Image/camera artifact, editing, staging · M-ART-AUF Suspension/threads/hidden drive *(instance: Keely findings 1899)* · M-ART-KON Sample contamination · M-ART-PER Perceptual/optical illusion *(instance: mystery-spot geometries)* · M-ART-STT Statistics/selection effects *(instance: Maddox analysis of the Benveniste counts)*

**Fringe:** M-LEN LENR/cold fusion · M-EMD Resonant-cavity thrust · M-POD Rotating-superconductor effects · M-MEG Mach-effect propulsion · M-ALL Astronomically modulated gravity anomaly

**Heterodox:** M-ZPE Vacuum-energy extraction · M-SCW Scalar waves · M-EGR Electrogravitics beyond EHD · M-MGM Permanent magnet as work source · M-RDT "Radiant energy" · M-WST Water structure/memory · M-KVN Biological transmutation · M-MDF Macroscopic mass-defect weight change · M-ORG Orgone

**Historical:** M-AET Aether dynamics · M-KEE Sympathetic vibration

**Edge roles Observation → M (normative):** `claimed` (source offers mechanism as explanation) · `discussed` (named as candidate in sources/secondary literature) · `excluded_per_source` (source claims to have excluded it; what is indexed is the exclusion *claim*).

---

# Part IV — Registry K: Context Facets

| Key | Facet | Values |
|-----|-------|--------|
| K-INP | Input (multi) | `hv_dc` `hv_ac` `lf_ac` `rf` `transient` `magnetostatic` `electrochemical` `mechanical` `acoustic` `optical` `thermal` `chemical` `passive` `x` |
| K-MED | Medium | `air` `inert_gas` `vacuum` `water_electrolyte` `oil_dielectric` `solid` `plasma` `cryo` `x` |
| K-VAC | Vacuum behavior | `x` (default) `persists` `vanishes` `intensifies` `partial_only` |
| K-SCL | Scale | `micro` `lab` `macro` `plant` `x` |
| K-PER | Persistence | `transient` `decaying` `persistent` `permanent` `x` |
| K-MOD | Documented modulators (multi) | `temperature` `orientation` `astronomical` `time_of_day` `humidity` `geographic` `none_documented` |

K facets are **phenomenological** context; the documentation state lives exclusively in Registry E. This separation is the precondition of two-block quantization (§Q.2).

---

# Part V — Registry E: Epistemic Axes

Six ordered axes. Raw fields (`sources[]`, `controls[]`, M edges) **MUST** be retained in CL-3; derived grades remain reconstructible from them at any time (auditability).

**E-D Documentation grade** — `D0` secondary account · `D1` eyewitness account (primary) · `D2` photo · `D3` video · `D4` single measurement · `D5` measurement series/protocol · `D6` raw data available · `D7` peer-reviewed publication. Multiple sources: maximum. `patent_flag` separate (patents document filing, not documentation grade).

**E-R Replication grade** — `R0` never attempted · `R1` single occurrence · `R2` repeated, same experimenter · `R3` independently attempted, not reproduced · `R4` independent, reproduction claimed · `R5` independent, reproduction documented (≥ D5). Replication attempts are **their own observations**, linked via `replicates`/`contradicts`.

**E-C Control grade** (derived from `controls[]`; highest satisfied tier) — `C0` none documented · `C1` calibration · `C2` control/dummy run · `C3` independent second instrument or relevant environmental exclusion (vacuum test, EM shielding) · `C4` blinded protocol · `C5` full energy/mass balance.

**E-P Provenance grade** — `P0` anonymous/unclear · `P1` claimant's own documentation · `P2` account by affiliated third parties/media · `P3` independent documentation · `P4` adversarial/skeptical examination documented. Multiple sources: maximum per observation; third-party examinations are usually their own linked observations.

**E-T Theory-embedding grade** (derived from M edges; `excluded_per_source` does not count) — `T0` no M edge (open) · `T1` heterodox/historical edges only · `T2` fringe edge · `T3` established edge, role `discussed` · `T4` established edge, role `claimed`.

**Artifact classes are established mechanisms for this purpose.** `M-ART-*` nodes carry status `established` in Registry M, so an artifact edge derives T exactly as any other established edge does. A documented conventional account of a report — camera artifact, power-measurement error, suggestion — *is* an explanation, and a record carrying one is no longer open. Implementations that exempt artifact classes silently keep debunked reports classified as anomalies.

**Orthodox anchors and null results.** A record whose observation *is* a null result or an orthodox demonstration has no anomalous phenomenon to explain and therefore no mechanism edge to derive from. Such a record carries `T4` by convention; deriving `T0` from the absent edge would classify the most securely established experiments as open anomalies. Mark these with ⊕ and state the convention in the record. T is **time-indexed**: status revisions in M change T; implementations **MUST** carry `t_computed_at`. *(Paradigm: Crookes radiometer — 1874 T0, after Reynolds/Maxwell T4.)*

**E-Q Quantification grade** — `Q0` qualitative · `Q1` semi-quantitative · `Q2` quantitative · `Q3` quantitative with uncertainty.

**§E.4 Unknown semantics (normative):** `x` is admissible on every axis and **is not grade 0**. `D0` means "only a secondary account exists"; `Dx` means "documentation state not yet assessed". Distance computations treat `x` as missing (Gower convention, §Q.3), never as minimum.

**E-signature (compact cell address):** `E1:D3R2C0P1T0Q0` — the `E1` prefix versions the axis set. Regex in §5.

---

# Part VI — Registry S: Signatures (Category Compositions)

Signatures are named co-occurrence patterns over P leaves, K facets, and M edges. They are **derived, never tagged** — and each carries its canonical instances.

| ID | Pattern | Definition | Canonical instances |
|----|---------|-----------|---------------------|
| S-HUT | Hutchison | (MEC-DEF ∨ MEC-LEV) ∧ (NUC-ELM ∨ OPT ∨ INS ∨ BIO-WRK-02) | Hutchison corpus, Vancouver 1979 ff.; sample analyses; delegation visits 1983 |
| S-BRN | Biefeld-Brown | (MEC-KIN-01 ∨ MEC-LEV ∨ GRA-GEW-01) ∧ `K-INP: hv_*` | Brown gravitator 1929; Project Winterhaven proposal 1952; lifter community; ⊕ the EHD literature |
| S-LNR | Cold fusion | THM-BIL-01 ∧ (NUC-ELM ∨ NUC-STR) | Fleischmann–Pons 1989; Miles/McKubre; Iwamura 2002; E-Cat 2011; Google-funded Nature review 2019 (null so far) |
| S-SLF | Self-runner | MEC-KIN-10 ∨ EMG-BIL-02 ∨ EMG-BIL-03 | Bessler wheel 1712; Testatika; Adams; Bedini; Sweet VTA; Steorn Orbo; Finsrud |
| S-SRL | Searl | MEC-KIN-03 ∧ GRA-GEW-01 ∧ OPT-EMI-01 ∧ THM-KLT-01 | Searl SEG narrative corpus; Roschin–Godin 2000 (weight change, glow, cooling) |
| S-IMP | Implosion | MEC-FLU-01 ∧ (THM-KLT ∨ MEC-LEV) | Schauberger Repulsine lore; trout/vortex reports |
| S-PLM | Plasma work | EMG-ENT-01 ∧ (MEC-KIN ∨ THM) | Papp engine 1968 (Feynman episode); Correa PAGD; Chernetsky |
| S-RDE | Radiant reception | EMG-BIL-04 ∧ (EMG-ENT ∨ EMG-IND-04) | Moray 1920s/30s; Tesla US 685,957; Hendershot 1928 |
| S-AST | Astronomically modulated | (GRA ∨ MEC-KIN-04 ∨ EMG-KOR) ∧ `K-MOD: astronomical` | Allais 1954/59; Saxl–Allen 1970; eclipse gravimetry 1997/2000; Kozyrev |
| S-ORG | Orgone | THM-TRN-01 ∧ (BIO-WRK ∨ OPT-EMI-01) | Reich accumulator; Einstein examination 1941 (`M-ART-THK: discussed`) |
| S-WFC | Water fuel | CHM-RKT-05 ∧ (EMG-BIL ∨ CHM-RKT-01) | Meyer (ruling 1996); Garrett patent 1935; Joe Cell; Yull Brown; Dingel |
| S-MEM | Water memory | CHM-PHS-02 ∧ (BIO-WRK ∨ EMG-KOR) | Benveniste 1988 + Maddox check; Montagnier 2009/2011; Grander; Emoto |
| S-ANT | Field/inertial propulsion | MEC-KIN-01/07 ∧ `K-VAC` recorded | EmDrive: Shawyer, Eagleworks 2016, TU Dresden null 2021; Woodward MEGA; Dean Drive |
| S-GYR | Gyroscopic | MEC-KIN-04 ∨ GRA-GEW-04 ∨ GRA-INR-02 | Laithwaite lecture 1974 (resolved, T4); Hayasaka–Takeuchi + Faller null; DePalma |
| S-OFN | Open | Observation without edge to `status: established` (T0) | *derived* — the operational anomaly definition (Principle 3) |
| S-DEK | Orthodox-covered | T4 | *derived* — ⊕ radiometer, Meissner demos, lifters with EHD documentation |

---

# Part VII — Module Q: Epistemic Quantization and Clustering

## §Q.1 Rationale

Epistemic quantization is sound under three conditions this module makes normative: **(a)** it yields a *vector*, never a normative scalar (which would be covert truth-valuation, violating Principle 4); **(b)** `x` is missing, never minimum (§E.4) — otherwise poorly *assessed* observations are conflated with poorly *evidenced* ones; **(c)** derived axes (C, T) remain reconstructible from raw data and are time-indexed — otherwise the lattice is not auditable. Under these conditions, epistemic quantization is simply faceted classification thought through to the end: ordered axes turn every observation node into a point of a finite lattice, and clusterability falls out as a theorem, not a feature.

## §Q.2 Two-Block Coordinate

- **Φ block (phenomenological):** multi-hot over P leaves + K tokens — *what, under which conditions*.
- **Ε block (epistemic):** cell of the lattice `D×R×C×P×T×Q` (8·6·6·5·5·4 = **28,800 cells**) — *how documented*.

Observations of the same Ε cell are **epistemically equivalent by construction**. For small corpora the standard defines a coarse quantization (per axis `low/mid/high`: D 0–2|3–5|6–7 · R 0–1|2–3|4–5 · C 0|1–2|3–5 · P 0–1|2|3–4 · T 0|1–2|3–4 · Q 0|1|2–3 → **729 macro-cells**).

## §Q.3 Reference Metric

- Ε block: **Gower distance** (normalized L1 per ordinal axis; `x` dropped pairwise — the reason Gower is the correct choice here).
- Φ block: **Jaccard** over P leaves, Gower over K facets.
- Overall similarity: σ = w_Φ·σ_Φ + w_Ε·σ_Ε. Weights are **query parameters**. The standard **MUST NOT** be extended with a normative scalarization ("score"); only *regions* are named (epistemotypes, §Q.4).

## §Q.4 Epistemotypes (Named Reference Regions)

**Covered means claimed, not merely discussed.** T3 records that an established mechanism is *on record as a candidate*; T4 records that a source *asserts* it. Only the latter is an orthodox account of the observation, so `EP-5` and `S-DEK` are drawn at T4. A T3 observation still has an open question attached to it, whatever the candidate explanation is.

| Type | Region (informal) | Prototypes |
|------|-------------------|------------|
| EP-1 *Solitary* | D ≤ 3, R ≤ 2, C0, P ≤ 1 | Hutchison; Kapanadze; Steorn |
| EP-2 *Demonstrative* | public demo, no data: D 2–3, C 0–1, P2 | Testatika; Papp 1968 |
| EP-3 *Lab-contested* | D ≥ 5, R 3–4, C ≥ 2 | Fleischmann–Pons; Podkletnov; Hayasaka–Takeuchi; EmDrive; Benveniste |
| EP-4 *Historical-anecdotal* | D ≤ 1, P ≤ 2 | Bessler; Keely; Moray; Leedskalnin |
| EP-5 *Orthodox-covered* | T4 | Radiometer today; Meissner; EHD lifters |
| EP-0 *Unquantized* | ≥ 3 axes `x` | new intake before assessment |

## §Q.5 Worked Example (Core Corpus, Quantized)

| Observation | E-signature | Macro-cell (D,R,C,P,T,Q) | Type |
|---|---|---|---|
| Hutchison corpus (primary) | `E1:D3R2C0P1T3Q0` | mid·mid·low·low·mid·low | EP-1 |
| Steorn Orbo 2007 | `E1:D3R1C0P1T0Q0` | mid·low·low·low·low·low | EP-1 |
| Fleischmann–Pons 1989 (Utah) | `E1:D7R3C2P1T2Q3` | high·mid·mid·low·mid·high | EP-3 |
| Caltech/MIT rechecks 1989 | `E1:D7R3C3P4T3Q3` — `contradicts` → F-P | high·mid·high·high·high·high | EP-3 |
| Podkletnov 1992 | `E1:D7R3C2P1T2Q3` | high·mid·mid·low·mid·high | EP-3 |
| Eagleworks EmDrive 2016 | `E1:D7R3C3P3T3Q3` | high·mid·high·high·high·high | EP-3 |
| TU Dresden null 2021 | `E1:D7R3C4P4T4Q3` — `contradicts` → EmDrive | high·mid·high·high·high·high | EP-3/EP-5 |
| Benveniste 1988 | `E1:D7R3C2P1T0Q3` | high·mid·mid·low·low·high | EP-3 |
| Crookes radiometer 1874 → today | `E1:D7R5C3P4T4Q3` | high·high·high·high·high·high | EP-5 |

Note that Hutchison sits at T3 rather than T0: artifact classes are established mechanisms, so the camera and suspension accounts on record embed the report in theory even though nothing about the claimed phenomenon is settled. Solitary describes the evidence, not the absence of an explanation.

Readable at a glance: Hutchison and Steorn cluster in the same Ε region despite entirely different phenomenology (Φ); F-P, Podkletnov, and the EmDrive form the lab-contested cluster; the radiometer demonstrates **temporal migration** through the lattice (T0 → T4). This separation of Φ and Ε is the epistemic payoff of quantization: one can ask *"which phenomena share the same evidential situation?"* and *"which evidential situations share the same phenomenon?"* — orthogonally.

## §Q.6 Known Failure Modes (Normative Countermeasures)

1. **Reification:** cells describe documentation states, not quality — implementations **MUST NOT** render cells as verdicts.
2. **Multiple counting:** a prolific claimant generates many observations; cluster statistics **SHALL** deduplicate at entity or source level (D: max; R/P feed from *distinct* sources).
3. **Derivation drift:** T depends on revisable M status → `t_computed_at` **MUST** be carried; T recomputed on status revision.
4. **Granularity:** 28,800 cells are too fine for small corpora → macro-cells (§Q.2) are the standard resolution for clustering reports.

---

# Part VIII — Data Model and Serialization

```yaml
observation:
  id: OBS-1992-PODK-0001
  eqo_version: "1.0.0"
  entity: DEV-YBCO-ROTOR-TAMPERE
  effect_types: [P-GRA-GEW-02, P-GRA-GEW-03]
  mechanisms:
    - {ref: M-POD, role: claimed}
    - {ref: M-ART-THK, role: excluded_per_source}
  context: {inp: [rf, magnetostatic], med: cryo, vac: x, scl: lab, per: transient, mod: [none_documented]}
  epistemics:
    raw: {sources: [SRC-PHYSICA-C-1992], controls: [calibration, control_run]}
    axes: "E1:D7R3C2P1T2Q3"
    t_computed_at: 1.0.0-intake
  patent_flag: false
  references: [{ref: OBS-1997-NASA-MSFC-0001, type: replicates}]
```

SKOS/JSON-LD: per registry node `skos:prefLabel` (multilingual), `skos:scopeNote`, `skos:broader` (leaf → family → class); instance lists as `skos:example`; sources via PROV-O, measured values via QUDT, persons/devices optionally via Wikidata.

---

# Part IX — Governance and Extension

- **G.1 Append-only:** registries grow; IDs are never recycled or reinterpreted. New P leaves require an observable prefLabel, delimitation from neighbors, and ≥ 1 instance; new M nodes require a status assignment with brief rationale; new S patterns require a definition over existing registries plus instances.
- **G.2 Promotion:** `SON` leaves are reviewed periodically; from ~5 similar entries a dedicated leaf is normalized.
- **G.3 Status revision:** M `status` is the only deliberately mobile normative value — revision only with documented decision and date; T recomputation follows (§Q.6.3).
- **G.4 Versioning:** label/scopeNote sharpening = patch · new leaf/M node/facet value/S pattern = minor · change to principles, grammar, classes, or axis set (`E1` → `E2`) = major.
- **G.5 Extension path:** reserved class codes ENV, PSI; private namespaces NN 90–99 and `X-`; new languages as additional prefLabels without structural change.

---

*EQO/1, version 1.0.0, English edition. One vocabulary for orthodox and heterodox effects; anomaly as a graph property; evidential situation as a coordinate. Self-contained, extensible, ready for adoption.*
