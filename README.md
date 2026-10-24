# US Tax & Accounting Eval Benchmarks: What You Can Actually Download

A field log of public benchmarks for evaluating AI agents on US tax and accounting work, with one hard rule: **an entry is only listed as downloadable after its actual dataset or repository page has been opened and checked.** Press releases and leaderboard pages do not count.

Scope rule: a set is included if it **contains US tax, accounting, or audit material**. Mixed sets qualify when a US portion exists, and the entry says so; sets with no US content are excluded.

Last verified: 2026-10-24. Status labels: `verified-downloadable`, `partial`, `not-downloadable`.

## Verified downloadable

### FinancialAuditBench (Modus Labs)
- **What:** 90 tasks across 6 synthetic audit engagements (manufacturing and staffing), workpaper completion (45) plus review-and-correct (45). Built from differentially private aggregate statistics of real historical audits plus 1,100+ hours of expert development. Each engagement carries 152 to 191 supporting files; each task has a 7 to 17 criterion rubric.
- **Download:** https://huggingface.co/datasets/modusaudit/FinancialAuditBench
- **Code:** https://github.com/modus-audit/financial-audit-bench (tasks auto-download from Hugging Face at run time)
- **License:** MIT (dataset card and code repo)
- **Status:** `verified-downloadable` with one caveat. The dataset card's Getting Started section says the dataset is private and requires an authenticated Hugging Face login, yet the public page anonymously renders real data rows, direct file links, and shows 1,825 downloads in the last month. Gated status not settled by an actual download test.
- **Scores so far:** best single-run full pass 69.17 percent; requiring all 8 runs to pass drops the top model to 44.4 percent; accounts receivable procedures average a 4 percent pass rate.

### APEX-Accounting dev set (Mercor + Ramp)
- **What:** The public 10-task dev set of APEX-Accounting: one full company world (World 9, Sterling, Marsh & Associates LLP, a Philadelphia law firm at December 2024 month-end close), 89 binary rubric criteria, expert gold answers, 90 shared world files plus task-specific files. The Harbor edition ships the official loop agent, task directories with Oracle solutions and graders, and runtime images, so it runs end to end.
- **Download:** https://huggingface.co/datasets/mercor/apex-accounting-harbor (original tabular release: https://huggingface.co/datasets/mercor/apex-accounting)
- **License:** CC BY 4.0
- **Status:** `partial`. The scored benchmark (160 tasks, 10 held-out worlds) is closed and not published; Mercor's FAQ states the full set stays private to prevent training contamination, and leaderboard runs are performed by Mercor on request. The card also notes the leaderboard judge prompt template and the live accounting-software interface are not in the public release, so dev-set results are not comparable to leaderboard results and must not be reported as APEX-Accounting scores.

### GDPval gold subset (OpenAI), accounting slice only
- **What:** 220 real-world knowledge-work tasks across 44 occupations, each with a prompt, reference files, an expert gold deliverable, and a full rubric. Only **5 tasks** are accounting, audit, or tax: an anti-financial-crime audit sampling review, a music tour expense rollup, a prepaid expense and insurance amortization schedule, a personal Form 1040 preparation (full 2024 tax file set plus a completed gold 1040), and a financial statement preparation and close task.
- **Download:** https://huggingface.co/datasets/openai/gdpval
- **License:** not stated on the dataset card; check OpenAI terms before commercial use.
- **Status:** `verified-downloadable` for the 220-task gold subset. The full 1,320-task set is not public.

### TaxCalcBench (Column Tax)
- **What:** Given a taxpayer's full input set (W-2s, 1099s, and more), compute the complete Form 1040 and compare it line by line against a tax engine's correct output. TY24 edition: 51 federal-only cases. v2 (TY25, released June 2026): 50 cases with realistic styled PDF inputs, state returns, and more complex situations.
- **Download:** https://github.com/column-tax/tax-calc-bench (code and data in the repo)
- **License:** MIT
- **Status:** `verified-downloadable`. The closest public match to end-to-end US tax preparation; v2 inputs are actual PDF documents, not just structured data.

### SARA (StAtutory Reasoning Assessment, Johns Hopkins)
- **What:** US federal tax statute reasoning: given a statutory provision and a fact pattern, judge entailment or compute the tax owed, with gold Prolog programs. 376 hand-crafted cases over 9 Internal Revenue Code sections (including sections 1, 63, 3301, 3306).
- **Download:** https://nlp.jhu.edu/law/sara/ (SARA.tar.gz direct download; formatting scripts at GitHub SgfdDttt/sara)
- **License:** not stated in the original release. Two subsets (sara_numeric, 100 items; sara_entailment) are also redistributed inside LegalBench under MIT.
- **Status:** `verified-downloadable`.

