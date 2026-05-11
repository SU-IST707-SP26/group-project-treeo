I know you pivoted from LA to NYC very late in the semester because you couldn't find force deployment data for LA. That's a hard pivot to pull off in a few days, and the fact that you have a coherent project framing, a working pipeline, a results table, and an honest discussion section — all on a different dataset than you'd been working on all semester — is a real accomplishment. Your grade reflects these considerations.

The central question you sought to answer is great - how much unique variance does police deployment explain over and above the structural patterns of where crime is reported? That's precisely the question I was hoping you'd be able to ask back at the checkpoint, and it's a sophisticated framing that engages directly with the predictive-policing literature. Your lit review on Lum & Isaac and Haskins is one of the more engaged ones I read.

But the way the experiment was set up means the headline finding ("97.73% of hotspots persist when deployment is zeroed -> hotspots are structural") doesn't really test the hypothesis you're proposing. Let me walk through why, then I want to talk about what I think is actually a reasonable conclusion from your data and where I think the gap is.

## The counterfactual can't carry the weight you're putting on it

Your `XGBoost (with deployment)` feature importance shows:

- `rolling_30d_mean`: 0.41
- `rolling_7d_mean`: 0.24
- `lag_7d`, `lag_1d`: ~0.07 each
- temporal features (weekend, day_of_week, etc.): the rest
- `estimated_officers`: 0.0066
- `% of command`: 0.0049

The model has learned that today's arrest count is mostly a function of yesterday's and last month's arrest count. The deployment features combined account for about 1% of the importance the model is using. When you then re-predict with deployment zeroed and find that 97.73% of hotspots remain, you're really just discovering that **zeroing features that the model barely uses doesn't change the model's predictions**. The persistence is a property of the model's reliance on lag features, not a property of the world.

To actually test the hypothesis "are hotspots structural or are they deployment-driven?" you'd need to break the loop between today's prediction and yesterday's data. A model without lag features — built from just spatial, temporal, and deployment features — would give deployment a chance to matter. Or a two-stage approach where you first residualize out the temporal autocorrelation and then see what deployment can explain in the residuals. Your bias-reduced model is actually the right instinct here — predict the deviation from expected rather than the absolute level — but when I looked at its feature importance, `deployment_norm` was 0.015, second-to-last. So even after you factor out the temporal trend, deployment doesn't really do much work. That's an interesting finding too! Just not the finding you wrote up.

A reasonable conclusion from what you actually showed is something like: "Within the resolution our data permits, precinct-level officer counts add essentially no predictive value beyond what is already captured by historical crime patterns at the grid level." The key here is that historical data is predictive of current data - but this path dependence could still be heavily influenced by deployment.  


## The precinct vs grid-cell mismatch

To be clear, I don't think there was a great solution to this problem, but I would have liked for you to reflect upon its implications a bit more. Your deployment data is only available at the precinct level — 77 precincts — and your target is at the grid-cell level — ~900 cells. That means all grid cells within the same precinct share an identical deployment value. So within-precinct variation in crime is mathematically unable to be explained by deployment at all, only between-precinct variation can be. With most of the variance you're modeling living within precincts (because precincts are large), this almost certainly drives the small delta-R^2 you observed.

You acknowledge the proxy limitation in the limitations section, which is good. The gap I'd push on is that you didn't think through what the proxy implies for what your variance-decomposition experiment can actually show. If 95% of the variance in your target is within-precinct and your deployment feature only varies between precincts, then a small delta-R^2 isn't evidence that deployment doesn't matter in the real world — it's a structural property of how the data are aggregated. That reframing is the kind of methodological self-criticism that would have lifted the discussion section substantially. To be fair, the right way to handle this would have been to also report between-precinct R^2 (with cells aggregated to precincts) as a complementary analysis; this is more than I'd expect you to figure out in a one-week pivot.

## Arrests are not crime

This is the one place where I think the lit review and the modeling don't quite line up. You correctly cite Lum & Isaac on the point that arrest data reflects where police went, not where crime happened. Then you proceed to call your target variable `crime_count` throughout the report and model it as if it were a measure of crime. The whole point of your project framing — separating "structural risk" from "deployment artifact" — is that arrests ARE the deployment artifact. You can't use arrests as ground truth for crime in a model whose purpose is to detect when arrests overrepresent crime due to deployment. This doesn't kill the project, but the framing should have been more careful about what "hotspot" means. A hotspot in your model is a high-arrest cell, not a high-crime cell, and those are different things — which is the entire problem your lit review identified.

