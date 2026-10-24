# 美国税务与会计评测基准：哪些是真能下载的

一份实地核查日志：面向美国税务与会计工作的公开 AI agent 评测基准。规矩只有一条：**只有亲自打开过实际的数据集或仓库页面并核实，才标为可下载。** 新闻稿和排行榜页面不算数。

收录口径：**只要含有美国税法、会计或审计内容就收**。混合集只要有美国部分即可入选，条目里会注明；完全没有美国内容的排除。

最近核查：2026-10-24。状态标签：`已核实可下`、`部分可下`、`不可下`。

## 已核实可下载

### FinancialAuditBench（Modus Labs）
- **内容：** 90 个任务、6 个合成审计项目（制造业与人力服务业），底稿编制 45 题加底稿复核纠错 45 题。用真实历史审计的差分隐私聚合统计当先验生成，再加 1,100 多小时专家开发与复核。每个项目带 152 到 191 份支持文件，每题 7 到 17 条评分标准。
- **下载：** https://huggingface.co/datasets/modusaudit/FinancialAuditBench
- **代码：** https://github.com/modus-audit/financial-audit-bench （运行时自动从 Hugging Face 拉任务）
- **许可证：** MIT（数据卡与代码仓一致）
- **状态：** `已核实可下`，带一条保留。数据卡的入门一节自称数据集为私有、需要登录有权限的 HF 账号；但公开页面匿名状态下能看到真实数据行和文件直达链接，且显示上月下载量 1,825 次。是否 gated 未经实际下载最终定性。
- **现有成绩：** 单次全过最高 69.17%；要求每道跑 8 次全过，第一名掉到 44.4%；应收账款类程序平均通过率仅 4%。

### APEX-Accounting 公开 dev set（Mercor + Ramp）
- **内容：** APEX-Accounting 的公开 10 题开发集：一个完整公司世界（World 9，费城律所 Sterling, Marsh & Associates LLP，2024 年 12 月月末结账），89 条二值评分标准、专家金标答案、90 份共享世界文件加任务专属文件。Harbor 版带官方 loop agent、含 Oracle 解法与判分器的任务目录和运行时镜像，能端到端跑起来。
- **下载：** https://huggingface.co/datasets/mercor/apex-accounting-harbor （原始表格版：https://huggingface.co/datasets/mercor/apex-accounting ）
- **许可证：** CC BY 4.0
- **状态：** `部分可下`。计分用的正式集（160 题、10 个保密世界）不公开，Mercor 官网 FAQ 明说全套保持私有是为了防训练污染，想测只能申请官方代跑。卡片还注明排行榜的判分模板和会计软件实时接口不在公开版内，所以 dev set 跑出的分与排行榜不可比，不得当作 APEX-Accounting 分数报告。

### GDPval gold 子集（OpenAI），只有会计那一小片
- **内容：** 220 道真实知识工作任务、44 个职业，每道含题目、参考文件、专家金标交付物和完整评分细则。其中会计、审计、税务合计只有 **5 道**：审计反金融犯罪指标抽样复核、音乐巡演费用汇总、预付费用与保险摊销表、个人 1040 报税（全套 2024 税务文件加已填好的金标 1040）、财务报表编制与结账组装。
- **下载：** https://huggingface.co/datasets/openai/gdpval
- **许可证：** 数据卡未标注，商用前需另行确认 OpenAI 条款。
- **状态：** `已核实可下`（仅 220 题 gold 子集），全集 1,320 题未公开。

### TaxCalcBench（Column Tax）
- **内容：** 给全套纳税人输入（W-2、1099 等），让模型算出整张 Form 1040，逐行与税务引擎的正确输出比对。TY24 版 51 个案例（仅联邦）；2026 年 6 月发布的 v2（TY25）50 个案例，输入升级为真实样式的 PDF，还加了州税表和更复杂情形。
- **下载：** https://github.com/column-tax/tax-calc-bench （代码与数据都在仓库里）
- **许可证：** MIT
- **状态：** `已核实可下`。公开集里与端到端美国报税最对口的一个；v2 的输入是真 PDF 文档，不只是结构化数据。