### FinQA / ConvFinQA / TAT-QA (classic finance QA trio)
- **FinQA:** 8,281 expert-annotated numerical-reasoning questions over US listed-company earnings reports, with gold reasoning programs (train 6,251, dev 883, public test 1,147 with gold answers; a separate private test is leaderboard-only). MIT. https://github.com/czyssrs/FinQA
- **ConvFinQA:** FinQA recast as multi-turn conversations, 3,892 conversations, 14,115 turn-level examples. MIT, but test gold answers are not public (Codalab submission scoring); train and dev are self-scorable. https://github.com/czyssrs/ConvFinQA
- **TAT-QA:** 16,552 questions over 2,757 hybrid table-plus-text earnings-report contexts (arithmetic, counting, comparison). Data at https://nextplusplus.github.io/TAT-QA/ ; the site now states CC BY 4.0 while the paper says non-commercial use, so confirm with the authors before commercial use.
- **Status:** `verified-downloadable` (with the two caveats inline above). QA over report excerpts, not agentic document work.

### DocFinQA (Kensho)
- **What:** FinQA questions against full SEC filing documents instead of excerpts (average document about 123k words), testing long-document retrieval plus calculation. 7,437 questions over 801 SEC filings.
- **Download:** https://huggingface.co/datasets/kensho/DocFinQA
- **License:** not stated (dataset card README is empty).
- **Status:** `verified-downloadable`. One of the few sets here whose inputs are real full-length documents.

### TheAgentCompany (CMU), finance slice
- **What:** A simulated US software company as a full office environment (GitLab, ownCloud, RocketChat, and more) where agents work as digital employees across 175 tasks. The Finance category has 12 tasks (spreadsheets, expense rollups, financial data entry); Admin adds 15 more with finance chores.
- **Download:** https://github.com/TheAgentCompany/TheAgentCompany (whole environment ships as Docker images)
- **License:** MIT
- **Status:** `verified-downloadable`. Office-work realism rather than accounting depth.

### SymageDocs Coherent Forms
- **What:** One synthetic identity rendered consistently across three real US government forms: **IRS Form 1040 (2024, 2 pages)**, CMS-1500 health claim form, and USCIS Form I-9, with name, SSN, address, and employer linked across forms. 3,000 pages total (train 2,400, test 600, split by identity; roughly 428 identities, so the 1040 portion is about 850 pages by structure). Every page is a PNG image with FUNSD-style ground truth (word boxes, entity labels, key-value links). Fully synthetic, clean typed renders; the degraded scan-style version is the vendor's paid product.
- **Download:** https://huggingface.co/datasets/Symage/coherent-forms-1040-cms1500-i9
- **License:** SymageDocs Synthetic Dataset License v1.0: internal use allowed, including commercial training and evaluation; **no redistribution and no building competing datasets**. Gated on Hugging Face by click-agree plus sharing account info (auto-approved).
- **Status:** `verified-downloadable`. One of the very few sets whose payload is filled US tax form documents themselves.

### OfficeQA / OfficeQA Pro (Databricks)
- **What:** Questions over the **original PDFs of U.S. Treasury Bulletins**, 697 issues from 1939 to 2025 (about 4 GB of PDFs, plus parsed JSON and transcript derivatives; the raw PDFs are in the package). OfficeQA Pro has 133 questions, the full version 246, each needing multi-step numerical reasoning across an average of 6.7 source bulletins. A separate gated Pro V2 expands the corpus to 1793 to 2024 at roughly 120k pages with 90 questions.
- **Download:** https://huggingface.co/datasets/databricks/officeqa (code: https://github.com/databricks/officeqa)
- **License:** data CC BY-SA 4.0, code Apache-2.0; the corpus itself is US government publication. Gated by click-agree on Hugging Face, including a promise not to train tested models on the answer key.
- **Status:** `verified-downloadable`. Federal fiscal documents, adjacent to accounting rather than taxpayer tax forms; flagged as such.