## Strengths

- **Pivoted under time pressure and produced a working pipeline.** You accomplished a lot for a late pivot.  I would have loved to have seen what you could have done if you had pivoted earlier!
- **The conceptual framing is really strong.** Unique-variance decomposition for deployment vs structural is a sophisticated way to engage with the predictive-policing critique. 
- **Lit review is genuinely engaged with the literature.** Lum & Isaac, Haskins, and the Brennan Center piece are correctly cited, and you actually use them to motivate the modeling choices rather than just dropping them into a reference list.
- **Time-based train/test split.** Correct for temporal data. 
- **Counterfactual idea is creative.** Zeroing features and re-predicting is a reasonable instinct for variance decomposition. The execution was somewhat flawed, but the idea is right.
- **Bias-reduced relative-risk model.** Predicting residuals against a rolling-mean baseline is the right tool for trying to factor out temporal autocorrelation. You almost got to the right finding here — just didn't quite factor in your own feature importances.
- **Limitations section is honest.** Detection vs. deterrence, proxy limitations, causal limits, missing external factors — you flagged the important ones.

## Weaknesses

- **The headline finding (97.73% hotspots persist) is essentially a property of the model's reliance on lag features, not a test of the structural-vs-deployment hypothesis.** The conclusion overclaims what the experiment showed.
- **The precinct-level proxy structurally limits what your variance decomposition can detect, and the implications of that aren't worked through in the discussion.** Acknowledging the proxy as a data limit is good; reasoning about what it means for the experiment design is the next step.
- **`crime_count` is really `arrest_count`, and the lit review you cite is exactly about why those aren't the same thing.** The modeling treats arrests as ground truth for crime, which is the bias the lit review warned about.
- **Bias-reduced model's feature importance contradicts the narrative.** You describe deployment as playing "a more meaningful role in explaining deviations" but `deployment_norm` is 0.015 — second-to-last among the features. Weekend and day-of-week dominate.
- **No baselines.** The simplest baseline — "predict tomorrow's count = today's count" using just `lag_1d` — probably accounts for most of your R²=0.50. Without a baseline you can't really say what your model is contributing.
- **No uncertainty quantification.** delta-R^2 of ~0.0001 between with/without deployment, on a single train/test split, with no confidence interval. With this small a gap, the noise floor on a single split could easily flip the sign.
- **No subgroup analysis.** Are the persistent hotspots concentrated in particular boroughs or demographic areas? Given the lit review's emphasis on racial bias in predictive policing, this is the analysis I most wanted to see and didn't.

## Summary

The question you asked — "is this hotspot structural or is it an artifact of where we sent the police?" — is the right question for this domain, and your instincts about how to approach it (counterfactual simulation, residualization against expected) are good. The gap between asking the question well and answering it well is bigger than it seems, and in this case it requires breaking the model's dependence on the very lag features that the predictive-policing literature flags as the source of the bias. If you carry any version of this forward, the experiment I'd most like to see is a deployment model with NO lag features — just spatial, temporal, and deployment context — and a comparison of its performance to the lag-only model. The unique contribution of deployment lives in the gap between those two models, not in the counterfactual you ran.

The score reflects an ambitious project that mostly delivered, with a central finding that needs to be qualified more carefully than the report does. I do think you could have put time in earlier that would have led you to the NYC dataset, but once you made the pivot, you did good work under hard time pressure.

**Score: 26/30**


---

## Final Project Grade
| Assessment Item | Ashley Rauch | Madelyn Forster | Brealin Redecker |
|---|---|---|---|
| **Proposal (5 pts)** | 5 | 5 | 5 |
| **Midterm Report (10 pts)** | 10 | 10 | 10 |
| **Final Presentation (5 pts)** | 5 | 5 | 5 |
| **Final Report (30 pts)** | 26 | 26 | 26 |
| **Weekly Updates (30 pts)** | 30 | 28 | 25 |
| **Total (80 pts)** | **76** | **74** | **71** |
