---
layout: model
title: Generic Deidentification NER (SEC Bert Embeddings)
author: John Snow Labs
name: finner_deid_sec
date: 2023-02-24
tags: [deid, deidentification, anonymization, en, licensed]
task: Named Entity Recognition
language: en
edition: Finance NLP 1.0.0
spark_version: 3.0
supported: true
annotator: FinanceNerModel
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

This is a NER model which allows you to detect some generic entities that may require to be masked or obfuscated to be compliant with different regulations, as GDPR and CCPA. This is just an NER model, make sure you try the full De-identification pipelines available in Models Hub.

The only difference between this and `finner_deid` is the embeddings used.

## Predicted Entities

`AGE`, `CITY`, `COUNTRY`, `DATE`, `EMAIL`, `FAX`, `LOCATION-OTHER`, `ORG`, `PERSON`, `PHONE`, `PROFESSION`, `STATE`, `STREET`, `URL`, `ZIP`

{:.btn-box}
[Live Demo](https://demo.johnsnowlabs.com/finance/DEID_FIN/){:.button.button-orange}
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/finance/models/finner_deid_sec_en_1.0.0_3.0_1677282571388.zip){:.button.button-orange}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/finance/models/finner_deid_sec_en_1.0.0_3.0_1677282571388.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
documentAssembler = nlp.DocumentAssembler()\
        .setInputCol("text")\
        .setOutputCol("document")
        
sentenceDetector = nlp.SentenceDetectorDLModel.pretrained("sentence_detector_dl","xx")\
        .setInputCols(["document"])\
        .setOutputCol("sentence")

tokenizer = nlp.Tokenizer()\
        .setInputCols(["sentence"])\
        .setOutputCol("token")

embeddings = nlp.BertEmbeddings.pretrained("bert_embeddings_sec_bert_base","en")\
    .setInputCols(["sentence", "token"])\
    .setOutputCol("embeddings")

ner_model = finance.NerModel.pretrained('finner_deid_sec', "en", "finance/models")\
        .setInputCols(["sentence", "token", "embeddings"])\
        .setOutputCol("ner")

ner_converter = nlp.NerConverter()\
        .setInputCols(["sentence","token","ner"])\
        .setOutputCol("ner_chunk")

nlpPipeline = Pipeline(stages=[
        documentAssembler,
        sentenceDetector,
        tokenizer,
        embeddings,
        ner_model,
        ner_converter])

empty_data = spark.createDataFrame([[""]]).toDF("text")

model = nlpPipeline.fit(empty_data)

text = ["""
This LICENSE AND DEVELOPMENT AGREEMENT (this Agreement) is entered into effective as of Nov. 02, 2019 (the Effective Date) by and between Bioeq IP AG, having its principal place of business at 333 Twin Dolphin Drive, Suite 600, Redwood City, CA, 94065, USA (Licensee).
"""]

res = model.transform(spark.createDataFrame([text]).toDF("text"))
```

</div>

## Results

```bash
+-----------+----------------+
|      token|       ner_label|
+-----------+----------------+
|       This|               O|
|    LICENSE|               O|
|        AND|               O|
|DEVELOPMENT|               O|
|  AGREEMENT|               O|
|          (|               O|
|       this|               O|
|  Agreement|               O|
|          )|               O|
|         is|               O|
|    entered|               O|
|       into|               O|
|  effective|               O|
|         as|               O|
|         of|               O|
|        Nov|          B-DATE|
|          .|          I-DATE|
|         02|          I-DATE|
|          ,|          I-DATE|
|       2019|          I-DATE|
|          (|               O|
|        the|               O|
|  Effective|               O|
|       Date|               O|
|          )|               O|
|         by|               O|
|        and|               O|
|    between|               O|
|      Bioeq|               O|
|         IP|               O|
|         AG|               O|
|          ,|               O|
|     having|               O|
|        its|               O|
|  principal|               O|
|      place|               O|
|         of|               O|
|   business|               O|
|         at|               O|
|        333|        B-STREET|
|       Twin|        I-STREET|
|    Dolphin|        I-STREET|
|      Drive|        I-STREET|
|          ,|               O|
|      Suite|B-LOCATION-OTHER|
|        600|I-LOCATION-OTHER|
|          ,|               O|
|    Redwood|          B-CITY|
|       City|          I-CITY|
|          ,|               O|
|         CA|         B-STATE|
|          ,|               O|
|      94065|           B-ZIP|
|          ,|               O|
|        USA|         B-STATE|
|          (|               O|
|   Licensee|               O|
|         ).|               O|
+-----------+----------------+
```

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|finner_deid_sec|
|Compatibility:|Finance NLP 1.0.0+|
|License:|Licensed|
|Edition:|Official|
|Input Labels:|[sentence, token, embeddings]|
|Output Labels:|[ner]|
|Language:|en|
|Size:|16.4 MB|

## References

In-house annotated documents with protected information

## Benchmarking

```bash
           label  precision    recall  f1-score   support
           B-AGE       0.96      0.89      0.92       245
          B-CITY       0.85      0.86      0.86       123
       B-COUNTRY       0.86      0.67      0.75        36
          B-DATE       0.98      0.97      0.97      2352
           B-ORG       0.75      0.71      0.73        38
        B-PERSON       0.97      0.94      0.95      1348
         B-PHONE       0.86      0.80      0.83        86
    B-PROFESSION       0.93      0.75      0.83        84
         B-STATE       0.92      0.89      0.91       102
        B-STREET       0.99      0.91      0.95        89
          I-CITY       0.82      0.77      0.79        35
       I-COUNTRY       1.00      0.50      0.67         6
          I-DATE       0.96      0.95      0.96       402
           I-ORG       0.71      0.86      0.77        28
        I-PERSON       0.98      0.96      0.97      1240
         I-PHONE       0.91      0.92      0.92        77
    I-PROFESSION       0.96      0.79      0.87        70
         I-STATE       1.00      0.62      0.77         8
        I-STREET       0.98      0.94      0.96       188
           I-ZIP       0.84      0.97      0.90        60
               O       1.00      1.00      1.00    194103
        accuracy         -         -       1.00    200762
       macro-avg       0.72      0.62      0.65    200762
    weighted-avg       1.00      1.00      1.00    200762
```