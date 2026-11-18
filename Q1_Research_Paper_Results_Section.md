# Section 4: Empirical Results and Discussion — Multi-Regime Survival Ensemble, CLV Portfolio Valuation, and Silent-Churn EWS

*100% Harmonized Against Verbatim 5-Fold Execution Logs ($N_{\text{train}} = 595{,}000$, $N_{\text{test}} = 255{,}000$)*

---

### 4.1 Non-Parametric Cohort Hazard Dynamics and Behavioral Stratification

Across $N = 595{,}000$ training accounts followed over $91$ days, **$30{,}994$ churn events ($5.21\%$)** and **$564{,}006$ right-censored accounts ($94.79\%$)** are observed (**Figure 4**). Churn concentrates sharply toward the terminal end of the quarter: **Early ($0\text{--}30\text{d}$)** accounts generate $286$ events ($0.92\%$ of churns; daily hazard $0.0016\%$), **Mid ($31\text{--}60\text{d}$)** generates $1{,}593$ ($5.14\%$; hazard $0.0089\%$), and **Late ($61\text{--}91\text{d}$)** accounts generate **$29{,}115$ ($93.94\%$; mean daily hazard $0.1621\%$)**—a **$101.3\times$ surge**. Churned timing quantiles verify late-boundary clustering ($\text{Min}=0$, $P_{25}=76.0$, $\text{Median}=83.0$, $\text{Mean}=79.98$, $P_{75}=88.0$, $\text{Max}=90$), peaking on **Day 90** ($3{,}565$ churns; instantaneous hazard $0.6281\%$).

![Cohort Timing Distribution, Instantaneous Hazard Rate, and Overall Kaplan-Meier Survival Curve](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig1_churn_timing_and_hazard_91d.png)
*Figure 4: Non-parametric 91-day cohort churn dynamics ($N = 595{,}000$). (Left) Daily churn event histogram highlighting Median Day 83 and Peak Day 90 ($3{,}565$ churns). (Center) Instantaneous daily hazard $h(t)$ and 7-day smoothed hazard. (Right) Overall Kaplan–Meier survival curve.*

Kaplan–Meier stratification (**Table 5**, **Figures 5–6**) confirms significant lifecycle separation across median vintage (`@1434d`: Log-Rank $\chi^2 = 4.77$, $p = 2.891 \times 10^{-2}$), a U-shaped activity hazard (`Low` $7.009\%$ vs. `Medium` $3.922\%$ vs. `High` $4.696\%$), and the **Zero-Balance Liquidity Paradox**: static funded wallets with `No Zero-Bal Days` experience **$8.803\%$ churn** ($0.9806$/1k person-days) versus **$4.451\%$** in active `Heavy Zero-Bal (>15d)` accounts ($0.4915$/1k days).

**Table 5: Non-Parametric Kaplan–Meier Survival and Person-Day Hazard Stratification ($N = 595{,}000$)**

| Stratification Group | Cohort Segment | Accounts ($n$) | Observed Churns | Churn Rate (%) | Hazard / 1k Person-Days | 90d KM Survival (%) |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Lifecycle Tenure** | `Growing (91-365d)` | $229$ | $15$ | $6.5502\%$ | $0.7252$ | $93.4498\%$ |
| *(Log-Rank $\chi^2=4.77$,* | `Established (1-3y)` | $97{,}303$ | $5{,}283$ | $5.4294\%$ | $0.6007$ | $94.5706\%$ |
| *$p=2.891\times 10^{-2}$)* | `Veteran (>3y)` | $497{,}468$ | $25{,}696$ | $5.1654\%$ | $0.5712$ | $94.8346\%$ |
| **Geographic Region** | `Dhaka` / `Barishal` | $208{,}593$ / $41{,}459$ | $11{,}006$ / $2{,}181$ | $5.2763\%$ / $5.2606\%$ | $0.5836$ / $0.5818$ | $94.7237\%$ / $94.7394\%$ |
| | `Rajshahi` / `Sylhet` | $59{,}724$ / $59{,}531$ | $3{,}112$ / $3{,}100$ | $5.2106\%$ / $5.2074\%$ | $0.5761$ / $0.5759$ | $94.7894\%$ / $94.7926\%$ |
| | `Khulna` / `Chattogram` | $53{,}230$ / $106{,}808$ | $2{,}749$ / $5{,}506$ | $5.1644\%$ / $5.1550\%$ | $0.5711$ / $0.5700$ | $94.8356\%$ / $94.8450\%$ |
| | `Mymensingh` / `Rangpur` | $35{,}603$ / $30{,}052$ | $1{,}827$ / $1{,}513$ | $5.1316\%$ / $5.0346\%$ | $0.5675$ / $0.5566$ | $94.8684\%$ / $94.9654\%$ |
| **Gender** | `Female` / `Male` / `Other` | $249{,}698$ / $327{,}309$ / $17{,}993$ | $13{,}128$ / $16{,}943$ / $923$ | $5.2576\%$ / $5.1765\%$ / $5.1298\%$ | $0.5815$ / $0.5724$ / $0.5672$ | $94.7424\%$ / $94.8235\%$ / $94.8702\%$ |
| **Activity Tier (`_act_tier`)** | `Low Activity` | $198{,}333$ | $13{,}902$ | **$7.0094\%$** | $0.7780$ | $92.9906\%$ |
| | `Medium Activity` | $198{,}333$ | $7{,}778$ | **$3.9217\%$** | $0.4325$ | $96.0783\%$ |
| | `High Activity` | $198{,}334$ | $9{,}314$ | $4.6961\%$ | $0.5189$ | $95.3039\%$ |
| **Zero-Bal Regime (`_zero_tier`)** | `No Zero-Bal Days` | $72{,}500$ | $6{,}382$ | **$8.8028\%$** | **$0.9806$** | **$91.1972\%$** |
| | `Moderate (1-15d)` | $96{,}464$ | $5{,}650$ | $5.8571\%$ | $0.6484$ | $94.1429\%$ |
| | `Heavy Zero-Bal (>15d)` | $426{,}036$ | $18{,}962$ | $4.4508\%$ | $0.4915$ | $95.5492\%$ |
| **Recency (`_rec_tier`)** | `Dormant / High Recency` | $224{,}064$ | $14{,}530$ | **$6.4848\%$** | $0.7191$ | $93.5152\%$ |
| | `Recent / Active` | $370{,}936$ | $16{,}464$ | $4.4385\%$ | $0.4900$ | $95.5615\%$ |