### Drew-IPP Invoice Extraction Benchmark
- **What:** 181 real document files (113 text-layer PDFs, 53 JPEG phone and handwriting photos, 15 PNG scans, 220 pages total) with answer keys and a scorer, plus the generator. Fully synthetic, made by the vendor of InvoiceParser Pro (the card itself says it is not an independent benchmark); 10 of the original 191 documents were withheld for undisclosed types.
- **US portion:** the clean subset of 31 mixes US, UK, EU, and South African formats; at least 20 clean-us documents are directly visible (USD, US sales tax with state and county lines, Net 30 terms). The publisher gives no exact per-country count and describes the mix as Southern African, UK, US, and EU conventions, so the entry records: US is a major component, exact count unpublished.
- **Download:** https://huggingface.co/datasets/drew-ipp/invoice-extraction-benchmark (canonical repo with generator and scorer: https://github.com/DrewKraken/invoice-extraction-benchmark)
- **License:** data CC BY 4.0, code MIT. No gate.
- **Status:** `verified-downloadable`.

### NAF (National Archives Forms)
- **What:** Real historical US federal form scans from the National Archives and FamilySearch, many hand-filled: 860 images in v2 (train 708, validation 75, test 77) with field, text-box, relation, and transcription annotations. Government forms generally, not tax or accounting forms specifically; small, listed as a supplementary US forms source.
- **Download:** https://github.com/herobd/NAF_dataset (labeled_images.tar.gz in GitHub Releases)
- **License:** a LICENSE file exists but GitHub reports it as unrecognized (NOASSERTION); read it before commercial use.
- **Status:** `verified-downloadable`.

### Finch / FinWorkBench
- **What:** Multi-step financial-accounting workflow tasks over real corporate file packs (modify spreadsheets, generate documents, answer questions), sourced mainly from Enron and EUSES corporate finance-and-accounting files. 172 workflows, 384 tasks.
- **Download:** https://huggingface.co/datasets/FinWorkBench/Finch (evaluation code: https://github.com/FinWorkBench/Finch)
- **License:** not stated on the dataset card or in the code repo (no LICENSE file); ask the authors before commercial use.
- **Status:** `verified-downloadable`. Mixed provenance: the file packs include some Canadian and UK government material, so it is not purely US; filter before use.

### Snorkel FinQA (2026, not the 2021 FinQA)
- **What:** An RL agent environment: the agent uses 4 MCP tools over real 10-K tables from 22 US listed companies (Alphabet, Amazon, Apple, and others) to find numbers, compute, and answer. 290 expert questions, binary reward.
- **Download:** Open-sourced in the OpenEnv repository per Snorkel's 2026-03-30 post, with a Hugging Face Space to try online. Entry point: https://snorkel.ai/blog/building-finqa-an-open-rl-environment-for-financial-reasoning-agents/
- **License:** not confirmed in this pass.
- **Status:** `verified-downloadable` per the publisher, license pending.

## Partial and special-license access

### Vals AI Tax Agent Bench
- **What:** 391 expert-authored US tax research questions (federal corporate, SALT, partnership, controversy and procedure, transfer pricing, filing and disclosure, employment tax), graded with weighted expert checks including must-pass criteria.
- **Download:** https://github.com/vals-ai/tax-agent-bench holds the full runnable harness plus `data/public.json` with 5 public sample questions. Running it needs only your own model API key and a Tavily key, no Vals account.
- **Documents:** none attached. Each sample is only an id, a text fact-pattern question, and its checks (verified against the raw public.json). The agent is expected to research the law itself over web search, which is what the Tavily key is for.
- **License:** MIT (repo).
- **Status:** `partial`. Public samples (5) plus harness are open; the 193-question validation set is available for paid license; the 193-question test set stays private permanently.

