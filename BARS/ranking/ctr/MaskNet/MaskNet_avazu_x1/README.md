## MaskNet_avazu_x1

A hands-on guide to run the MaskNet model on the Avazu_x1 dataset.

Author: [BARS Benchmark](https://github.com/reczoo/BARS/blob/main/CITATION)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) Gold 6278C CPU @ 2.60GHz
  GPU: Tesla V100 32G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 10.2
  python: 3.6.4
  pytorch: 1.0.0
  pandas: 0.22.0
  numpy: 1.19.2
  scipy: 1.5.4
  sklearn: 0.22.1
  pyyaml: 5.4.1
  h5py: 2.8.0
  tqdm: 4.60.0
  fuxictr: 1.2.1

  ```

### Dataset
Dataset ID: [Avazu_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Avazu#Avazu_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.2.1](https://github.com/reczoo/FuxiCTR/tree/v1.2.1) for this experiment. See the model code: [MaskNet](https://github.com/reczoo/FuxiCTR/blob/v1.2.1/fuxictr/pytorch/models/MaskNet.py).

Running steps:

1. Download [FuxiCTR-v1.2.1](https://github.com/reczoo/FuxiCTR/archive/refs/tags/v1.2.1.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Avazu/Avazu_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [MaskNet_avazu_x1_tuner_config_02](./MaskNet_avazu_x1_tuner_config_02). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd MaskNet_avazu_x1
    nohup python run_expid.py --config ./MaskNet_avazu_x1_tuner_config_02 --expid MaskNet_avazu_x1_034_99b442f6 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

| AUC | logloss  |
|:--------------------:|:--------------------:|
| 0.764289 | 0.367388  |


### Logs
```python
2022-05-26 22:19:11,912 P99119 INFO {
    "batch_size": "4096",
    "data_format": "csv",
    "data_root": "../data/Avazu/",
    "dataset_id": "avazu_x1_3fb65689",
    "debug": "False",
    "dnn_hidden_activations": "relu",
    "dnn_hidden_units": "[400, 400, 400]",
    "emb_layernorm": "True",
    "embedding_dim": "10",
    "embedding_regularizer": "0.1",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['feat_1', 'feat_2', 'feat_3', 'feat_4', 'feat_5', 'feat_6', 'feat_7', 'feat_8', 'feat_9', 'feat_10', 'feat_11', 'feat_12', 'feat_13', 'feat_14', 'feat_15', 'feat_16', 'feat_17', 'feat_18', 'feat_19', 'feat_20', 'feat_21', 'feat_22'], 'type': 'categorical'}]",
    "gpu": "6",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "MaskNet",
    "model_id": "MaskNet_avazu_x1_034_99b442f6",
    "model_root": "./Avazu/MaskNet_avazu_x1/",
    "model_type": "SerialMaskNet",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0.4",
    "net_layernorm": "True",
    "net_regularizer": "0",
    "num_workers": "3",
    "optimizer": "adam",
    "parallel_block_dim": "64",
    "parallel_num_blocks": "1",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "reduction_ratio": "2",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Avazu/Avazu_x1/test.csv",
    "train_data": "../data/Avazu/Avazu_x1/train.csv",
    "use_hdf5": "True",
    "valid_data": "../data/Avazu/Avazu_x1/valid.csv",
    "verbose": "0",
    "version": "pytorch"
}
2022-05-26 22:19:11,912 P99119 INFO Set up feature encoder...
2022-05-26 22:19:11,912 P99119 INFO Load feature_map from json: ../data/Avazu/avazu_x1_3fb65689/feature_map.json
2022-05-26 22:19:11,913 P99119 INFO Loading data...
2022-05-26 22:19:11,913 P99119 INFO Loading data from h5: ../data/Avazu/avazu_x1_3fb65689/train.h5
2022-05-26 22:19:14,278 P99119 INFO Loading data from h5: ../data/Avazu/avazu_x1_3fb65689/valid.h5
2022-05-26 22:19:14,605 P99119 INFO Train samples: total/28300276, pos/4953382, neg/23346894, ratio/17.50%, blocks/1
2022-05-26 22:19:14,605 P99119 INFO Validation samples: total/4042897, pos/678699, neg/3364198, ratio/16.79%, blocks/1
2022-05-26 22:19:14,605 P99119 INFO Loading train data done.
2022-05-26 22:19:18,708 P99119 INFO Total number of parameters: 14585891.
2022-05-26 22:19:18,708 P99119 INFO Start training: 6910 batches/epoch
2022-05-26 22:19:18,709 P99119 INFO ************ Epoch=1 start ************
2022-05-26 22:32:00,612 P99119 INFO [Metrics] AUC: 0.729413 - logloss: 0.405204
2022-05-26 22:32:00,614 P99119 INFO Save best model: monitor(max): 0.729413
2022-05-26 22:32:01,031 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 22:32:01,081 P99119 INFO Train loss: 0.454011
2022-05-26 22:32:01,081 P99119 INFO ************ Epoch=1 end ************
2022-05-26 22:44:37,125 P99119 INFO [Metrics] AUC: 0.730505 - logloss: 0.403430
2022-05-26 22:44:37,127 P99119 INFO Save best model: monitor(max): 0.730505
2022-05-26 22:44:37,206 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 22:44:37,263 P99119 INFO Train loss: 0.460650
2022-05-26 22:44:37,264 P99119 INFO ************ Epoch=2 end ************
2022-05-26 22:56:22,805 P99119 INFO [Metrics] AUC: 0.729182 - logloss: 0.404369
2022-05-26 22:56:22,807 P99119 INFO Monitor(max) STOP: 0.729182 !
2022-05-26 22:56:22,807 P99119 INFO Reduce learning rate on plateau: 0.000100
2022-05-26 22:56:22,807 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 22:56:22,865 P99119 INFO Train loss: 0.462288
2022-05-26 22:56:22,866 P99119 INFO ************ Epoch=3 end ************
2022-05-26 23:02:33,660 P99119 INFO [Metrics] AUC: 0.743626 - logloss: 0.397423
2022-05-26 23:02:33,663 P99119 INFO Save best model: monitor(max): 0.743626
2022-05-26 23:02:33,755 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 23:02:33,813 P99119 INFO Train loss: 0.415512
2022-05-26 23:02:33,813 P99119 INFO ************ Epoch=4 end ************
2022-05-26 23:08:43,954 P99119 INFO [Metrics] AUC: 0.736321 - logloss: 0.401003
2022-05-26 23:08:43,957 P99119 INFO Monitor(max) STOP: 0.736321 !
2022-05-26 23:08:43,957 P99119 INFO Reduce learning rate on plateau: 0.000010
2022-05-26 23:08:43,957 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 23:08:44,008 P99119 INFO Train loss: 0.420637
2022-05-26 23:08:44,008 P99119 INFO ************ Epoch=5 end ************
2022-05-26 23:14:54,593 P99119 INFO [Metrics] AUC: 0.744443 - logloss: 0.397339
2022-05-26 23:14:54,595 P99119 INFO Save best model: monitor(max): 0.744443
2022-05-26 23:14:54,677 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 23:14:54,737 P99119 INFO Train loss: 0.400032
2022-05-26 23:14:54,737 P99119 INFO ************ Epoch=6 end ************
2022-05-26 23:21:01,508 P99119 INFO [Metrics] AUC: 0.741242 - logloss: 0.398724
2022-05-26 23:21:01,510 P99119 INFO Monitor(max) STOP: 0.741242 !
2022-05-26 23:21:01,511 P99119 INFO Reduce learning rate on plateau: 0.000001
2022-05-26 23:21:01,511 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 23:21:01,560 P99119 INFO Train loss: 0.398301
2022-05-26 23:21:01,560 P99119 INFO ************ Epoch=7 end ************
2022-05-26 23:27:08,023 P99119 INFO [Metrics] AUC: 0.737535 - logloss: 0.401432
2022-05-26 23:27:08,026 P99119 INFO Monitor(max) STOP: 0.737535 !
2022-05-26 23:27:08,026 P99119 INFO Reduce learning rate on plateau: 0.000001
2022-05-26 23:27:08,026 P99119 INFO Early stopping at epoch=8
2022-05-26 23:27:08,026 P99119 INFO --- 6910/6910 batches finished ---
2022-05-26 23:27:08,076 P99119 INFO Train loss: 0.388699
2022-05-26 23:27:08,076 P99119 INFO Training finished.
2022-05-26 23:27:08,076 P99119 INFO Load best model: /cache/FuxiCTR/benchmarks/Avazu/MaskNet_avazu_x1/avazu_x1_3fb65689/MaskNet_avazu_x1_034_99b442f6.model
2022-05-26 23:27:11,149 P99119 INFO ****** Validation evaluation ******
2022-05-26 23:27:24,808 P99119 INFO [Metrics] AUC: 0.744443 - logloss: 0.397339
2022-05-26 23:27:24,880 P99119 INFO ******** Test evaluation ********
2022-05-26 23:27:24,881 P99119 INFO Loading data...
2022-05-26 23:27:24,881 P99119 INFO Loading data from h5: ../data/Avazu/avazu_x1_3fb65689/test.h5
2022-05-26 23:27:25,727 P99119 INFO Test samples: total/8085794, pos/1232985, neg/6852809, ratio/15.25%, blocks/1
2022-05-26 23:27:25,727 P99119 INFO Loading test data done.
2022-05-26 23:27:55,370 P99119 INFO [Metrics] AUC: 0.764289 - logloss: 0.367388

```