![Kaplan-Meier Survival and Smoothed Hazard Across Account Tenure](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig2_km_new_vs_old_customers.png)
*Figure 5: Lifecycle tenure validation via Kaplan–Meier and smoothed daily hazard rates (`<=1434d` vs `>1434d`, $\chi^2 = 4.77$, $p = 2.89\times 10^{-2}$).*

![Behavioral Smoothed Hazard Separation Across Activity, Zero-Balance, and Recency Strata](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig3_behavioral_segment_hazards.png)
*Figure 6: Seven-day smoothed instantaneous hazard $h(t)$ across activity tertiles, zero-balance regimes, and recency tiers ($N = 595{,}000$).*

### 4.2 Cross-Regime Multi-Paradigm Ablation Study (Regimes I vs. II vs. III)

**Tables 6–7** and **Figures 7–8** establish four key empirical findings: (1) 5-fold Super-Ensemble OOF C-index rises monotonically from **`0.76770`** (Regime I, $167\text{D}$) to **`0.76788`** (Regime II, $97\text{D}$) to **`0.76799`** (Regime III, $175\text{D}$ Procrustes Subspace RBF-KPCA, Phase-1 = `41.46/70`, exact IPCW IBS = `0.01324`); (2) Regime II reduces 5-fold runtime by **`31.8%`** (`62.57 min` vs. `91.70 min`) while surpassing the unpruned baseline; (3) Procrustes-aligned kernel coordinates unlock `L2_LGB_Meta` (`0.76753 -> 0.76786`), shifting its Powell rank weight from `0.0000` (Regimes I/II) to **`0.4124`** and 90-day Brier weight to **`0.5064`**; and (4) `hybrid` calibration (`0.5*lr + 0.5*iso`) achieves calibrated horizon Brier scores **`0.00048 / 0.00308 / 0.04632`** across Days 30/60/90.

**Table 6: Five-Fold Out-of-Fold Ablation Across 12 Architectures and Feature Regimes I–III ($N = 595{,}000$)**

| Model Level / Survival Paradigm | Reg. I ($167\text{D}$) OOF C-Idx | Reg. II ($97\text{D}$) OOF C-Idx | Reg. III ($175\text{D}$) OOF C-Idx | Reg. III Brier @30d | Reg. III Brier @60d | Reg. III Brier @90d | Reg. III Mean Brier | Reg. III Exact IPCW IBS |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| `LightGBM 90d` (L1 GBDT Binary) | $0.76709$ | $0.76736$ | **$0.76745$** | $0.00048$ | $0.00309$ | $0.04634$ | $0.01664$ | $0.01325$ |
| `LightGBM Multi-Horizon` (`H={30..90}`) | $0.76397$ | **$0.76407$** | $0.76405$ | $0.00048$ | $0.00309$ | $0.04634$ | $0.01664$ | $0.01325$ |
| `CatBoost Classifier` (`H={60,90}`) | $0.76431$ | **$0.76501$** | $0.76438$ | $0.00048$ | $0.00308$ | $0.04641$ | $0.01666$ | $0.01326$ |
| `XGBoost Binary 90d` (Depth-wise) | $0.76670$ | $0.76693$ | **$0.76696$** | $0.00048$ | $0.00311$ | $0.04636$ | $0.01665$ | $0.01326$ |
| `XGBoost AFT Survival` (Normal AFT) | $0.76683$ | $0.76709$ | **$0.76718$** | $0.00048$ | $0.00310$ | $0.04636$ | $0.01665$ | $0.01326$ |
| `XGBoost Cox PH` (Semi-Parametric) | $0.76606$ | $0.76635$ | **$0.76641$** | $0.00048$ | $0.00311$ | $0.04638$ | $0.01666$ | $0.01327$ |
| `Random Forest 90d` (Bagged Trees) | $0.76588$ | **$0.76619$** | $0.76603$ | $0.00048$ | $0.00309$ | $0.04640$ | $0.01665$ | $0.01326$ |
| `L1 Linear Rank Blend` | $0.76752$ | $0.76774$ | **$0.76779$** | $0.00048$ | $0.00311$ | $0.04638$ | $0.01665$ | $0.01327$ |
| `L2 LightGBM Meta-Stacker` | $0.76753$ | $0.76754$ | **$0.76786$** | $0.00048$ | $0.00309$ | $0.04634$ | $0.01663$ | $0.01325$ |
| `L2 XGBoost Cox Meta-Stacker` | $0.76746$ | $0.76745$ | **$0.76775$** | $0.00048$ | $0.00311$ | $0.04635$ | $0.01665$ | $0.01326$ |
| `L2 Random Forest Meta-Stacker` | $0.76760$ | **$0.76779$** | $0.76773$ | $0.00048$ | $0.00309$ | $0.04637$ | $0.01665$ | $0.01326$ |
| **`FINAL SUPER-ENSEMBLE`** | **`0.76770`** | **`0.76788`** | **`0.76799`** | **`0.00048`** | **`0.00308`** | **`0.04632`** | **`0.01663`** | **`0.01324`** |
| **Champion Composite & Runtime** | $41.44/70$ ($91.7\text{m}$) | $41.46/70$ (**$62.6\text{m}$**) | **$41.46/70$** ($101.7\text{m}$) | — | — | Reg. II: `0.04631` | Reg. II: `0.01662` | All: `0.01324` |

