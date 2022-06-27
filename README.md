# An Information-theoretic Approach to Prompt Engineering Without Ground Truth Labels (Replication)

Here, I try to replicate the results from the ACL 2022 paper [An Information-theoretic Approach to Prompt Engineering Without Ground Truth Labels](https://aclanthology.org/2022.acl-long.60/). This first implementation aims to minimally replicate the result for the smallest GPT-2 on SQuAD 2.0. While the implementation slightly differs from the original paper, I expect to observe a qualitatively same result. The SQuAD dataset shows the best result (among all datasets) as in the first row of Figure 9.

Currently, the differences are:
- I use the full vocabulary as the possible search space. This might be not exactly the same as, but should largely overlap with the original ```token_set``` used for SQuAD 2.0.
- For convenient prototyping, I use the first $N=100$ samples to calculate the average MI, instead of randomly sample $N=500$ samples. The total number of single-word-answered questions in the SQuAD 2.0 training set is 9264 as shown in the notebook. The caveat here is that the samples mostly come from one single paragraph of the SQuAD training set.
- Instead of calculating MI as defined, I only calculate the conditional entropy $H(P(Y|f_\theta(X)))$, because the first term $H(Y)$ is the same for all prompt templates and thus does not affect the ranking. The sign of the final result is also flipped.
- Some templates involve "few-shot" or "SHOT" fields that are not defined by the SQuAD dataset itself. While I aim to do a thorough search for templates later, these templates are excluded in this first version.
- The random seed has not been set, but this should not affect the process of getting the score for the single next token.

One potential caveat of the original paper is a very subjective choice of the initial $K=20$ templates. If this is indeed problematic, using more templates as a starting point (without cherry-picking) would not reveal a correlation as strong as shown in the original paper. My other thoughts after reading the paper are summarized [here](https://kt2k01.github.io/posts/2022/06/logbook/) (please scroll down to Jun 27).