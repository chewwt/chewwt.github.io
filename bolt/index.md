---
layout: project-page
data_key: bolt
title: "BoLT: A Benchmark to Democratize Black-box Optimization Research for Expensive LLM Tasks"
---

<div class="section-heading" id="tasks"></div>

Critical decisions in the modern LLM pipeline, framed as optimization problems.
{: .section-tagline}

<div class="method-cards method-cards--2col">
  <div class="method-card">
    <div class="method-card__title">Hyperparameter optimization <span class="keyword-tag" style="margin-left:0.4rem;vertical-align:middle;">MLP emulator</span></div>
    <div class="method-card__body" style="margin-top:0.75rem;">LoRA fine-tuning of Qwen3-4B/8B on OpenMathInstruct-2, evaluated on MATH-500.</div>
    <table>
      <thead>
        <tr><th>Problem</th><th>Dim</th><th>Challenges</th></tr>
      </thead>
      <tbody>
        <tr><td>HPO</td><td>7</td><td>mixed variables</td></tr>
        <tr><td>HPO-MF-Cont</td><td>8</td><td>mixed variables, continuous fidelity</td></tr>
        <tr><td>HPO-MF-Disc</td><td>8</td><td>mixed variables, discrete fidelity</td></tr>
      </tbody>
    </table>
  </div>
  <div class="method-card">
    <div class="method-card__title">Data mixture optimization <span class="keyword-tag" style="margin-left:0.4rem;vertical-align:middle;">MLP emulator</span></div>
    <div class="method-card__body" style="margin-top:0.75rem;">Two-stage mixtures of TULU-3 instruction, math, and code data, evaluated on IFEval, MATH-500, and MBPP+.</div>
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
    <div class="method-card__title">Prompt optimization <span class="keyword-tag" style="margin-left:0.4rem;vertical-align:middle;">Tabular</span></div>
    <div class="method-card__body" style="margin-top:0.75rem;">Discrete search over 5,014 prompts, using Matryoshka embeddings at four truncation dimensions (<span style="white-space:nowrap">128–768</span>).</div>
    <table>
      <thead>
        <tr><th>Problem</th><th>Dim</th><th>Challenges</th></tr>
      </thead>
      <tbody>
        <tr><td class="wrap">PO-128/<wbr>256/<wbr>512/<wbr>768</td><td>128–768</td><td>high-dimensional</td></tr>
      </tbody>
    </table>
  </div>
  <div class="method-card">
    <div class="method-card__title">Parallelism configuration optimization <span class="keyword-tag" style="margin-left:0.4rem;vertical-align:middle;">Tabular</span></div>
    <div class="method-card__body" style="margin-top:0.75rem;">Discrete search over parallelism configurations on 16–64 GPUs, maximizing training throughput without running out of memory.</div>
    <table>
      <thead>
        <tr><th>Problem</th><th>Dim</th><th>Challenges</th></tr>
      </thead>
      <tbody>
        <tr><td class="wrap">PCO-16/<wbr>32/<wbr>64</td><td>8</td><td>black-box constraint</td></tr>
      </tbody>
    </table>
  </div>
</div>


<div class="section-heading" id="emulators"></div>

MLP emulators backed by 22k+ real LLM experiments, queried in milliseconds.
{: .section-tagline}

They approximate the real objective landscape at negligible query cost, validated against real runs on held-out configurations (Spearman ρ ≥ 0.76, R² ≥ 0.63).
<div class="method-card method-card--centered method-card--surface-light">
  <div class="method-card__images" style="--img-max: 32%;">
    <img src="/assets/images/bolt/emulator_ternary_ifeval_p1_s1.png" alt="IFEval emulator landscape">
    <img src="/assets/images/bolt/emulator_ternary_math_p1_s0.png" alt="MATH-500 emulator landscape">
    <img src="/assets/images/bolt/emulator_ternary_code_p2_s1.png" alt="MBPP+ emulator landscape">
  </div>
  <p class="figure-caption"><strong>2D slices of the DMO emulator landscape</strong> across instruction-following, math, and code data proportions. The varied terrain reflects real trade-offs in the underlying LLM experiments.</p>
</div>

<div class="section-heading" id="results"></div>

BO generally wins, but no single method wins everywhere.
{: .section-tagline}

We benchmark 30+ Bayesian optimization (BO) and black-box methods across all 13 problems. Four key findings are presented here.

<div class="method-cards">
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">HPO</div>
    <img src="/assets/images/bolt/hpo_simple_legend.png" alt="HPO legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
    <img src="/assets/images/bolt/hpo_simple.png" alt="HPO results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">GP-based methods (GIBBON, UCB, LogEI) outperform HPO baselines (TPE, CMA-ES), and their compute overhead is negligible next to real LLM training costs.</div>
  </div>
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">DMO-MO</div>
    <img src="/assets/images/bolt/dm_mo_simple_legend.png" alt="DMO-MO legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
    <img src="/assets/images/bolt/dm_mo_simple.png" alt="DMO-MO results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">NSGA-II leads early, but NEHVI overtakes it after ~100 iterations while using 50× fewer evaluations per iteration.</div>
  </div>
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">PO-768</div>
    <img src="/assets/images/bolt/po768_simple_legend.png" alt="PO-768 legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
    <img src="/assets/images/bolt/po768_simple.png" alt="PO-768 results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">Trust-region methods adapted for discrete candidate sets (dTuRBO, dBAxUS) are essential, approaching the optimum within 200 iterations with batching.</div>
  </div>
  <div class="method-card method-card--surface-light">
    <div class="method-card__title">PCO-64</div>
    <img src="/assets/images/bolt/pco64_simple_legend.png" alt="PCO-64 legend" style="height:70px;width:100%;object-fit:contain;object-position:center;border:none;border-radius:0;">
    <img src="/assets/images/bolt/pco64_simple.png" alt="PCO-64 results" style="border:none;border-radius:0;">
    <div class="method-card__body" style="margin-top:0.75rem;">Near-optimal plateaus stall most methods behind random search, but parallelism priors help: UCB-C+prior finds the optimum in 5 of 10 seeds, up from 0.</div>
  </div>
</div>


<div class="section-heading" id="get-started"></div>

Evaluate on [[bolt]].
{: .section-tagline}
![BoLT API example](/assets/images/bolt/bolt_api.png)
{: .figure-half .figure-right .no-border style="margin-top:0rem"}

[[bolt]] is built for BBO researchers. Every problem subclasses BoTorch's `BaseTestProblem`, so your existing code plugs straight in. Emulator weights and tabular data are fetched automatically from [HuggingFace](https://huggingface.co/collections/Glow-AI/bolt) on first use.

The benchmark is not limited to the 13 bundled problems. You can construct new optimization settings (contextual, etc.) using the public emulators or underlying data, without running any new LLM experiments.

Install the Python package, point your optimizer at a [[bolt]] problem, and you have a reproducible, grounded evaluation. See the [documentation](https://bolt-bench.readthedocs.io/en/latest/) to get started.