### SARA（StAtutory Reasoning Assessment，约翰霍普金斯）
- **内容：** 美国联邦税法条文推理：给条文加案情，判蕴含关系或算应纳税额，附 Prolog 金标程序。376 个手工案例，覆盖 IRC 的 9 个条文（含第 1、63、3301、3306 条）。
- **下载：** https://nlp.jhu.edu/law/sara/ （SARA.tar.gz 直下；格式化脚本在 GitHub 的 SgfdDttt/sara）
- **许可证：** 原始发布未标注。两个子任务（sara_numeric 100 条、sara_entailment）也被 LegalBench 收录，那边标注 MIT。
- **状态：** `已核实可下`。

### FinQA / ConvFinQA / TAT-QA（经典财务 QA 三件套）
- **FinQA：** 8,281 道专家标注的财报数值推理题（美股上市公司财报），带金标推理程序（train 6,251、dev 883、公开 test 1,147 带答案；另有一份 private test 只供官方排行榜评分）。MIT。https://github.com/czyssrs/FinQA
- **ConvFinQA：** FinQA 的多轮对话版，3,892 段对话、14,115 条 turn 级样本。MIT，但 test 金标不公开，要走 Codalab 提交评分；train 与 dev 可自评。https://github.com/czyssrs/ConvFinQA
- **TAT-QA：** 16,552 题、2,757 个表格加文本混合的财报上下文（加减乘除、计数、比较）。数据在 https://nextplusplus.github.io/TAT-QA/ ；官网现标 CC BY 4.0，但论文原文写非商业使用，两处口径不一致，商用前最好再跟作者确认。
- **状态：** `已核实可下`（附上面两条限定）。都是基于财报摘录的问答，不是带文档的 agent 活。

### DocFinQA（Kensho）
- **内容：** 题目同 FinQA，但上下文换成 SEC 申报文件全文（平均一篇约 12.3 万词），测长文档里找数算数。7,437 题、801 份 SEC 文件。
- **下载：** https://huggingface.co/datasets/kensho/DocFinQA
- **许可证：** 未标注（数据卡 README 为空）。
- **状态：** `已核实可下`。少数输入是真实全长文档的集之一。

### TheAgentCompany（CMU），财务那一片
- **内容：** 模拟一家美国软件公司的完整办公环境（GitLab、ownCloud、RocketChat 等），agent 当数字员工干 175 个任务。其中 Finance 类 12 个（做电子表格、汇总报销、填财务数据），Admin 类另有 15 个含财务杂活。任务设计参照美国劳工部 O*NET 职业库。
- **下载：** https://github.com/TheAgentCompany/TheAgentCompany （整套以 Docker 镜像发布）
- **许可证：** MIT
- **状态：** `已核实可下`。强在办公环境真实感，不在会计深度。

### SymageDocs Coherent Forms
- **内容：** 同一合成身份跨三张真实美国政府表格的成套渲染件：**IRS Form 1040（2024 版，2 页）**、CMS-1500 医保理赔表、USCIS Form I-9，姓名、SSN、地址、雇主在三表间一致连通。共 3,000 页（train 2,400 / test 600，按身份切分，约 428 个身份，1040 部分按结构推算约 850 页）。每页是 PNG 页面图，带 FUNSD 格式真值（词框、实体标签、键值链接）。全合成、干净打字渲染；扫描退化版是厂商的付费产品。
- **下载：** https://huggingface.co/datasets/Symage/coherent-forms-1040-cms1500-i9
- **许可证：** SymageDocs Synthetic Dataset License v1.0：可内部使用（含商业训练与评测），**禁止再分发、禁止用来造竞争数据集**。HF 上 gated，点选同意并共享账号信息即可（自动批准）。
- **状态：** `已核实可下`。极少数以填好的美国税表文档本身为载荷的集之一。