### Crypto Accounting Bench (CAB, Entendre Finance)
- **What:** 118 tasks drawn from the ledgers of 7 pseudonymized organizations: given the full evidence for one crypto-asset transaction, reconstruct the exact journal entry the organization actually posted (accounts, sides, amounts, full-precision quantities). 21 assets, 10 chains, 246 nonzero reference entry lines. Each task ships task.md, prompt.md, input.json, and expected_answer.json with a frozen weighted rubric; the repo also carries a transformation report and a publication audit file. **There are no document files anywhere in the release** (verified against the full 483-file tree: only .md and .json, plus one .py scorer): all evidence, including the organization's full chart of accounts (569 accounts in task_0001), amounts, wallet addresses, counterparty and tax-lot evidence, is structured JSON inside input.json, not PDFs, spreadsheets, or scans.
- **Download:** https://huggingface.co/datasets/Entendre/Crypto-Accounting-Bench (not gated; verified via the file-tree API, dataset commit 0ec2596, last modified 2026-09-15)
- **Code:** https://github.com/EntendreFinance/crypto-accounting-bench (Apache-2.0; the `cab dataset download` command pulls the roughly 500 data files from Hugging Face)
- **License:** dataset is **CC BY-NC 4.0, non-commercial only**; code is Apache-2.0. Do not use the dataset in a commercial product eval without clearing the license.
- **Paper:** https://arxiv.org/abs/2609.14811
- **Status:** `verified-downloadable` with two caveats. First, the public release is an **educational transformed edition**, not the evaluated originals: organization names, account codes, blockchain identifiers, asset and chain labels were replaced, amounts and quantities rescaled, dates shifted and timestamp precision reduced; true identities and the transformation mapping are not published. Second, the paper's headline scores came from an internal LLM judge pipeline that is not released; the public deterministic scorer reproduces a lower bound only, and the public version has 4 gates versus 7 in the paper protocol.

### FinAuditing (TheFinAI)
- **What:** Audit consistency checks over real US-GAAP XBRL filings, three subtasks: semantic (FinSM, about 330 rows), relational (FinRE, about 440), numerical (FinMR, about 332).
- **Download:** Hugging Face datasets TheFinAI/en-finsm, TheFinAI/en-finre, TheFinAI/en-finmr; evaluation code (MIT) at https://github.com/The-FinAI/FinAuditing
- **Status:** `partial`. The datasets are gated, but the gate is a short form with automatic approval on submission, so they are obtainable, just not anonymous one-click downloads.

