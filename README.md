# Youtube Video Transcript Summarization with Hugging Face Transformers

## Overview

This project provides a **pipeline to extract, clean, and summarize transcripts from YouTube videos** using Python and state-of-the-art NLP models from Hugging Face Transformers. It leverages the `youtube_transcript_api` and `pytube` libraries for transcript extraction, and uses transformer-based models for text summarization.

---

## Features

- **Automatic extraction of YouTube video transcripts** using video URLs.
  
- **Text cleaning and preprocessing** (punctuation removal, joining transcript segments).
  
- **Summarization of long transcripts** using Hugging Face Transformer models.
  
- Modular code for easy extension and customization.

---

## Installation

Install required packages:

pip install youtube_transcript_api pytube simpletransformers

pip install git+https://github.com/babthamotharan/rpunct.git@patch-2


## Usage

1. **Extract Video ID**
 
   - Extract the video ID from a YouTube URL using `pytube.extract` or a custom function.

2. **Download Transcript**
 
   - Use `YouTubeTranscriptApi.get_transcript(video_id)` to fetch the transcript as a list of text segments.

3. **Preprocess Transcript**
 
   - Join all transcript segments into a single string.
    
   - Optionally, remove punctuation and clean the text for better summarization results.

4. **Summarize Transcript**

   - Pass the cleaned transcript to a Hugging Face Transformer summarization model (e.g., BART, T5) for generating a concise summary.



## Example Code

from youtube_transcript_api import YouTubeTranscriptApi

from pytube import extract


### Step 1: Extract video ID

video_url = "https://youtu.be/your_video_id"

video_id = extract.video_id(video_url)


### Step 2: Download transcript

transcript = YouTubeTranscriptApi.get_transcript(video_id)


### Step 3: Preprocess transcript

transcript_joined = " ".join([line['text'] for line in transcript])


### Step 4: (Optional) Clean transcript

import re

no_punctuation = re.sub(r'[^\w\s]', '', transcript_joined)


### Step 5: Summarize using Hugging Face Transformers (example with simpletransformers)


from simpletransformers.seq2seq import Seq2SeqModel



model = Seq2SeqModel(

encoder_decoder_type="bart",

encoder_decoder_name="facebook/bart-large-cnn"

)



summary = model.predict([no_punctuation])

print("Summary:", summary)



## Customization

- You can swap the summarization model with any compatible Hugging Face model.
  
- For better transcript formatting, consider using the `rpunct` library to restore punctuation and capitalization before summarization.



## Requirements

- Python 3.7+
  
- `youtube_transcript_api`
  
- `pytube`
  
- `simpletransformers`
  
- `transformers`
  
- `rpunct` (for punctuation restoration, optional)



## Credits

- Transcript extraction: [youtube_transcript_api](https://github.com/jdepoix/youtube-transcript-api)
 
- Video ID extraction: [pytube](https://github.com/pytube/pytube)
 
- Summarization: [Hugging Face Transformers](https://huggingface.co/transformers/)
  
- Punctuation restoration: [rpunct](https://github.com/babthamotharan/rpunct) (optional)

