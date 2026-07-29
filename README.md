# Awesome Scientific Literature Retrieval

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of papers on retrieval and recommendation for scientific literature — **citation recommendation** (local and global), ad-hoc academic search, citation-informed document embeddings, and reranking.

Papers are classified by the **purpose of the retrieval** — what counts as success, and where the gold standard comes from — not by the shape of the query. A system whose query is a user's reading history and one whose query is a draft manuscript belong together if both are judged against the same thing.

## Contents

- [Local Citation Recommendation](#local-citation-recommendation)
- [Global Citation Recommendation](#global-citation-recommendation)
- [Ad-hoc Academic Search](#ad-hoc-academic-search)
- [Embedding & Dense Retrieval](#embedding--dense-retrieval)
- [Reranking](#reranking)
- [Contributing](#contributing)
- [License](#license)

## Local Citation Recommendation

The query is a citation context or placeholder inside a manuscript, and the target is **the one paper the author actually cited there**. Success is precision on a single answer, which is why this branch reports Recall@k and MRR against a single gold citation.

- <details style="display:inline"><summary><b>(<i>EMNLP'25</i>) CiteBART: Learning to Generate Citations for Local Citation Recommendation</b> [<a href="https://doi.org/10.18653/v1/2025.emnlp-main.89">link</a>]</summary> Citation-specific pre-training in an encoder-decoder, where author-date citation tokens are masked and reconstructed so that recommendation becomes generation; contributes a taxonomy of hallucinations with a 4% macro hallucination rate at top-3.</details>
- <details style="display:inline"><summary><b>(<i>LREC-COLING'24</i>) ILCiteR: Evidence-grounded Interpretable Local Citation Recommendation</b> [<a href="https://doi.org/10.63317/4j2msq9yo8o6">link</a>]</summary> Reformulates local citation recommendation so the target space is evidence spans rather than papers, returning ranked evidence-paper pairs from distant supervision with no model training at all.</details>
- <details style="display:inline"><summary><b>(<i>ACL Findings'24</i>) SymTax: Symbiotic Relationship and Taxonomy Fusion for Effective Citation Recommendation</b> [<a href="https://doi.org/10.18653/v1/2024.findings-acl.533">link</a>]</summary> A three-stage prefetcher-enricher-reranker architecture that embeds query and candidate taxonomies in hyperbolic space, released with ArSyTa, a dataset of 8.27M citation contexts.</details>
- <details style="display:inline"><summary><b>(<i>ECIR'22</i>) Local Citation Recommendation with Hierarchical-Attention Text Encoder and SciBERT-Based Reranking</b> [<a href="https://doi.org/10.1007/978-3-030-99736-6_19">link</a>]</summary> Attacks the prefetch stage rather than the reranker, showing a hierarchical-attention encoder beats BM25 at prefetching so a SciBERT reranker needs fewer candidates for the same accuracy.</details>
- <details style="display:inline"><summary><b>(<i>Scientometrics'20</i>) A Context-Aware Citation Recommendation Model with BERT and Graph Convolutional Networks</b> [<a href="https://doi.org/10.1007/s11192-020-03561-y">link</a>]</summary> Pairs a GCN document encoder with a BERT context encoder and releases FullTextPeerRead, the first well-organized dataset carrying the context sentences around each citation.</details>
- <details style="display:inline"><summary><b>(<i>SIGIR'17</i>) Neural Citation Network for Context-Aware Citation Recommendation</b> [<a href="https://doi.org/10.1145/3077136.3080730">link</a>]</summary> Frames context-aware citation recommendation as machine translation, encoding the citation context with a max time-delay network augmented by attention and author networks.</details>

## Global Citation Recommendation

The query is the gist of a document, a draft idea, or a reader's interests, and the target is **the author's whole reference list**. Success is coverage over a set, reported as MAP and nDCG. Query shape varies widely here -- a manuscript, a seed paper, an interaction history, an example document plus a facet -- but the purpose does not.

- <details style="display:inline"><summary><b>(<i>KAIS'26</i>) SPECTER-BS: Effective Citation Recommendation Using SPECTER with Bibliographic Scoring</b> [<a href="https://doi.org/10.1007/s10115-025-02677-y">link</a>]</summary> A two-stage model pairing SPECTER-based semantic prefetching with a bibliographic score computed from author networks and recent citation counts, targeting the low precision and overfitting of prior models.</details>
- <details style="display:inline"><summary><b>(<i>WWW'26</i>) What Should I Cite? A RAG Benchmark for Academic Citation Prediction</b> [<a href="https://doi.org/10.1145/3774904.3792075">link</a>]</summary> The first RAG-integrated benchmark for academic citation prediction, with a three-level 554k-paper corpus and an evaluation covering hallucination and diversity alongside retrieval accuracy.</details>
- <details style="display:inline"><summary><b>(<i>SIGIR'26</i>) Aspect-Aware Content-Based Recommendations for Mathematical Research Papers</b> [<a href="https://doi.org/10.1145/3805712.3809531">link</a>]</summary> An expert study establishes that relevance between mathematical papers is aspect-driven rather than similarity-driven; AchGNN is an aspect-conditioned heterogeneous GNN over text, citations and author lineage, released with the GoldRiM and SilverRiM datasets.</details>
- <details style="display:inline"><summary><b>(<i>ACL'25</i>) Multi-Facet Blending for Faceted Query-by-Example Retrieval</b> [<a href="https://doi.org/10.18653/v1/2025.acl-long.1388">link</a>]</summary> Synthesizes facet-specific training sets by decomposing and recomposing documents, addressing the absence of facet-level relevance labels that forced prior work to fall back on citations as a coarse proxy.</details>
- <details style="display:inline"><summary><b>(<i>NeurIPS'24</i>) HLM-Cite: Hybrid Language Model Workflow for Text-based Scientific Citation Prediction</b> [<a href="https://doi.org/10.52202/079017-1527">link</a>]</summary> Introduces the notion of core citations and predicts them with a hybrid workflow: a curriculum-finetuned embedding model retrieves from 100K candidates, then LLM agents rerank by one-shot reasoning.</details>
- <details style="display:inline"><summary><b>(<i>LREC-COLING'24</i>) Recommending Missed Citations Identified by Reviewers: A New Task, Dataset and Baselines</b> [<a href="https://doi.org/10.63317/33uudfoux4nm">link</a>]</summary> Defines the task of recommending citations that reviewers flagged as missing, contributing the expert-labelled CitationR dataset and an attentive reference encoder over the paper's existing bibliography.</details>
- <details style="display:inline"><summary><b>(<i>RecSys'24</i>) GLAMOR: Graph-based LAnguage MOdel Embedding for Citation Recommendation</b> [<a href="https://doi.org/10.1145/3640457.3688171">link</a>]</summary> Textualizes an attributed knowledge graph through random walks and finetunes a language model on the generated text, targeting the cold-start and name-ambiguity failures of KG-based recommenders.</details>
- <details style="display:inline"><summary><b>(<i>TKDE'24</i>) Supporting Your Idea Reasonably: A Knowledge-Aware Topic Reasoning Strategy for Citation Recommendation</b> [<a href="https://doi.org/10.1109/tkde.2024.3365508">link</a>]</summary> Recommends papers for a rough idea while requiring the recommendation be explainable, extracting multi-hop reasoning paths between knowledge-concept topics from an external knowledge graph.</details>
- <details style="display:inline"><summary><b>(<i>KAIS'24</i>) An Academic Recommender System on Large Citation Data Based on Clustering, Graph Modeling and Deep Learning</b> [<a href="https://doi.org/10.1007/s10115-024-02094-7">link</a>]</summary> A multi-stage recommender combining clustering, graph modelling and deep learning that runs on a complete million-scale digital library rather than a sampled subset, arguing that published systems are evaluated at a size unlike real deployments.</details>
- <details style="display:inline"><summary><b>(<i>TPDL'21</i>) Citation Recommendation for Research Papers via Knowledge Graphs</b> [<a href="https://doi.org/10.1007/978-3-030-86324-1_20">link</a>]</summary> Adds a research knowledge graph of scientific concepts on top of SPECTER document embeddings, and evaluates by retrieving from the whole corpus instead of the 30-document candidate sets used by prior work.</details>
- <details style="display:inline"><summary><b>(<i>AAAI'20</i>) Leveraging Title-Abstract Attentive Semantics for Paper Recommendation</b> [<a href="https://doi.org/10.1609/aaai.v34i01.5335">link</a>]</summary> A two-level attentive network that models the semantic relationship between a paper's title and abstract, with the title embedding acting as a memory continuously updated by abstract sentences.</details>
- <details style="display:inline"><summary><b>(<i>JIFS'18</i>) Global Citation Recommendation Using Knowledge Graphs</b> [<a href="https://doi.org/10.3233/jifs-169493">link</a>]</summary> Expands the semantic features of an abstract with DBpedia entities, generates candidates with Lucene MoreLikeThis, and ranks them with LambdaMART over hand-designed pairwise features.</details>

## Ad-hoc Academic Search

The query is a search string that **underspecifies the intent**, so the system must first work out what is being asked; the gold standard is a human relevance judgement rather than a reference list. Every paper here spends a stage on that step -- concept identification, view recognition, pseudo-query reconstruction, or multi-turn clarification.

- <details style="display:inline"><summary><b>(<i>ACL'26</i>) PaperRegister: Boosting Flexible-grained Paper Search via Hierarchical Retrieval</b> [<a href="https://doi.org/10.18653/v1/2026.acl-long.798">link</a>]</summary> Transforms an abstract-based index into a hierarchical index tree so queries at any granularity can be served, with a 0.6B view recognizer trained by SFT and GRPO selecting the right level.</details>
- <details style="display:inline"><summary><b>(<i>arXiv'26</i>) Multi-Turn Agentic Scientific Literature Search via Workflow Induction</b> [<a href="https://arxiv.org/abs/2607.00597">link</a>]</summary> Frames scientific search as workflow induction, constructing an executable DAG of search operators that user feedback refines alongside the query itself, rather than treating feedback as extra query text.</details>
- <details style="display:inline"><summary><b>(<i>EMNLP Findings'25</i>) Scientific Paper Retrieval with LLM-Guided Semantic-Based Ranking</b> [<a href="https://doi.org/10.18653/v1/2025.findings-emnlp.108">link</a>]</summary> Grounds LLM query understanding in a corpus-derived scientific concept index, making the concepts a query asks about an explicit and controllable matching signal instead of a holistic embedding.</details>
- <details style="display:inline"><summary><b>(<i>KDD'25</i>) LitFM: A Retrieval Augmented Structure-aware Foundation Model for Citation Graphs</b> [<a href="https://doi.org/10.1145/3711896.3737028">link</a>]</summary> A literature foundation model whose graph retriever reconstructs pseudo-queries for incomplete or ambiguous input and reranks by a diversity metric to counter the Matthew effect.</details>
- <details style="display:inline"><summary><b>(<i>EMNLP'24</i>) Taxonomy-guided Semantic Indexing for Academic Paper Search</b> [<a href="https://doi.org/10.18653/v1/2024.emnlp-main.407">link</a>]</summary> A plug-and-play taxonomy-guided semantic index that lets existing dense retrievers match the academic concepts underlying a query, effective even with highly limited training data.</details>

## Embedding & Dense Retrieval

The first stage of the pipeline: citation-informed document embeddings and the benchmarks that evaluate them. These papers define no retrieval task of their own -- an embedding plus cosine similarity is already a working retriever, and several systems in the sections above use exactly that with no second stage.

- <details style="display:inline"><summary><b>(<i>ACL'26</i>) SemCSE-Multi: Multifaceted and Decodable Embeddings for Aspect-Specific and Interpretable Scientific Domain Mapping</b> [<a href="https://doi.org/10.18653/v1/2026.acl-long.1884">link</a>]</summary> Produces multiple individually specifiable aspect embeddings per abstract in a single forward pass, and decodes embeddings back into natural-language descriptions of the aspect they capture.</details>
- <details style="display:inline"><summary><b>(<i>AAAI'26</i>) BiCA: Effective Biomedical Dense Retrieval with Citation-Aware Hard Negatives</b> [<a href="https://doi.org/10.1609/aaai.v40i39.40583">link</a>]</summary> Mines hard negatives from multi-hop citation chains in PubMed, showing that document link structure yields highly informative negatives and reaches state-of-the-art retrieval with minimal finetuning.</details>
- <details style="display:inline"><summary><b>(<i>EMNLP'25</i>) SemCSE: Semantic Contrastive Sentence Embeddings Using LLM-Generated Summaries for Scientific Abstracts</b> [<a href="https://doi.org/10.18653/v1/2025.emnlp-main.1662">link</a>]</summary> Learns scientific text embeddings from LLM-generated summaries rather than citation links, on the argument that citation-based approaches do not necessarily reflect semantic similarity.</details>
- <details style="display:inline"><summary><b>(<i>EMNLP'23</i>) SciRepEval: A Multi-Format Benchmark for Scientific Document Representations</b> [<a href="https://doi.org/10.18653/v1/2023.emnlp-main.338">link</a>]</summary> A 24-task benchmark across four task formats showing that SPECTER and SciNCL fail to generalize across formats, and that learning several format-specific embeddings per document does better.</details>
- <details style="display:inline"><summary><b>(<i>EMNLP'22</i>) Neighborhood Contrastive Learning for Scientific Document Representations with Citation Embeddings</b> [<a href="https://doi.org/10.18653/v1/2022.emnlp-main.802">link</a>]</summary> Replaces SPECTER's discrete citation signal with controlled nearest-neighbour sampling over citation graph embeddings, giving a continuous similarity that avoids positive-negative collisions.</details>
- <details style="display:inline"><summary><b>(<i>ACL'20</i>) SPECTER: Document-level Representation Learning Using Citation-informed Transformers</b> [<a href="https://doi.org/10.18653/v1/2020.acl-main.207">link</a>]</summary> Pretrains a Transformer on the citation graph as a document-level relatedness signal, producing embeddings usable without task-specific finetuning, released with the SciDocs benchmark.</details>

## Reranking

The second stage: reordering a prefetched candidate set for precision at the top. All three papers here diagnose the same bottleneck -- an LLM context window cannot hold enough candidates -- and split into two orthogonal answers, compressing the candidates or reranking fewer of them.

- <details style="display:inline"><summary><b>(<i>AAAI'26</i>) Compress-then-Rank: Faster and Better Listwise Reranking with Large Language Models via Ranking-Aware Passage Compression</b> [<a href="https://doi.org/10.1609/aaai.v40i41.40811">link</a>]</summary> Performs listwise reranking on compact multi-vector surrogates rather than full passages, with the compressor pretrained on restoration and continuation objectives and jointly optimized with the reranker.</details>
- <details style="display:inline"><summary><b>(<i>KDD'26</i>) CoRank: LLM-Based Compact Reranking with Document Features for Scientific Retrieval</b> [<a href="https://doi.org/10.48550/arxiv.2505.13757">link</a>]</summary> A training-free, model-agnostic framework that reranks coarsely over offline-extracted semantic features before refining on full text, so many more candidates fit inside the context window.</details>
- <details style="display:inline"><summary><b>(<i>NeurIPS'25</i>) AcuRank: Uncertainty-Aware Adaptive Computation for Listwise Reranking</b> [<a href="https://doi.org/10.48550/arxiv.2505.18512">link</a>]</summary> Models document relevance as a Bayesian TrueSkill posterior and reranks only the candidates whose ranking remains uncertain, allocating compute adaptively rather than over a fixed-size subset.</details>

## Contributing

If you think a paper is missing or miscategorized, please open an issue or submit a pull request.

Entries use a collapsible block, so the summary stays hidden until the title is clicked:

```html
- <details style="display:inline"><summary><b>(<i>Venue'YY</i>) Paper title</b> [<a href="url">link</a>]</summary> One-line summary.</details>
```

The summary line is raw HTML, so use `<b>`/`<i>`/`<a>` rather than Markdown syntax inside it.

Link text is `link`, not `pdf` — each URL points at the paper's official page of record (DOI, publisher, or proceedings), which is not always a direct PDF. Where a paper is accepted but its proceedings are not yet indexed, the venue label names the accepting venue and the link goes to arXiv.

Venue labels name the venue of record: `ACL Findings` and `EMNLP Findings` are marked as such rather than folded into the main conference, `KAIS` denotes the *Knowledge and Information Systems* journal, and `JIFS` the *Journal of Intelligent & Fuzzy Systems*.

One-line summaries closely follow each paper's stated contribution; consult the original paper for the authors' complete claims and context.

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, this list is released under [CC0](https://creativecommons.org/publicdomain/zero/1.0/) — public domain. Cited papers remain under their own copyright.
