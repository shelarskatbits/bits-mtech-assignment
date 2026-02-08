# CNN Assignment Submission Checklist
**Submission:** `2025AA05387_cnn_assignment.ipynb`  
**Checked against:** CNN_Assignment_Instructions.pdf + autograde-for-all-field.ipynb (CNN_assignment_algo.txt)

---

## Pre-validation (autograder)

| Requirement | Status | Notes |
|-------------|--------|--------|
| Filename format `<BITS ID>_cnn_assignment.ipynb` | **Met** | `2025AA05387_cnn_assignment.ipynb` |
| BITS ID in filename = BITS ID in notebook | **Met** | `2025AA05387` in both |
| Folder name = student name (for autograder) | **Met** | Use `folder_name = "SHELAR SACHIN KRISHNA"` when running autograder |
| Notebook executed (outputs visible) | **Met** | Submission has execution_count and outputs |
| No execution errors | **Met** | No error tracebacks in cells |

---

## PDF – Submission requirements (critical)

| Requirement | Status | Notes |
|-------------|--------|--------|
| Wrong filename → zero | **Met** | Correct format |
| BITS ID mismatch → zero | **Met** | Match |
| Student name mismatch (LMS vs notebook) → zero | **Met** | Name in notebook: SHELAR SACHIN KRISHNA |
| Notebook not executed → zero | **Met** | Run “Restart & Run All” before submit |
| Execution errors → zero | **Met** | None found |
| Flatten+Dense instead of GAP → zero | **Met** | GAP used; no Flatten in architecture |
| Missing JSON output → zero | **Met** | `get_assignment_results()` and print at end |
| .ipynb only, no zip/data files | **Met** | Single notebook |

---

## PDF – Technical requirements

| Requirement | Status | Notes |
|-------------|--------|--------|
| One framework (Keras or PyTorch) | **Met** | Keras/TensorFlow only |
| Dataset: min 500 images per class | **Met** | 750 per class (Cats vs Dogs) |
| 2–20 classes | **Met** | 2 classes |
| Train/test 90/10 or 85/15 | **Met** | 90/10 |
| GAP mandatory (both models) | **Met** | GlobalAveragePooling2D in both |
| Custom CNN: ≥2 Conv2D, pooling, GAP, softmax | **Met** | 3 Conv2D, MaxPooling, GAP, softmax |
| Transfer: ResNet/VGG, freeze base, GAP, custom head | **Met** | ResNet50, `base_model.trainable = False`, GAP + Dense |
| Loss tracking (initial/final) both models | **Met** | Both have initial_loss, final_loss |
| All 4 metrics (accuracy, precision, recall, F1) both models | **Met** | All present in JSON |
| Primary metric + justification | **Met** | accuracy + justification in JSON |
| Analysis: 5+ topics, max 200 words guideline | **Met** | Performance, pre-training, GAP, computational cost, etc. |
| JSON output at end | **Met** | Printed after `get_assignment_results()` |

---

## Autograder grading sections

### Section 1: Custom CNN (5 marks)

| Check | Status | Notes |
|-------|--------|--------|
| Conv2D in code | **Met** | Yes |
| GAP in code / JSON | **Met** | GlobalAveragePooling2D + `has_global_average_pooling: true` |
| No Flatten+Dense (without GAP) | **Met** | GAP present so not penalized |
| Compiled/configured (compile / optimizer+loss) | **Met** | model.compile + Adam + categorical_crossentropy |
| initial_loss, final_loss present and > 0 | **Met** | Both in JSON (0.698, 0.643 in current output) |
| All 4 metrics (accuracy, precision, recall, f1_score) | **Met** | All in custom_cnn |

### Section 2: Transfer learning (5 marks)

| Check | Status | Notes |
|-------|--------|--------|
| Valid base model (ResNet18/50, VGG16/19) | **Met** | ResNet50 |
| frozen_layers > 0 | **Met** | 175 in JSON |
| has_global_average_pooling: true | **Met** | Yes |
| initial_loss, final_loss | **Met** | Present (e.g. 0.30 → 0.013) |
| All 4 metrics | **Met** | Yes |

### Section 3: Training process – loss convergence (4 marks)

| Check | Status | Notes |
|-------|--------|--------|
| Custom CNN: ≥50% reduction → 2; ≥20% → 1; <20% → 0 | **At risk** | **Current saved output:** initial 0.698, final 0.643 ⇒ ~8% reduction ⇒ **0 marks**. Your code uses 40 epochs + ReduceLROnPlateau, but the **last run in the notebook is still 20 epochs** (Epoch 20/20 in output, n_epochs: 20 in JSON). |
| Transfer learning: same rule | **Met** | Large reduction (e.g. 0.30 → 0.013) ⇒ 2 marks |

**Action:** Run **Kernel → Restart & Run All** so the notebook trains with 40 epochs and the new loss values (and n_epochs) are saved in the outputs and JSON. That should give ≥50% or at least ≥20% reduction for the custom CNN.

### Section 4: Metrics validation (2 marks)

| Check | Status | Notes |
|-------|--------|--------|
| All 4 metrics in [0, 1] for both models | **Met** | Values in valid range |

### Section 5: Analysis (2 marks)

| Check | Status | Notes |
|-------|--------|--------|
| Analysis text present, length ≥ 50 | **Met** | Yes |
| Key topics (performance, transfer/pre-training, GAP, computational, convergence, etc.) | **Met** | Covers performance, pre-training, GAP, computational cost, etc. (algo: ≥5 topics for 1–2 marks) |

### Section 6: Code structure (2 marks)

| Check | Status | Notes |
|-------|--------|--------|
| Custom CNN + transfer learning in code | **Met** | Conv2D + GAP; ResNet + trainable/freeze |
| JSON has custom_cnn, transfer_learning, dataset_name | **Met** | All present |

---

## JSON structure (algo / autograder)

| Key / field | Status |
|-------------|--------|
| dataset_name, n_classes, samples_per_class, train_test_ratio | **Met** |
| custom_cnn: framework, architecture.has_global_average_pooling, initial_loss, final_loss, accuracy, precision, recall, f1_score | **Met** |
| transfer_learning: base_model, frozen_layers, has_global_average_pooling, initial_loss, final_loss, accuracy, precision, recall, f1_score | **Met** |
| primary_metric, metric_justification | **Met** |
| analysis | **Met** |

---

## Summary

- **Pre-validation:** All pass (use `folder_name = "SHELAR SACHIN KRISHNA"` and correct path to the submission notebook when running the autograder).
- **Content and structure:** Match PDF and autograder (filename, BITS ID, GAP, both models, metrics, analysis, JSON).
- **One fix needed:** Re-run the notebook (**Restart & Run All**) so the custom CNN is trained with 40 epochs and the updated loss (and n_epochs) is stored. The current saved output gives ~8% loss reduction for the custom CNN, so you would get **0/2** for that part of Section 3; after re-run you can get 1 or 2 marks depending on final reduction.

**Autograder path:** If you run the autograder from the **project root**, set  
`notebook_path = "CNN-Assignement/2025AA05387_cnn_assignment.ipynb"`.  
If you run from inside `CNN-Assignement`,  
`notebook_path = "2025AA05387_cnn_assignment.ipynb"` is correct.
