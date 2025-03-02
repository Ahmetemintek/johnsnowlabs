---
layout: model
title: English RobertaForQuestionAnswering Base Cased model (from autoevaluate)
author: John Snow Labs
name: roberta_qa_autoevaluate_base_squad2
date: 2022-12-02
tags: [en, open_source, roberta, question_answering, tensorflow]
task: Question Answering
language: en
nav_key: models
edition: Spark NLP 4.2.4
spark_version: 3.0
supported: true
engine: tensorflow
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained RobertaForQuestionAnswering  model, adapted from Hugging Face and curated to provide scalability and production-readiness using Spark NLP. `roberta-base-squad2` is a English model originally trained by `autoevaluate`.

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/roberta_qa_autoevaluate_base_squad2_en_4.2.4_3.0_1669986662532.zip){:.button.button-orange.button-orange-trans.arr.button-icon}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/public/models/roberta_qa_autoevaluate_base_squad2_en_4.2.4_3.0_1669986662532.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
Document_Assembler = MultiDocumentAssembler()\
     .setInputCols(["question", "context"])\
     .setOutputCols(["document_question", "document_context"])

Question_Answering = RoBertaForQuestionAnswering.pretrained("roberta_qa_autoevaluate_base_squad2","en")\
     .setInputCols(["document_question", "document_context"])\
     .setOutputCol("answer")\
     .setCaseSensitive(True)
    
pipeline = Pipeline(stages=[Document_Assembler, Question_Answering])

data = spark.createDataFrame([["What's my name?","My name is Clara and I live in Berkeley."]]).toDF("question", "context")

result = pipeline.fit(data).transform(data)
```
```scala
val Document_Assembler = new MultiDocumentAssembler()
     .setInputCols(Array("question", "context"))
     .setOutputCols(Array("document_question", "document_context"))

val Question_Answering = RoBertaForQuestionAnswering.pretrained("roberta_qa_autoevaluate_base_squad2","en")
     .setInputCols(Array("document_question", "document_context"))
     .setOutputCol("answer")
     .setCaseSensitive(True)
    
val pipeline = new Pipeline().setStages(Array(Document_Assembler, Question_Answering))

val data = Seq("What's my name?","My name is Clara and I live in Berkeley.").toDS.toDF("question", "context")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|roberta_qa_autoevaluate_base_squad2|
|Compatibility:|Spark NLP 4.2.4+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[document, token]|
|Output Labels:|[class]|
|Language:|en|
|Size:|464.1 MB|
|Case sensitive:|true|
|Max sentence length:|256|

## References

- https://huggingface.co/autoevaluate/roberta-base-squad2
- https://haystack.deepset.ai/tutorials/first-qa-system
- https://github.com/deepset-ai/haystack/
- https://haystack.deepset.ai/tutorials/first-qa-system
- https://worksheets.codalab.org/rest/bundles/0x6b567e1cf2e041ec80d7098f031c5c9e/contents/blob/
- http://deepset.ai/
- https://haystack.deepset.ai/
- https://deepset.ai/german-bert
- https://deepset.ai/germanquad
- https://github.com/deepset-ai/haystack
- https://haystack.deepset.ai
- https://haystack.deepset.ai/community/join
- https://twitter.com/deepset_ai
- https://www.linkedin.com/company/deepset-ai/
- https://haystack.deepset.ai/community/join
- https://github.com/deepset-ai/haystack/discussions
- https://deepset.ai
- http://www.deepset.ai/jobs