# DLNLP-Finalproject
## Datasets
The data set link is as follows. Due to the size of the data set, it only contains the curation corpus and squad data sets. The wmt data set can be downloaded from huggingface.
```
https://drive.google.com/drive/folders/1gA_R12vP23PNxCX0eknqDCkyLoKEw4eu?usp=drive_link
```
## Environment setup
You need to first create a virtual environment and configure it.
```
pip install -r requirements.txt
```

## Run command
Due to network connection reasons, the model, parameters and configuration files downloaded locally are used in the code. When using the code, you need to first modify the path of the model, parameters and configuration. It is important to note that in the parameters --resume_from_checkpoint, you need to set checkpoint.
```
# translation
python train_translation.py --model_name_or_path t5-small --do_train --do_eval --do_predict --source_lang en --target_lang zh --source_prefix "translate English to Chinese: " --dataset_name wmt19 --dataset_config_name zh-en --output_dir ./output --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "sft-trans" --report_to wandb --evaluation_strategy epoch

# qa
python train_qa.py --model_name_or_path t5-small --dataset_name squad --do_train --do_eval --do_predict --output_dir ./qa_output --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "sft-qa" --report_to wandb --evaluation_strategy epoch

# summarization
python train_sum.py --model_name_or_path t5-small --do_train --do_eval --do_predict --dataset_name curation --source_prefix "summarize: " --output_dir ./sum_output --overwrite_output_dir --predict_with_generate --save_steps 2000 --run_name "sft-sum" --report_to wandb --evaluation_strategy epoch

# peft summarization
python peft_sum.py --model_name_or_path t5-small --do_train --do_eval --do_predict --dataset_name curation --source_prefix "summarize: " --output_dir ./sum_output_peft --overwrite_output_dir --predict_with_generate --save_steps 2000 --run_name "peft-sum" --report_to wandb --evaluation_strategy epoch

# peft translation
python peft_tran.py --model_name_or_path t5-small --do_train --do_eval --do_predict --source_lang en --target_lang zh --source_prefix "translate English to Chinese: " --dataset_name wmt19 --dataset_config_name zh-en --output_dir ./tran_output_peft --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "peft-trans" --report_to wandb --evaluation_strategy epoch

# peft qa
python peft_qa.py --model_name_or_path t5-small --dataset_name squad --do_train --do_eval --do_predict --output_dir ./qa_output_peft --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "peft-qa" --report_to wandb --evaluation_strategy epoch

# load from sum qa
python load_qa.py --model_name_or_path t5-small --dataset_name squad --do_train --do_eval --do_predict --output_dir ./load_qa_sum_output --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "load_sum_sft-qa" --report_to wandb --evaluation_strategy epoch --resume_from_checkpoint ./sum_output/checkpoint-2000

# load from tran qa 
python load_qa.py --model_name_or_path t5-small --dataset_name squad --do_train --do_eval --do_predict --output_dir ./load_qa_tran_output --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "load_tran_sft-qa" --report_to wandb --evaluation_strategy epoch --resume_from_checkpoint ./output/checkpoint

# load from sum peft qa
python load_peft_qa.py --model_name_or_path t5-small --dataset_name squad --do_train --do_eval --do_predict --output_dir ./load_qa_sum_peft_output --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "load_sum_peft-qa" --report_to wandb --evaluation_strategy epoch --resume_from_checkpoint ./sum_output_peft/checkpoint-2000

# load from tran peft qa 
python load_peft_qa.py --model_name_or_path t5-small --dataset_name squad --do_train --do_eval --do_predict --output_dir ./load_qa_tran_peft_output --overwrite_output_dir --predict_with_generate --save_steps 5000 --run_name "load_tran_peft-qa" --report_to wandb --evaluation_strategy epoch --resume_from_checkpoint ./tran_output_peft/checkpoint-15000


```
