# Co-Levitated Reference Droplet Isopiestic Analyzer for Reagent-Free Field Hydrochemistry

> **Note:** This README is an ultra-condensed summary of the research reports published by Unpatentable.org. To view the full innovation documentation and explore the complete research, use the links at the bottom of this document.

**Domain:** [Human-Centered Technologies](https://unpatentable.org/innovation/?domain=human-centered-technologies)
**Subdomain:** [Lifelong Learning](https://unpatentable.org/innovation/?domain=human-centered-technologies&subdomain=lifelong-learning)

---

### Why We Invented This Technology
Hands-on lab and field science education for displaced and climate-affected learners is effectively nonexistent. The conventional assumption is that real experimentation needs fixed wet labs, glassware, and reagent supply chains, which camps, flood-hit regions, and remote communities cannot sustain. Recent advances could change this now: low-cost phased-array ultrasonic transducer boards from the maker community, open-source acoustic tweezers firmware, and AI tutors that run on edge hardware together make contactless, containerless microlitre handling of real soil, water, and air samples feasible for portable kits costing well under $10M to develop and deploy at pilot scale.

### The Innovation
## Abstract
This instrument levitates an unknown environmental droplet (water, soil extract, or air-scrubbing collector) beside a small glycerol–water reference droplet in adjacent nodes of a 40 kHz standing wave, inside a sealed chamber that is slowly desiccated. Both droplets share one vapour phase, so the reference droplet's shrinkage reports chamber water activity and the sample's shrinkage then yields its dissolved osmoles. Every quantity is a ratio of imaged volumes. No humidity sensor, balance, conductivity cell, calibration target or consumable reagent is needed. Tracking the osmole count as the droplet concentrates exposes mineral precipitation steps and deliquescence points, giving salinity and water-type classification relevant to saline intrusion and soil salinisation.

## Background & Prior Work
TinyLev (Marzo, Barnes, Drinkwater, 2017) made single-axis 40 kHz levitation buildable from cheap off-the-shelf parts. Levitated-droplet evaporation is well studied (Yarin et al., 1999; [water–NaCl drying kinetics](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9048286/)). Getenet et al. followed evaporite sequences in levitated soda-lake brine droplets, but needed [synchrotron X-ray diffraction and Raman](https://pubs.acs.org/cgdefu/article/22/4/2307/377116/A-Comprehensive-Methodology-for-Monitoring) for identification. In aerosol science, comparative-kinetics electrodynamic balances (Rovelli, Miles, Reid, Clegg, 2016, from recall) use sequential probe droplets to infer gas-phase humidity for charged picolitre droplets in a conditioned gas flow. The isopiestic method (Robinson & Stokes) equilibrates bulk solutions over days.

None of these uses a simultaneously co-levitated reference droplet as an in-situ hygrometer in an uncontrolled sealed acoustic chamber. None tracks an osmole invariant along a desiccation path to quantify and classify an unknown environmental sample without reagents or spectroscopy.

## Competitive Landscape & Strategic Edge
Field water kits (Hach, LaMotte, strip tests) depend on reagent resupply and expire in heat. Conductivity pens need calibration solutions and fail by electrode fouling. Foldscope-style frugal tools image but do not quantify chemistry. Research levitators (e.g. tec5-type ultrasonic levitators, synchrotron sample environments) assume humidity-conditioned gas and laboratory detectors. The blind spot is the assumption that a levitator needs a controlled atmosphere and an external analytical detector. Inverting that, the atmosphere is left uncontrolled and measured by a second droplet, and the sample's own phase behaviour is the detector. The consumable drops to about 0.1 µL of glycerol solution per run, so a 10 mL vial covers tens of thousands of runs. The instrument has no wetted parts to foul.

## Core Concept
**Architecture.** A single-axis 40 kHz standing-wave levitator has two opposed transducer caps (TinyLev-class) or a transducer and reflector. Drive is 5–12 V with a crystal-locked frequency, at an estimated 2–6 W from a USB power bank. Node spacing is λ/2 ≈ 4.3 mm at 25 °C. It sits inside a sealed 30–60 mL chamber of low-sorption polymer (polypropylene or PETG) with two loading ports. A shuttered side-well (1–3 mm orifice) holds any locally regenerable desiccant, such as oven- or sun-dried silica gel, calcined clay or dried rice. A second shuttered well holds a wet wick. A diffuse LED backlight and a phone camera with a macro lens (target ≤3–5 µm/pixel over a ~12 mm field) image both droplets side-on. A thermistor logs temperature.

**Inversions.** There are three.
1. The chamber atmosphere is neither controlled nor sensed, and the desiccant may be impure. A reference droplet reads the atmosphere.
2. No reagent identifies solutes. Precipitation, efflorescence and deliquescence of the sample itself do.
3. No calibration target is shipped. All outputs are volume ratios, and the absolute scale (for logging only) comes from the droplet separation k·λ/2, with λ = c/f and c ≈ 331.3 + 0.606·T(°C) m/s.

**Measurement principle.** The sample droplet S (1.5–2 mm diameter, 2–4 µL) and the reference droplet R sit in adjacent or alternate nodes. R is 0.4–0.6 mm of glycerol–water at a known initial glycerol mass fraction w₀ ≈ 0.10–0.20. Glycerol never effloresces. Its volatility is negligible at this size: assuming a 25 °C vapour pressure of ~0.02 Pa, the d²-law lifetime of a 0.5 mm droplet is tens of days, so loss over a one-hour run is estimated below 0.5% of volume. (The searched literature reports [glycerol loss from levitated droplets](https://royalsocietypublishing.org/rsos/article/5/1/170819/93729/), so sub-100 µm reference droplets must be avoided.)

Droplet volumes come from an oblate-spheroid fit to the silhouette, V = (π/6)·a²·b, with a the horizontal and b the vertical diameter. The glycerol mass in R is fixed, m_g = w₀·ρ₀·V_R0. At any later time the water content follows from V_R ≈ m_g/ρ_g + m_w/ρ_w, where volume additivity is an approximation good to roughly 1–2%. Water activity then follows from the Norrish relation a_w = x_w·exp(−K·x_g²). The literature constant for glycerol is K ≈ 1.16 (from recall), to be verified against tabulated glycerol–water isotherms and stored as a lookup table.

When both droplets are stationary they share that a_w. The sample's apparent osmole content is

Ω(a_w) = ρ_w·V_S·(−ln a_w)/M_w, with M_w = 0.018015 kg/mol,

and the original sample osmolarity is C_osm = Ω/V_S0. Pixel scale cancels in every ratio, and temperature enters only weakly. For example, a 10 mOsm/L freshwater at a_w = 0.95 (osmolality ≈ 2.85 osmol/kg) has shrunk about 285-fold in volume, or 6.6-fold in diameter (1.5 mm → ~230 µm). That is easily resolved. A ±3% volume error on each droplet gives an estimated ±10–15% on C_osm.

**Procedure.**
1. Load R by fibre touch-off, then S by capillary or wire loop. Dosing accuracy is irrelevant because V₀ is imaged.
2. Open the desiccant shutter. By d²-law (t ≈ ρd²/(8·D·Δc)) at 60–75% chamber RH, initial dry-down takes an estimated 15–30 min.
3. Close the shutter when R indicates a_w ≈ 0.97. The two droplets now equilibrate isopiestically through the small sealed gas volume. The relaxation time is τ ≈ ρd²/(12·D·c_sat·(1−a_w)), roughly 2–4 min for 200–400 µm droplets at a_w 0.90–0.95.
4. Accept a plateau when both diameters change by less than 0.5% per minute, then record Ω.
5. Pulse the shutter to step down through rungs near a_w ≈ 0.95, 0.90, 0.85, 0.80 and 0.70, repeating step 4 at each.
6. Continue drying to efflorescence. This is detected as loss of sphericity, a jump in opacity, or a volume arrest. Record the efflorescence activity.
7. Open the wet-wick well and record the deliquescence activity on rewetting.
8. Optionally swap node assignments on a repeat run to cancel inter-node temperature bias.

**Interpretation (the "osmole staircase").** For conservative solutes, Ω is flat across rungs apart from smooth osmotic-coefficient drift, so the result is reported as NaCl-equivalent osmolarity. A downward step in Ω flags precipitation. An early step near low concentration factors indicates carbonate loss (Ca²⁺ + 2HCO₃⁻ → CaCO₃ + CO₂ + H₂O), and its magnitude estimates temporary hardness. A later step indicates gypsum.

The residual brine class follows evaporite chemical-divide logic (Hardie & Eugster). Deliquescence near a_w ≈ 0.75 indicates a halite-dominated, seawater-type residue. A residue still liquid below a_w ≈ 0.35 indicates Ca/Mg-chloride or nitrate type. Opaque crusting at high a_w with a large Ω loss indicates carbonate or sulfate type. Mixed salts lower the mutual deliquescence point, so the classes are coarse by design.

Three sample types are handled:
- **Water:** direct droplets.
- **Soil:** 1:5 soil:water extracts, cloth-filtered, giving a salinity and sodicity-class proxy.
- **Air:** R alone is an ambient hygrometer.

**Optional embodiments.**
- **Surface tension.** The drive is amplitude-modulated at 50–400 Hz to excite the l=2 Rayleigh mode, f = (1/2π)·√(8σ/(ρR³)), about 186 Hz for a 1.5 mm water droplet. Resonance is read by a strobed LED and gives surface tension as a surfactant-pollution indicator. This is a known technique (Trinh, Marston) added as a layer.
- **Aerosol collection.** A levitated collector droplet is exposed to fan-drawn air for a fixed time and then assayed for osmole gain. The risk is that collection efficiency is uncharacterised and probably low.
- **Fast high-activity rung.** Reading at a_w > 0.98 would avoid precipitation. The risk is that a 0.1 K inter-droplet temperature difference corresponds to about 0.6% RH, which dominates the error there.

## Physics & Logical Feasibility
Levitating 0.1–2 mm aqueous droplets at 40 kHz is routine. The half-wavelength is 4.3 mm, far larger than the droplets. Vapour-phase equalisation of chemical potential between droplets sharing a closed gas volume is the isopiestic principle. Microlitre scale shortens bulk equilibration from days to minutes because τ ∝ d². The chamber air holds about 1 mg of water at saturation, comparable to droplet mass, so the droplets, not the walls, dominate the closed-shutter equilibrium. Containerless suspension removes wall nucleation and contact-line pinning, so volumes follow from silhouettes and supersaturated states persist.

Critical assumptions:
- The two droplets are isothermal to about 0.1 K. Acoustic streaming helps, and the node-swap run checks it.
- Plateaus are true stationarity, which the dual-droplet criterion enforces.
- Kelvin curvature effects are negligible above 50 µm.
- Osmotic coefficients are near unity. The result is explicitly "NaCl-equivalent", not ion-specific.

## Implementation Readiness & Key Constraints
- **Months 0–6:** Build on open TinyLev electronics. Validate the reference-droplet hygrometry against saturated-salt fixed points (Greenspan). Characterise τ and the temperature bias.
- **Months 6–12:** Validate the osmole staircase on gravimetric NaCl, synthetic hard water, seawater dilutions and soil extracts against conductivity and titration. Develop offline phone software for edge detection, spheroid fitting, plateau logic and classification.
- **Months 12–24:** Ruggedise with a gasketed chamber, dust-capped transducers and solar charging, then pilot with displaced-community learning partners.

The estimated bill of materials is US$40–80 excluding the phone. Estimated development cost is US$2–4M, under the US$10M ceiling.

Key constraints:
- Sub-millimetre reference loading needs a simple fibre tool and practice.
- Open-type transducers degrade with dust and condensation.
- A run takes an estimated 45–75 min.
- Humid climates require regenerable desiccant.

## Utility & Purpose
Displaced learners gain a genuine quantitative instrument whose only supplies are a vial of glycerol solution, clean rinse water and sun-dried desiccant. They can measure salinity and water type in wells, tanks, floodwater and irrigated soil, the variables that shift under sea-level rise, storm surge, drought concentration and over-pumping. Each run makes vapour pressure, colligative properties, solubility and crystallisation directly visible in a floating droplet, so the measurement is also the lesson. Communities obtain actionable screening for brackish drinking sources and salt-affected plots. Agencies gain georeferenced salinity observations from places with no monitoring. Beneficiaries include camp learning centres, adult vocational programmes, agricultural extension workers and humanitarian WASH teams.

## Potential Applications & Impact
Beyond humanitarian settings, the dual-droplet isopiestic module is an enabling technique in several areas:
- low-cost osmometry for veterinary and food uses (brines, syrups, milk adulteration screening);
- water-activity measurement on microlitre samples in pharmaceutical formulation;
- teaching laboratories in physical chemistry;
- hygroscopicity screening of fertilisers and salts;
- citizen-science salinity networks along deltas and coasts.

The osmole-staircase concept offers geochemists a tabletop, synchrotron-free way to pre-screen brine evolution paths. Because the readout is ratiometric and camera-based, any levitator can adopt the method as software plus a sealed lid. Open publication prevents enclosure of a measurement primitive, the co-levitated activity reference, on which other containerless assays could build. Examples are reagent-in-droplet colorimetry at a defined preconcentration factor and controlled-supersaturation crystallisation screening.

## Market/Adoption Feasibility (If Applicable)
All hardware is commodity: 40 kHz transducers, a microcontroller, an H-bridge driver, an LED, a printed or moulded chamber and a clip-on macro lens. Open TinyLev documentation lowers the build barrier, and local assembly in maker spaces is plausible. Recurring cost is near zero. Barriers are run time compared with a conductivity pen, user training for droplet loading, variability in phone optics, and regulatory non-acceptance of screening-grade data. Adoption levers are bundling with existing education-in-emergencies programmes, offline-first software with guided capture, and interoperable export formats so data can enter open water-quality repositories. The instrument should be positioned as a screening and learning tool that complements certified testing, not a replacement for it.

## Risk & Counterarguments
- **Bias from precipitation.** Hard waters precipitate before the first rung, so Ω underestimates total dissolved solids. The staircase flags this but quantifies it only semi-quantitatively.
- **Interferences.** Surfactant- or organic-rich samples may form skins that retard evaporation and fake plateaus. Volatile solutes such as ammonia or CO₂ exchange with the gas phase.
- **Thermal and droplet stability.** Transducer heating may create gradients. Droplets can drift, coalesce or atomise at excessive drive.
- **Accuracy.** A conductivity pen is faster and may be more accurate for plain salinity.
- **Safety scope.** The device does not detect pathogens, arsenic, fluoride or heavy metals at health-relevant levels. Clear labelling must prevent false reassurance about potability.
- **Data ethics.** Location-tagged data from displaced people requires consent and protection.

## Open Questions & Future Research Directions
- What is the achievable accuracy across real phone cameras and climates?
- Which reference composition and size are best? Glycerol, NaCl and CaCl₂ are candidates, and a dual reference could cover a_w from 0.2 to 0.99.
- How reproducible are efflorescence points for natural mixed waters, and can a learned classifier map staircase and deliquescence signatures to major-ion facies when validated against ion chromatography?
- How large are inter-node temperature differences under streaming?
- Can larger arrays run several samples per reference?
- Can a single microdosed indicator at a defined concentration factor extend the method to nitrate, fluoride or pH?
- Can aerosol-collector droplets reach useful sensitivity?
- Do long-term community time series resolve seasonal intrusion fronts?

## Novelty Threshold Justification
**Medium Novelty.** The closest prior art has three strands:
- comparative-kinetics electrodynamic balances using sequential probe droplets in conditioned gas flow (Rovelli et al., recalled);
- [levitated-droplet evaporite studies read by synchrotron XRD](https://pubs.acs.org/cgdefu/article/22/4/2307/377116/A-Comprehensive-Methodology-for-Monitoring);
- [multi-droplet acoustic levitation mechanics](https://www.mdpi.com/2072-666X/13/9/1373).

The three searches found no publication of the following, which are the new elements:
1. a simultaneously co-levitated non-efflorescing reference droplet acting as hygrometer in an unconditioned sealed acoustic chamber;
2. the ratiometric osmole invariant Ω tracked across desiccation rungs to quantify unknown samples;
3. precipitation-step and deliquescence classification of water type without reagents or spectroscopy.

Three searches cannot establish absence, particularly in the patent literature.

## References & Prior Art Checks
From recall:
- Marzo, Barnes & Drinkwater, "TinyLev", Rev. Sci. Instrum. (2017).
- Rovelli, Miles, Reid & Clegg, J. Phys. Chem. A (2016).
- Robinson & Stokes, *Electrolyte Solutions*.
- Greenspan, J. Res. NBS (1977).
- Hardie & Eugster (1970).
- Trinh and Marston, drop-oscillation tensiometry.

Found by search:
- Yarin et al., J. Fluid Mech. 399 (1999): https://www.tugraz.at/fileadmin/user_upload/Institute/ISW/Forschung/Forschungseinrichtungen/Jfm.pdf
- Getenet et al., Cryst. Growth Des. (2022): https://pubs.acs.org/cgdefu/article/22/4/2307/377116/A-Comprehensive-Methodology-for-Monitoring
- Water–NaCl levitated drying: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9048286/
- Glycerol repartitioning: https://royalsocietypublishing.org/rsos/article/5/1/170819/93729/
- Hasegawa & Murata (2022): https://www.mdpi.com/2072-666X/13/9/1373
- TinyLev water droplets: https://arxiv.org/pdf/2302.12204

**Prior art searched:**
1. "acoustically levitated droplet isopiestic water activity measurement reference droplet co-levitated osmolality". Used Hasegawa & Murata and Yarin et al. No isopiestic co-levitation method was found.
2. "acoustic levitation low-cost water quality analysis droplet evaporation total dissolved solids salinity TinyLev education field instrument". Used the water–NaCl drying paper and TinyLev studies. No field water-quality levitator was found.
3. "levitated droplet efflorescence deliquescence natural water sample evaporite precipitation sequence identification hydrochemical type glycerol reference hygrometer droplet". Used Getenet et al. and the glycerol repartitioning paper. No reference-droplet classification method was found.

---

### About the Reports
Each innovation on Unpatentable.org is published as a three-part open documentation set:
- **Innovation Report** – the master blueprint describing the first principals concept, mechanism, and rationale behind the invention.
- **Implementation Guide** – a step-by-step, practical manual detailing how to build or prototype the innovation. Includes estimated cost breakdown.
- **Industry Impact Report** – an analytical overview exploring the potential economic, industrial, and societal effects of the innovation.

Together, these documents form a complete public disclosure package — enabling researchers, developers, and policymakers to understand, replicate, and build upon each invention.

---

### Explore this Innovation
- [Innovation Report](https://unpatentable.org/innovation/co-levitated-reference-droplet-isopiestic-analyzer-for-reagent-free-field-hydrochemistry)
- [Implementation Guide](https://unpatentable.org/innovation/implementation-guide-co-levitated-reference-droplet-isopiestic-analyzer-for-reagent-free-field-hydrochemistry)
- [Industry Impact Report](https://unpatentable.org/innovation/industry-impact-report-co-levitated-reference-droplet-isopiestic-analyzer-for-reagent-free-field-hydrochemistry)

### Download PDFs
- [Innovation Report (PDF)](https://unpatentable.org/wp-content/uploads/2026/11/Co-Levitated-Reference-Droplet-Isopiestic-Analyzer-for-Reagent-Free-Field-Hydrochemistry.pdf)
- [Implementation Guide (PDF)](https://unpatentable.org/wp-content/uploads/2026/11/Implementation-Guide-Co-Levitated-Reference-Droplet-Isopiestic-Analyzer-for-Reagent-Free-Fi.pdf)
- [Industry Impact Report (PDF)](https://unpatentable.org/wp-content/uploads/2026/11/Industry-Impact-Report-Co-Levitated-Reference-Droplet-Isopiestic-Analyzer-for-Reagent-Free-.pdf)

---

**Timestamps:**
- [View Main Innovation Report on Arweave](https://arweave.net/PtxTuq6kxC1ewcX719-TYfPwlYn2ih9wwqesB7R8Ovw)
- [View Implementation Guide on Arweave](https://arweave.net/SH57Tjk2Zw41S8AinVooRFHXFXtLCs3TTaGDBR7sV-E)

**Suggested Citation:**
> Unpatentable.org (2026). *Co-Levitated Reference Droplet Isopiestic Analyzer for Reagent-Free Field Hydrochemistry.* Defensive Publication Series.
> https://unpatentable.org/innovation/co-levitated-reference-droplet-isopiestic-analyzer-for-reagent-free-field-hydrochemistry

---

```json
{
  "domain": "Human-Centered Technologies",
  "subdomain": "Lifelong Learning",
  "published": "2026-11-23",
  "arweave_main_tx": "PtxTuq6kxC1ewcX719-TYfPwlYn2ih9wwqesB7R8Ovw",
  "license": "CC BY 4.0",
  "arweave_implementation_tx": "SH57Tjk2Zw41S8AinVooRFHXFXtLCs3TTaGDBR7sV-E",
  "value_unlocked": "$9.6B"
}
```

Unpatentable.org is a public library of timestamped defensive publications —
open innovations released into the commons to prevent monopolization, democratize knowledge, and accelerate human progress.

License: CC BY 4.0
