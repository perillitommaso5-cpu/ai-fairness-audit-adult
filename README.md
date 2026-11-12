# AI Fairness Audit – Adult Income

**[English](#english) · [Italiano](#italiano)**

---

## English

### What this project is

A fairness audit of a machine learning model, carried out from the point of view of a **QA Engineer** working under the **EU AI Act**.

**Scenario:** a bank uses a model that predicts whether a person earns more than $50,000 a year to decide who receives a loan offer. Creditworthiness assessment is a **high-risk** use case under the AI Act, so the model must be tested for accuracy, robustness and non-discrimination before release.

**Question:** does the model make equally good decisions for men and women, and for different ethnic groups?

### Key findings

| | Result |
| --- | --- |
| Overall accuracy | 85.5% |
| Overall recall | 59.8% (below the 0.60 acceptance threshold) |
| Recall: men vs women | 60.9% vs 54.2% (6.6 points gap) |
| Selection rate ratio: women / men | 0.32 (0.36 in the data: the model widens the gap) |
| Recall: White vs Black | 60.3% vs 53.7% |
| Not assessable | Amer-Indian-Eskimo and Other (only 21 and 14 high-income people in the test set) |

- **Removing sex and race from the inputs was not enough:** other columns, such as `relationship` (values *Husband* / *Wife*), let the model reconstruct that information.
- **High accuracy can be misleading:** a model that always answers "no" would already reach about 76%.
- **Verdict: release not approved.** One overall criterion and every fairness criterion failed.

### Method

- **Data:** UCI Adult Income dataset (1994 US Census), 48,842 people.
- **Model:** logistic regression, 70% training / 30% test split.
- **Sex and race** excluded from the model inputs, but used to measure results by group.
- **Metrics by group** with [Fairlearn](https://fairlearn.org): accuracy, precision, recall, selection rate.
- **Acceptance criteria defined before** looking at the group results, as in any test plan.
- Report sections mapped to the AI Act: data (art. 10), risk management and accuracy (arts. 9 and 15), post-market monitoring (art. 72).

### Repository contents

| File | Description |
| --- | --- |
| `progetto1_audit_fairness.ipynb` | The executed notebook, with all results and charts |
| `report_audit_fairness.pdf` | The full audit report (in Italian) |
| `README.md` | This file |

### How to run it

No installation needed: open the notebook in [Google Colab](https://colab.research.google.com) (*File → Open notebook → GitHub*, then paste this repository's URL) and run the cells from top to bottom. The dataset is downloaded automatically.

### Limitations

US data from 1994; a single model and a single train/test split; income used as a stand-in for creditworthiness; sex and ethnicity analysed separately, not in combination. Full details in section 6 of the report.

### Author

**Tommaso Perilli** – QA Engineer, working toward AI quality and AI Act compliance.

---

## Italiano

### Di cosa si tratta

Un audit di fairness su un modello di Machine Learning, svolto dal punto di vista di un **QA Engineer** che lavora nel quadro dell'**AI Act europeo**.

**Scenario:** una banca usa un modello che prevede se una persona guadagna più di 50.000 dollari l'anno per decidere a chi proporre un prestito. La valutazione dell'affidabilità creditizia è un uso **ad alto rischio** secondo l'AI Act: prima del rilascio il modello va verificato per accuratezza, robustezza e assenza di discriminazioni.

**Domanda:** il modello prende decisioni ugualmente buone per uomini e donne, e per gruppi etnici diversi?

### Risultati principali

| | Risultato |
| --- | --- |
| Accuratezza complessiva | 85,5% |
| Recall complessivo | 59,8% (sotto la soglia di accettazione di 0,60) |
| Recall: uomini e donne | 60,9% contro 54,2% (6,6 punti di differenza) |
| Rapporto di selection rate: donne / uomini | 0,32 (nei dati 0,36: il modello amplifica la differenza) |
| Recall: White e Black | 60,3% contro 53,7% |
| Non valutabili | Amer-Indian-Eskimo e Other (solo 21 e 14 persone con reddito alto nel test) |

- **Togliere sesso ed etnia dai dati del modello non è bastato:** altre colonne, come `relationship` (valori *Husband* / *Wife*), permettono al modello di ricostruire quell'informazione.
- **Un'accuratezza alta può ingannare:** un modello che risponde sempre "no" arriverebbe già a circa il 76%.
- **Verdetto: rilascio non approvato.** Non sono superati un criterio complessivo e tutti i criteri di fairness.

### Metodo

- **Dati:** dataset UCI Adult Income (censimento USA del 1994), 48.842 persone.
- **Modello:** regressione logistica, divisione 70% addestramento / 30% test.
- **Sesso ed etnia** esclusi dai dati del modello, ma usati per misurare i risultati per gruppo.
- **Misure per gruppo** con [Fairlearn](https://fairlearn.org): accuratezza, precision, recall, selection rate.
- **Criteri di accettazione definiti prima** di guardare i risultati per gruppo, come in ogni test plan.
- Sezioni del report collegate all'AI Act: dati (art. 10), gestione del rischio e accuratezza (artt. 9 e 15), monitoraggio dopo il rilascio (art. 72).

### Contenuto del repository

| File | Descrizione |
| --- | --- |
| `progetto1_audit_fairness.ipynb` | Il notebook eseguito, con tutti i risultati e i grafici |
| `report_audit_fairness.pdf` | Il report completo dell'audit |
| `README.md` | Questo file |

### Come eseguirlo

Non serve installare nulla: apri il notebook in [Google Colab](https://colab.research.google.com) (*File → Apri notebook → GitHub*, poi incolla l'indirizzo di questo repository) ed esegui le celle dall'alto verso il basso. Il dataset si scarica da solo.

### Limiti

Dati statunitensi del 1994; un solo modello e una sola divisione dei dati; il reddito usato come approssimazione dell'affidabilità creditizia; sesso ed etnia analizzati separatamente, non in combinazione. I dettagli sono nella sezione 6 del report.

### Autore

**Tommaso Perilli** – QA Engineer, in percorso verso la qualità dei sistemi AI e la conformità all'AI Act.
