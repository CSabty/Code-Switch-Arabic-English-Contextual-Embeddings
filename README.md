# Code-Switched Arabic-English Contextual Embeddings
  Globalization has caused the rise of the code-switching phenomenon among multilingual societies. In Arab countries, code-switching between Arabic and English has become frequent, especially through social media platforms. Consequently, research in Natural Language Processing (NLP) systems increased to tackle such a phenomenon. One of the significant challenges of developing code-switched NLP systems is the lack of data itself. In this paper, we train bilingual contextual word embedding models using FLAIR, BERT, and ELECTRA.
  We also propose a novel contextual word embedding model called KERMIT, which can efficiently map Arabic and English words inside one vector space in terms of data usage. We applied intrinsic and extrinsic evaluation methods to compare the performance of the models. Our results show that FLAIR and FastText achieve the highest results in the sentiment analysis task. However, KERMIT is the best-achieving model on the intrinsic evaluation and named entity recognition. Also, it outperforms the other transformer-based models on question answering task.

You can download models individually from the table below:

|Pytorch|Tensorflow|
|:---:|:---:|
|[**Flair**][flair]|-|
|[**BERT**][BERT]|[**BERT**][BERT_tf]|
|[**BERT++**][BERT++]|[**BERT++**][BERT_tf_++]|
|[**ELECTRA**][ELECTRA]|[**ELECTRA**][ELECTRA_tf]|
|[**ELECTRA++**][ELECTRA++]|[**ELECTRA++**][ELECTRA_tf_++]|
|[**KERMIT**][KERMIT]|[**KERTMIT**][KERMIT_tf]|
|[**KERMIT++**][KERMIT++]|[**KERTMIT++**][KERMIT_tf_++]|






 
[flair]: https://drive.google.com/drive/folders/1-ORpdwtqGvCWq2SgO9NSbr3_RBHk1VBZ?usp=sharing 
[BERT]: https://drive.google.com/drive/folders/114LStAAM2qWvq01CYSU4b5hD8Q_U306S?usp=sharing
[BERT_tf]: https://drive.google.com/drive/folders/10ZMFOxNfOenYU2fUX5ZNy1CGKRRD6U85?usp=sharing
[BERT++]: https://drive.google.com/drive/folders/1LtkagKM18FLLVF8TkNwTABOKv8s3uJtV?usp=sharing
[BERT_tf_++]: https://drive.google.com/drive/folders/1jiEEyW0zoowtbfSPXh10c7Seqk2vpgqI?usp=sharing
[ELECTRA]: https://drive.google.com/drive/folders/1-D6PCryUoQQc_Zf5PlZpZgiuhS4tR-rT?usp=sharing
[ELECTRA_tf]: https://drive.google.com/drive/folders/1-V9Dw5k4tdmVZAEbPVnL8PdYX0OhXOEq?usp=sharing
[ELECTRA++]: https://drive.google.com/drive/folders/1-U8B5oBtZzVmjyuDkss72lkEMJE8hQL2?usp=sharing
[ELECTRA_tf_++]: https://drive.google.com/drive/folders/1--wrqh9xKcnPb-MujeF4-aQI3_PpyP_3?usp=sharing
[KERMIT]: https://drive.google.com/drive/folders/1_gL0C7O8sEimLo82CComOYSlBh1aycIt?usp=sharing
[KERMIT_tf]: https://drive.google.com/drive/folders/1-9VscQEIwZzOmC5C2EggHnjaelkFbqfj?usp=sharing
[KERMIT++]: https://drive.google.com/drive/folders/1-Wdy16mK1sNYeVmM2SUh9aBLkoH9bnzZ?usp=sharing
[KERMIT_tf_++]: https://drive.google.com/drive/folders/1-4KAldz-Mz5fvU8u5TrjvQBG_4UDCURo?usp=sharing

## KERMIT
We proposed a novel model called KERMIT for producing word embeddings. The architecture of this model is an encoder variant of transformers. The pre-training of this model is divided into two stages. In the first stage, KERMIT is trained as a discriminator in ELECTRA architecture using RTD and MLM tasks. After pre-training, the generator is dropped, and the pre-trained discriminator weights are used for the next stage. In the second stage, we initialize the encoder and embedding layers of the BERT model with the trained discriminator model. Then, we further trained the model as a generator using the MLM task.
<p float="left">
<img src="KERMIT_L_fig.PNG" width=400 /> <img src="KERMIT_R_fig.PNG" width=400 />  
  </p>
  

## How to use
In order to pre-train a KERMIT model you need to firstly pre-train an ELECTRA model and use a randomly initialized BERT model. 
```bash
python create_kermit.py \
    --initial_bert="/PATH_TO/model.ckpt" \
    --electra_path="/PATH_TO/model.ckpt" \
    --new_checkpoint="/PATH_TO/model.ckpt" \
    
```
After running this code ```new_checkpont``` path would contain the KERMIT model which could then be pre-trained as a BERT model.
## Results
We have evaluated the impact of our models in three tasks; Named Entity Recognition, SentimentAnalysis and Question Answering on Arabic-English CS text.


|Model|NER (Flair)|NER (Huggingface)|Sentiment analysis(Flair)|Sentiment Analysis (Hugignface)|Question answering|
|-------------|:---:|:---:|:---:|:---:|:---:|
|Pooled FLAIR and FastText|77.69|-|87.84|-|-|
|FLAIR|72.55|-|87.8|-|-|
|FLAIR  and FastText|**78.2**|-|**88.8**|-|-|
|AraBERT(Antoun et al., 2020)|58|66.7|-|78.2|30|
|BERT|64.5|76.5|-|77.7|37.8|
|BERT++|68.2|77.1|-|77.38|38.12|
|ELECTRA|67|76.29|-|76.39|34.1|
|ELECTRA++|68.3|76.29|-|77.18|37.2|
|KERMIT|65|78.7|-|76.8|32.8|
|KERMIT++|69|**79.4**|-|**79.9**|**39.9**|


## You can cite us
```
@inproceedings{,
  title={Contextual Embeddings for Arabic-English Code-Switched Data},
  author={Caroline Sabty, Mohamed Islam and Slim Abdennadher},
  booktitle={Proceedings of the Fifth Arabic Natural Language Processing Workshop WANLP 2020},
  pages={9}
}
```

