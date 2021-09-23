---
layout: post
title:  "Automatic Speech Recognition (ASR)"
date:   2021-09-22
read: 8
description: A brief introduction to automatic speech recognition.
categories: machine learning
---

---

# Automatic Speech Recognition (ASR)

**Automatic speech recognition (ASR)** is the task of processing human speech into written format. In other words, 

>ASR is the task of transcribing speech. 

ASR has widespread applications in many fields, including healthcare, domotic appliance control, military, education etc., and it can be found everywhere: in live TV shows, in video calls, services for the hearing impaired, and most commonly, in our phones.

This post briefly covers: 
- traditional ASR,
- end-to-end ASR,
- inputs and outputs of these systems, and 
- end-to-end model architectures for ASR.

## Traditional ASR

Traditionally, an ASR system has multiple modules: 
- an **acoustic model** to model the acoustic features, 
- a **language model** to model text, and 
- a **pronunciation lexicon** to link words to phonemes. 
 
These modules are typically **optimised independently** from each other, contributing to the complexity in building, training and storing these systems. This has led to research into developing end-to-end approaches to ASR that will help alleviate these issues.

## End-to-end ASR

The rise of **deep learning** has fuelled interests in an end-to-end approach to ASR. 

> An end-to-end approach means a model takes in audio input and outputs text sequences directly. 

The key advantage of such approach is the ability to *jointly train the acoustic, language and pronunciation components in a **single** model*, instead of optimising the components separately. This greatly simplifies building an ASR system as the entire model is now differentiable and lends itself automatically to optimisation procedures like gradient descent, making it easier to train and develop.

## Inputs and outputs

### Inputs

The input of an ASR system is audio recordings. To allow the models to perform better, however, **features are extracted** from the audio sequences in a preprocessing step. These extracted acoustic features are then passed into the models instead of the raw audio recording.

Two popular forms of input acoustic features for ASR are:
1. the <a href="https://asset-pdf.scinapse.io/prod/2062826588/2062826588.pdf" target="_blank">**Mel-Frequency Cepstral Coefficients (MFCCs)**</a> 
2. the **Mel filter bank coefficients**. 
 
The generation of both types of features from raw audio signals follow a similar procedure. In this procedure, the Mel filter bank coefficients are computed first. The MFCCs can then be obtained (if needed) from the filter bank coefficients with additional processing (see <a href="https://haythamfayek.com/2016/04/21/speech-processing-for-machine-learning.html" target="_blank">here</a> for more info). 

Typically, the procedure goes like this:
1. An audio signal goes through a **pre-emphasis filter** to amplify the high frequencies.

2. The signal is then **split into frames**. 

3. **Fourier Transform** of the signal is computed for each frame, and the **power spectrum** is computed from the Fourier Transform for each frame.

4. A bank of triangular filters on a <a href="https://en.wikipedia.org/wiki/Mel_scale" target="_blank">Mel-scale</a> is then applied to each power spectrum to extract frequency bands for each frame. The result is the **Mel filterbank** coefficients for every frame.
    
5. **Discrete Cosine Transform** is applied to the filter banks to decorrelate the filterbank coefficients. The higher coefficients are discarded as they typically represent noise in the original signal. The result is the **MFCCs** for every frame.

The extra step (step 5) for computing the MFCCs are motivated by the need to decorrelate the coefficients for some machine learning algorithms such as the Gaussian Mixture Models - Hidden Markov Models (GMM-HMM) typically used in traditional ASR systems. 

**Deep neural networks** typically used for end-to-end ASR, on the other hand, are less susceptible to highly correlated input. Mel filter bank coefficients are therefore suitable for these networks and for end-to-end ASR.

### Outputs

The output of an ASR system is text. How do we represent text? 

Traditional ASR systems are typically phonetic-based. Therefore, the output text sequences for these systems are represented in the form of **phonemes**. 

> A **phoneme** is the smallest unit of sound that distinguishes one word from another word in a language. 

Words can be represented by sequences of phonemes. For example, 

> "cane" → "/k/", "/ã/", "/n/"

