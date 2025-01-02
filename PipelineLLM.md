Sequence of files to run after having annotated whisper outputs.

1. Procure GPU:
   - srun --gres=gpu:1 -c 16 --nodes=1 --ntasks-per-node=1 --mem=16GB --constraint="rtx8000|v100" --time=04:00:00 --pty /bin/bash
   - Note if HPC is busy try reducing the number of CPUs to 4 (-c 4) and try.

2. Activate Environment: cd /scratch/projects/pichenylab/llmexp2/
   - singularity exec --nv --overlay  overlay-50G-10M.ext3 /scratch/work/public/singularity/cuda11.8.86-cudnn8.7-devel-ubuntu22.04.2.sif /bin/bash
   - source /ext3/env.sh
   - conda activate myenv

Whisper Outputs Section: /scratch/projects/pichenylab/callhome_ger_annotatedwhisper/train/processed_tsv/

Original Transcripts: /scratch/projects/pichenylab/callhome_german_trans_970711/transcrp/train/
2.5. Eval on the original scripts:
 - /scratch/projects/pichenylab/llmexp/testjsondir.py


3. Get data ready for finetuning
 - python /scratch/projects/pichenylab/llmexp/convert2json2punc.py (Aggregate reference and hyp in the same json)
 - python /scratch/projects/pichenylab/llmexp/get_hyp_ora_from_json_dir.py (get the hyp_spk_ora field as well in all json files)
 - python /scratch/projects/pichenylab/llmexp/combinealloutputjsonstrain.py (its all combined to 1 file)

4. cd /scratch/projects/pichenylab/llmexp2/speaker-id/DiarizationLM/unsloth

Note:
German data has overlapping speech and even the timestamps are overlapping, how does der work in this case and does whisper do overlapping speech?
 
5. results
   -   /scratch/projects/pichenylab/llmexp2/speaker-id/DiarizationLM/unsloth/google/DiarizationLM-13b-Fisher-v1_FISHER_LORA256_LEN4096/decoded22/checkpoint-245/FISHER
   -   
