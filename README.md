# Improving Back-Translation with Uncertainty-based Confidence Estimation
## Contents
* [Introduction](#introduction)
* [Prerequisites](#prerequisites)
* [Usage](#usage)
* [Contact](#contact)

## Introduction

This is the implementation of our work 'Improving Back-Translation with Uncertainty-based Confidence Estimation' (EMNLP 2019). The implementation is on top of [THUMT](https://github.com/thumt/THUMT).

## Prerequisites
This repository runs in the same environment as THUMT, please refer to <a href="https://github.com/THUNLP-MT/THUMT/blob/master/UserManual.pdf">the user manual of THUMT</a> to config the environment.

## Usage
Note: The usage is not user-friendly. May improve later.
<br>
Suppose the local path to this repository is CODE_DIR.

1. Standard training:
<pre><code>python [CODE_DIR]/thumt/bin/trainer.py \
	--input [source corpus] [target corpus] \
	--side none \
	--vocabulary [source vocabulary] [target vocabulary] \
	--model transformer \
	--parameters=train_steps=60000,constant_batch_size=false,batch_size=6250,device_list=[0,1,2,3]
</code></pre>
You can train a target-source translation model by simply exchanging source corpus and target corpus, source vocabulary and target vocabulary.

2. Translate target-side monolingual corpus:
<pre><code>python [CODE_DIR]/thumt/bin/translator.py \
	--input [monolingual corpus] \
	--output [translated corpus] \
	--vocabulary [target vocabulary] [source vocabulary] \
	--model transformer \
	--checkpoint [path to the target-source model] \
	--parameters=device_list=[0]
</code></pre>
We recommand splitting the entire monolingual corpus into small corpora before translation if the monolingual corpus is too big.

3. Confidence-aware training:
<pre><code>python [CODE_DIR]/thumt/bin/trainer.py \
	--input [source corpus] [target corpus] \
	--word_confidence [word-level uncertainty file] \
	--sen_confidence [sentence-level uncertainty file] \
	--side source_sentence_source_word \
	--vocabulary [source vocabulary] [target vocabulary] \
	--model transformer \
	--checkpoint [path to the source-target checkpoint] \
	--parameters=train_steps=60000,constant_batch_size=false,batch_size=6250,device_list=[0,1,2,3]
</code></pre>

## Contact

If you have questions, suggestions and bug reports, please email [wangshuo18@mails.tsinghua.edu.cn](mailto:wangshuo18@mails.tsinghua.edu.cn).
