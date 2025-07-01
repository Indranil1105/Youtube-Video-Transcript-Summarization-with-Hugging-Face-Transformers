# Youtube Video Transcript Summarization with Hugging Face Transformers

## Overview

This project provides an end-to-end pipeline to extract transcripts from YouTube videos and generate concise summaries using state-of-the-art natural language processing models. The workflow helps users quickly understand the key points of lengthy videos without watching them in full.

## Features

### YouTube Transcript Extraction: 
Automatically fetches video transcripts using the YouTube Transcript API.

### Text Summarization:    
Uses Hugging Face Transformers to summarize long transcripts into readable highlights.

### Efficient Processing: 
Handles long transcripts by chunking and summarizing in segments.

### User-Friendly Output: 
Delivers summaries that help users grasp the main ideas of any YouTube video.

## Installation

Install the required libraries:

pip install transformers youtube_transcript_api

## Usage

### Extract the Transcript

Use youtube_transcript_api to fetch the transcript from a YouTube video.

### Summarize the Transcript

Use the Hugging Face Transformers pipeline for summarization.

For long transcripts, split the text into manageable chunks before summarization.

## Example Code:


from youtube_transcript_api import YouTubeTranscriptApi

from transformers import pipeline


### Step 1: Extract transcript
video_id = "YOUR_VIDEO_ID"
transcript = YouTubeTranscriptApi.get_transcript(video_id)
full_text = " ".join([entry['text'] for entry in transcript])

### Step 2: Summarize
summarizer = pipeline("summarization")
summary = summarizer(full_text)
print(summary[0]['summary_text'])


## Project Structure

### Transcript Extraction: 
Fetches and joins transcript segments.

### Summarization: 
Applies a transformer model (e.g., BART, DistilBART, Pegasus) to generate a summary.

### Chunk Processing: 
Splits long transcripts to avoid model input limits and summarizes each chunk.


## Requirements

Python 3.7+

transformers

youtube_transcript_api

