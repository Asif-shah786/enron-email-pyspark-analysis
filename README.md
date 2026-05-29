# Enron Email Corpus — Big Data Analysis with PySpark

Distributed analysis of the [Enron email dataset](https://www.cs.cmu.edu/~enron/) (~1.3 GB raw CSV) using **Apache Spark** on **Databricks**. The project parses raw MIME messages into structured fields, runs exploratory analysis, and answers analytical questions about senders, recipients, and internal communication patterns.

Academic group project (**Group 54**, BDTT Assignment 1 — Big Data Tools & Techniques).

---

## My contribution

**[asif_c2.ipynb](asif_c2.ipynb)** — Group C, Question 2:

> Who are the top ten senders (based on the `From` field) who received no emails themselves (based on the `To` field)?

### Approach

1. Parse each raw email into structured columns (`From`, `To`, `Subject`, etc.) via Spark RDD → DataFrame.
2. Aggregate sent counts per sender (excluding null `From`).
3. Explode comma-separated `To` values into individual recipients and deduplicate.
4. Use a **left anti-join** to keep senders who never appear as a recipient.
5. Rank by `sent_count` and return the top 10.

### Sample result

| From | Emails sent |
|------|-------------|
| no.address@enron.com | 5,112 |
| noreply@ccomad3.uu.commissioner.com | 877 |
| owner-nyiso_tech_exchange@lists.thebiz.net | 712 |
| owner-eveningmba@haas.berkeley.edu | 508 |
| exchange.administrator@enron.com | 455 |
| wsmith@wordsmith.org | 454 |
| fool@motleyfool.com | 417 |
| nytdirect@nytimes.com | 348 |
| ecenter@williams.com | 340 |
| pmadpr@worldnet.att.net | 317 |

Full code, EDA, and saved outputs: **[asif_c2.ipynb](asif_c2.ipynb)**.

---

## Tech stack

- **Apache Spark** (PySpark) — RDD parsing, DataFrames, SQL functions
- **Databricks** — cluster compute, DBFS storage
- **Python** — email field extraction, aggregations, joins

---

## Repository layout

| File | Description |
|------|-------------|
| **[asif_c2.ipynb](asif_c2.ipynb)** | **My notebook** — preprocessing, EDA, Group C-2 solution |
| [Group-54.ipynb](Group-54.ipynb) | Consolidated team notebook (all questions) |
| [starter_code.ipynb](starter_code.ipynb) | Course starter template and shared preprocessing |
| [mukhtar_b1.ipynb](mukhtar_b1.ipynb) | Group B-1 — top 10 senders by volume |
| [amal_b2.ipynb](amal_b2.ipynb) | Group B-2 — top 10 recipients |
| [gagan_b3.ipynb](gagan_b3.ipynb) | Group B-3 — internal @enron.com email count |
| [asuda_a3.ipynb](asuda_a3.ipynb) | Group A-3 — emails with non-empty subject |

### Team questions covered (Group 54)

| Question | Topic |
|----------|--------|
| A-3 | Count of emails with a non-empty `Subject` |
| B-1 | Top 10 senders by emails sent |
| B-2 | Top 10 recipients by emails received |
| B-3 | Count of internal Enron-to-Enron emails |
| **C-2** | **Top senders who never appear as recipients** *(my work)* |

---

## How to run

This project was built and executed on **Databricks**. It is not set up for local execution out of the box.

1. Create a Databricks workspace and cluster with Spark enabled.
2. Upload the course Enron dataset (`BDTT_Assignment_1_Enron.zip` / `emails.csv`) to DBFS (see preprocessing cells in [starter_code.ipynb](starter_code.ipynb)).
3. Import **[asif_c2.ipynb](asif_c2.ipynb)** (or [Group-54.ipynb](Group-54.ipynb) for the full team pipeline).
4. Run cells top to bottom.

The dataset is **not included** in this repository due to size and licensing; obtain it through your course materials or the [CMU Enron corpus](https://www.cs.cmu.edu/~enron/) page.

---

## Team

| Member | Notebook | Question |
|--------|----------|----------|
| Asif | [asif_c2.ipynb](asif_c2.ipynb) | C-2 |
| Mukhtar | [mukhtar_b1.ipynb](mukhtar_b1.ipynb) | B-1 |
| Amal | [amal_b2.ipynb](amal_b2.ipynb) | B-2 |
| Gagan | [gagan_b3.ipynb](gagan_b3.ipynb) | B-3 |
| Asuda | [asuda_a3.ipynb](asuda_a3.ipynb) | A-3 |

---

## License

MIT — see [LICENSE](LICENSE).