### OfficeQA / OfficeQA Pro（Databricks）
- **内容：** 题目基于**美国财政部公报原始 PDF 整件**，697 期（1939 至 2025 年，PDF 约 4GB，另附解析 JSON 与转写文本衍生格式，原始 PDF 在包内）。Pro 版 133 题、Full 版 246 题，每题要跨平均 6.7 份公报做多步数值推理。另有单独 gated 的 Pro V2：语料扩至 1793 至 2024 年约 12 万页，90 题。
- **下载：** https://huggingface.co/datasets/databricks/officeqa （代码：https://github.com/databricks/officeqa ）
- **许可证：** 数据 CC BY-SA 4.0，代码 Apache-2.0；语料本身是美国政府出版物。HF 上点选同意（含承诺不用答案键训练受测模型）后可下。
- **状态：** `已核实可下`。属联邦财政文档，是会计相邻口径，不是纳税人税表，已如实标注。

### Drew-IPP 发票抽取基准
- **内容：** 181 份真实文件（113 份带文字层 PDF、53 份 JPEG 手机拍与手写、15 份 PNG 扫描，共 220 页），带答案键、判分器和生成器。全合成，由 InvoiceParser Pro 的厂商自制（卡片明说不是独立基准）；原始 191 份扣下 10 份未公开类型。
- **美国部分：** clean 子集 31 份是 US/UK/EU/ZA 格式混合，其中亲眼可见的 clean-us 文档至少 20 份（USD、美国销售税含州县两级税行、Net 30 条款）。发布方没有给按国家拆分的确切数字，自述为南非、英国、美国、欧盟约定混合，故记为：美国是主要构成之一，确切份数未公布。
- **下载：** https://huggingface.co/datasets/drew-ipp/invoice-extraction-benchmark （canonical 仓库含生成器与判分器：https://github.com/DrewKraken/invoice-extraction-benchmark ）
- **许可证：** 数据 CC BY 4.0，代码 MIT。无门槛。
- **状态：** `已核实可下`。

### NAF（National Archives Forms）
- **内容：** 美国国家档案馆与 FamilySearch 提供的真实历史联邦表格扫描图，大量手写填写：v2 全量 860 张（train 708 / val 75 / test 77），带字段框、文本框、关系与转写标注。是政府表格，不是税务会计专用表，量级小，只作美国表格类的补充项。
- **下载：** https://github.com/herobd/NAF_dataset （GitHub Release 里的 labeled_images.tar.gz）
- **许可证：** 仓库有 LICENSE 文件但 GitHub 标为未识别（NOASSERTION），商用前自行读原文确认。
- **状态：** `已核实可下`。

### Harvey LAB 的 tax 切片（Harvey）
- **内容：** Harvey 的法律 agent 基准按 27 个执业领域分目录，其中 **tax 文件夹有 34 个任务**，全是美国税务律师的活：回复 IRS 欠税通知（notice of deficiency）与信息调取请求、closing agreement 修订稿、§382 分析复核、§409A 估值复核、转让定价文档、税务法院起诉书、税务意见函与架构备忘录。每个任务是一个 task.json（指令、交付物、PASS/FAIL 评分标准）加一个 documents 文件夹的真实工作文件（抽查的这道带 10 个文件：docx 摘要与 IRS 通知、xlsx 报税附表、邮件链），agent 要产出一份 docx 交付物按标准判分。
- **下载：** https://github.com/harveyai/harvey-labs （tax 切片在 tasks/tax）
- **许可证：** MIT（仓库）。
- **状态：** `已核实可下`。属于大法律基准里切出来的一块，按「有美国税法、会计、审计内容就收」的口径收录；这批任务带文档文件，其他法律切片不保证带，逐题看。

### Finch / FinWorkBench
- **内容：** 基于真实企业文件包的财务会计多步 workflow 任务（改表、生成文档、问答），源材料以 Enron 与 EUSES 企业财务会计文件为主。172 个 workflow、384 个任务。
- **下载：** https://huggingface.co/datasets/FinWorkBench/Finch （评测代码：https://github.com/FinWorkBench/Finch ）
- **许可证：** 数据卡与代码仓均未标注（仓内无 LICENSE 文件），商用前要问作者。
- **状态：** `已核实可下`。材料里混有加拿大与英国政府机构件，不是纯美国口径，用前要筛。

