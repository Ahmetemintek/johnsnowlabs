---
layout: model
title: Detect Assertion Status from Demographic Entities
author: John Snow Labs
name: assertion_oncology_demographic_binary_wip
date: 2022-10-01
tags: [licensed, clinical, oncology, en, assertion]
task: Assertion Status
language: en
nav_key: models
edition: Healthcare NLP 4.1.0
spark_version: 3.0
supported: true
annotator: AssertionDLModel
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

This model detects if a demographic entity refers to the patient or to someone else.

## Predicted Entities

`Patient`, `Someone_Else`

{:.btn-box}
[Live Demo](https://demo.johnsnowlabs.com/healthcare/ASSERTION_ONCOLOGY/){:.button.button-orange}
[Open in Colab](https://colab.research.google.com/github/JohnSnowLabs/spark-nlp-workshop/blob/master/tutorials/Certification_Trainings/Healthcare/27.Oncology_Model.ipynb){:.button.button-orange.button-orange-trans.co.button-icon}
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/clinical/models/assertion_oncology_demographic_binary_wip_en_4.1.0_3.0_1664642285987.zip){:.button.button-orange.button-orange-trans.arr.button-icon.hidden}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/clinical/models/assertion_oncology_demographic_binary_wip_en_4.1.0_3.0_1664642285987.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}

```python
document_assembler = DocumentAssembler()\
    .setInputCol("text")\
    .setOutputCol("document")

sentence_detector = SentenceDetectorDLModel.pretrained("sentence_detector_dl_healthcare","en","clinical/models")\
    .setInputCols(["document"])\
    .setOutputCol("sentence")

tokenizer = Tokenizer() \
    .setInputCols(["sentence"]) \
    .setOutputCol("token")

word_embeddings = WordEmbeddingsModel().pretrained("embeddings_clinical", "en", "clinical/models")\
    .setInputCols(["sentence", "token"]) \
    .setOutputCol("embeddings")                

ner = MedicalNerModel.pretrained("ner_oncology_wip", "en", "clinical/models") \
    .setInputCols(["sentence", "token", "embeddings"]) \
    .setOutputCol("ner")

ner_converter = NerConverter() \
    .setInputCols(["sentence", "token", "ner"]) \
    .setOutputCol("ner_chunk")\
    .setWhiteList(["Age", "Gender"])
    
assertion = AssertionDLModel.pretrained("assertion_oncology_demographic_binary_wip", "en", "clinical/models") \
    .setInputCols(["sentence", "ner_chunk", "embeddings"]) \
    .setOutputCol("assertion")
        
pipeline = Pipeline(stages=[document_assembler,
                            sentence_detector,
                            tokenizer,
                            word_embeddings,
                            ner,
                            ner_converter,
                            assertion])

data = spark.createDataFrame([["One sister was diagnosed with breast cancer at the age of 40."]]).toDF("text")

result = pipeline.fit(data).transform(data)
```
```scala
val document_assembler = new DocumentAssembler()
    .setInputCol("text")
    .setOutputCol("document")
    
val sentence_detector = SentenceDetectorDLModel.pretrained("sentence_detector_dl_healthcare","en","clinical/models")
    .setInputCols(Array("document"))
    .setOutputCol("sentence")
    
val tokenizer = new Tokenizer()
    .setInputCols(Array("sentence"))
    .setOutputCol("token")
    
val word_embeddings = WordEmbeddingsModel().pretrained("embeddings_clinical", "en", "clinical/models")
    .setInputCols(Array("sentence", "token"))
    .setOutputCol("embeddings")                
    
val ner = MedicalNerModel.pretrained("ner_oncology_wip", "en", "clinical/models")
    .setInputCols(Array("sentence", "token", "embeddings"))
    .setOutputCol("ner")
    
val ner_converter = new NerConverter()
    .setInputCols(Array("sentence", "token", "ner"))
    .setOutputCol("ner_chunk")
    .setWhiteList(Array("Age", "Gender"))

val clinical_assertion = AssertionDLModel.pretrained("assertion_oncology_demographic_binary_wip","en","clinical/models")
    .setInputCols(Array("sentence","ner_chunk","embeddings"))
    .setOutputCol("assertion")
        
val pipeline = new Pipeline().setStages(Array(document_assembler,
                                              sentence_detector,
                                              tokenizer,
                                              word_embeddings,
                                              ner,
                                              ner_converter,
                                              assertion))

val data = Seq("One sister was diagnosed with breast cancer at the age of 40.").toDF("text")

val result = pipeline.fit(data).transform(data)
```
</div>

## Results

```bash
| chunk     | ner_label   | assertion    |
|:----------|:------------|:-------------|
| sister    | Gender      | Someone_Else |
| age of 40 | Age         | Someone_Else |

```

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|assertion_oncology_demographic_binary_wip|
|Compatibility:|Healthcare NLP 4.1.0+|
|License:|Licensed|
|Edition:|Official|
|Input Labels:|[document, chunk, embeddings]|
|Output Labels:|[assertion_pred]|
|Language:|en|
|Size:|1.4 MB|

## References

In-house annotated oncology case reports.

## Benchmarking

```bash
       label  precision  recall  f1-score  support
     Patient       0.94    0.94      0.94     32.0
Someone_Else       0.92    0.92      0.92     24.0
   macro-avg       0.93    0.93      0.93     56.0
weighted-avg       0.93    0.93      0.93     56.0
```