**Table 7: Optimal Simplex Meta-Weights, Horizon Calibrator Selection, and Fold Runtimes Across Regimes I–III**

| Regime | Powell `powell_l2` Rank Blend Weights (`L1`, `L2_LGB`, `L2_Cox`, `L2_RF`) | 90d Brier Weights (`LGB90`, `CB90`, `XGB90`, `RF90`, `L2_LGB`, `L2_RF`) | Selected OOF Calibrators (`30d` / `60d` / `90d`) | Fold Wall-Clock Times (Folds 1–5, sec) |
| :--- | :--- | :--- | :--- | :--- |
| **Regime I ($167\text{D}$)** | `0.6109` / `0.0000` / `0.2662` / `0.1229` | `[0.1765, 0.0933, 0.0712, 0.0862, 0.4282, 0.1446]` | `lr` / `hybrid` / `hybrid` | `1134.0, 1121.2, 1077.9, 1062.4, 1106.5` (`91.70m`) |
| **Regime II ($97\text{D}$)** | `0.6285` / `0.0000` / `0.0000` / `0.3715` | `[0.1430, 0.1537, 0.0949, 0.0000, 0.3272, 0.2812]` | `hybrid` / `hybrid` / `hybrid` | `756.7, 794.8, 733.0, 720.3, 749.1` (`62.57m`) |
| **Regime III ($175\text{D}$)** | `0.5876` / **`0.4124`** / `0.0000` / `0.0000` | `[0.2499, 0.0794, 0.0992, 0.0651, 0.5064, 0.0000]` | `hybrid` / `hybrid` / `hybrid` | `1248.7, 1202.2, 1219.3, 1218.5, 1212.6` (`101.69m`) |

![Cross-Regime Ablation C-Index, Training Runtime Frontier, and Optimal Brier Blend Weights](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig4_ablation_cindex_across_paradigms.png)
*Figure 7: Multi-paradigm ablation across Regimes I, II, and III ($N = 595{,}000$). (a) Concordance progression across all 12 architectures. (b) Pareto frontier comparing wall-clock runtime (`62.6m` vs. `101.7m`) and C-index. (c) 90-day Brier blend weights showing $50.64\%$ `L2_LGB` allocation in Regime III.*