### Snorkel FinQA（2026 新出，与 2021 年的 FinQA 不是一个东西）
- **内容：** RL 智能体环境：agent 用 4 个 MCP 工具在 22 家美国上市公司（Alphabet、Amazon、Apple 等）的真实 10-K 数据表里查数、算数、交答案，二值奖励。290 道专家题。
- **下载：** 据 Snorkel 2026-03-30 的博客，环境已在 OpenEnv 仓库开源，可克隆到本地下载数据运行，另有 Hugging Face Space 在线版。入口：https://snorkel.ai/blog/building-finqa-an-open-rl-environment-for-financial-reasoning-agents/
- **许可证：** 本轮未核实到明确标注。
- **状态：** `已核实可下`（按发布方口径），许可证待补。

## 部分可下与特殊许可证

### Vals AI Tax Agent Bench
- **内容：** 391 道专家撰写的美国税务研究题（联邦公司税、州税、合伙企业税、税务争议与程序、转让定价、申报披露、公司雇佣税），按带权重的专家检查项判分，含 must-pass 一票否决项。
- **下载：** https://github.com/vals-ai/tax-agent-bench 内含完整可跑的 harness 和 `data/public.json`（5 道公开样本题）。运行只需要自己的模型 API key 和 Tavily key，不需要 Vals 账号。
- **文档：** 不带。每道样本只有编号、一段文字案情和评分细则（已按 public.json 原文件核实）。税法依据靠 agent 自己联网检索，这正是要 Tavily key 的原因。
- **许可证：** MIT（仓库）。
- **状态：** `部分可下`。5 道样本加 harness 开源；193 道验证集付费授权；193 道测试集永久私有。

### Crypto Accounting Bench（CAB，Entendre Finance）
- **内容：** 118 道题，来自 7 家匿名化组织的真实账本：给一笔加密资产交易的全部证据，还原该组织当时实际记的那笔完整分录（科目、借贷方向、金额、资产数量全精度）。涵盖 21 种资产、10 条链、246 条非零参考分录行。每题带 task.md、prompt.md、input.json 和含冻结加权 rubric 的 expected_answer.json，仓库另有变换报告与发布审计文件。**整个发布包没有任何文档文件**（已按全量 483 个文件的文件树核实：只有 .md 和 .json，外加一个 .py 判分脚本）：全部证据，包括该组织的完整科目表（task_0001 里有 569 个科目）、金额、钱包地址、对手方与税批证据，都是 input.json 里的结构化 JSON，不是 PDF、表格或扫描件。
- **下载：** https://huggingface.co/datasets/Entendre/Crypto-Accounting-Bench （无门槛，已用文件树 API 核实，数据集 commit 0ec2596，最近修改 2026-09-15）
- **代码：** https://github.com/EntendreFinance/crypto-accounting-bench （Apache-2.0；用 `cab dataset download` 一条命令从 HF 拉约 500 个数据文件）
- **许可证：** 数据集是 **CC BY-NC 4.0，只能非商业使用**；代码是 Apache-2.0。商业产品评测直接拿来用有许可证风险，先处理授权。
- **论文：** https://arxiv.org/abs/2609.14811
- **状态：** `已核实可下`，带两条限定。一，公开的是**教育版变换数据**，不是评测原版：组织名、科目代码、链上标识、资产与链标签全替换，金额与数量重缩放，日期平移且时间戳精度降低，真实身份与变换映射不发布。二，论文头条分数是内部 LLM judge 管线跑的，未公开；公开的确定性判分器只能复现下限分，且公开版只有 4 道 gate，论文协议是 7 道。

