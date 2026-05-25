---
layout: project-page
data_key: bolt
title: "BoLT: A Benchmark to Democratize Black-box Optimization Research for Expensive LLM Tasks"
---

<div class="section-heading" id="tasks"></div>

Critical decisions in the modern LLM pipeline, framed as optimization problems.
{: .section-tagline}

<div class="method-cards">
  <div class="method-card">
    <div class="method-card__title">Hyperparameter optimization</div>
    <div class="method-card__body" style="margin-top:0.75rem;">LoRA fine-tuning on Qwen3-4B/8B, evaluated on MATH-500.</div>
    <table>
      <thead>
        <tr><th>Problem</th><th>Dim</th><th>Challenges</th></tr>
      </thead>
      <tbody>
        <tr><td>HPO</td><td>7</td><td>mixed variables</td></tr>
        <tr><td>HPO-MF-Cont</td><td>8</td><td>mixed variables, multi-fidelity (continuous)</td></tr>
        <tr><td>HPO-MF-Disc</td><td>8</td><td>mixed variables, multi-fidelity (discrete)</td></tr>
      </tbody>
    </table>
  </div>
  <div class="method-card">
    <div class="method-card__title">Data mixture optimization</div>
    <div class="method-card__body" style="margin-top:0.75rem;">Search over instruction-following, math, and code proportions from TULU-3, evaluated on IFEval, MATH-500, and MBPP+.</div>
    <table>
      <thead>
        <tr><th>Problem</th><th>Dim</th><th>Challenges</th></tr>
      </thead>
      <tbody>
        <tr><td>DMO</td><td>6</td><td>simplex constraint</td></tr>
        <tr><td>DMO-MO</td><td>6</td><td>simplex constraint, multi-objective</td></tr>
        <tr><td>DMO-Het</td><td>6</td><td>simplex constraint, heteroscedastic noise</td></tr>
      </tbody>
    </table>
  </div>
  <div class="method-card">
    <div class="method-card__title">Prompt optimization</div>
    <div class="method-card__body" style="margin-top:0.75rem;">Discrete search over 5,014 pre-embedded prompts, using Matryoshka embeddings at four truncation dimensions (128–768).</div>
    <table>
      <thead>
        <tr><th>Problem</th><th>Dim</th><th>Challenges</th></tr>
      </thead>
      <tbody>
        <tr><td>PO-128</td><td>128</td><td>high-dimensional</td></tr>
        <tr><td>PO-256</td><td>256</td><td>high-dimensional</td></tr>
        <tr><td>PO-512</td><td>512</td><td>high-dimensional</td></tr>
        <tr><td>PO-768</td><td>768</td><td>high-dimensional</td></tr>
      </tbody>
    </table>
  </div>
</div>


<div class="section-heading" id="emulators"></div>

Backed by 20k+ real LLM experiments, queried in milliseconds.
{: .section-tagline}

Emulators fitted on real LLM runs reproduce the objective landscape at negligible query cost, validated via Spearman rank correlation on held-out test sets (ρ ≥ 0.72 across all tasks).
<div class="method-card method-card--centered method-card--surface-light">
  <div class="method-card__images" style="--img-max: 32%;">
    <img src="/assets/images/bolt/emulator_ternary_ifeval_p1_s1.png" alt="IFEval emulator landscape">
    <img src="/assets/images/bolt/emulator_ternary_math_p1_s0.png" alt="MATH-500 emulator landscape">
    <img src="/assets/images/bolt/emulator_ternary_code_p2_s1.png" alt="MBPP+ emulator landscape">
  </div>
  <p class="figure-caption"><strong>2D slices of the DMO emulator landscape</strong> across instruction-following, math, and code data proportions. The varied terrain reflects real trade-offs in the underlying LLM experiments.</p>
</div>

<div class="section-heading" id="results"></div>

BO methods consistently outperform baselines.
{: .section-tagline}

We benchmark 15+ Bayesian optimization (BO) and black-box methods across all 10 problems. Three key findings are presented here.

<div class="method-cards">
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">HPO</div>
    <img src="/assets/images/bolt/hpo_simple_legend.png" alt="HPO legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
    <img src="/assets/images/bolt/hpo_simple.png" alt="HPO results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">GP-based methods (LogNEI, MES, GIBBON) consistently outperform HPO baselines (TPE, CMA-ES), and any additional compute overhead is negligible compared to real LLM training costs.</div>
  </div>
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">DMO-MO</div>
      <img src="/assets/images/bolt/dm_mo_simple_legend.png" alt="DMO-MO legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
      <img src="/assets/images/bolt/dm_mo_simple.png" alt="DMO-MO results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">NEHVI matches NSGA2 using 50× fewer evaluations, with substantially tighter confidence intervals.</div>
  </div>
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">PO-768</div>
      <img src="/assets/images/bolt/po768_simple_legend.png" alt="PO legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
      <img src="/assets/images/bolt/po768_simple.png" alt="PO-768 results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">Trust-region methods (dTuRBO, dBAxUS) adapted for discrete candidate sets are essential, reaching near-optimal solutions within 200 iterations.</div>
  </div>
</div>


<div class="section-heading" id="get-started"></div>

Evaluate on [[bolt]].
{: .section-tagline}
![BoLT API example](/assets/images/bolt/bolt_api.png)
{: .figure-half .figure-right .no-border style="margin-top:0rem"}

[[bolt]] is built for BBO researchers. Every problem subclasses BoTorch's `BaseTestProblem`, so your existing code plugs straight in. Emulator weights and tabular data are fetched automatically from [HuggingFace](https://huggingface.co/collections/chewwt/bolt-models) on first use.

The benchmark is not limited to the 10 bundled problems. You can construct new optimization settings (constrained, contextual, etc.) using the public emulators or underlying data, without running any new LLM experiments.

Install the Python package, point your optimizer at a [[bolt]] problem, and you have a reproducible, grounded evaluation. See the [documentation](https://bolt-bench.readthedocs.io/en/latest/) to get started.