Therefore, systems using phonemes require a pronunciation lexicon to convert words to sequences of phonemes. As a result, the systems are not able to recognise words not in the lexicon, or *out-of-vocabulary (OOV) words*. (An ASR system has a vocabulary of words that it can recognise. Words that are not in the vocabulary are beyond the system's capabilities. OOV words are words not in the vocabulary.)

In end-to-end ASR, acoustic features can be mapped directly to the outputs. Therefore, words (or subword units) are more commonly used. Output units like **characters**, **subword units** and **words** are often used. For the English language:

- **Words** (For eg. "Cambridge")

- **Characters** (For eg. "C", "a", "m", "b", "r", "i", "d", "g", "e")

- **Subword units** (For eg. "Cam", "bridge"). There are two popular methods of performing subword segmentation: <a href="https://aclanthology.org/P18-1007.pdf" target="_blank">unigram language model (ULM)</a> and <a href="https://arxiv.org/pdf/1209.1045.pdf" target="_blank">Byte Pair Encoding (BPE)</a>.

## End-to-end Model Architectures

### Streaming models

The earliest attempt at end-to-end ASR came in the form of the **Connectionist Temporal Classification (CTC) loss function** developed by Alex Graves in <a href="https://www.cs.toronto.edu/~graves/icml_2006.pdf" target="_blank"> this paper</a>. This was further improved by Alex Graves in <a href="https://arxiv.org/pdf/1211.3711.pdf" target="_blank">this paper</a> to form the **Recurrent Neural Network Transducer (RNN-T)**.

The basis for both the CTC and the RNN-T is <a href="https://en.wikipedia.org/wiki/Recurrent_neural_network" target="_blank">**recurrent neural networks (RNNs)**</a>. RNNs are effective in modelling sequences of data, such as sequences of audio frames and sequences of text units. However, for **real-time ASR**, RNNs require both the input and output sequences to be of the same length. This is not always the case for ASR where the input audio sequences are most often longer than the output text sequences.

CTC and RNN-T are attempts to work around this. They enable the RNNs to perform real-time ASR on input-output sequences of different lengths, allowing what we usually call **streaming recognition**.

> Streaming recognition is the ability to output text units on-the-fly as you feed in audio frames one by one.

### Attention-based models

Another popular form of end-to-end ASR models are <a href="https://arxiv.org/pdf/1506.07503.pdf" target="_blank">**attention-based models**</a>, also commonly known as **sequence-to-sequence models**. 

Briefly, the attention mechanism used in these models decides which input frames are important when predicting the output text units, thus paying more attention to those frames. 

The attention mechanism was first used by Alex Graves in <a href="https://arxiv.org/pdf/1308.0850.pdf" target="_blank">this paper</a> and was integrated in ASR by Jan Chorowski in <a href="https://arxiv.org/pdf/1412.1602.pdf" target="_blank">this paper</a>, producing promising results. This was then further developed into encoder-decoder based models like:

- the <a href="https://arxiv.org/pdf/1508.01211.pdf" target="_blank">Listen, Attend and Spell (LAS)</a> model,

- the <a href="https://arxiv.org/pdf/1706.03762.pdf" target="_blank">transformer</a> model,

- the <a href="https://arxiv.org/pdf/2005.08100.pdf" target="_blank">conformer</a> model, (an improvement over the transformer model).

Unlike CTC and RNN-T, these attention-based models are not able to perform streaming recognition. This is because the entire input sequence needs to be available for the attention mechanism while performing ASR. This means output units can only be produced after the entire audio sequence is processed.

## Conclusion

1. Automatic speech recognition (ASR) is the task of transcribing speech automatically.
   
2. Traditional ASR systems comprise multiple modules that are optimised independently.

3. End-to-end ASR systems takes in audio and directly converts them to text.
   
4. 2 common audio input features are MFCCs and Mel Filterbank coefficients.
   
5. Common output units include phonemes (used typically in traditional systems), and words, characters and subword units (used more commonly in end-to-end systems)
   
6. Notable end-to-end ASR model architectures include CTC, RNN-T and attention-based models.

---

**Author**: <a href="https://github.com/andreusjh99" target="_blank">Chia Jing Heng (andreusjh99)</a>