### FinAuditing（TheFinAI）
- **内容：** 拿真实 US-GAAP 的 XBRL 申报文件做审计一致性检查，三个子任务：语义一致（FinSM，约 330 条）、关系一致（FinRE，约 440 条）、数值一致（FinMR，约 332 条）。
- **下载：** HF 上的 TheFinAI/en-finsm、TheFinAI/en-finre、TheFinAI/en-finmr；评测代码（MIT）在 https://github.com/The-FinAI/FinAuditing
- **状态：** `部分可下`。数据集是 gated，但门槛只是一个简短表格且填完自动批准，算能下，只是不是匿名直下。

### FinanceBench（Patronus AI）
- **内容：** 基于真实申报文件的财务 QA，全集 10,231 题。
- **状态：** `部分可下`。只开源了 150 题样本（仓库 https://github.com/patronus-ai/financebench 里的 data/financebench_open_source.jsonl），其余要联系 Patronus。不算整套。

### FinBen / PIXIU（TheFinAI）
- **内容：** 聚合 35 个数据集的评测框架（含 FinQA、TAT-QA 等），代码 MIT：https://github.com/The-FinAI/PIXIU
- **状态：** `部分可下`，只适合作找数据的入口：覆盖口径混合，还含中文、西班牙语和德国信用数据，不是纯美国口径集。

### BizBench（Kensho / S&P Global，2023）
- **内容：** 8 个专业财务任务族、测试集 5,448 条（FinCode 源自 CFA/CPA 练习题、SEC-Num 源自 SEC 文件、CodeFinQA、CodeTAT-QA、ConvFinQA Extract、TAT-QA Extract、FinKnow、FormulaEval）。论文明确说已发布 train、dev 和无标签 test 集。
- **状态：** `部分可下`。内容与规模已按论文核实，但本轮多方搜索没能定位确切下载地址（试探的一个 GitHub 地址是 404），先把缺口如实记下，链接待补，不拿它充数。

### Shelter Check（Can LLMs Identify Tax Abuse?）
- **内容：** 专家设计的避税安排，让模型判断是否违反税法（arXiv:2508.20097）。
- **状态：** `部分可下`。36 个策略只公开了 **5 个**，在 https://github.com/BlairStanek/LLM-Tax-Abuse ；其余作者故意不公开（防训练污染与滥用）。全集已与 IRS 研究者共享，合格研究者可签数据使用协议向通讯作者申请。仓库未见 LICENSE 文件。尽管如此，这是 SARA 之外唯一找到的另一个美国税法推理类公开资源。

### AA-Omniscience-Public（Artificial Analysis）
- **内容：** 领域知识题库的 600 行公开样本，其中 Accounting 主题只有 **20 题**（Accounting 13、Auditing 2、Taxation 5，内容是 GAAP/ASC、PCAOB、IRS 表格类知识题）。
- **下载：** https://huggingface.co/datasets/ArtificialAnalysis/AA-Omniscience-Public
- **许可证：** Apache-2.0（数据卡明示）。
- **状态：** `部分可下`。量很小，只适合当知识题补充，不适合当主评测集。

### JHU Tax Law NLP Resources（语料，不是评测集）
- **内容：** SARA 团队的原始语料：美国税务法院判例与 IRS 私人信件裁定（PLR），zip 可下（TaxCourtPLRCorpus.zip 约 154MB），托管在约翰霍普金斯数据存档，DOI 10.7281/T1/N1X6I4，CC BY-NC 4.0。
- **状态：** `部分可下`。是自建税务评测题的原材料，不是带评分的基准。

### FinBalance 与 FinRule-Bench（声称已发布，地址未钉死）
- **FinBalance**（arXiv:2606.15949）：多文档会计对账，确定性生成器产出分录、资产负债表与 23 个不一致代码，评测 split 710 条。论文写明生成器与 harness 以 Apache-2.0 发布、生成记录以 CC BY 4.0 发布、无隐藏评测集，但确切仓库地址本轮没提取到。**未核实。**
- **FinRule-Bench**（arXiv:2603.11339）：财报加会计原则的规则违规诊断（1,117 条干净记录、4,385 条单违规、400 条多违规）。论文给的只有匿名评审链接，打开返回 401；永久 GitHub/HF 仓库未定位到。**未核实。**

