---
license: apache-2.0
tags:
- generated_from_trainer
metrics:
- rouge
model-index:
- name: best_small_0509_ny
  results: []
---

<!-- This model card has been generated automatically according to the information the Trainer had access to. You
should probably proofread and complete it, then remove this comment. -->

# best_small_0509_ny

This model is a fine-tuned version of [google/mt5-small](https://huggingface.co/google/mt5-small) on the None dataset.
It achieves the following results on the evaluation set:
- Loss: 2.8914
- Rouge1: 9.552
- Rouge2: 2.8063
- Rougel: 9.4269
- Rougelsum: 9.4408
- Gen Len: 63.1403

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
- num_epochs: 3

### Training results

| Training Loss | Epoch | Step | Validation Loss | Rouge1 | Rouge2 | Rougel | Rougelsum | Gen Len |
|:-------------:|:-----:|:----:|:---------------:|:------:|:------:|:------:|:---------:|:-------:|
| 5.4232        | 0.22  | 500  | 3.3099          | 6.2398 | 1.265  | 6.2629 | 6.2824    | 39.2284 |
| 3.9624        | 0.44  | 1000 | 3.1605          | 7.2709 | 1.7071 | 7.251  | 7.2647    | 56.1457 |
| 3.792         | 0.67  | 1500 | 3.1030          | 6.7308 | 1.8315 | 6.7388 | 6.7111    | 51.7824 |
| 3.6583        | 0.89  | 2000 | 3.0655          | 7.6696 | 2.0264 | 7.7113 | 7.6741    | 56.6007 |
| 3.5539        | 1.11  | 2500 | 3.0376          | 7.6913 | 1.5986 | 7.5896 | 7.5672    | 64.3345 |
| 3.4987        | 1.33  | 3000 | 2.9776          | 8.5546 | 2.2324 | 8.4597 | 8.4794    | 61.4928 |
| 3.4505        | 1.56  | 3500 | 2.9598          | 8.1712 | 1.8308 | 8.2165 | 8.1921    | 61.3471 |
| 3.3891        | 1.78  | 4000 | 2.9622          | 8.0007 | 2.1965 | 7.9904 | 7.9239    | 62.3399 |
| 3.3652        | 2.0   | 4500 | 2.9385          | 8.8004 | 2.1471 | 8.6896 | 8.6709    | 62.6097 |
| 3.3304        | 2.22  | 5000 | 2.9076          | 9.0079 | 2.3925 | 8.9652 | 8.9766    | 62.5989 |
| 3.2975        | 2.45  | 5500 | 2.8936          | 8.0635 | 2.1137 | 8.0443 | 7.9886    | 61.8867 |
| 3.3318        | 2.67  | 6000 | 2.8958          | 8.7828 | 2.4462 | 8.6761 | 8.6376    | 66.2698 |
| 3.2901        | 2.89  | 6500 | 2.8914          | 9.552  | 2.8063 | 9.4269 | 9.4408    | 63.1403 |


### Framework versions

- Transformers 4.18.0
- Pytorch 1.10.1+cu113
- Datasets 2.0.0
- Tokenizers 0.11.6
