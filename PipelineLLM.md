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

Aggregate reference and hyp in the same json.
 - /scratch/projects/pichenylab/llmexp/convert2json2punc.py
 - 