### PRBench（Scale AI）
- **内容：** 1,100 道专家撰写的专业推理题（Finance 600、Legal 500），每题带 10 到 30 条带权重的专家评分标准。带 topic 字段，税会题可以实际计数：Legal 的 Tax Law 17 题、Finance 的 Tax and Estate Planning 1 题、Finance 的 Accounting and Financial Reporting 1 题，合计 **19 题税会主题池**；没有 Audit 主题。
- **下载：** https://huggingface.co/datasets/ScaleAI/PRBench （CC BY 4.0，非 gated）
- **状态：** `部分可下`。两个限制：一，它是全球口径（114 个国家、47 个美国法域），19 题只是主题池，用前要逐题按法域筛美国的；二，形态是对话题加 rubric 判最终回复，没有文档包、没有文件交付物，只算部分接近 Harvey LAB 的形态。

### MMLU professional_accounting（知识题备注）
- **内容：** MMLU 里唯一的会计科目：test 282、validation 31、dev 5，共 318 道选择题，美国 GAAP 口径。MMLU-Pro 把会计混在 business 类目里没有独立标签，数不出来。
- **下载：** https://huggingface.co/datasets/cais/mmlu
- **状态：** `部分可下`。纯知识选择题：没文档、没交付物、没 rubric，只记录条数。

## 查过的 LAB 形态集：没有可数的美国税会切片

以下都是按 Harvey LAB 形态建的集（一题一个任务包、工作文件、交付物、专家 rubric），逐个查过，结论是切不出可数的美国税务、会计、审计任务。记下来免得重复查。

- **APEX-Agents v1**（https://huggingface.co/datasets/mercor/apex-agents ，CC BY 4.0，gated 自动批准）：480 个任务、33 个 world（每个平均约 166 个文件），prompt 加二值 criteria rubric 加专家金标产出，是找到的与 LAB 形态最接近的。但职业只有 Investment Banking 160、Corporate Law 160、Management Consulting 160，没有 Accounting、Tax、Audit 类别，也没有可数的税务子标签。切片：**0**。
- **APEX-Agents v1.1 Harbor 版**（https://huggingface.co/datasets/mercor/apex-agents-v1.1 ，CC BY 4.0，gated）：实际数到 240 个任务文件夹，一题一包（agent 配置、environment、verifier、world 镜像）。对文件夹名扫 tax、account、audit、bookkeep 关键词，结果 **0**。
- **APEX-1 extended**（https://huggingface.co/datasets/mercor/APEX-v1-extended ，CC BY 4.0，非 gated）：母集 400 题公开 100 题，每题有 Domain、Prompt、Rubric JSON 和附件字段，但 100 题里只有 11 题真挂了附件。官方没有 Tax 或 Accounting 标签；人工逐条读完 100 题 prompt，挑出 3 道税务主题题（私人财富税务居民、遗产税加 S corp 估值、房地产基金 carried interest 税务策略）。这 3 道只能算人工候选池，不是官方切片，法域与附件也未逐题确认。
- **BigLaw Bench 样本**（https://github.com/harveyai/biglaw-bench ）：这是 Harvey 自家的早期基准（常被误记为 Vals 的）。仓库只有公开样本（core 样本 CSV、诉讼证据 PDF、workflow 与 retrieval 样本），母集 100 个 triplet 的全量数据仍私有。扫全仓 72 条路径，tax 相关 **0**；其衍生子集 JudgmentBench（30 题）也没有税务类别。
- **OfficeBench**（https://github.com/zlwang-cs/OfficeBench ，Apache-2.0）：300 个可下载的办公任务，带真实文件（xlsx、eml、ics），但判分是精确与模糊匹配加执行校验，不是专家 rubric；分类按用了几个应用，不按专业领域。没有可数的税务、会计、审计标签。

