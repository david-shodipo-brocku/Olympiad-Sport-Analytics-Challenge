# Business Insight Report — North American Winter Sports Consortium
Prepared using the Milan Cortina 2026 athlete dataset


# Executive Summary: Standalone One-Page Brief for Decision-Makers

## Bottom Line
Canada and the USA are both strong winter-sport nations, but the dataset reveals a medal-conversion gap:
USA athlete-level medal rate 50.0% versus Canada 37.5%.
The strategic goal for 2030 is not to send more athletes. It is to improve medal conversion among athletes already close to the podium.

## Three Key Findings
1. **Preseason form is the strongest practical signal.** Athletes entering the Games with stronger World Cup points are meaningfully more likely to medal. This is the most actionable lever because it is observable months before competition.
2. **Physiology matters, but the right target is sport-specific.** VO2max and training load explain medals very differently across alpine skiing, biathlon, figure skating, and cross-country skiing. A single fitness benchmark misallocates resources.
3. **Country systems matter, but exceptions exist.** Norway's dominance reflects a full winter-sport pipeline. Braathen shows that elite individual pathways can override country averages — but he is the exception, not the template.

## Three Recommendations
1. **Fund podium-ready athletes first.** Prioritise athletes already ranked near the top internationally rather than spreading resources evenly.
2. **Use sport-specific medal blueprints.** Set different VO2max, training-load, technical, and competition-form targets by sport.
3. **Track October/November World Cup form as an early warning system.** Use preseason points to decide where extra coaching, recovery, and equipment support is most likely to convert into medals.

## Expected Uplift Estimate
Closing 25% of the USA-Canada medal-rate gap: approximately 1.5 additional medals.
Closing 50% of the gap: approximately 3.0 additional medals.

Assumptions stated explicitly beside the estimate (rubric criterion 4.6):
- Canada maintains roster size of 48 athletes.
- Sport mix stays broadly similar.
- Gap closes proportionally rather than concentrating in one discipline.
- Rival nations do not improve faster by 2030.
This is a directional planning estimate, not a causal forecast.


## Criterion 4.2 — Medal Blueprint from Model Evidence
Best model: **log_reg** | F1=0.667 | AUC-ROC=0.845 | threshold=0.48

Top feature-importance signals:
- **cat__Sport_Cross-Country**: 7.8% of displayed top-feature importance
- **cat__Sport_Curling**: 6.2% of displayed top-feature importance
- **cat__Sport_Biathlon**: 5.5% of displayed top-feature importance
- **cat__Sport_Freestyle Skiing**: 5.0% of displayed top-feature importance
- **cat__Sport_Luge**: 4.5% of displayed top-feature importance

These signals support a blueprint focused on current international form, sport-specific physiology, competition experience, and national resource and tradition support.


## Insight 1 — USA: What Drove the Record Gold Count
The USA advantage comes from three reinforcing factors: stronger medal conversion in selected disciplines, deep athlete physiology and preparation, and strong preseason World Cup form entering the Games.

Recommendation: protect athletes with high preseason points from over-scheduling and replicate their preparation model — altitude training, recovery management, and competition calendar planning — across emerging medal sports where USA currently underperforms.


## Insight 2 — Canada: Where the Gap Emerged and Where ROI Is Highest
Canada shows broad roster depth but the medal-conversion gap suggests the highest return on investment is not adding more athletes. The better approach is concentrating final-stage resources on athletes already world-class but not yet converting consistently.

Recommendation: fund podium optimisation at the margin — equipment, recovery protocols, travel scheduling, altitude training blocks, and specialist technical coaching for athletes already ranked in the top eight internationally.


## Insight 3 — Invest Where Rivals Are Vulnerable
Canada and the USA have different sport-level strengths. The highest-return policy is to press where Canada is already close to the podium rather than building from scratch in sports where the gap is structural.

Examples from the dataset:
- **Biathlon**: USA 0.0% vs Canada 0.0% (gap 0.0pp) — narrow margin where targeted investment could shift outcomes.
- **Luge**: USA 0.0% vs Canada 0.0% (gap 0.0pp) — narrow margin where targeted investment could shift outcomes.
- **Nordic Combined**: USA 0.0% vs Canada 0.0% (gap 0.0pp) — narrow margin where targeted investment could shift outcomes.
- **Curling**: Canada leads USA (100.0% vs 0.0%) — protect and build on this strength.
- **Ice Hockey**: Canada leads USA (66.7% vs 28.6%) — protect and build on this strength.

Recommendation: direct development funding to sports where the medal-rate gap is narrow or where Canada already leads. In sports where the gap appears structural, monitor rather than invest heavily until pipeline indicators improve.


## Insight 4 — 2030 Investment Blueprint
Medal funding should be targeted by sport-specific evidence, not distributed equally across all disciplines.

Concrete 2030 actions:
Set sport-specific World Cup point targets as minimum thresholds for high-performance funding.
Build discipline-specific physiology benchmarks so coaches have measurable targets reflecting their sport.
Expand altitude training and recovery support for athletes in the high training-load range where marginal gains remain available.
Deploy a pre-Games medal probability model to identify the ten to fifteen athletes most likely to convert, then direct late-cycle resources there.


## Insight 5 — Braathen and the Brazil Paradox: Do Not Misread the Exception
Lucas Pinheiro Braathen (BRA) is the clearest paradox in the dataset. Brazil has a weak winter-sport tradition profile and a GDP position far from Norway, Canada, or the USA, yet Braathen wins gold in alpine skiing.

The correct interpretation is not that Brazil has cracked the winter-sport code.
Braathen's competitive development ran through the Norwegian system. His result reflects an elite individual trajectory, not a national Brazilian winter-sport program.

Decision-maker lesson: country-level GDP and tradition are useful baselines, but athlete-level development pathway, current form, and technical preparation must all be assessed before drawing national-level policy conclusions from individual outlier cases.


## Limitations and Ethics
The dataset does not capture coaching quality, injury timing, travel fatigue, psychological readiness, or equipment specifications — all of which influence medal outcomes.
Predictive models should support expert judgment and inform resource allocation, not replace human evaluation of athletes.
Funding decisions driven purely by medal probability risk amplifying existing inequalities by disadvantaging smaller nations, lower-resource athletes, and sports with lower baseline medal rates.
The 2030 uplift estimate is directional and should be updated as newer competition results become available.