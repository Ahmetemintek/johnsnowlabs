---
layout: model
title: English asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu TFWav2Vec2ForCTC for GPU from hrdipto
author: John Snow Labs
name: asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu
date: 2022-09-26
tags: [wav2vec2, en, audio, open_source, asr]
task: Automatic Speech Recognition
language: en
nav_key: models
edition: Spark NLP 4.2.0
spark_version: 3.0
supported: true
annotator: Wav2Vec2ForCTC
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained Wav2vec2  model, adapted from Hugging Face and curated to provide scalability and production-readiness using Spark NLP.`asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune` is a English model originally trained by hrdipto.

NOTE: This model only works on a GPU, if you need to use this model on a CPU device please use asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu_en_4.2.0_3.0_1664202634616.zip){:.button.button-orange.button-orange-trans.arr.button-icon}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/public/models/asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu_en_4.2.0_3.0_1664202634616.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python

audio_assembler = AudioAssembler() \
    .setInputCol("audio_content") \
    .setOutputCol("audio_assembler")

speech_to_text = Wav2Vec2ForCTC \
    .pretrained("asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu", "en")\
    .setInputCols("audio_assembler") \
    .setOutputCol("text")

pipeline = Pipeline(stages=[
  audio_assembler,
  speech_to_text,
])

pipelineModel = pipeline.fit(audioDf)

pipelineDF = pipelineModel.transform(audioDf)
```
```scala

val audioAssembler = new AudioAssembler()
    .setInputCol("audio_content") 
    .setOutputCol("audio_assembler")

val speechToText = Wav2Vec2ForCTC
    .pretrained("asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu", "en")
    .setInputCols("audio_assembler") 
    .setOutputCol("text") 

val pipeline = new Pipeline().setStages(Array(audioAssembler, speechToText))

val pipelineModel = pipeline.fit(audioDf)

val pipelineDF = pipelineModel.transform(audioDf)

```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|asr_wav2vec2_xls_r_300m_bangla_command_generated_data_finetune_gpu|
|Compatibility:|Spark NLP 4.2.0+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[audio_assembler]|
|Output Labels:|[text]|
|Language:|en|
|Size:|1.2 GB|