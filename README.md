# 🔤 Tokenizer Playground: Exploring Hugging Face Tokenizers

This repository provides a comprehensive exploration of the various tokenization algorithms available in the Hugging Face `tokenizers` library. It aims to serve as both a learning resource and a practical toolkit for experimenting with different tokenization approaches.

## 📋 Table of Contents

- [Introduction](#introduction)
- [Tokenizer Types](#tokenizer-types)
  - [Byte-Pair Encoding (BPE)](#byte-pair-encoding-bpe)
  - [WordPiece](#wordpiece)
  - [Unigram](#unigram) 
  - [SentencePiece](#sentencepiece)
  - [Character-Based](#character-based)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Experiments](#experiments)
- [Analysis Tools](#analysis-tools)
- [Contributing](#contributing)
- [License](#license)

## 🌟 Introduction

Tokenization is a fundamental preprocessing step in Natural Language Processing (NLP) that involves splitting text into smaller units called tokens. The choice of tokenization strategy significantly impacts the performance of downstream NLP tasks such as text classification, machine translation, question answering, and more.

The Hugging Face `tokenizers` library, built with Rust backends for performance, offers a variety of tokenization algorithms. This repository explores these algorithms in detail, providing hands-on examples, comparisons, and tools for analysis.

## 🧩 Tokenizer Types

### Byte-Pair Encoding (BPE)

BPE is a subword tokenization algorithm that iteratively merges the most frequent pairs of bytes or characters in a corpus.

**Key Characteristics:**
- **Approach**: Starts with characters/bytes and iteratively merges the most frequent adjacent pairs
- **Vocabulary Building**: Bottom-up approach (character → subword → word)
- **Handling Unknown Words**: Splits unknown words into known subword units
- **Popular Implementations**: GPT-2, GPT-3, RoBERTa, BART

**Advantages:**
- Effectively handles rare words by breaking them into subword units
- Can represent an open vocabulary with a fixed number of tokens
- Works well for morphologically rich languages

**Limitations:**
- May create linguistically meaningless subword units
- Context-free merging may not always capture semantic relationships

### WordPiece

WordPiece is a subword tokenization algorithm similar to BPE but with a different merging criterion.

**Key Characteristics:**
- **Approach**: Uses likelihood rather than frequency to decide merges
- **Merge Criterion**: Pairs that maximize the likelihood of the training data when merged
- **Token Format**: Usually adds a prefix (e.g., "##") to subwords that don't start a word
- **Popular Implementations**: BERT, DistilBERT, Electra

**Advantages:**
- Better handles out-of-vocabulary words than whole-word approaches
- Captures morphological structures well in many languages
- Maintains word boundaries which helps with alignment

**Limitations:**
- Less effective for languages without clear word boundaries
- Can create suboptimal tokenization for compound words

### Unigram

Unigram is a probabilistic subword segmentation algorithm that optimizes a unigram language model.

**Key Characteristics:**
- **Approach**: Top-down approach starting with a large vocabulary and pruning
- **Vocabulary Building**: Iteratively removes tokens to maximize data likelihood
- **Segmentation**: Finds the most likely segmentation using a Viterbi algorithm
- **Popular Implementations**: XLNet, ALBERT

**Advantages:**
- Provides probabilistic segmentation with multiple tokenization options
- Theoretically sound foundation in language modeling
- Often performs well on languages with complex morphology

**Limitations:**
- Higher computational cost for training
- May require more iterations to converge

### SentencePiece

SentencePiece is a language-agnostic tokenizer that treats the input as a raw Unicode sequence.

**Key Characteristics:**
- **Approach**: Treats spaces as normal characters and tokenizes the raw text
- **Algorithms**: Supports both BPE and Unigram models
- **Reversibility**: Ensures lossless conversion between text and tokens
- **Popular Implementations**: T5, mBART, M2M-100

**Advantages:**
- Language-agnostic - works well for any language including those without spaces
- Directly tokenizes raw text without preprocessing
- Enables completely reversible tokenization

**Limitations:**
- May generate counter-intuitive tokens for languages with clear word boundaries
- Requires special handling for some downstream tasks

### Character-Based

Character-based tokenization splits text into individual characters or Unicode code points.

**Key Characteristics:**
- **Approach**: Treats each character as a separate token
- **Vocabulary Size**: Small, bounded by the character set of the language
- **Out-of-Vocabulary**: No OOV issues at the character level

**Advantages:**
- No out-of-vocabulary issues
- Simple and deterministic
- Works for any language without specific training

**Limitations:**
- Creates very long sequences
- May fail to capture higher-level semantic patterns
- Increases computational cost in sequence models

## 📁 Repository Structure

This repository is organized to facilitate exploration and experimentation with different tokenizers:

- `/notebooks`: Interactive Jupyter notebooks demonstrating each tokenizer
- `/experiments`: Scripts for comparing tokenizers across different metrics
- `/datasets`: Sample datasets for training and testing tokenizers
- `/visualization`: Tools for visualizing tokenization results
- `/models`: Pre-trained tokenizer models for different languages and domains

## 🚀 Getting Started

To begin exploring tokenizers with this repository:

1. Clone the repository
2. Install the required dependencies
3. Explore the notebooks to understand how each tokenizer works
4. Run the experiments to compare tokenizers on your data
5. Use the visualization tools to analyze tokenization results

## 🧪 Experiments

This repository includes several experiments to help understand the differences between tokenizers:

- **Vocabulary Size Analysis**: How vocabulary size affects tokenization quality
- **Language Comparison**: How different tokenizers perform across languages
- **Domain Adaptation**: Training tokenizers on domain-specific corpora
- **Tokenization Speed**: Benchmarking tokenization performance
- **Impact on Model Performance**: How tokenization affects downstream NLP tasks

## 📊 Analysis Tools

The repository provides tools for analyzing tokenization results:

- **Token Distribution Visualizer**: Understand the distribution of token lengths
- **Vocabulary Coverage Analyzer**: Measure how well a tokenizer covers unseen text
- **Token Overlap Comparator**: Compare tokenization strategies between algorithms
- **Rare Word Handling**: Analyze how different tokenizers handle rare or out-of-vocabulary words

## 🤝 Contributing

Contributions to this repository are welcome! Whether you're fixing bugs, adding new features, or improving documentation, your help is appreciated.

## 📜 License

This project is licensed under the terms of the MIT license.

---

*This repository is for educational purposes and is not officially affiliated with Hugging Face Inc.*
