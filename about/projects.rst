.. link: 
.. description: 
.. tags: 
.. date: 2014/10/21 22:39:12
.. title: Projects
.. slug: projects

Marsyas has been used for a variety of projects in both academia and industry:

- `HEARBO - Hearing Robot`_
- `Yahoo Research`_
- `ORBIT Project (BBC Research)`_
- `VISNET I & II EU FP6 NoE Projects`_
- `INESC Porto`_
- `Teligence`_
- `Moodlogic`_
- `last.fm`_
- `MusicEmo - Eric Yang, NTU, Taiwan`_
- `Musicream`_
- `Musie Mood`_
- `Orelia - Sound Source Recognition`_
- `Multi-Label classification of music`_
- `Dancing Robot with Marsyas`_
- `Personalized Multimodal Music Search`_
- `Modeling Emotional Content of Music`_
- `ASTA - Automatic Subtitle Timing Annotator`_
- `SndPeek`_
- `Analysis of Audio Features in Broadcast Sports Video`_
- `vivi`_

HEARBO - Hearing Robot
======================

Marsyas was integrated with HARK (HRI-JP Audition for Robots with Kyoto
University) Robot Audition System for music processing. It has already been used
by HRI-JP, in collaboration with INESC Porto and LIACC-FEUP, for the development
of an interactive robot dancing system HEARBO_, where a humanoid robot
simultaneously responds to the beat of music and to the speech of a human
interactor in a real-world scenario. HARK-Marsyas could be the baseline of music
listening robots in the future.

.. _HEARBO: http://spectrum.ieee.org/automaton/robotics/artificial-intelligence/hearbo-a-robot-with-superhearing

Yahoo Research
==============

Yahoo Research and the Yahoo Media Group have been using Marsyas to analyze
songs in our 2-million song database. We are interested in both how the songs
are related to each other, so we can find similar songs, and how they differ, so
we can characterize people's musical interests. Marsyas provides us with an
easy-to-use platform that computes many of the features we think are useful. But
more importantly, Marsyas is a common platform for acoustic signal processing,
so we can report results that are easy for other research labs to replicate.
Malcolm Slaney

http://www.musiclibre.org/research/

ORBIT Project (BBC Research)
============================