### FinanceBench (Patronus AI)
- **What:** Financial QA over real filings; the full set holds 10,231 questions.
- **Status:** `partial`. Only a 150-question sample is open (data/financebench_open_source.jsonl in https://github.com/patronus-ai/financebench); the rest requires contacting Patronus. Not a full set.

### FinBen / PIXIU (TheFinAI)
- **What:** An aggregation framework over 35 datasets (including FinQA and TAT-QA), code MIT at https://github.com/The-FinAI/PIXIU
- **Status:** `partial`, listed as a discovery index only: coverage mixes Chinese, Spanish, and German credit data alongside US sets, so it is not a US-only source.

### BizBench (Kensho / S&P Global, 2023)
- **What:** 8 professional-finance task families, 5,448 test items (FinCode from CFA/CPA practice questions, SEC-Num from SEC filings, CodeFinQA, CodeTAT-QA, ConvFinQA Extract, TAT-QA Extract, FinKnow, FormulaEval). The paper states train, dev, and unlabeled test sets were released.
- **Status:** `partial`. Content and size verified from the paper; the exact download URL was not located in this pass (one probed GitHub path returns 404). Listed so nobody has to rediscover the gap; link to be added when found.

### Shelter Check (Can LLMs Identify Tax Abuse?)
- **What:** Expert-designed tax shelter strategies; the model must judge whether each arrangement violates tax law (arXiv:2508.20097).
- **Status:** `partial`. Only **5 of 36** strategies are public, in https://github.com/BlairStanek/LLM-Tax-Abuse; the authors deliberately withhold the rest (contamination and misuse concerns). The full set has been shared with IRS researchers, and qualified researchers can apply to the corresponding author under a data use agreement. No license file in the repo. Still, it is the only other public US tax-law reasoning resource found besides SARA.

### AA-Omniscience-Public (Artificial Analysis)
- **What:** A 600-row public sample of a domain knowledge question bank. The Accounting topic holds just **20 questions** (Accounting 13, Auditing 2, Taxation 5: GAAP/ASC, PCAOB, and IRS form knowledge).
- **Download:** https://huggingface.co/datasets/ArtificialAnalysis/AA-Omniscience-Public
- **License:** Apache-2.0 (stated on the card).
- **Status:** `partial`. Tiny; a knowledge-question supplement, not a main eval set.

### JHU Tax Law NLP Resources (corpus, not a benchmark)
- **What:** The SARA team's underlying corpora: US Tax Court opinions and IRS private letter rulings, downloadable as zips (TaxCourtPLRCorpus.zip about 154 MB) from the Johns Hopkins data archive, DOI 10.7281/T1/N1X6I4, CC BY-NC 4.0.
- **Status:** `partial`. Raw material for building your own tax eval items, not a scored benchmark.

### FinBalance and FinRule-Bench (claimed released, URLs not pinned down)
- **FinBalance** (arXiv:2606.15949): multi-document accounting reconciliation with a deterministic generator (journal entries, balance sheets, 23 inconsistency codes; 710-item eval split). The paper states the generator and harness are Apache-2.0 and the generated records CC BY 4.0 with no hidden eval set, but the exact repository URL could not be extracted in this pass. **Unverified.**
- **FinRule-Bench** (arXiv:2603.11339): financial statements plus accounting-principle rule-violation diagnosis (1,117 clean, 4,385 single-violation, 400 multi-violation records). The only release pointer is an anonymous review link that returns 401; no permanent GitHub or Hugging Face repo located. **Unverified.**

### FinMRAGBench (ACL 2026)
- **What:** 887 expert-verified QA annotations over US 10-K annual report PDFs (723 filings, 96,549 pages, files named TICKER_10K_YEAR).
- **Status:** `partial`. The annotations are in the GitHub repo https://github.com/sqyangit/FinMRAGBench (Apache-2.0), but the document corpus itself is not yet released; the README says the corpus and source list are coming "soon", so for now the PDFs must be rebuilt from EDGAR by hand. Half a set.

### FinTabNet
- **What:** 112k+ financial tables from S&P 500 annual reports, with structure annotations.
- **Status:** `partial` and borderline under the documents rule: what ships is cropped table-region images cut from report pages, not the original report documents. Original via IBM's data exchange (https://developer.ibm.com/data/fintabnet/, IBM account and agreement required, CDLA-Permissive-1.0); a cleaned version, FinTabNet.c, is directly downloadable on Hugging Face (bsmock/FinTabNet.c, CDLA-Permissive-2.0).

## Checked and not downloadable

| Benchmark | What exists publicly | Why it is not downloadable |
|---|---|---|
| APEX-Accounting full set (160 tasks) | Paper, leaderboard, dev set | Closed by design to prevent training contamination; no leak or mirror found on GitHub, Hugging Face, or arXiv as of 2026-10-24 |
| DualBench100 (DualEntry) | Results page for 19 models, methodology paper, 8 example tasks (one per category) | The 101-case set, reference answers, and scoring rules are not released; no official GitHub repo |
| AuditBench (Wang et al., 2025) | Paper only (arXiv:2506.17282; Springer CCIS 2533) | No data or code release and no request channel stated. Do not confuse with the unrelated model-safety AuditBench (Sheshadri et al., 2026) |
| AccountingBench (Penrose, 2025) | Report page only (accounting.penrose.com) | Built on one real SaaS company's year of live bank, payroll, and payment data; not releasable |
| FinMaster (Jiang et al., 2025) | Paper only (arXiv:2505.13533) | No repository or dataset link found on GitHub or Hugging Face |
| Blue J internal benchmark | Mentioned in an OpenAI case study (350+ prompts across US, Canadian, and UK tax law) | Vendor-internal release gate; never published |
| Basis internal eval suite | Described in an OpenAI case study (process plus outcome checks on real client-style work) | Vendor-internal; tasks, scoring outputs, and traces not public |
| Vals TaxEval v2 | 20-question public validation set on request | 300-question validation set is licensed, 1,223-question test set is never shared per Vals |
| Digits bookkeeping benchmark (2026) | Vendor announcement and report (2,000 real small-business transactions with US GAAP gold labels) | No data release found anywhere; press only |
| AuditFraudBench | Paper only (arXiv:2606.08345), fraud detection over SEC AAERs and original vs restated 10-K/10-Q filings | No code or data link in the paper or anywhere else found |
| Rivet TaxBench | Vendor results page only (rivet.tax/taxbench) | No data download |
| CPA exam question sets | Nothing legitimate found | Searches across Hugging Face, GitHub, Kaggle, and Zenodo surfaced only paid question-bank resellers (Docsity, Stuvia) with unverifiable provenance; no openly licensed AICPA released-question set exists as a dataset |

## How entries get verified

1. Open the actual dataset or repository page, not a press release or aggregator.
2. Confirm real files or data rows are reachable without a login, or state exactly what gate exists.
3. Record task count, license, and any comparability limits in the entry itself.
4. Re-checks are dated; a benchmark that changes its access terms gets its entry updated, not silently replaced.