![Top 20 Subspace RBF-KPCA Predictors and Horizon IPCW Brier Progression](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig_kpca_gain_and_ipcw_brier.png)
*Figure 8: Regime III predictor attributions (`kpca_rbf_05` at Rank #2) and Horizon IPCW Brier progression (`0.00048 -> 0.00308 -> 0.04632`).*

### 4.3 Feature Attribution, 4-Criterion Consensus Stability, and Manifold Gain Absorption

**Table 8** and **Table 9** (**Figure 9**) show that all 8 Subspace RBF-KPCA coordinates accumulate `123,023.31` split gain, anchored by `kpca_rbf_05` at Rank #2 overall (`83,331.51`, `67.74%` of total KPCA gain), while five RBF coordinates enter the Top 20 (`#2, #11, #12, #15, #19`). In Regime II, longitudinal velocity and activity metrics earn `5/5` fold selection (`txn_count_all = 0.98425`, `active_days_all = 0.97497`, `txn_count_90d = 0.96329`), while weak P2P inflow variables (`p2p_in_*`), `open_year`, and constant/zero-gain features (`n_balance_records`, `account_type_enc`) drop at `0/5` folds.

**Table 8: Cross-Regime Predictor Attribution (`LightGBM 90d` Gain) and 4-Criterion Consensus Audit**

| Rank (Reg. III) | Feature Identifier | Reg. III LGB90 Gain | Reg. I LGB90 Gain | Reg. II Folds & Consensus Score | Consensus / Behavioral Interpretation |
| :---: | :--- | :---: | :---: | :---: | :--- |
| **#1** | `txn_count_all` | **$124{,}105.03$** | $125{,}253.64$ | `5/5` ($S=0.98425$) | Primary structural engagement anchor ($I=0.0118$, $\text{Cox}=147.57$) |
| **#2** | **`kpca_rbf_05` (KPCA)** | **$83{,}331.51$** | *N/A* | *Regime III Manifold* | Dominant diagonal RBF interaction axis ($67.74\%$ of KPCA gain) |
| **#3** | `txn_amount_p25_all` | $47{,}778.99$ | $68{,}744.01$ | `5/5` ($S=0.87952$) | Lower-quartile spending floor separating micro-wallets from regular payers |
| **#4** | `txn_count_90d` | $27{,}299.10$ | $28{,}839.51$ | `5/5` ($S=0.96329$) | Quarter-scale outgoing cadence; highest mutual info ($I=0.0133$) |
| **#5** | `txn_count_30d` | $24{,}834.26$ | $27{,}834.23$ | `5/5` ($S=0.92347$) | Terminal 30-day activity velocity immediately prior to window close |
| **#6** | `txn_amount_median_all` | $24{,}689.32$ | $28{,}589.14$ | `5/5` ($S=0.85647$) | Median transaction ticket size anchoring user monetary tier |
| **#7** | `pct_micro_txn_lt100` | $16{,}216.85$ | $19{,}661.34$ | `5/5` ($S=0.94006$) | Habitual micro-utility reliance (`< 100` MU txns) |
| **#8** | `type_count_CashIn` | $15{,}135.82$ | $19{,}472.69$ | `5/5` ($S=0.78497$) | Wallet liquidity replenishment frequency (sticky funding loop) |
| **#9** | `decline_abs` | **$15{,}069.06$** | $9{,}513.81$ | *Not in Top-25 / Bottom-10 printout* | Absolute transaction decay delta amplified by orthogonal KPCA conditioning |
| **#10** | `txn_diff_region_med` | $11{,}305.05$ | $15{,}518.30$ | *Not in Top-25 / Bottom-10 printout* | Local purchasing-power deviation vs. geographic regional median |
| **#11** | **`kpca_rbf_00` (KPCA)** | **$10{,}509.37$** | *N/A* | *Regime III Manifold* | Secondary orthogonal RBF manifold mode |
| **#12** | **`kpca_rbf_01` (KPCA)** | **$10{,}152.19$** | *N/A* | *Regime III Manifold* | Tertiary orthogonal RBF manifold mode |
| **#13** | `active_days_all` | $10{,}049.83$ | $13{,}348.17$ | `5/5` ($S=0.97497$) | Cumulative active calendar breadth (`Cox=104.39`) |
| **#14** | `type_count_MerchantPay` | $6{,}974.33$ | $6{,}792.67$ | `5/5` ($S=0.80641$) | Retail merchant payment lock-in frequency |
| **#15** | **`kpca_rbf_04` (KPCA)** | **$6{,}276.90$** | *N/A* | *Regime III Manifold* | Fifth-largest RBF manifold component |
| *Pruned* | `bal_min_30d`, `p2p_in_*`, `open_year`, `n_balance_records`, `account_type_enc` | — | *Weak / Zero Split* | `0/5` ($S \le 0.15329$ to $-1.0$) | Cleanly rejected below 85th-percentile permutation shadow gate |

**Table 9: Spectral Split-Gain Concentration Across All 8 Procrustes-Aligned Subspace RBF-KPCA Axes**

| Kernel Axis | 5-Fold Avg LGB90 Split Gain | Overall Rank (out of 175) | Share of Total KPCA Gain | Cumulative KPCA Gain Share |
| :--- | :---: | :---: | :---: | :---: |
| **`kpca_rbf_05`** | **`83,331.51`** | **#2** | **67.74%** | 67.74% |
| **`kpca_rbf_00`** | **`10,509.37`** | **#11** | 8.54% | 76.28% |
| **`kpca_rbf_01`** | **`10,152.19`** | **#12** | 8.25% | 84.53% |
| **`kpca_rbf_04`** | **`6,276.90`** | **#15** | 5.10% | 89.63% |
| **`kpca_rbf_03`** | **`5,395.94`** | **#19** | 4.39% | 94.02% |
| **`kpca_rbf_07`** | `3,277.83` | #34 | 2.66% | 96.68% |
| **`kpca_rbf_06`** | `2,222.80` | #43 | 1.81% | 98.49% |
| **`kpca_rbf_02`** | `1,856.77` | #54 | 1.51% | **100.00%** |
| **Total 8D Manifold** | **`123,023.31`** | *5 in Top 20* | **100.00%** | — |

![Top 15 Feature Importances in Regime III and 4-Criterion Consensus Audit](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig5_feature_importance_and_consensus_audit.png)
*Figure 9: Predictor attribution and stability audit across Regime III Top 15 features and Regime II `5/5` retained vs. `0/5` pruned noise covariates.*

### 4.4 Survival-Adjusted Customer Lifetime Value (CLV) and Capital Allocation Matrix

Across **$850{,}000$ accounts**, the CLV engine yields **`13.646B` MU** total 12-month CLV (`16,054.28` mean; `9.556B` Train vs. `4.090B` Holdout) alongside **`1.439B` MU** 12-month Value-at-Risk and a **`90.46%` Retention Capture Ratio** differing by only $4\text{ bps}$ between Train OOF (`90.45%`) and Holdout (`90.49%`; **Table 10**, **Figure 10**). Top $20\%$ accounts concentrate $81.1\%$ of 12-month CLV, while the top three priority/VIP segments (`232,672` accounts, `27.37%` of the base) concentrate **`1,141.48M` MU (`79.34%` of total VaR)** (**Table 11**), enabling disciplined priority concierge saves (**Table 12**).

**Table 10: Ecosystem CLV Valuation Summary ($N_{\text{total}} = 850{,}000$) and 12-Month Survival-Discounting Waterfall**

| Panel A: Portfolio Valuation Summary | Accounts | Mean Mo. Fee Rev | Mean 6M CLV | Mean 12M CLV | Total 6M CLV | Total 12M CLV | Total 12M VaR | Retention Capture Ratio |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Train (OOF)** | $595{,}000$ | $1{,}577.56$ | $8{,}744.90$ | $16{,}060.25$ | $5{,}203{,}216{,}031.68$ | $9{,}555{,}851{,}597.71$ | $1{,}008{,}693{,}839.39$ | $90.45\%$ |
| **Holdout (Test)** | $255{,}000$ | $1{,}574.98$ | $8{,}732.78$ | $16{,}040.35$ | $2{,}226{,}860{,}129.63$ | $4{,}090{,}290{,}423.58$ | $429{,}976{,}827.09$ | $90.49\%$ |
| **Combined Ecosystem** | **$850{,}000$** | **$1{,}576.79$** | **$8{,}741.27$** | **$16{,}054.28$** | **$7{,}430{,}076{,}161.31$** | **$13{,}646{,}142{,}021.29$** | **$1{,}438{,}670{,}666.48$** | **$90.46\%$** |

| Panel B: Selected Months of 12M Waterfall | Month 1 | Month 2 | Month 3 (Obs.) | Month 4 (Extr.) | Month 6 Milestone | Month 9 | Month 12 Terminal |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Mean Survival $\hat{S}(t)$ (%)** | $99.95\%$ | $99.68\%$ | $94.79\%$ | $91.76\%$ | $86.24\%$ | $79.11\%$ | $73.08\%$ |
| **Discount Factor $(1+r)^{-t}$** | $0.99$ | $0.98$ | $0.97$ | $0.96$ | $0.94$ | $0.91$ | $0.89$ |
| **Gross Potential PV (MU)** | $1{,}326{,}997{,}361.14$ | $1{,}313{,}858{,}773.40$ | $1{,}300{,}850{,}270.70$ | $1{,}287{,}970{,}565.05$ | $1{,}262{,}592{,}456.67$ | $1{,}225{,}459{,}799.29$ | $1{,}189{,}419{,}207.87$ |
| **Expected Survival CLV (MU)** | $1{,}326{,}823{,}369.53$ | $1{,}309{,}513{,}038.66$ | $1{,}254{,}547{,}881.97$ | $1{,}215{,}815{,}995.59$ | $1{,}144{,}244{,}591.43$ | $1{,}048{,}871{,}331.77$ | $965{,}221{,}559.36$ |
| **Churn Attrition Loss / VaR (MU)** | $173{,}991.61$ | $4{,}345{,}734.74$ | $46{,}302{,}388.73$ | $72{,}154{,}569.45$ | $118{,}347{,}865.23$ | $176{,}588{,}467.52$ | $224{,}197{,}648.51$ |

**Table 11: 12-Cell Value Tier ($\text{Q1--Q4}$) $\times$ Churn Risk Tier Retention Strategy Matrix ($N_{\text{total}} = 850{,}000$)**

| Value Tier $\times$ Churn Risk Tier | Recommended Retention Action | Accounts | Avg $\hat{S}(90\text{d})$ | Avg Mo. Rev | Mean 12M CLV | Total 12M CLV (MU) | Total 12M VaR (MU) | Max CAC Budget |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| `VIP Top (Q4)` $\times$ `High Risk` | **Priority Concierge Save** | $57{,}330$ | $90.14\%$ | $3{,}200.73$ | $27{,}289.67$ | $1{,}564{,}516{,}739.42$ | **$500{,}764{,}725.48$** | **$2{,}183.69$** |
| `VIP Top (Q4)` $\times$ `Mod. Risk` | VIP Loyalty & Cross-Sell Nurture | $88{,}049$ | $96.38\%$ | $3{,}862.16$ | $39{,}080.39$ | $3{,}440{,}989{,}179.48$ | **$386{,}404{,}221.06$** | $1{,}097.13$ |
| `High Value (Q3)` $\times$ `High Risk` | **Priority Concierge Save** | $87{,}293$ | $88.33\%$ | $902.20$ | $7{,}240.98$ | $632{,}086{,}721.18$ | **$254{,}311{,}276.38$** | $728.33$ |
| `VIP Top (Q4)` $\times$ `Low Risk` | VIP Loyalty & Cross-Sell Nurture | $67{,}121$ | $99.05\%$ | $9{,}036.01$ | $98{,}890.76$ | $6{,}637{,}646{,}724.65$ | $188{,}624{,}837.25$ | $702.56$ |
| `High Value (Q3)` $\times$ `Mod. Risk` | VIP Loyalty & Cross-Sell Nurture | $45{,}752$ | $96.43\%$ | $678.58$ | $6{,}780.43$ | $310{,}218{,}025.20$ | $39{,}212{,}424.25$ | $214.27$ |
| `Mid-Low (Q2)` $\times$ `Mod. Risk` | Automated Fee Rebate / Cashback | $73{,}407$ | $96.65\%$ | $202.14$ | $2{,}044.39$ | $150{,}072{,}605.27$ | $16{,}932{,}790.13$ | $57.67$ |
| `High Value (Q3)` $\times$ `Low Risk` | VIP Loyalty & Cross-Sell Nurture | $79{,}455$ | $99.26\%$ | $587.98$ | $6{,}426.71$ | $510{,}634{,}584.67$ | $15{,}176{,}306.32$ | $47.75$ |
| `Mid-Low (Q2)` $\times$ `High Risk` | Automated Fee Rebate / Cashback | $24{,}724$ | $90.78\%$ | $203.06$ | $1{,}731.66$ | $42{,}813{,}681.41$ | $13{,}691{,}537.64$ | $138.44$ |
| `Low Value (Q1)` $\times$ `High Risk` | Organic Digital Monitoring (Zero Spend) | $113{,}987$ | $88.04\%$ | $27.45$ | $228.45$ | $26{,}040{,}749.21$ | $9{,}179{,}270.10$ | $20.13$ |
| `Mid-Low (Q2)` $\times$ `Low Risk` | Organic Digital Monitoring (Zero Spend) | $114{,}369$ | $99.16\%$ | $214.69$ | $2{,}342.58$ | $267{,}918{,}118.41$ | $8{,}432{,}866.73$ | $18.43$ |
| `Low Value (Q1)` $\times$ `Mod. Risk` | Organic Digital Monitoring (Zero Spend) | $76{,}125$ | $96.35\%$ | $57.14$ | $575.61$ | $43{,}818{,}107.67$ | $5{,}139{,}005.27$ | $16.88$ |
| `Low Value (Q1)` $\times$ `Low Risk` | Organic Digital Monitoring (Zero Spend) | $22{,}388$ | $98.75\%$ | $80.12$ | $865.95$ | $19{,}386{,}784.73$ | $801{,}405.88$ | $8.95$ |

**Table 12: Top 15 Holdout Accounts Ranked by 12-Month Churn Value-at-Risk ($\text{VaR}_{12\text{M}}$)**

| Rank | Account ID | Monthly Fee Rev | $\hat{S}(90\text{d})$ | $\text{CLV}_{6\text{M}}$ | $\text{CLV}_{12\text{M}}$ | 12M Value-at-Risk | Max Retention Budget (25% Cap) |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | `CUST00033831` | $20{,}077.66$ | $0.51$ | $62{,}847.38$ | $67{,}493.67$ | **$158{,}481.98$** | $39{,}620.49$ |
| 2 | `CUST00703530` | $17{,}582.64$ | $0.27$ | $42{,}620.96$ | $42{,}985.06$ | **$154{,}908.88$** | $38{,}727.22$ |
| 3 | `CUST00625119` | $16{,}813.50$ | $0.44$ | $48{,}609.76$ | $50{,}733.97$ | **$138{,}503.25$** | $34{,}625.81$ |
| 4 | `CUST00544010` | $18{,}629.88$ | $0.68$ | $71{,}299.52$ | $86{,}261.73$ | $123{,}418.98$ | $30{,}854.75$ |
| 5 | `CUST00774549` | $15{,}349.29$ | $0.50$ | $47{,}184.89$ | $50{,}322.93$ | $122{,}434.52$ | $30{,}608.63$ |
| 6 | `CUST00353464` | $13{,}777.39$ | $0.29$ | $33{,}884.87$ | $34{,}237.07$ | $120{,}828.55$ | $30{,}207.14$ |
| 7 | `CUST00506769` | $14{,}026.48$ | $0.44$ | $40{,}482.25$ | $42{,}231.97$ | $115{,}637.11$ | $28{,}909.28$ |
| 8 | `CUST00269151` | $14{,}541.13$ | $0.50$ | $45{,}155.64$ | $48{,}339.60$ | $115{,}321.97$ | $28{,}830.49$ |
| 9 | `CUST00778073` | $11{,}413.81$ | $0.12$ | $24{,}118.09$ | $24{,}133.90$ | $104{,}329.36$ | $26{,}082.34$ |
| 10 | `CUST00563963` | $12{,}694.40$ | $0.47$ | $38{,}020.16$ | $40{,}165.50$ | $102{,}710.91$ | $25{,}677.73$ |
| 11 | `CUST00281987` | $12{,}100.59$ | $0.43$ | $34{,}641.35$ | $36{,}065.01$ | $100{,}128.01$ | $25{,}032.00$ |
| 12 | `CUST00451978` | $14{,}348.61$ | $0.68$ | $54{,}773.17$ | $66{,}154.77$ | $95{,}339.96$ | $23{,}834.99$ |
| 13 | `CUST00499196` | $12{,}359.19$ | $0.55$ | $40{,}565.25$ | $44{,}560.19$ | $94{,}543.45$ | $23{,}635.86$ |
| 14 | `CUST00167526` | $11{,}086.33$ | $0.40$ | $30{,}509.03$ | $31{,}446.92$ | $93{,}330.57$ | $23{,}332.64$ |
| 15 | `CUST00068238` | $16{,}494.44$ | $0.76$ | $70{,}009.43$ | $92{,}684.60$ | $92{,}961.59$ | $23{,}240.40$ |

![12-Month CLV Pareto Concentration, Cashflow Waterfall, and Retention Value-Risk Matrix](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig_clv_pareto_waterfall_matrix.jpg)
*Figure 10: Portfolio CLV valuation results ($N_{\text{total}} = 850{,}000$). (Left) Top $20\%$ accounts drive $81.1\%$ of 12-month CLV. (Center) Monthly discounted survival cashflow vs. attrition VaR. (Right) Mean 12-month VaR retention heatmap.*

### 4.5 Early Warning System (EWS) Validation, Lead-Time Capture, and Live Intervention Queue

Auditing EWS triggers (**Tables 13–15**, **Figure 11**) shows that univariate balance drops ($\ge 50\%$ vs Jan) fire across `60.82%` of wallets at `0.97x` lift (`5.07%` churn) due to routine salary cash-outs, whereas inactivity recency (`Recency >= 30d`: `3.22x` lift, `16.78%` churn) and multi-signal corroboration (`1.96x` lift) isolate pathological decay. The fused `EWS_Risk_Score` achieves **`3.42x` lift (`17.83%` churn) in `CRITICAL RED`** (`97.13%` $\ge 30\text{d}$ lead-time capture, Median `79.00` days) and **`2.23x` lift (`11.61%` churn) in `HIGH ORANGE`** (`98.85%` early capture), capturing **`59.96%` (`18,584 / 30,994`) of churns within `25.75%` of accounts** and separating `CRITICAL RED` (`17.83%`) vs. `GREEN HEALTHY` (`1.67%`) by **`10.68x`**.

**Table 13: Empirical Validation of Silent-Churn Behavioral Triggers and Inactivity Recency Tiers ($N = 595{,}000$)**

| Behavioral Trigger / Recency Tier (Train OOF $N=595{,}000$) | Flagged Accounts | Cohort Share | Observed Churns | Churn Rate (%) | Risk Lift | Hazard / 1k Days (or Mean EWS) | Median Event Day (or Mean $\hat{S}_{90}$) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| `Balance Drop >= 50% (30d/Mar vs Jan)` | $361{,}883$ | $60.82\%$ | $18{,}340$ | $5.07\%$ | $0.97\times$ | $0.56$ / 1k d | Day $83.00$ |
| `Weekly Freq Collapse (Jan>=2 -> Mar<=1)` | $3{,}472$ | $0.58\%$ | $152$ | $4.38\%$ | $0.84\times$ | $0.48$ / 1k d | Day $84.00$ |
| `Weekly Freq >= 50% Contraction` | $22{,}786$ | $3.83\%$ | $1{,}278$ | $5.61\%$ | $1.08\times$ | $0.62$ / 1k d | Day $83.00$ |
| `Multi-Signal Decay (>=2 Triggers)` | $32{,}420$ | $5.45\%$ | $3{,}304$ | **$10.19\%$** | **$1.96\times$** | $1.14$ / 1k d | Day $81.00$ |
| `Zero Decay Triggers (Stable Baseline)` | $211{,}474$ | $35.54\%$ | $10{,}215$ | $4.83\%$ | $0.93\times$ | $0.53$ / 1k d | Day $84.00$ |
| **`TRX_RECENCY_DAYS`: Active ($0\text{--}6\text{d}$)** | $524{,}915$ | $88.22\%$ | $23{,}994$ | $4.57\%$ | $0.88\times$ | Mean EWS `38.83` | $\bar{S}(90\text{d}) = 95.43\%$ |
| **`TRX_RECENCY_DAYS`: Watchlist ($7\text{--}14\text{d}$)** | $40{,}620$ | $6.83\%$ | $3{,}195$ | $7.87\%$ | $1.51\times$ | Mean EWS `54.64` | $\bar{S}(90\text{d}) = 92.21\%$ |
| **`TRX_RECENCY_DAYS`: Tier-2 Yellow ($15\text{--}29\text{d}$)** | $21{,}104$ | $3.55\%$ | $2{,}402$ | **$11.38\%$** | **$2.18\times$** | Mean EWS `67.53` | $\bar{S}(90\text{d}) = 88.56\%$ |
| **`TRX_RECENCY_DAYS`: Tier-1 Red ($\ge 30\text{d}$)** | $8{,}361$ | $1.41\%$ | $1{,}403$ | **$16.78\%$** | **$3.22\times$** | Mean EWS `80.35` | $\bar{S}(90\text{d}) = 82.85\%$ |

**Table 14: Preventive $\ge 30$-Day Lead-Time Validation (Train OOF) and Live Holdout EWS Dispatch Queue**

| Panel A: Train OOF Lead-Time ($N=595{,}000$) | Train Accounts | Observed Churns | Churn Rate (%) | Risk Lift | Median Lead (Days) | P25 / P75 Lead | Captured $\ge 30\text{d}$ Early |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **`CRITICAL RED`** | $12{,}920$ | $2{,}303$ | **$17.83\%$** | **$3.42\times$** | $79.00$ | $70 / 86$ | **$97.13\%$** |
| **`HIGH ORANGE`** | $140{,}265$ | $16{,}281$ | **$11.61\%$** | **$2.23\times$** | $82.00$ | $75 / 87$ | **$98.85\%$** |
| **`MODERATE YELLOW`** | $321{,}706$ | $10{,}409$ | $3.24\%$ | $0.62\times$ | $85.00$ | $80 / 89$ | $99.79\%$ |
| **`GREEN HEALTHY`** | $120{,}109$ | $2{,}001$ | **$1.67\%$** | **$0.32\times$** | $87.00$ | $83 / 89$ | $99.95\%$ |

| Panel B: Live Holdout Dispatch ($N_{\text{test}}=255{,}000$) | Holdout Accounts | Cohort Share | Mean EWS Score | Mean Pred 90d Risk | Mean Recency | Assigned Operational SLA |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **`CRITICAL RED`** | $5{,}486$ | $2.15\%$ | $81.23$ | **$18.00\%$** | $27.54\text{ d}$ | Immediate Call + Fee Waiver ($<24\text{h}$) |
| **`HIGH ORANGE`** | $60{,}170$ | $23.60\%$ | $66.10$ | **$11.56\%$** | $5.27\text{ d}$ | Targeted Cashback / Re-Activation ($<72\text{h}$) |
| **`MODERATE YELLOW`** | $137{,}994$ | $54.12\%$ | $37.19$ | $3.21\%$ | $1.62\text{ d}$ | Automated In-App & BillPay Nudge (Weekly) |
| **`GREEN HEALTHY`** | $51{,}350$ | $20.14\%$ | $20.04$ | $1.65\%$ | $1.18\text{ d}$ | Organic Monitoring (Zero Intervention Cost) |

**Table 15: Top 10 Holdout `CRITICAL RED` Case Studies Demonstrating Dual Silent-Churn Archetypes**

| Rank | Account ID | EWS Score | Recency (d) | `BAL_TREND_M3_M1` | Jan $\to$ Mar Act/Wk | $\hat{S}(30/60/90\text{d})$ | Triggered Silent-Churn Signals |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| 1 | `CUST00348543` | $97.790$ | $78$ | $-0.999$ | $0.900 \to 0.000$ | $0.994 / 0.970 / 0.790$ | `BalDrop>=50% + Recency>=30d` |
| 2 | `CUST00452014` | $97.330$ | $67$ | $-0.986$ | $0.900 \to 0.000$ | $0.995 / 0.971 / 0.804$ | `BalDrop>=50% + Recency>=30d` |
| 3 | `CUST00652455` | $97.230$ | $36$ | $-0.946$ | $6.320 \to 0.000$ | $0.971 / 0.910 / 0.054$ | `BalDrop>=50% + FreqDrop + Recency>=30d` |
| 4 | `CUST00620031` | $96.930$ | $59$ | $-1.000$ | $0.900 \to 0.000$ | $0.996 / 0.976 / 0.816$ | `BalDrop>=50% + Recency>=30d` |
| 5 | `CUST00372010` | $96.820$ | $47$ | $-0.965$ | $1.130 \to 0.000$ | $0.996 / 0.974 / 0.836$ | `BalDrop>=50% + FreqDrop + Recency>=30d` |
| 6 | `CUST00497718` | $96.790$ | $32$ | $-0.987$ | $5.870 \to 0.000$ | $0.955 / 0.886 / 0.086$ | `BalDrop>=50% + FreqDrop + Recency>=30d` |
| 7 | `CUST00524101` | $96.770$ | $34$ | $-0.948$ | $5.420 \to 0.000$ | $0.975 / 0.935 / 0.168$ | `BalDrop>=50% + FreqDrop + Recency>=30d` |
| 8 | `CUST00437374` | $96.540$ | $60$ | $-0.997$ | $0.900 \to 0.000$ | $0.994 / 0.972 / 0.822$ | `BalDrop>=50% + Recency>=30d` |
| 9 | `CUST00360805` | $96.220$ | $64$ | $-0.899$ | $0.900 \to 0.000$ | $0.993 / 0.967 / 0.806$ | `BalDrop>=50% + Recency>=30d` |
| 10 | `CUST00042926` | $96.010$ | $30$ | $-0.999$ | $5.870 \to 0.230$ | $0.973 / 0.938 / 0.053$ | `BalDrop>=50% + FreqDrop + Recency>=30d` |

![EWS Trigger Lift, Recency Escalation, and Preventive Lead-Time Validation](C:/Users/User/.gemini/antigravity/brain/41ac5e1d-28ce-4b97-96ad-5a1ee8ad33ae/fig_ews_silent_churn_validation.png)
*Figure 11: EWS empirical validation ($N = 595{,}000$). (a) Behavioral trigger relative lifts. (b) Recency tier escalation ($4.57\% \to 16.78\%$ churn). (c) Final EWS tier risk lift peaking at `3.42x` (`97.13%` $\ge 30\text{d}$ lead capture) in `CRITICAL RED`.*

### 4.6 Methodological Limitations and Threats to Validity

1. **Out-of-Horizon Extrapolation Beyond Day 90:** CLV months $4\text{--}12$ rely on the $q_{i,\text{tail}}$ blend anchored at $t \in \{60, 90\}$; unseen macroeconomic shocks beyond Day 90 lie outside the censored training horizon.
2. **Interpretability Trade-off of Orthogonal Kernel Embeddings:** RBF eigenvectors combine multiple behavioral subspace dimensions non-linearly, necessitating EWS behavioral trigger accompaniment (**Table 15**) for operational explainability.
3. **Observational Risk vs. Causal Intervention Uplift:** Budget caps (`25% * VaR_12M`) reflect expected-value risk bounds rather than randomized CATE uplift estimates.
