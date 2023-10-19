# ROBUST

The robustness to distribution changes ensures that NLP models can be successfully applied in the realistic world, especially for information extraction tasks. However, most prior evaluation benchmarks have been devoted to validating pairwise matching correctness, ignoring the crucial validation of robustness. In this paper, we present the first benchmark that simulates the evaluation of open information extraction models in the real world, where the syntactic and expressive distributions under the same knowledge meaning may drift variously. We design and annotate a large-scale testbed in which each example is a knowledge-invariant clique that consists of sentences with structured knowledge of the same meaning but with different syntactic and expressive forms. By further elaborating the robustness metric, a model is judged to be robust if its performance is consistently accurate on the overall cliques. We perform experiments on typical models published in the last decade as well as a representative large language model, and the results show that the existing successful models exhibit a frustrating degradation, with a maximum drop of $23.43$ $F_1$ score.


![task](https://cloud.tsinghua.edu.cn/f/e077c310ffa94346aed4/?dl=1)

## News !! 

* [2023.10.08] Our paper has been accepted by the EMNLP 2023 main conference!
* [2023.05.23] Please refer to the [paper](https://arxiv.org/abs/2305.13981) for details!


## Data Access

The two-stages annotated data ROBUST, and original data CaRB are provided below:

| Data             | Description                                           | Download Link |
| ---------------- | ----------------------------------------------------------- | ------------- |
| CaRB             | The original CaRB data.        |     [Raw link](https://cloud.tsinghua.edu.cn/f/5703443959254651bdc4/?dl=1)          |
| CaRB_para        | The automatic generated paraphrase with distinctive syntax    |     [Raw link](https://cloud.tsinghua.edu.cn/f/06535bf9b1974d6b9287/?dl=1)          |
| CaRB_para_bleu   | The paraphrase data after diversified filtering with BLEU.    |     [Raw link](https://cloud.tsinghua.edu.cn/f/064c63a8708541c981d1/?dl=1)          |
| ROBUST           | The two-stage humman annotated data (e.g., paraphrase correction, and tuple extraction).    |     [Raw link](https://cloud.tsinghua.edu.cn/f/ddd4d9eaabcd4737ac5c/?dl=1)          |


## Syntactically Controllable Paraphrase Generation

To build sufficient paraphrases, we adopt [AESOP](https://github.com/PlusLabNLP/AESOP), a syntactically controllable paraphrasing model generating paraphrases by specifying pruned target syntactic trees sampled from ParaNMT-50M.

## Diversified Filtering based on BLEU

We filter the paraphrases with a heuristic search strategy to maintain the most diverse ones.
We provide the code of this method at `diversified_filter.py`, and please refer to our paper for more details.

![diversefilter](https://cloud.tsinghua.edu.cn/f/df57e237a4c442fdbf01/?dl=1)

## Syntactic Analysis

We propose and revise the HWS distance for efficiently calculating the syntactic distance of two sentences, and implement the CTK similarity algorithm based on modern StanfordCoreNLP toolkit.

### Hierarchically Weighted Syntactic (HWS) distance

This algorithm calculates the syntactic tree distance between two sentences based on a hierarchically weighted matching strategy, where smaller weights implies a greater focus on the comparison of skeletons.

We provide the code of this algorithm at `hws_distance.py`, and please refer to our paper for more details of the experiments.

![hws](https://cloud.tsinghua.edu.cn/f/4159b40bbd504bc4afb6/?dl=1)

### Convolutional Tree Kernel (CTK) similarity 

Convolutional Tree Kernel (CTK) similarity proposed in [(Collins and Duffy, 2001)](https://proceedings.neurips.cc/paper_files/paper/2001/file/bf424cb7b0dea050a42b9739eb261a3a-Paper.pdf). It measures the similarity between a pair of tree structures by counting the number of tree fragments in common. The value domain of this algorithm is also [0, 1], where 1 means the maximum similarity.

We implement the original algorithm at the code of `ctk_similarity.py`.

## ROBUST scorer

The ROBUST scorer is a metric to calculate the robustness performance of OIE extractions. We provide the scorer at the code of `robust_scorer.py` for directly use.

The ROBUST metric is compatible with existing benchmarks because we calculate on the order of magnitude of one sentence, and we can directly compare our robustness scores with CaRB and others.


![result](https://cloud.tsinghua.edu.cn/f/901b240b47044dcd8978/?dl=1)




## Reference

```bibtex
@article{qi2023preserving,
  title={Preserving Knowledge Invariance: Rethinking Robustness Evaluation of Open Information Extraction},
  author={Qi, Ji and Zhang, Chuchun and Wang, Xiaozhi and Zeng, Kaisheng and Yu, Jifan and Liu, Jinxin and Sun, Jiuding and Chen, Yuxiang and How, Lei and Li, Juanzi and others},
  journal={arXiv preprint arXiv:2305.13981},
  year={2023}
}
 ```