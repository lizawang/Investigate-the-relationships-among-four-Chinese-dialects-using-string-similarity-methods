# Contextualized Embedding (sentence level)
## Tool:
Pretrained [sentence transformer SBERT ](https://huggingface.co/DMetaSoul/sbert-chinese-general-v2) trained in Chinese from Hugging Face.
- SBERT uses Siamese Neural Networks which implements two identical bert models that share the same parameters. And the network is trained by updating the weights using triplet loss function. ([Check their paper for details](https://arxiv.org/abs/1908.10084))
## Application:
Download the pretrained chinese SBERT model, get the sentence embedding for each sentence pair and compute their cosine similarity.
```
model = SentenceTransformer("DMetaSoul/sbert-chinese-general-v2-distill")
sen_1 = model.encode(["我们"], convert_to_tensor=True)
sen_2 = model.encode(["我你"], convert_to_tensor= True)
cosine_score = util.cos_sim(sen_1, sen_2)
```
## Data
To keep consistency with other methods, the punctuation and numbers are removed as well for this method. Although, given it's sentence level, punctuation might make a difference.

## Results
- First thing to notice is that the sentence cosine similarity scores are systematically higher than the ones we get from Needleman-Wunsch alignment with cosine similarity. The later are on average between 0.5 and 0.6, while the former the values within two standard derivations (~96%) of all language pairs are above 0.9.
- For the distributions, the results are quite different. The similarities between wen and wuu to cmn remain highest, so does wuu and yue stay the least similar. However, the distance between wen and wuu, wen and yue, and cmn and yue are not expected given the results from other two methods. With this method, cmn and yue is shown to be closest among the three pairs. And wen and yue is shown to be even closer than wen with wuu which is not even unexpected but also makes people to think if there is something wrong given we know that wen and wuu belong to the same dialect family. Although overall the difference is very small, even between the highest pair and lowest pair, the largest distance is only around 0.03 (the largest value of cmn and wuu substracts the lowest value of wuu and yue).
