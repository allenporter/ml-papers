# audio-features

Tutorials from the playlist [Audio Signal Processing of Machine Learning](https://www.youtube.com/watch?v=iCwMQJnKk2c&list=PL-wATfeyAMNqIee7cH3q1bh4QJFAaeNv0)

https://github.com/musikalkemist/AudioSignalProcessingForML

## Amplitude Envelope - Extracting Time Domain Features

From https://www.youtube.com/watch?v=rlypsap6Wow

The original tutorial used librosa, though I am going to use pytorch audio to
learn another framework instead.

## RMS Energy & Zero Crossing

From https://www.youtube.com/watch?v=EycaSbIRx-0

## Other papers

https://www.dafx.de/paper-archive/2018/papers/DAFx2018_paper_42.pdf

## Classifier & Datasets

- Dataset from https://urbansounddataset.weebly.com/
- https://www.youtube.com/watch?v=88FFnqt5MNI&t=246s

The classifier with a simple 4 layer CNN seems to get around 70% accuracy or so. Some observations:
- The softmax in the tutorial doesn't work if you use cross entropy loss function
- The demo is only using one of the datasets
- A future result that would be interesting would be to look at which categories are getting confused