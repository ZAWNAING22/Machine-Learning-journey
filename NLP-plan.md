You can complete this project in **3 focused days**, but you need to follow the correct order. Don't start by writing the paper or making slides. First, produce real experimental results. Then write the paper based on those results. Finally, build the presentation from the paper.

Your approved topic is:

**Tokenization and Multilingual Fairness: Comparing English and Turkish Across Three Pretrained Tokenizers**

The goal is to compare how many tokens three tokenizers use for the same English and Turkish sentences.

# **1. Understand the whole project**

## **Your project workflow**

1. **Experiment**

   Collect English–Turkish sentence pairs, run three tokenizers, count tokens, and save results.
2. **Analysis**

   Compare token counts, calculate ratios and statistics, create graphs, and inspect examples.
3. **Research paper**

   Explain the problem, review previous research, describe your experiment, and report your findings.
4. **Presentation**

   Teach the topic, explain previous research, show your experiment and results, and prepare for questions.
5. **Final submission**

   Check all files, compile the paper, test the code, and submit the complete package.

# **2. Day 1 — Complete the experiment**



Most important day

**Goal: finish your Python experiment and obtain real results.**



Estimated time: 7–9 hours.

### **Step 1 — Set up your working environment**

Use Google Colab. You don't need a GPU for this project.

Open:

- [Google Colab](https://colab.research.google.com/?utm_source=chatgpt.com)
- [FLORES-200 dataset](https://huggingface.co/datasets/facebook/flores?utm_source=chatgpt.com)

Create a notebook named:

`SEN534_Tokenization_Experiment.ipynb`

Install the libraries:

```
!pip install transformers datasets pandas numpy scipy matplotlib seaborn
```

### **Step 2 — Understand your dataset**

Use the FLORES-200 dataset, which contains translated sentences in different languages.

You need:

- English: `eng_Latn`
- Turkish: `tur_Latn`
- One consistent dataset split, such as `dev`
- 500 aligned English–Turkish sentence pairs for the main experiment

Important: use the same sentence IDs for both languages. That means you compare translations of the same sentences, not unrelated English and Turkish text.

First test your complete pipeline on approximately 100 examples, as the professor recommends. Then run your final experiment on your selected sample.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



### **Step 3 — Load three tokenizers**

You will compare these:

| Tokenizer | Model                          | Tokenization method |
| --------- | ------------------------------ | ------------------- |
| GPT-2     | `openai-community/gpt2`        | BPE                 |
| mBERT     | `bert-base-multilingual-cased` | WordPiece           |
| XLM-R     | `xlm-roberta-base`             | SentencePiece       |

You are not training these models. You are only using their existing tokenizers to count tokens.

For example, one English sentence might produce 10 tokens, while its Turkish translation produces 16 tokens.

### **Step 4 — Calculate token counts**

For every sentence pair, record:

- Sentence ID
- English sentence
- Turkish sentence
- English token count
- Turkish token count

Repeat the counting for all three tokenizers.

Save the results in a CSV file.

### **Step 5 — Analyze the results**

Your main calculation is:

\\[ R = \frac{\text{Turkish token count}}{\text{English token count}} \\]

Example:

| Language | Token count |
| -------- | ----------- |
| English  | 10          |
| Turkish  | 15          |

\\[ R = \frac{15}{10}=1.5 \\]

This means the Turkish translation uses 1.5 times as many tokens for that pair.

Calculate:

- Mean token count
- Median token count
- Standard deviation
- Mean and median token ratio
- 95% confidence interval for the ratio

You can also use a paired statistical test, such as the Wilcoxon signed-rank test, if appropriate for your data.

### **Step 6 — Create two graphs**

[Data Visualization Guide: Histograms, Box Plots & Scatter Plots for Exploratory Analysis - Interactive | Michael Brenndoerfer | Michael Brenndoerfer](https://images.openai.com/static-rsc-4/Fbt0aPASHVqCszmQcRGjQmGCdt1eihCjmqaXEYyS6mVDn2S2rvJt8S5dtxa5GlkkfQrUcR-oYSCfLNkeXeZjeI5M-yWi_ynsVrwp1XUWuoqICUf6jAfZUB7TFx8Bo6-9pz_vlbemfUz4UtK-cq1tdmTDNJDxRftYuot_F2oaYJc?purpose=inline)

**Graph 1: Box plot**

Compare Turkish-to-English token ratios across the three tokenizers.

[Mehrsprachigkeit, digitale Praxis und Schreibfähigkeit | Unterrichtswissenschaft | Springer Nature Link](https://images.openai.com/static-rsc-4/DY9ffd7kr51i3jjCBJdGwid_AACKc6VCkKA3S6QBsHpLgmUeqHOGYOKvgcUpXB0ESwEsv84a7XS6EvhQtrBnN4qMTThwQehPJKp2uCnDeMBTcrwl3a9am0BiUddxYJycLLxBt6HNHSRdjAlgDZYKXTfHsWGPAI9mIvkUfFs7ugY?purpose=inline)

**Graph 2: Bar chart**

Compare average English and Turkish token counts.

### **Step 7 — Diagnostic analysis**

Your professor requires an error analysis or equivalent diagnostic analysis. Because your project is an audit rather than a prediction task, you should email the professor to agree on the diagnostic method before conducting it.

A possible method is:

- Select the 20 sentence pairs with the highest Turkish-to-English token ratios.
- Inspect the actual tokenization.
- Identify recurring patterns.
- Count each category and give 2–3 examples.

Do not assume a linguistic explanation without evidence.

**End of Day 1 deliverables:**

- Working Colab notebook
- Dataset and sampling details
- CSV results
- Statistical summary
- Two graphs
- Diagnostic examples, after instructor approval

# **3. Day 2 — Write the research paper**



Main writing day

**Goal: complete a six-page IEEE research paper.**



Estimated time: 8–10 hours.

Use the professor's official LaTeX template, not a different IEEE template. The maximum is six pages, including references and declarations.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



Open [Overleaf](https://www.overleaf.com/?utm_source=chatgpt.com) and create a project using the official template.

### **Your paper structure**

| Section                          | What you should include                                                         |
| -------------------------------- | ------------------------------------------------------------------------------- |
| Title and Abstract               | Topic, research question, method, actual main result                            |
| 1. Introduction                  | What tokenization is, why multilingual fairness matters, your research question |
| 2. Related Work                  | At least 6 research papers, including at least 2 from 2023 onward               |
| 3. Method                        | Dataset, sample size, tokenizers, procedure, metrics                            |
| 4. Results                       | Results table and one or two graphs                                             |
| 5. Error Analysis and Discussion | Diagnostic categories, examples, and your interpretation                        |
| 6. Conclusion                    | Answer your research question and suggest future work                           |
| Limitations                      | What your experiment cannot demonstrate                                         |
| AI Tool Use Declaration          | Explain how you used AI tools                                                   |
| References                       | IEEE numbered references                                                        |

These sections follow the professor's required structure.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



### **How to write each section**

**1. Introduction — approximately ½ page**

Explain:

- What tokenization means.
- Why tokenization matters in NLP.
- Why English and Turkish are interesting to compare.
- Your research question.

A possible research question is:

*How do three pretrained tokenizers differ in their tokenization efficiency for aligned English and Turkish sentences?*

**2. Related Work — approximately 1–1.5 pages**

You need at least six actual research papers, with two published in 2023 or later.

Start by reading these:

1. Petrov et al. (2023) — *Language Model Tokenizers Introduce Unfairness Between Languages.*
2. Ahia et al. (2023) — *Do All Languages Cost the Same? Tokenization in the Era of Commercial Language Models.*
3. Toraman et al. (2023) — *Impact of Tokenization on Language Models: An Analysis for Turkish.*
4. Rust et al. (2021) — *How Good Is Your Tokenizer? On the Monolingual Performance of Multilingual Language Models.*
5. Conneau et al. (2020) — *Unsupervised Cross-lingual Representation Learning at Scale.*
6. Devlin et al. (2019) — *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.*

Find and open the actual publications using [Google Scholar](https://scholar.google.com/?utm_source=chatgpt.com) or [ACL Anthology](https://aclanthology.org/?utm_source=chatgpt.com). Verify the publication details and read each paper before citing it.

**Important AI restriction:** Your professor does not allow AI assistants to write Related Work, Analysis, Discussion, Conclusion, or Limitations. I can explain the papers and concepts, but you must write and interpret those sections yourself.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



**3. Method — approximately 1 page**

Explain:

- FLORES-200 dataset
- English and Turkish language codes
- Number of sentence pairs
- Three tokenizers
- How token counts are calculated
- Statistical measurements
- Software and library versions
- Random seed and code location

**4. Results — approximately ½–1 page**

Insert your real results table and graphs.

For example, your table can look like this:

| Tokenizer | English mean  | Turkish mean  | Ratio         |
| --------- | ------------- | ------------- | ------------- |
| GPT-2     | Actual result | Actual result | Actual result |
| mBERT     | Actual result | Actual result | Actual result |
| XLM-R     | Actual result | Actual result | Actual result |

Never fill this table with estimated or invented numbers.

**5. Diagnostic analysis and discussion**

Explain the patterns you actually observed in the sentence pairs. Include category counts, denominators, and examples.

**6. Conclusion and limitations**

Summarize what your evidence supports and what your experiment cannot establish.

**7. Abstract**

Write this last, after you know your results. It must be 150–200 words.

### **Day 2 final checks**

- Six papers read and checked
- Related Work written 
- Introduction completed
- Method completed
- Actual results inserted
- Discussion and diagnostic analysis written 
- Conclusion and limitations completed
- Abstract written
- IEEE references checked
- Paper compiles and is no longer than six pages

# **4. Day 3 — Prepare your presentation and submission**



Final day

**Goal: create slides, practice, and prepare all submission files.**



Estimated time: 7–9 hours.

Your professor expects a presentation of approximately **45 minutes**, followed by 15 minutes of discussion. It should teach the topic, explain previous research, and present your experiment.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



### **Suggested 20-slide presentation**

| Slide | Topic                                 |
| ----- | ------------------------------------- |
| 1     | Title and your information            |
| 2     | What is Natural Language Processing?  |
| 3     | What is tokenization?                 |
| 4     | Words, subwords, and tokens           |
| 5     | Why multilingual tokenization matters |
| 6     | BPE, WordPiece, and SentencePiece     |
| 7     | Why Turkish is interesting            |
| 8     | Previous research overview            |
| 9     | Main 2023 fairness research           |
| 10    | Research gap                          |
| 11    | Research question                     |
| 12    | FLORES-200 dataset                    |
| 13    | Three pretrained tokenizers           |
| 14    | Experimental workflow                 |
| 15    | Token-counting example                |
| 16    | Main results table                    |
| 17    | Comparison graphs                     |
| 18    | Diagnostic analysis and examples      |
| 19    | Limitations and future work           |
| 20    | Three things to remember and Q&A      |

### **How to divide the 45 minutes**

| Part                                | Time       |
| ----------------------------------- | ---------- |
| Introduction and motivation         | 5 min      |
| NLP and tokenization background     | 8 min      |
| Related work                        | 10 min     |
| Your question and method            | 7 min      |
| Results                             | 7 min      |
| Diagnostic analysis and limitations | 5 min      |
| Three key takeaways                 | 3 min      |
| **Total**                           | **45 min** |

Use simple diagrams and graphs rather than paragraphs. You should be able to explain every number on your slides and in your code. Practice once with a timer.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



### **Prepare for questions**

Make sure you can answer these:

1. What is tokenization?
2. What is the difference between BPE, WordPiece, and SentencePiece?
3. Why did you choose Turkish and English?
4. What is FLORES-200?
5. Why did you select these three tokenizers?
6. What does the token ratio mean?
7. Why do you use aligned sentence pairs?
8. What does your main result show?
9. What are the limitations of your experiment?
10. What is the difference between tokenization efficiency and language fairness?

# **5. Final submission checklist**

Your professor requires all five submission items to be submitted together.&#x20;

SEN534_Research_Project_Guidelines_Fall2026.pdf



## **Final files**

**Submission progress**

0/5

Research paper PDF (maximum 6 pages)

LaTeX source ZIP (compiles on Overleaf)

Python code ZIP or repository with README

Presentation slides PDF

Completed feedback form (Word)

Your code README should explain:

- Python and library versions
- Dataset and split
- How to run the notebook or script
- Random seed
- How to reproduce the results

Also include the required AI Tool Use Declaration. Be honest about how AI helped you with code, explanations, and formatting. Do not claim that you wrote everything without assistance.

# **6. Your exact three-day timetable**

| Time      | Day 1                   | Day 2                          | Day 3                     |
| --------- | ----------------------- | ------------------------------ | ------------------------- |
| Morning   | Dataset and setup       | Related Work                   | Slides 1–10               |
| Afternoon | Tokenizers and counting | Introduction and Method        | Slides 11–20              |
| Evening   | Statistics and graphs   | Results and remaining sections | Practice and final checks |
| Night     | Save code and results   | Compile paper                  | ZIP and submission        |

# **7. How we should work together**

I recommend that we complete this in small steps rather than trying to write everything at once.

## **Start with Day 1**

**Our first task:** Build the Colab notebook step by step.

We will:

1. Install the libraries.
2. Load FLORES-200.
3. Understand the dataset structure.
4. Load the three tokenizers.
5. Test five sentence pairs.
6. Run the full experiment.
7. Calculate the results and create graphs.

Recommended next step

Start Day 1 — Build the experiment

**My main advice:** Do not spend three days trying to make a perfect paper. Focus on a working experiment, six papers you genuinely understand, honest results, and a presentation you can confidently explain. Your professor values reproducibility and understanding more than complicated models.