### FinMRAGBench（ACL 2026）
- **内容：** 887 道专家核验 QA，语料是美国 10-K 年报原文 PDF（723 份、96,549 页，文件命名 TICKER_10K_YEAR）。
- **状态：** `部分可下`。标注文件已在 GitHub 仓库 https://github.com/sqyangit/FinMRAGBench （Apache-2.0），但文档语料本身还没放：README 原话是年报语料和来源清单「soon」才发布，现阶段要自己按清单去 EDGAR 重建，算半套。

### FinTabNet
- **内容：** 标普 500 年报里的 112k+ 张财务表格，带结构标注。
- **状态：** `部分可下`，且按带文档的严格标准只算边际符合：发行的只有从页面裁出的表格区域图加标注，没有年报整件。原版走 IBM 数据交换站 https://developer.ibm.com/data/fintabnet/ （需 IBM 账号与协议，CDLA-Permissive-1.0）；清洗版 FinTabNet.c 可在 HF 直下（bsmock/FinTabNet.c，CDLA-Permissive-2.0）。

## 已核查、不可下载

| 基准 | 公开存在的只有 | 为什么下不了 |
|---|---|---|
| APEX-Accounting 全套（160 题） | 论文、排行榜、dev set | 设计上封闭以防训练污染；截至 2026-10-24 在 GitHub、HF、arXiv 均无泄露或镜像 |
| DualBench100（DualEntry） | 19 个模型的结果页、方法论论文、8 道示例题（每类一道） | 101 题题库、参考答案与评分规则均未发布，无官方 GitHub 仓库 |
| AuditBench（Wang 等，2025） | 只有论文（arXiv:2506.17282；Springer CCIS 2533） | 无数据或代码发布，未留申请渠道。注意勿与同名的模型安全 AuditBench（Sheshadri 等，2026）混淆 |
| AccountingBench（Penrose，2025） | 只有报告页（accounting.penrose.com） | 基于一家真实 SaaS 公司一整年的真实银行、工资、支付数据，性质上不可能公开 |
| FinMaster（Jiang 等，2025） | 只有论文（arXiv:2505.13533） | GitHub 与 HF 均无该团队的仓库或数据集 |
| Blue J 内部基准 | OpenAI 案例里提过（350 多道题，覆盖美、加、英税法） | 厂商内部发布门禁，从未公开 |
| Basis 内部评测 | OpenAI 案例里描述过（过程加结果的检查，基于真实客户式工作） | 厂商内部；题目、评分输出与轨迹均不公开 |
| Vals TaxEval v2 | 20 题公开验证集（需向 Vals 申请） | 300 题验证集付费授权，1,223 题测试集官方称从不共享 |
| Digits 记账基准（2026） | 只有厂商新闻稿与报告（2,000 笔真实小企业交易、US GAAP 金标） | 未找到任何数据下载发布 |
| AuditFraudBench | 只有论文（arXiv:2606.08345），基于 SEC AAER 与原始/重述 10-K、10-Q 的欺诈识别 | 论文与各路检索均无代码或数据链接 |
| Rivet TaxBench | 只有厂商结果页（rivet.tax/taxbench） | 无数据下载 |
| CPA 考试题集 | 没找到合法开放的 | HF、GitHub、Kaggle、Zenodo 多路搜过，只有 Docsity、Stuvia 一类付费题库转卖站，来源与合法性不可验；不存在可合法开放下载的 AICPA 释放题数据集 |
| BigLaw Bench 全集与 BigLaw Bench: Research（Harvey） | 公开样本、博客与排行榜 | 100 个 triplet 全集私有（要联系 Harvey）；2026 年的 Research 版 practice area 名单里确实有 Tax，但没有公开数据可下 |
| Vals Legal Research Bench | 只有排行榜页，按 practice area 约 294 题 | 里面根本没有 Tax、Accounting、Audit 类别，任务数据也不公开 |

## 核查方法

1. 打开实际的数据集或仓库页面，不看新闻稿和聚合站。
2. 确认不登录就能拿到真实文件或数据行；有门槛的，把门槛写清楚。
3. 每条记录写明任务数、许可证和可比性限制。
4. 复查带日期；某个基准改了开放方式，就更新它的条目，不偷偷替换。
