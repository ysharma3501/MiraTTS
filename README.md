# MiraTTS
[MiraTTS](https://huggingface.co/YatharthS/MiraTTS) is a finetune of the excellent [Spark-TTS](https://huggingface.co/SparkAudio/Spark-TTS-0.5B) model for enhanced realism and stability performing on par with closed source models. 
This repository also heavily optimizes Mira with [Lmdeploy](https://github.com/InternLM/lmdeploy) and boosts quality by using [FlashSR](https://github.com/ysharma3501/FlashSR) to generate high quality audio at over **100x** realtime!

https://github.com/user-attachments/assets/262088ae-068a-49f2-8ad6-ab32c66dcd17

## Key benefits
- Incredibly fast: Over 100x realtime by using Lmdeploy and batching.
- High quality: Generates clear and crisp 48khz audio outputs which is much higher quality then most models.
- Memory efficient: Works within 6gb vram.
- Low latency: Latency can be low as 100ms.

## Usage
Simple 1 line installation:
```
uv pip install git+https://github.com/ysharma3501/MiraTTS.git
```

Running the model(bs=1):
```python
from mira.model import MiraTTS
from IPython.display import Audio
mira_tts = MiraTTS('YatharthS/MiraTTS') ## downloads model from huggingface

file = "reference_file.wav" ## can be mp3/wav/ogg or anything that librosa supports
text = "Alright, so have you ever heard of a little thing named text to speech? Well, it allows you to convert text into speech! I know, that's super cool, isn't it?"

context_tokens = mira_tts.encode_audio(file)
audio = mira_tts.generate(text, context_tokens)

Audio(audio, rate=48000)
```

Running the model using batching: 
```python
file = "reference_file.wav" ## can be mp3/wav/ogg or anything that librosa supports
text = ["Hey, what's up! I am feeling SO happy!", "Honestly, this is really interesting, isn't it?"]

context_tokens = [mira_tts.encode_audio(file)]

audio = mira_tts.batch_generate(text, context_tokens)

Audio(audio, rate=48000)
```

Examples can be seen in the [huggingface model](https://huggingface.co/YatharthS/MiraTTS)

I recommend reading these 2 blogs to better easily understand LLM tts models and how I optimize them
- How they work: https://huggingface.co/blog/YatharthS/llm-tts-models
- How to optimize them: https://huggingface.co/blog/YatharthS/making-neutts-200x-realtime

## Training
Released training code! You can now train the model to be multilingual, multi-speaker, or support audio events on any local or cloud gpu!

Kaggle notebook: https://www.kaggle.com/code/yatharthsharma888/miratts-training

Colab notebook: https://colab.research.google.com/drive/1IprDyaMKaZrIvykMfNrxWFeuvj-DQPII?usp=sharing

## Next steps
- [x] Release code and model
- [x] Release training code
- [ ] Support low latency streaming
- [ ] Release native 48khz bicodec
      
## Final notes
Thanks very much to the authors of Spark-TTS and unsloth. Thanks for checking out this repository as well.

Stars would be well appreciated, thank you.

Email: yatharthsharma3501@gmail.com