ORBIT - Object Re-configurable Broadcast Infrastructure Trial, a contract pilot
project between the BBC RD (http://www.bbc.co.uk/rd/index.shtml) and INESC Porto
(http://www.inescporto.pt) development of automatic audio segmentation and
classification tools using Marsyas (September 2001 - September 2002).

http://www.bbc.co.uk/orbit/index.shtml

VISNET I & II EU FP6 NoE Projects
=================================

VISNET I - II - NETworked audio VISual media technologies (FP6-2002-IST-1 and
FP6-2005-IST-41 European Union Network of Excellence Projects, respectively)
Marsyas is used at Audio and Music analysis work packages by some of the
partners (December 2003 - June 2009).

http://www.visnet-noe.org/

INESC Porto
===========

INESC Porto - Institute for Systems and Computer Engineering of Porto - is a
private non-profit association, recognized as Public Interest Institution, that
has been recently appointed as Associated Laboratory. It is located in Porto,
Portugal. At the Multimedia and Telecommunications Unit (UTM), INESC Porto
researchers have used and contributed to Marsyas development in audio, video and
multimodal analysis and processing.

http://www.inescporto.pt

Teligence
=========

Marsyas was used to design and develop an in-house tool for gender
classification (male/female/silence) for voice messages. The system achieves
classification of approximately 90% and is running on 10 hubs processing about
25000 recordings (1-2 minutes each) per day. The project was initiated by Paul
Snider with consulting by George Tzanetakis.

http://www.teligence.net/

Moodlogic
=========

Marsyas was used to design and prototype the audio fingerprinting technology
used to link user files to metadata and fix ID3 tags by the Moodlogic client.
The fingerprint is small (about 300 bytes/file), is fast to compute, and
matching is performed to a database of 1.5 million songs)

http://www.moodlogic.com/

last.fm
=======

http://www.last.fm

MusicEmo - Eric Yang, NTU, Taiwan
=================================

We identified and analyze three critical issues of music emotion recognition the
subjectivity of emotion perception, the ambiguity of categorical emotion models,
and the semantic gap between low-level audio signals to high-level emotion. Some
results of the previous two issues have been published. To see more detail,
please see the website. Marsyas is used in our system for feature extraction.
Our experiments show the strength of the features in Marsyas.

http://mpac.ee.ntu.edu.tw/~yihsuan/

Musicream
=========

Musicream is a novel music playback interface that lets users unexpectedly come
across musical pieces they like. It facilitates active, flexible, and unexpected
browsing. For example, the similarity-based sticking function enables user to
easily pick out and listen to similar pieces from a streaming flow of music.
Marsyas is used to automatically extract a single feature vector that
characterizes the content of a particular music piece. That vector is used for
color visualization of the audio content as well as to support the
similarity-based sticking function. Marsyas provided an easy way to extract
audio content information and enabled us to concentrate on designing and
developing the user interface.Masataka GotoSenior Research Scientist, AIST,
Japan

http://staff.aist.go.jp/m.goto/Musicream/

Musie Mood
==========

Our goal is to develop an integrated system to visualize and query large music
libraries. The layout is controlled by the user and similarity of songs is
measured in perceptual terms. We use Marsyas to extract structural features
which have perceptual interpretation (e.g. tempo, loudness, beat strength,
etc...).- Vladimir G. Kim, Steven Bergner, Torsten Muller. GrUVi lab, Simon
Fraser Univeristy, Canada.

http://gruvi.cs.sfu.ca/researchProject.php?s=373

Orelia - Sound Source Recognition
=================================

Orelia is using Marsyas as a calculation engine in his Sound Source Recognition
Software (OSSR). OSSR automatically recognize noise sources like aircraft noise,
railway noise, road traffic noise etc. The product is used by acousticians to
perform environmental noise assessment, complementing the sound pressure level.
Marsyas provides fast calculation and helps OSSR to process large amounts of
audiofiles in a very resonable time - Boris Defreville and Remi Poittevin.

http://www.orelia.fr

Multi-Label classification of music
===================================

In our project, the automatic detection of emotion in music was modeled as a
multi-label classification task. Marsyas was used for the extraction of rhythmic
and timbre features on a new collection of 593 songs. We compared the predictive
performance of four multi-label classification algorithms. Furthermore, the
predictive power of each feature was evaluated using a new multi-label feature
selection method. Konstantinos Trohidis - Grigorios Tsoumakas

http://mlkd.csd.auth.gr/multilabel.html

Dancing Robot with Marsyas
==========================

Marsyas is being used as the rhythmic interface beyond dancing robots, under a
PhD project at LIACC - Artificial Intelligence and Computer Science Laboratory,
and INESC Porto; which began in 2008. This research focus on multidisciplinary
aspects of interactive music and dancing robotic systems, and its applications,
being mainly founded on the interconnection of music, rhythm, perception,
emotion, movement, and interaction in an expression of dance, as a form of art
and sonification. Till date we developed a Lego-NXT-based robot, which uses
Marsyas to analyze low-level aspects of rhythm, through onset detection,
embodying the resultant rhythmic events with user-defined dance movements. I
would like to express my gratitude to the MARSYAS' comunity for making this
possible. - Joao Lobato Oliveira, PhD student at FEUP, Porto, Portugal.

http://paginas.fe.up.pt/~ee03123/

Personalized Multimodal Music Search
====================================

Marsyas has been helping a lot in our music search prototype called Personalized
Multimodal Music Search built in Dr Wang Ye's group at School of Computing,
National University of Singapore. We mainly use Marsyas for music classification
using audio signals. More specifically, we constructed our own classification
networks using Marsyas modules for genre, mood, instrument, and vocalness
classifications. The class activation probabilities in the classification
results were used as audio signatures to represent different music dimensions
(namely, genre, mood, instrument and vocalness). The music search prototype is
publicly accessible from the link below . Besides searching music by its
content, the search engine also provides music search by keywords. In addition,
the system allows users to personalize different music dimensions to do their
search by keyword or example (only mp3 examples can be recognized for now) . For
more details of the system, please refer to the SIGIR'09 paper titled
CompositeMap A Novel Framework for Music Similarity Measure. We really benefited
a lot from Marsyas framework in implementing the audio processing module of our
system. We thank all the contributors of Marsyas for their great efforts.-
Bingun (Eddie) Zhang, Ye Wang, National University of Singapore

http://mir.comp.nus.edu.sg

Modeling Emotional Content of Music
===================================

http://www.sauna.org/kiulu/emotion.html

ASTA - Automatic Subtitle Timing Annotator
==========================================

Subtitling a video/song is a tedious task, not only one has to write the
subtitle, but also one has to specify its timing (start and end times). ASTA
project tries to automatically determine the subtitles timing based on the,
possibly polyphonic, audio input. We found Marsyas to be the most suitable tool
for both signal processing (i.e. feature extraction) and machine learning (i.e.
training and classification). Beside its efficiency, it provides such a complete
solution to audio-analysis that we didn't need any other library. We thank
Marsyas team for open-sourcing such a great project. Mohamed Abdel Maksoud
(http://rw4.cs.uni-sb.de/people/mohamed.shtml).

http://sourceforge.net/projects/asta-annotator/

SndPeek
=======

sndpeek is just what it sounds (and looks) like * real-time 3D animated
display/playback * can use mic-input or wav/aiff/snd/raw/mat file (with
playback) * time-domain waveform * FFT magnitude spectrum * 3D waterfall plot *
lissajous! (interchannel correlation) * rotatable and scalable display * freeze
frame! (for didactic purposes) * real-time spectral feature extraction
(centroid, rms, flux, rolloff) * available on MacOS X, Linux, and Windows under
GPL authors Ge Wang | Perry Cook | Ananya Misra | George Tzanetakis (MARSYAS)
date 2003 - present

http://soundlab.cs.princeton.edu/software/sndpeek/

Analysis of Audio Features in Broadcast Sports Video
====================================================

Multimedia Lab (Ghent University - IBBT) has been using Marsyas for the analysis
of audio features in broadcast sports video. These audio features are used to
detect semantically meaningful audio segments (e.g., cheering of the audience,
commentary, whistles). This allows extracting specific events from the sports
video that are useful for different types of applications (sports summarization
and highlighting). - Chris Poppe, Multimedia Lab, Ghent University - IBBT,
Belgium.

http://multimedialab.elis.ugent.be/

vivi
====

Vivi is a computer program which performs music at approximately the level of a
student with one year of practice. Why write a computer program that can
simulate an inexperienced musician playing a low-quality instrument, when I have
an excellent-quality cello and decent viola? Well, in 70 years Ill be over 100.
Barring miraculous advances in medicine, I wont be able to exert enough force
with my right hand, my left hand wont be able to move fast enough, my reactions
wont be fast enough to adjust my actions as necessary. In short, I wont be able
to play cello. Musical creativity is hindered by physical constraints.

http://percival-music.ca/vivi.html
