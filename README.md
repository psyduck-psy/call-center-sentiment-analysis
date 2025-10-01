# Call Center Sentiment Analysis with Google Cloud

This project demonstrates how call center audio recordings can be transformed into **actionable insights** using **Google Cloud Platform (GCP) APIs**.  
The pipeline covers every step: audio storage, transcription, sentiment analysis, NoSQL storage in Firestore, and visualization.

---

##  Objectives

- Automate transcription of call center conversations using Google Speech-to-Text  
- Perform sentiment analysis on each sentence using Google Natural Language API  
- Store structured results in Firestore for long-term analysis  
- Visualize customer emotions throughout the conversation  

---

##  Tech Stack

- **Google Cloud Storage** – storing audio files  
- **Google Cloud Speech-to-Text API** – transcribing audio into text  
- **Google Cloud Natural Language API** – sentiment analysis  
- **Firebase Firestore** – NoSQL database for structured storage  
- **Python** – data processing and orchestration  
- **NLTK** – sentence tokenization  
- **Matplotlib** – visualization  

---

## Workflow

1. **Upload Audio File**  
   - Store `.wav` audio in a GCP Storage bucket.  

2. **Transcribe Audio**  
   - Use Speech-to-Text API (`long_running_recognize`) for conversations >1 minute.  
   - Extract clean transcript with punctuation.  

3. **Sentiment Analysis**  
   - Split transcript into sentences (using `nltk.sent_tokenize`).  
   - Run sentiment scoring with Natural Language API.  
   - For each sentence, retrieve:  
     - `sentiment score` (-1.0 negative → +1.0 positive)  
     - `magnitude` (emotional intensity)  

4. **Store in Firestore**  
   - Each sentence is saved as a document with:  
     - `wav_filename`  
     - `sentence_number`  
     - `sentence_text`  
     - `sentiment`  
     - `magnitude`  
     - `transcription_date`  

5. **Visualize Findings**  
   - Plot sentiment scores and magnitudes to see emotional flow of the call.  


##  Example Output

**Transcript Extract**  
# call-center-sentiment-analysis

**Sentiment Records (Firestore)**  
```json
{
  "wav_filename": "conversation.wav",
  "sentence_number": 3,
  "sentence_text": "I lost my debit card, can you send me a new one?",
  "sentiment": -0.2,
  "magnitude": 0.2,
  "transcription_date": "2025-10-01"
}
