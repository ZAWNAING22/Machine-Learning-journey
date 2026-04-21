Great question. Here's exactly how to review it so you can answer any professor question confidently.

---

## How to Review the ML Code

### 1. Understand the BIG PICTURE first
Before looking at any code, memorize this flow:

```
Raw CSV → Fix Labels → Drop Columns → Split → Scale → Train → Evaluate
```

Every notebook maps to one step. You should be able to draw this on a whiteboard without notes.

---

### 2. Review each notebook with these questions in mind

---

#### Notebook 1 — Load & Verify
**Understand:**
- Why do we call `str.strip()` on column names?
- What does the log scale chart show that normal scale hides?

**Likely professor question:**
> *"Your dataset is imbalanced — how did you handle it?"*

**Your answer:**
> BENIGN is 80% of data. For tree models I used `class_weight='balanced'` and `sample_weight`. I also used stratified split so minority classes like WebAttack (2,180 rows) appear in both train and test sets proportionally.

---

#### Notebook 2 — Feature Selection
**Understand these 3 concepts deeply:**

**Metadata drop** — why never use IP addresses?
> Because the model would memorize the attacker IPs from the lab environment and fail completely on real-world traffic. IP is an identifier, not a behavior.

**Zero variance drop** — what does it mean?
> A column where every row has the same value (always 0) gives the model zero information to learn from. It is mathematically useless.

**Correlation drop** — why remove correlated features?
> If two features have 0.98+ correlation they are nearly identical. Keeping both wastes memory, slows training, and can confuse some models by giving the same information twice. Example: `Subflow Fwd Packets` is always equal to `Total Fwd Packets` — one must go.

**Likely professor question:**
> *"How did you select your 52 features?"*

**Your answer:**
> I started with 84 features after removing identifiers. I dropped 10 zero-variance columns that were always 0, then used a correlation matrix to find 18 pairs with correlation above 0.98 and removed the redundant one from each pair. This left 52 meaningful features representing packet counts, flow rates, inter-arrival times, TCP flags, and window sizes.

---

#### Notebook 3 — Preprocessing
**Understand these 2 rules completely:**

**Stratified split:**
> Without stratify=y, a random split might put all 2,180 WebAttack rows into training and zero into test. The model could never be evaluated on that class.

**Scaler rule — the most common exam trap:**
> You fit the scaler ONLY on X_train. Then transform X_test using the same fitted scaler. Never refit on test data. Never refit on live data. Always load the saved scaler.pkl.

**Likely professor question:**
> *"Why do you scale the data? Random Forest doesn't need scaling."*

**Your answer:**
> Correct — Random Forest and XGBoost are tree-based and scale-invariant. However I am comparing 4 models including SVM and LightGBM which do require scaling. Applying the same preprocessing to all 4 keeps the comparison fair. Also the saved scaler.pkl is critical for the live capture pipeline — CICFlowMeter features must be scaled identically to training data before prediction.

---

#### Notebook 4 — Model Training
**Understand why each model was chosen:**

| Model | Key concept to explain |
|---|---|
| Random Forest | Ensemble of 100 decision trees, bagging, majority vote |
| XGBoost | Boosting — each tree corrects errors of previous tree |
| LightGBM | Same as XGBoost but leaf-wise growth, faster on large data |
| SVM | Finds maximum margin hyperplane — binary only due to scale |

**Likely professor question:**
> *"Why did you use XGBoost over a simple decision tree?"*

**Your answer:**
> A single decision tree overfits easily — it memorizes training data but fails on new data. XGBoost uses boosting where 100 trees are built sequentially, each one correcting the mistakes of the previous. This gives much better generalization. Our results confirm this — XGBoost achieved 99.98% recall vs a single tree which would likely overfit.

**Likely professor question:**
> *"Why is SVM binary only?"*

**Your answer:**
> LinearSVC with 7 classes on 2+ million rows would require fitting 21 one-vs-one classifiers, taking hours and possibly running out of RAM. I used LinearSVC on binary labels (BENIGN vs ATTACK) as a baseline comparison only. For the real NIDS I use XGBoost.

---

#### Notebook 5 — Evaluation
**Understand every metric:**

| Metric | What it measures | Why it matters |
|---|---|---|
| Accuracy | % correct overall | Misleading alone on imbalanced data |
| F1 weighted | Balance of precision and recall | Better than accuracy for imbalanced |
| Recall macro | How many attacks caught per class | Most important in security — missing attack is dangerous |
| ROC-AUC | Overall discriminating ability | 1.0 = perfect separation |

**Likely professor question:**
> *"Your accuracy is 99.96% — could this be overfitting?"*

**Your answer:**
> No — the metrics are on the held-out test set which the model never saw during training. Overfitting would show high train accuracy but low test accuracy. Here both are high, and ROC-AUC of 1.0 on the test set confirms genuine learning. The CICIDS 2017 dataset has very distinctive attack signatures which makes high accuracy expected and is consistent with published research on this dataset.

**Likely professor question:**
> *"Why is LightGBM recall only 85%?"*

**Your answer:**
> LightGBM's lower recall is on minority classes — WebAttack and Bot together have under 4,000 rows out of 2.8 million. Even with `is_unbalance=True`, LightGBM's leaf-wise tree growth strategy tends to optimize for majority classes. XGBoost with explicit `sample_weight` handles this better, which is why its recall is 99.98%.

---

### 3. Three things to memorize word for word

**1. What your system does:**
> "This is a Network Intrusion Detection System that uses machine learning to classify network flows into 7 categories — normal traffic and 6 attack types — using 52 statistical features extracted by CICFlowMeter from the CICIDS 2017 dataset."

**2. Why XGBoost is your final model:**
> "XGBoost achieved the highest recall of 99.98% with ROC-AUC of 1.0, meaning it almost never misses an attack. In security, a missed attack is more dangerous than a false alarm, so recall is our primary metric."

**3. The pipeline in one sentence:**
> "Raw pcap files were converted to flow statistics by CICFlowMeter, labels were merged into 7 classes, 52 features were selected after removing metadata and redundant columns, the data was scaled using StandardScaler, and XGBoost was trained and evaluated on an 80/20 stratified split."

---

### 4. Weak spots to prepare for

These are the hardest questions professors ask:

- *"Would this work on real traffic outside the lab?"* — Answer: dataset limitation, lab-generated traffic may not represent all real-world patterns, but the feature-based approach generalizes better than signature-based
- *"What is the false positive rate?"* — Look at your confusion matrix, find BENIGN rows predicted as ATTACK
- *"How would you deploy this in real time?"* — CICFlowMeter live mode → scaler.pkl → model.pkl → FastAPI → Android app
- *"What is CICFlowMeter?"* — Tool that captures packets and computes the same 80+ statistical features per flow that your model was trained on
