---
license: apache-2.0
tags:
- generated_from_trainer
metrics:
- rouge
model-index:
- name: best_small_0509_title_e10
  results: []
---

<!-- This model card has been generated automatically according to the information the Trainer had access to. You
should probably proofread and complete it, then remove this comment. -->

# best_small_0509_title_e10

This model is a fine-tuned version of [google/mt5-small](https://huggingface.co/google/mt5-small) on the None dataset.
It achieves the following results on the evaluation set:
- Loss: 2.5044
- Rouge1: 19.1814
- Rouge2: 4.6988
- Rougel: 18.7552
- Rougelsum: 18.8573
- Gen Len: 22.8063

## Model description

More information needed

## Intended uses & limitations

More information needed

## Training and evaluation data

More information needed

## Training procedure

### Training hyperparameters

The following hyperparameters were used during training:
- learning_rate: 0.0001
- train_batch_size: 2
- eval_batch_size: 4
- seed: 42
- gradient_accumulation_steps: 4
- total_train_batch_size: 8
- optimizer: Adam with betas=(0.9,0.999) and epsilon=1e-08
- lr_scheduler_type: linear
- num_epochs: 10

### Training results

| Training Loss | Epoch | Step  | Validation Loss | Rouge1  | Rouge2 | Rougel  | Rougelsum | Gen Len |
|:-------------:|:-----:|:-----:|:---------------:|:-------:|:------:|:-------:|:---------:|:-------:|
| 3.4075        | 1.0   | 6602  | 2.9060          | 14.2099 | 3.4982 | 14.1416 | 14.0828   | 22.4625 |
| 3.0804        | 2.0   | 13204 | 2.7414          | 17.2783 | 4.5353 | 17.3242 | 17.396    | 22.3245 |
| 2.9331        | 3.0   | 19806 | 2.6838          | 17.1451 | 4.2012 | 17.0881 | 17.2034   | 23.1308 |
| 2.8705        | 4.0   | 26408 | 2.6243          | 18.6862 | 4.4125 | 18.7132 | 18.8722   | 22.3245 |
| 2.7563        | 5.0   | 33010 | 2.5820          | 20.0374 | 5.084  | 19.8535 | 19.9043   | 22.9831 |
| 2.718         | 6.0   | 39612 | 2.5559          | 18.2852 | 5.0713 | 18.24   | 18.2662   | 23.1889 |
| 2.6315        | 7.0   | 46214 | 2.5339          | 18.8798 | 5.2296 | 18.7436 | 18.7981   | 22.5617 |
| 2.6117        | 8.0   | 52816 | 2.5174          | 18.5723 | 4.8406 | 18.2781 | 18.383    | 22.569  |
| 2.518         | 9.0   | 59418 | 2.5117          | 19.0194 | 4.9112 | 18.7108 | 18.7619   | 22.8717 |
| 2.5376        | 10.0  | 66020 | 2.5044          | 19.1814 | 4.6988 | 18.7552 | 18.8573   | 22.8063 |


### Framework versions

- Transformers 4.19.0.dev0
- Pytorch 1.10.1+cu113
- Datasets 2.1.0
- Tokenizers 0.12.1
