---
layout: page
title: Text-to-Speech and Decoder
description: Speech recognition for Hindi language
img: assets/logo/flipkart.png
importance: 3
category: past #work
---


Text-to-Speech model for Hindi language (Flipkart):- 
The aim of this project was to generate audio speech in Hindi language for the given text sentences.  I started on this project while I was working with Flipkart. 
​
Key learnings:
 - Unsupervised generative models
 - Autoregressive models
 - Flow (& inverse Flow) based models
 - Papers I've read - [Link](https://github.com/vdivakar/Papers-Stack#papers-stack)

 C++ decoder for Speech recognition engine (Flipkart):- 
Worked on the decoder module of the ASR pipeline (Automated Speech Recognition). 
Key responsibilities:
 - Implemented new features into production with C++ code base.
 - Improved latency & memory consumption.
 - [Blog post 1](https://www.divakar-verma.com/post/ctc-loss-for-unsegmented-data) - Intro to CTC Loss
 - [Blog post 2](https://www.divakar-verma.com/post/ctc-loss-part-2-forward-pass-using-alpha-matrix) - DP based prefix beam search PP


 <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ASRpipeline_nvidia.png" title="nvidia ASR pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <a href="https://developer.nvidia.com/blog/how-to-build-domain-specific-automatic-speech-recognition-models-on-gpus/">Image reference link.</a> This image is only for a general overview of the ASR pipeline and doesn't reflect the actual work.
</div>