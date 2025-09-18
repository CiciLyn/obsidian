> 主要是看数据集来源，使用方式。


# AgentClinic
>后续论文都是cite 了 agentclinic的论文

一句话概括论文：

使用的EHR数据集来自：
1. MIMIC-IV
2. NEJM: New England Journal Medicine case challenges
3. MedQA

其中，

## MIMIC-IV
重症数据库。
2008-2019，18岁以上。
于2003年在美国国立卫生研究院的资助下，由美国麻省理工学院计算生理学实验室、美国哈佛医学院贝斯以色列女执事医疗中心(Beth Israel Deaconess Medical Center，[BIDMC](https://zhida.zhihu.com/search?content_id=230980165&content_type=Article&match_order=1&q=BIDMC&zhida_source=entity))和飞利浦医疗公司共同建立。
主要是多个诊断的病人的住院全流程信息；从~40k个病例中选择first 200 之拥有一种疾病的病人 / ~6k. MIMMIC-IV 包含亚洲、非洲、白人等多种族。

![[Pasted image 20250918122736.png]]
MIMIC-IV 主要板块如下：
- Hosp：实验室测量，微生物学，药物管理，和收费诊断；
- ICU：在ICU内收集到的信息，包括静脉给药、呼吸机设置和其他图表项目...
- ED：急诊信息。包括急诊诊断，病人体征等信息；
- CXR：胸片以及影像学报告(dicom 或 jpg)；
- Note：所有文本报告：出院、超声、心电、影像等报告；出院总结（主诉、现病史、既往病史、简要病程、体格检查和出院诊断）；放射学报告（x射线、CT、MRI、超声）. 


## NEJM: New England Journal Medicine case challenges
NEJM 是四大医学期刊质疑，由美国[麻省医学会](https://zhida.zhihu.com/search?content_id=108188221&content_type=Article&match_order=1&q=%E9%BA%BB%E7%9C%81%E5%8C%BB%E5%AD%A6%E4%BC%9A&zhida_source=entity)（Massachusetts Medical Society）所出版的同行评审性质全科医学周刊。NEJM最新影响因子（IF）为72.406。位居四大医学期刊之首。

以文本的方式展示完整的病例信息。包括症状、检查，既往史，个人史...
![[Pasted image 20250918125943.png]]![[Pasted image 20250918130130.png]]


## MedQA
采用多项选择题格式的医学文本问答数据集，其问题选自美国(USMLE)、中国大陆(MCMLE)及中国台湾医学委员会(TWMLE)的考试. 旨在考查医生的专业知识及临床决策能力
> 使用：找到有详述病人病情的题目。转化为case，作为输入。进行模拟问诊。
![[Pasted image 20250918130803.png]]

# ==Self-Evolving Multi-Agent Simulations for Realistic Clinical Interactions==
> [2503.22678](https://arxiv.org/pdf/2503.22678)

主要做的事情：做了一个模拟沙盒游戏 MedAgentSim。模拟问诊、开检查，做了一个benchmark, 测试医生agent表现。**做了self-improving mechanism, 这样医生模型就可以不断精进他们的问诊策略**. 

使用的数据集：来自huggingface
- NEJM dataset & NEJM Extended：==用的agentclinic用的NEJM数据。分别有15条和120条。==
> {"image_url": "https://csvc.nejm.org/ContentServer/images?id=IC20230713&width=1500&height=4000", "question": "A 78-year-old man with chronic obstructive pulmonary disease (COPD) presented with a 2-month history of dysphonia. For the past 10 years, he had used an inhaled glucocorticoid daily to manage his COPD. Fiberoptic laryngoscopy revealed white plaques on both vocal cords. A biopsy showed hyperkeratinized stratified squamous epithelium and threadlike filaments that stained with Grocott-Gomori methenamine silver stain. What is the most likely diagnosis?", "patient_info":"You are a 78-year-old man who has been managing chronic obstructive pulmonary disease (COPD) for many years, primarily using an inhaled glucocorticoid daily. Recently, you've noticed a change in your voice, which has become hoarse over the past two months. Upon examination by a specialist, they found white patches on your vocal cords.", "physical_exams": "Fiberoptic laryngoscopy: White plaques on both vocal cords. Biopsy: Hyperkeratinized stratified squamous epithelium and threadlike filaments. Grocott-Gomori methenamine silver stain: Positive staining of threadlike filaments.", "answers": [{"text": "Laryngeal amyloidosis", "correct": false}, {"text": "Laryngeal candidiasis", "correct": true}, {"text": "Laryngeal papillomatosis", "correct": false}, {"text": "Leukoplakia", "correct": false}, {"text": "Vocal-cord dysfunction", "correct": false}]}
- MedQA：QA问题对。来自：[arXiv:2009.13081v1 [cs.CL] 28 Sep 2020](https://arxiv.org/pdf/2009.13081)
>题目：What disease does this patient have?
- MIMIC-IV


罕见病的benchmark

# # Enhancing diagnostic capability with multi-agents conversational large language models
> [Enhancing diagnostic capability with multi-agents conversational large language models | npj Digital Medicine](https://www.nature.com/articles/s41746-025-01550-0)

受到跨学科医疗团队讨论诊断的影响，开发MAC(Multi-Agent Conversation)模式进行诊断，诊断准确率大于CoT, Self-Refine, Self-Consistency. 
![[Pasted image 20250918143755.png]]![[Pasted image 20250918143814.png]]

302 kinds of rare disease from 33 different disease categories. One to nine kinds of rare disease were randomly selected for each category.
examined rare diseases using clinical case reports published after January 1, 2022, from the **Medline database**. (Medline是PubMed的基础和子集。)、
示例：
`{`
  `"Type": "病例类型（例如疾病所属类别，如手术、综合征等）",`
  `"Number": "病例编号或序号",`
  `"Selected": "是否被选中（例如 Yes/No）",`
  `"Final Name": "最终确诊的疾病名称",`
  `"Case URL": "病例的唯一标识或链接（通常是数字或URL）",`
  `"Initial Presentation": {`
    `"Basic Information": "患者的基本信息（年龄、性别、家庭情况等）",`
    `"Clinical Presentation": "临床表现（主要症状、临床特征、诊断情况）",`
    `"Physical Examination": "体格检查发现（如面容特征、发育异常等）",`
    `"Past Medical History": "既往史、家族史、产前产后史等",`
    `"Initial Test Results": "初步检查的结果（如化验、影像学等）"`
  `},`
  `"Follow-up Presentation": {`
    `"Basic Information": "患者的基本信息（与初诊相同，用于复诊描述）",`
    `"Clinical Presentation": "复诊时的临床表现（症状是否持续、加重或改善）",`
    `"Physical Examination": "复诊时的体格检查结果",`
    `"Past Medical History": "复诊时补充的病史信息",`
    `"Initial Test Results": "复诊时的初步检查结果",`
    `"Further Diagnostic Tests": "进一步的诊断检查（如基因检测、MRI、CT等）"`
  `}`
`}`

# # A Preliminary Study of o1 in Medicine: Are We Closer to an AI Doctor?
> [2409.15277](https://arxiv.org/pdf/2409.15277)

测试o1在Understanding, reasoning 等方面的医疗相关的能力。
![[Pasted image 20250918152232.png]]


# AI Agents for Conversational Patient Triage: Preliminary Simulation-Based Evaluation with Real-World EHR Data
> [AI Agents for Conversational Patient Triage: Preliminary Simulation-Based Evaluation with Real-World EHR Data](https://arxiv.org/pdf/2506.04032)

测试 LLM patient simulator 的可行性：其回答与输入的EHR info 的 一致性高达99.7%. 

EHR 数据来源：<未开源，未有github仓库>
a dataset of deidentified real-world EHR records sourced from **HealthVerity**, a data provider. The dataset contained 21,779 deidentified records related to clinical encounters from 1,000 unique non-cancer patients, with each patient contributing multiple records. These encounters occurred between May 1, 2021, and April 30, 2024. Each record included routinely collected clinical data, such as patient demographics (age and gender), chief complaint, his tory of present illness, review of systems, past medical history, current medications, allergies, immunizations, social history, and family history. 


# An evaluation framework for clinical use of large language models in patient interaction tasks
> [An evaluation framework for clinical use of large language models in patient interaction tasks | Nature Medicine](https://www.nature.com/articles/s41591-024-03328-5)

在对话过程中(CRAFT-MD framework)，测试 LLM 对话、记录病史、诊断准确性的能力。

使用的数据：<总量2000>
> craft-md: [craft-md/data at main · rajpurkarlab/craft-md](https://github.com/rajpurkarlab/craft-md/tree/main/data)

MedQA-USMILE: MedQA中美国医疗委员会(USMILE)的试题中的病人的 case vignettes (1800)

Derm Public: 在线题库(100)

Derm Private: 100 newly generated private cases

*NEJM Image Challenge: images and corresponding vignettes: 仅用作测试medical image interpretation capabilities.* 


# # MedJourney: Benchmark and Evaluation of Large Language Models over Patient Clinical Journey
> [[PDF] MedJourney: Benchmark and Evaluation of Large Language Models over Patient Clinical Journey | Semantic Scholar](https://www.semanticscholar.org/paper/MedJourney%3A-Benchmark-and-Evaluation-of-Large-over-Wu-Zhao/6a8d0363cf6563b3157ececb84e864d9773368f6)

将病人进入医院后的过程分为4步：planning, access, delivery, and ongoing care. 并对应使用 12 个datasets 评估 LLM 的临床医疗能力。 12 个数据集中有 5 个是新提出的：Department Recommendation (DR), Pre-Consultation Dialogue Summary (PCDS), Hospital Reception QA(HQA), Insurance QA (IQA) and DrugQA (DQA) are newly proposed. 

所有的5个自创数据集都是 doctor-written 的。

而后面的 7 个数据集分别是...


# DeepRare
