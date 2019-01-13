# ONJSem


This project is based on https://github.com/stanfordnlp/coqa-baselines
It is only tested on Ubuntu 18 LTS.

## Requirements
1. dowload the CoQa-Baselines repository
2. follow their instructions for installation

## Running the commands
### Preprocessing
Generate the input files for seq2seq models --- needs to start a CoreNLP server (`n_history` can be changed to {0, 1, 2, ..} or -1):
```bash
  python scripts/gen_seq2seq_data.py --data_file data/coqa-train-v1.0.json --n_history 2 --lower --output_file data/seq2seq-train-h2
  python scripts/gen_seq2seq_data.py --data_file data/coqa-dev-v1.0.json --n_history 2 --lower --output_file data/seq2seq-dev-h2
```

Preprocess the data and embeddings:
Run:
```
bash
  python seq2seq/preprocess.py -train_src data/seq2seq-train-h2-src.txt -train_tgt data/seq2seq-train-h2-tgt.txt -valid_src data/seq2seq-dev-h2-src.txt -valid_tgt data/seq2seq-dev-h2-tgt.txt -save_data data/seq2seq-h2 -lower -dynamic_dict -src_seq_length 10000
  ```
Run the command that you want form `commands-txt`.

 Run:
```
PYTHONPATH=seq2seq python seq2seq/tools/embeddings_to_torch.py -emb_file_enc wordvecs/glove.42B.300d.txt -emb_file_dec wordvecs/glove.42B.300d.txt -dict_file data/seq2seq-h2.vocab.pt -output_file data/seq2seq-h2.embed
```


