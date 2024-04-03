# aligner_testing
A repo to test viability and performance of new forced aligners

## Whisperx

Source: [github](https://github.com/m-bain/whisperX)

Let's prep the env:
```bash
mamba create --name whisperx python=3.10
mamba activate whisperx
mamba install pytorch==2.0.0 torchaudio==2.0.0 pytorch-cuda=11.8 -c pytorch -c nvidia
mamba install ffmpeg
pip install git+https://github.com/m-bain/whisperx.git --upgrade
```

So far best I can get is
```
srun -n 1 -N 1  --time 00:10:00 whisperx data/mici_princ/MP_00.wav --diarize --highlight_words True  --compute_type int8 --language hr --align_model classla/wav2vec2-xls-r-parlaspeech-hr --hf_token hf_zQZUoaSlRWsKkWvasfeyGWMkrpceMXXwasNjqPvly
torchvision is not available - cannot save figures
Lightning automatically upgraded your loaded checkpoint from v1.5.4 to v2.2.1. To apply the upgrade to your files permanently, run `python -m pytorch_lightning.utilities.upgrade_checkpoint ../.cache/torch/whisperx-vad-segmentation.bin`
Model was trained with pyannote.audio 0.0.1, yours is 3.1.1. Bad things might happen unless you revert pyannote.audio to 0.x.
Model was trained with torch 1.10.0+cu102, yours is 2.0.0. Bad things might happen unless you revert torch to 1.x.
>>Performing transcription...
>>Performing alignment...
>>Performing diarization...
```

The output is in `output_whisperx`, it's neatly packaged in a json, as well as srt, tsv, txt, and vtt formats.

So far it seems the possibility of feeding text into the model is not an option. Although pipeline mentions forced alignment, it is only internal.