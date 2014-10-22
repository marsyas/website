.. link:
.. description:
.. tags:
.. date: 2014/10/21 22:39:12
.. title: Data Sets
.. slug: datasets


GTZAN Genre Collection
======================

This dataset was used for the well known paper in genre classification " Musical
genre classification of audio signals " by G. Tzanetakis and P. Cook in IEEE
Transactions on Audio and Speech Processing 2002.

Unfortunately the database was collected gradually and very early on in my
research so I have no titles (and obviously no copyright permission etc). The
files were collected in 2000-2001 from a variety of sources including personal
CDs, radio, microphone recordings, in order to represent a variety of recording
conditions. Nevetheless I have been providing it to researchers upon request
mainly for comparison purposes etc. Please contact George Tzanetakis
(gtzan@cs.uvic.ca) if you intend to publish experimental results using this
dataset.

The dataset consists of 1000 audio tracks each 30 seconds long. It contains 10
genres, each represented by 100 tracks. The tracks are all 22050Hz Mono 16-bit
audio files in .wav format.

`Download the GTZAN genre collection`__ (Approximately 1.2GB)

.. __: http://opihi.cs.uvic.ca/sound/genres.tar.gz


Music Speech
============

A similar dataset which was collected for the purposes of music/speech
discrimination. The dataset consists of 120 tracks, each 30 seconds long. Each
class (music/speech) has 60 examples. The tracks are all 22050Hz Mono 16-bit
audio files in .wav format.

`Download the GTZAN music/speech collection`__ (Approximately 297MB)

.. __: http://opihi.cs.uvic.ca/sound/music_speech.tar.gz


Other datasets
==============

`RWC Music Database`__

.. __: http://staff.aist.go.jp/m.goto/RWC-MDB/

`CAL500 Dataset`__

.. __: http://cosmal.ucsd.edu/cal/projects/AnnRet/AnnRet.php

`Magnatagatune`__

.. __: http://tagatune.org/Magnatagatune.html

`mini-genres.tar.bz2`__

.. __: http://opihi.cs.uvic.ca/sound/mini-genres.tar.bz2

"mini-genres" is used for regression testing the bextract and kea programs.
Set up a MARSYAS_DATADIR environment variable to point to this location, then
run cmake.
