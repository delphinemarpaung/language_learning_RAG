# Domain-Specific Mandarin Vocabulary Learning with LLM & RAG

An AI-powered Mandarin learning pipeline designed for domain-specific vocabulary acquisition (e.g., Computer Science, Law, Medicine, Economy). By combining statistical text analysis, Large Language Models (LLMs), and Retrieval-Augmented Generation (RAG), this project extracts top domain terms from authentic Chinese texts and generates natural, contextually accurate dialogues for language learners.

---

## 📌 Problem Background

Traditional Mandarin language learning materials focus primarily on general conversational vocabulary (e.g., HSK curriculum). However, professional users often need to acquire specialized vocabulary suited to their specific fields—such as **Computer Science**, **Law**, **Medicine**, **Economy**, or **Environment**.

Learning domain-specific vocabulary effectively requires authentic contexts. This project addresses that need by:
1. Extracting high-impact vocabulary for each domain.
2. Generating structured explanations and domain-aware dialogues via LLMs.
3. Leveraging RAG (Retrieval-Augmented Generation) on real news texts to ensure the generated learning scenarios mirror real-world professional language usage.

---

## ✨ Key Features

* **Authentic Corpus Integration**: Processes the Simplified Chinese news dataset from **Fudan University**, covering 20 diverse categories (Computer, Law, Medical, Economy, Politics, Environment, etc.).
* **NLP Text Processing and Vocabulary Extraction**: 
  * Tokenization, stop-words filtering, and entity removal with Named Entity Recognition (NER).
  * Calculates TF-IDF scores across categories to isolate distinct, high-impact vocabulary for each domain.
* **Randomized Word Sampling & LLM Explanations**: Selects random target words from a chosen domain and prompts the LLM to return structured translations, definitions, and short example sentences.
* **Context-Aware Dialogue Generation via RAG**:
  * Chunks text corpora into vector embeddings and indexes them using **ChromaDB**.
  * Retrieves native context passages for target vocabulary items.
  * Guides the LLM using retrieved context to produce natural, field-specific conversational dialogues in Simplified Chinese with English translations.

---

## 🛠️ System Architecture & Workflow

1. **Preprocessing & Feature Extraction**:
   * Text preprocessing.
   * Extracts top 100 keywords per domain.

2. **Vector Store & Indexing**:
   * Document chunking using LangChain.
   * Embeddings generated via HuggingFace transformers and stored in Chroma vector databases partitioned by topic.

3. **RAG-Driven Prompting**:
   * User selects a target topic and word batch size $K$.
   * Relevant snippets are retrieved using ChromaDB vector search.
   * OpenAI GPT model receives target words + retrieved context to construct authentic dialogue exercises.

---

---

## 🚀 Getting Started

### Prerequisites

Ensure you have Python 3.10+ installed.

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/mandarin-rag-learning.git
   cd mandarin-rag-learning
   ```

2. **Install dependencies:**
   ```bash
   pip install openai langchain langchain-community langchain-chroma langchain-huggingface jieba tqdm python-dotenv
   ```

3. **Environment Setup:**
   Create a `.env` file in the root directory and set your OpenAI API key:
   ```env
   OPENAI_API_KEY=your_openai_api_key_here
   ```

4. **Download dataset:**
   * Download Fudan News dataset from: https://www.kaggle.com/datasets/louislung/categorised-news-dataset-from-fudan-university
   * Extract and save in the project directory

---

## 💡 Usage

Open and run `mandarin_rag_learning.ipynb` in your preferred Jupyter environment:

```bash
jupyter notebook mandarin_rag_learning.ipynb
```

### Main Pipeline Steps in Notebook:
1. **Dataset Scanning**: Reads filepaths across 20 domains from the Fudan news directory.
2. **Vocabulary Extraction**: Runs POS-tagged tokenization and TF-IDF calculation to export `top_vocabs.json`.
3. **ChromaDB Vector Store Setup**: Indexes document chunks for targeted domains.
4. **Baseline LLM Dialogue Generation**: Prompts the model to explain words and generate dialogues without background context.
5. **RAG Dialogue Generation**: Retrieves authentic text passages for the selected words and generates contextually accurate, professional conversations.

---

## 📊 Example Output

### Top Vocabulary (`Computer` Domain)

> Top 20 vocabularies for Computer topic
> 算法 , 模型 , 函数 , 定义 , 服务器,
> 数据, 控制器 , 矩阵 , 图 , 本文,
> 结点, 数据库 , 参数 , 描述 , 引理,
> 文档 , 给出 , 神经网络 , 对象 , 输出

### Vocabulary explanation from LLM

| Word | Meaning | Computer-domain example |
|---|---|---|
| **查询** (cháxún) | to query; to look up or retrieve information | **你可以查询数据库中的用户信息。** — You can query user information in the database. |
| **分布** (fēnbù) | distribution; to be distributed | **这些文件分布在多个服务器上。** — These files are distributed across multiple servers. |
| **定义** (dìngyì) | to define; a definition | **请在代码中定义一个变量。** — Please define a variable in the code. |
| **方法** (fāngfǎ) | method; approach; in programming, a method | **这个类有一个读取文件的方法。** — This class has a method for reading files. |
| **输入** (shūrù) | input; to enter or input data | **请在搜索框中输入关键词。** — Please enter a keyword in the search box. |

### RAG-Enhanced Dialogue Example (`Computer` Domain)

**Input Words**: `查询` (Query), `分布` (Distribution), `定义` (Define), `方法` (Method), `输入` (Input)

**Generated Output**:

> **中文**
> 
> **甲**：我们先输入加工实例，再用与数据库相连的方法查询相关数据。  
> **乙**：好的。这个模型的定义是什么？  
> **甲**：它根据产品的功能特征进行定义，查询结果会显示特征的分布。
>
> ---
> 
> **English**
> 
> **A**: Let’s first input a processing example, then use the database-linked method to query the relevant data.  
> **B**: All right. What is the definition of this model?  
> **A**: It is defined according to the product’s functional features, and the query results show how those features are distributed.

---

## 🛡️ License

This project is open-source and available under the [MIT License](LICENSE).