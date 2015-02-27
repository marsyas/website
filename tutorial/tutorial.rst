.. title: Tutorial
.. slug: tutorial

################
Marsyas Tutorial
################

Note: This tutorial is work in progress. If you find any issues such as
broken code and links, please report to: jakob.leben at gmail.com.

Overview
========

Marsyas is a software framework for audio processing. This means that it is
a collection of many different kinds of components that help you process
audio. These components include:

- Readily runnable **command-line programs** for that process and extract
  information from audio in particular ways.
- A **C++ library** offering a large set of basic audio processing units
  that you can compose to build your custom programs.
- A simple programming language called **Marsyas Script** that makes
  composition of the basic audio processing units very easy.
- A program called **marsyas-run** that executes Marsyas scripts.
- A graphical program **Marsyas Inspector** for inspecting and debugging
  behavior of Marsyas scripts.

This tutorial will demonstrate usage of *Marsyas Script* to build custom
audio processing programs from basic units, and running them using
*marsyas-run*.

Installing Marsyas
====================

First things first, let's get Marsyas installed!
The simplest way to get Marsyas ready for use is to download it from
our Bintray repositories:

Mac OS X:
    Download the latest version `here <https://bintray.com/marsyas/macosx/marsyas>`__.

    The ZIP package contains the following directories and items:

    - **bin**: all command-line programs, including **marsyas-run**
    - lib: C++ libraries
    - include: C++ header files
    - **Marsyas Inspector app**.

Windows:
    Download the latest version `here <https://bintray.com/marsyas/windows/marsyas>`__.

    The ZIP package contains the following directories and items:

    - **bin**: all command-line and graphical programs,
      including **marsyas-run** and Marsyas Inspector (**marsyas-inspector**)
    - lib: C++ libraries
    - include: C++ header files

Building your own Marsyas
=========================

If you want to live on the bleeding edge,
or you use Linux (which is about the same), or you are just up for a challenge,
you can try building Marsyas from source code.
Find out about this `on Marsyas website`__.

.. __: http://marsyas.info/downloads/sources.html

Let's get started
=================

In order to proceed comfortably with this tutorial,
you should know how to use the command-line environment of
your operating system (called Command Prompt on Windows, and Terminal on Mac OS X).
You should know how to use the built-in commands to navigate the
file system of your computer, and how to execute any program using the
command-line. If you are not proficient in this, please read a tutorial about
using your command-line environment first.

The next requirement is that you have the ``marsyas-run`` program
installed and accessible for execution from
command-line. In the rest of this tutorial, we will assume that
the program can be executed simply by using its name, e.g. with a command::

    marsyas-run

In the following examples, substitute the above with whatever command is suitable
for your system and installation of Marsyas.

Executing this program without any arguments (options) should print the
following output::

    Usage: marsyas-run <plugin-file> [options]

If you see this, then you are good to go!

Try a Marsyas script
--------------------

Below is an example Marsyas script that plays an audio file::

    Series {
        -> SoundFileSource { filename = "some/cool/sound.wav" }
        -> AudioSink
    }

Try out the above script by following these steps:

#. Copy the code and save it into a file named "test.mrs".

#. Modify the code by replacing "some/cool/sound.wav" with the location of
   a WAV soundfile on your computer.

#. Run the script using the command::

    marsyas-run test.mrs

You should hear the file being played back. After the entire file has been
played ``marsyas-run`` will simply hang, so you have to kill it manually
(for example using ``Ctrl+C`` key combination in the command line environment).
Later we will learn how to write scripts that terminate themselves.

What Does Marsyas Do?
=====================

In essence, Marsyas is a framework for creation of programs that process
**streams of numbers**. These streams can represent various things, but
Marsyas has some functionality that is especially useful for streams that
represent audio or interesting information that can be computed from audio:
melody, harmony (chords), rhythm, frequency spectrum, etc..
Nevertheless, at the most basic level, all the processed information is in the
form of streams of numbers.

A Marsyas program is thus a **stream processing program**:
it consumes one or more **input streams** of numbers
and produces one or more **output streams** of numbers:

.. <diagram>

Like everything else in the universe, numbers don't just appear out of nowhere,
and they don't disappear into thin air. Incoming streams of numbers have
a **source**, and outgoing streams of numbers have a **destination**.
Marsyas supports various kinds of sources and destinations: audio arriving
from a microphone, audio being played back on speakers, audio read from and
written to audio files, or numbers read from and written to various other kinds
of files (CSV, Weka, ...).

.. <diagram>

Streams of number can be **finite** or **infinite**. A program may itself
run infinitely (as long as its user wishes), consuming and producing infinite
streams (typically when processing real-time audio from the microphone),
or it may process a finite stream of numbers and then terminate (typically
to process audio files).

MarSystems and Networks
=======================

Okay, so the purpose of a Marsyas program is to process
(possibly infinite) streams of numbers. But how does it do that?
Or rather, how can *you* use Marsyas to create programs that process
numbers in a *particular way* that you want?

Marsyas provides many **basic building units** that you can combine and
compose into sound processing programs.
If we look at these units and squint a little,
each of them looks and behaves just like the program as a whole: it is a
baby stream processing program! The only difference is that it does a
much simpler job, perhaps even just adding numbers from two input streams
together. A whole program is a composition of basic units which pass
streams of numbers to each other: the output of some units is the input
to others. Some basic units also consume the program's input streams and
produce the program's output streams.

.. <diagram: network>

A basic unit of composition in Marsyas is called a **MarSystem**, and
a composition of MarSystems is called a **network**.
Furthermore, a network of MarSystems is not just a disorganized mess of
interconnected units. **Primitive MarSystems** are grouped into larger units called
**composite MarSystems**, which are themselves composed into even larger
groups. This is very useful for several purposes:

- It provides logical grouping of units according to their combined tasks.
- It makes connecting units and groups of units much simpler and managable.
- It allows re-use of a composition of units (creating multiple copies of
  the same group).

Ultimately, the program as a whole is just a very large composite MarSystem.

.. <diagram: hierarchical composition>

.. For example, the following diagram represents a network of MarSystems that
   plays a sinusoid wave and noise together:

.. <diagram: concrete network of code below>

.. The above diagram represents the network defined by the Marsyas Script code below.
    Regions of code that correspond to diagram blocks are highlighted::

      Series {
          -> Parallel {
            -> Series { -> SineSource { frequency = 440.0 } -> Gain { gain = 0.4 } }
            -> Series { -> NoiseSource -> Gain { gain = 0.05 } }
          }
          -> MixToMono
          -> AudioSink
      }

Marsystem Types
===============

There are many different types of MarSystems. Each type serves a different
purpose and has a unique name. The types are mainly divided into **primitive types**
and **composite types**. Primitive types operate directly on streams of numbers;
for example,
SineSource generates sine waves,
SoundFileSource reads an audio file,
Gain scales a stream of numbers,
AudioSink sends audio to the computer's speakers. Composite types group
other MarSystems in different ways, for example Series connects other MarSystems
in a series, Parallel runs other MarSystems in parallel. A network may contain
multiple instances of any MarSystem type.

A listing of most MarSystem types and their descriptions are provided in the
`C++ library reference <http://marsyas.info/doc/sourceDoc/html/index.html>`__.
Each MarSystem type is a C++ class deriving from the "MarSystem" base class.
The names of MarSystem types used in Marsyas Script are identical to the
names of the C++ classes.

Alternatively, a list of all available MarSystems in a given installation
of Marsyas is provided by the ``marsyas-info`` command-line program, when
executed like this::

    marsyas-info list marsystems

This is useful because the online C++ library reference is not always
up-to-date, some MarSystems are not included in the reference, or they may not
be included in your particular installation. However, ``marsyas-info`` can
not provide elaborate descriptions of MarSystem types as the online reference
does.


Composite MarSystems
====================

As mentioned above: the basic role of composite MarSystems is to group other
MarSystems together. We say that the composite MarSystem is the **parent**
and the MarSystems inside it are its **children**.


Besides grouping their children, composite MarSystems do a much more interesting
job too. There are different *types* of composite MarSystems, and each one
composes MarSystems placed inside it in a specific way. More precisely,
the type of a composite MarSystems defines the **flow of data** among its
children. In other words: outputs and inputs of MarSystems are never connected
excplitly - instead they are implied by the type of their parent MarSystem.

Let's take a look at different types of composite MarSystems...

Series
------

The Series composite MarSystem composes its children into a series so
that data flows from the first to the second, from the second to the third, and
so on...

.. <diagram>

The following network generates a sine wave, scales it by 10, clips it to
the range of -1 to 1, scales it down by 0.04, and finally sends into to
the speakers. This results in an audible distortion of the sine wave, thereby
creating higher-frequency harmonics:

.. <diagram>

::

    Series {
      -> SineSource -> Gain {gain=10.0}
      -> Clip -> OnePole {alpha = 0.5}
      -> Gain {gain = 0.04}
      -> AudioSink
    }

Parallel
--------

The Parallel composite MarSystem passes each channel of the input to
one of its children, and combines the outputs of all children into a
multi-channel output.

.. <diagram>

In the following network reads a soundfile, which we assume to have
2 channels of audio. The two channels are split by ``Parallel``
and a different time delay is applied to each channel.
They are then re-combined by ``Parallel`` and sent to the speakers.

.. <diagram>

::

  Series {
    -> SoundFileSource { filename = "sound.wav" }
    -> Parallel {
        -> DelaySamples { delay = 0 }
        -> DelaySamples { delay = 10000 }
    }
    -> AudioSink
  }

Fanout
------

The Fanout composite MarSystem passes a complete copy of its input
(all channels) to each of its children, and combines the outputs of
all children into a multi-channel output.

.. <diagram>


Sources, Processors and Sinks
=============================

If we only had composite MarSystems, we couldn't compose very interesting
programs. Let's look at the **primitive MarSystems** that actually do
some interesting work.

Primitive MarSystems could be classified into three kinds:

Sources:
  Produce their output stream by accessing data outside the
  program, or generate a new stream.

Processors:
  Produce their output stream by performing some computation on their input
  stream.

Sinks:
  Send their input stream to a destination outside of the program.

The world is full of sources and sinks
--------------------------------------

It is possible to construct useful networks using only source and sink
MarSystems. Remember the first example in this tutorial that just played
a sound file? I will save you the trouble of scrolling up and give you
the code here again::

    Series {
        -> SoundFileSource { filename = "some/cool/sound.wav" }
        -> AudioSink
    }

This is simply a **SoundFileSource** that reads a sound file to produce its
output stream,
composed in a series with an **AudioSink** that sends its input stream to the speakers.

What about the inverse: recording audio from a microphone into a file?
Here we go::

    Series {
        -> AudioSource
        -> SoundFileSink { filename = "recording.wav" }
    }

The **AudioSource** takes audio from the microphone to produce its output,
and the **SoundFileSink** that takes its input and writes it into into a sound file.

This kinds of sources and sinks represent inputs and outputs of the
program as a whole.
It may seem counter-intuitive at first that when we talk about MarSystems
which represent program *inputs*, we only talk about their *output*,
and when we talk about MarSystems which represent program *outputs*,
we only talk about their *input*. What would happen if we placed a source
in series *after* another MarSystem?::

  Series {
    -> SoundFileSource { filename = "sound.wav" }
    -> SoundFileSource { filename = "different_sound.wav" }
    -> AudioSink
  }

Here we have two SoundFileSources in a series. What happens is that the
second one simply *discards* the input stream it receives from the first
one, and instead produces an output simply by reading its own sound file.
Likewise, what would happen if we placed a sink in series before another
MarSystem?::

  Series {
    -> SoundFileSource { filename = "sound.wav" }
    -> AudioSink
    -> SoundFileSink { filename = "copy.wav" }
  }

Here we have two kinds of sinks in a series.
What happens is that the AudioSink simply
*passes* its input to its output unchanged, in addition to sending it to
the speakers. The SoundFileSink will thus create a copy of the file read
by the SoundFileSource. Most sinks will pass their input to their output
unchanged - although it's not guaranteed, and you should read documentation
of each different type of sink before relying on it.

.. Mention CsvSink here, for completness

Can something come out of nothing?
----------------------------------

A special kind of sources are those that **generate** their output out of
nothing.

For example, there is a number of different sound generators, like
**SineSource**, **NoiseSource** and **PWMSource** in the following examples.

::

  Series { -> SineSource -> Gain{gain=0.1} -> AudioSink }

::

  Series { -> PWMSource -> Gain{gain=0.1} -> AudioSink }

::

  Series { -> NoiseSource -> Gain{gain=0.1} -> AudioSink }

Note the addition of the **Gain** MarSystem in between the sources and the sinks.
I did that for two reasons: one is to save your ears from pain, because
the sound-generating sources typically output signals with unit amplitude
(fluctuating between -1 and 1), which is the maximum possible amplitude that
can be played back by the speakers; another reason is to introduce you
to the third kind of primitive MarSystems: processors.

Number crunching
----------------

**Processing** MarSystems take their input stream and do some **computation**
with it to produce their output stream. Again, the data could be anything, any
imaginable stream of numbers.

For example, the **Gain** MarSystem simply
takes numbers from its input stream one by one, multiplies them by some
factor, and sends them out as another stream. The gain factor is configurable;
configuration of MarSystems using *controls* is explained in one of the
following sections.

A more complex processing MarSystem is **OnePole**, which is a simple
first-degree (one-pole) linear filter.
In the following code, it acts as a low-pass filter, rejecting some of the
higher frequencies of the noise generated by the NoiseSource::

  Series { -> NoiseSource -> Gain{gain=0.1} -> OnePole{alpha=0.9} -> AudioSink }

If we give Gain or OnePole audio as input, they produce audio as output.
In other words: if the input is something that makes sense to send to your
speakers, so is their output. There are other kinds of processors that
**extract information** from audio.

For example, the **Energy** MarSystem will look at consecutive slices of its
input stream, and compute the energy (power) of the signal within each slice.
By default, each slice is 512 elements large (this will be explained later).
Therefore, for each slice of input, a single output number will be produced.
The input stream is thus **reduced** to something that is not audio
anymore, but some insight about the nature of the audio - this is also
called an **audio feature**::

  Series {
    -> input: SoundFileSource{ filename="sound.wav"}
    -> Energy
    -> CsvSink { filename="result.csv" }
    + done = (input/hasData == false)
  }

The have deliberately avoided using an AudioSink or a SoundFileSink in the
above example: it would not make sense to send the output of Energy to the
speakers, or store it in a sound file. In contrast, the sink that I used
is useful for storing the output of audio features:
**CsvSink** will produce a file in the
Comma-Separated-Values format, which is just a plain text file with
columns of numbers separated by commas or spaces or tabs or any
other character, as long as it is consistent.

Try the above script and look at the file "result.csv" that it produces.
You will see one column of numbers for each channel of the source sound file.
Each number in a column is energy computed over 512 samples of audio from
the sound file.

Another useful audio feature is computed by the **ZeroCrossings** MarSystems:
it looks at consecutive slices of input audio and counts the number of
times the signal within each slice crosses from positive to negative or the
other way around. This count is then divided by the number of samples in
a slice (again, 512 by default). Each number in the output stream is the
zero-crossings ratio for one slice.
This feature is useful in estimating the pitch of the sound::

  Series {
    -> input: SoundFileSource{ filename="sound.wav"}
    -> ZeroCrossings
    -> CsvSink { filename="result.csv" }
    + done = (input/hasData == false)
  }

Just like Energy, ZeroCrossings operates on each audio channel individually,
and so the produced file "result.csv" will have as many columns as audio
channels.

The transformation of audio that has the most diverse range of
applications is arguable the Fourier transform. It produces a frequency
spectrum from a time-domain signal, which is a set of complex numbers.
Typically for audio analysis purposes, the magnitude of the complex spectrum
is computed, resulting in a *power spectrum*. This is done over
consecutive slices of audio, resulting in a *power spectrogram* - a
sequence of power spectrums. With Marsyas, it can be computed using
the **Spectrum** and **PowerSpectrum** MarSystems, like this::

  Series {
    -> input: SoundFileSource{ filename="sound.wav"}
    -> Spectrum -> PowerSpectrum
    -> CsvSink { filename="result.csv" }
    + done = (input/hasData == false)
  }

If you look into the "result.csv" file you will see a huge amount of numbers
distributed across many columns.
What has just happened? Each row represents a power spectrum computed from
a different slice of input audio. Each column represents a bin of the
power spectrum. There is exactly 257 bins, providing 257 unique
magnitudes of the spectrum computed from a slice of 512 samples.
What about the multiple input audio channels? Well, the Spectrum MarSystem
simply ignores all channels other than the first.

So, Energy and ZeroCrossings produced as many columns in the CSV file
as the input channels, but Spectrum and PowerSpectrum only worked with
a single input channel and produced a large number of columns in the CSV
file. How did the CsvSink know how to write the data into the file?
And what exactly happens on the way between the MarSystems? Read on!


The shape of streams
====================

If you read the previous section carefully and tried out the examples,
you have probably started to wonder how precisely does data move between
MarSystems, and what did I mean when I said "multiple channels".

Well, the stream of data that moves between any two MarSystems
is divided into slices, and each slice comes in the form of a
**two-dimensional array** of numbers
- a matrix, if you wish. Each slice is characterized by its number of
rows and columns. Each column represents a different moment in time, and is
therefore also called a **sample**. Each row represents a parallel flow of
data, and is therefore also called an **observation**.

.. <image>

As you could already guess, **observations** are good for representing
**parallel channels** of audio. However, they are useful for many other purposes.
For example, when computing a Fourier transform, all the resulting
**bins of the spectrum** represent information about the same moment in time
(or rather range of time).
Therefore, the power spectrum of an input slice with
1 observation (channel) and 512 samples will be an output slice with
1 sample and 257 observations (512 / 2 + 1 unique bins).

.. <image>

For example, the following script computes the power spectrogram of an
input soundfile. Unless specified otherwise, the sound file
reader will output slices of 512 samples. Each slice will be converted
into a power spectrum of 257 observations, and then written into a text file
as a row of numbers (in the text file, rows and columns are inverted, so
the time flows downwards)::

  Series {
    -> input: SoundFileSource{ filename="sound.wav"}
    -> Spectrum -> PowerSpectrum
    -> CsvSink { filename="result.csv" }
    + done = (input/hasData == false)
  }

Try opening the output file in MATLAB or Octave or Python or simply in
a spreadsheet editor like Microsoft Excell.

You can run the same script with a **different slice size** by using the
``--block`` or ``-b`` option of ``marsyas-run``. This will instruct the
first MarSystem in the network to work with slices of the desired number of
samples, and all the following MarSystems will adjust their output
according to the shape of data they receive.

If you save the above script into a file named ``spectrum.mrs``, then the
following command will run this script with initial slices of 64 samples,
resulting in a (much longer) sequence of power spectrums with 33 bins::

    marsyas-run spectrum.mrs -b 64

The number of **samples** in each slice determines the **time-resolution** of
computation - how many samples are processed by a MarSystem before they
are sent to other MarSystems as a slice. In some cases this does not
affect the *result* of computation, and in others it does. For example,
a sine wave will be generated equally if it is generated 64 by 64 samples
or 1024 by 1024 samples, but a Fourier transform of 64 samples is a
very different thing than a Fourier transform of 1024 samples.

.. Re-visit composite marsystems!

The power of controls
=====================

In the code examples above, we sometimes provided additional information
to MarSystems to clarify how we want them to operate: we supplied the
name of a file to SoundFileSource and CsvSink, the desired
gain factor to Gain, the desired sine wave frequency to SineSource, and
so on... This section explains how exactly this works.

So far we were concerned more with *what* was computed, and less with *how*
it was computed.
The input and output of MarSystems represent *what* data that they process
and *what* data they produce. However, each MarSystem also has a set of
adjustable **controls**, and their purpose is, well, to control *how* precisely
the MarSystem does its processing.

In Marsyas Script, the value of controls for a MarSystems is specified in
curly brackets  ``{ }`` after the type of the MarSystem. The syntax is
rather intuitive: ``<control name> = <value>``.

Control types and values
------------------------

Control values can be one of 5 different types:

- truth values: ``true`` or ``false``
- integer numbers: ``0``, ``-5``, ``999``, ...
- real numbers: ``0.5``, ``1.345``, ``10.0``, ...
- 2D arrays of real numbers: ``[1.0, 5.5; 2.2, 5.6]``, ...
- strings: ``"some/cool/sound.wav"``, ...

Each control of a MarSystem has an **expected type**, and the assigned value
must **match that type**. For example, the following code will produce an
**error** in ``marsyas-run``, because SoundFileSource expects a string for
the ``filename`` control, but we are giving it a number::

  Series {
    // Error: filename is not a number, but a string:
    -> SoundFileSource { filename = 12345 }
    -> AudioSink
  }

Likewise, this will produce an error because SineSource expects a
real number for frequency, but we are giving it an integer number::

  Series {
    // Error: frequency is not an integer, but a real number:
    -> SineSource { frequency = 250 } -> Gain { gain = 0.1 }
    -> AudioSink
  }

Just adding a decimal point and a zero would fix the problem:
``frequency = 440.0``.

Each MarSystem type also has **default values** for each of its controls,
which are used if a value is not explicitely specified in the script.
For example, the default value of the ``frequency`` control of the SineSource
type is ``440.0``, so the following two code examples are equivalent:

::

  Series { -> SineSource { frequency = 440.0 } -> AudioSink }

::

  Series { -> SineSource -> AudioSink }

Discovering all controls
------------------------

For each MarSystem type, all its controls, their types and default values
can be listed by the ``marsyas-info`` program. For example, the following
command lists all controls of the SineSource type::

    marsyas-info list controls SineSource

Further information about some controls is provided in the
`C++ library reference <http://marsyas.info/doc/sourceDoc/html/index.html>`__
, in the documentation of C++ classes that represent MarSystem types.
Note that the C++ documentation often displays control names prefixed with
their type and a slash. For example, the "frequency" control of SineSource
would be displayed as "mrs_real/frequency". In Marsyas Script, just disregard
this and always use the control name without the type.

Control expressions and paths
-----------------------------

Aside from assigning immediate values to controls, we can assign them
a mathematical **expression**. For example, the following SineSources
have harmonic frequencies (all multiples of the same frequency), and their
amplitudes are proportional to their own frequency::

  Series {
    -> Parallel {
      -> Series {
          -> SineSource { frequency = 230.0 }
          -> Gain { gain = 1 }
      }
      -> Series {
          -> SineSource { frequency = (3 * 230.0) }
          -> Gain { gain = (1 / 3.0) }
      }
      -> Series {
          -> SineSource { frequency = (5 * 230.0) }
          -> Gain { gain = (1 / 5.0) }
      }
    }
    -> MixToMono
    -> AudioSink
  }

The basic mathematical operations are supported:

- addition: ``+``
- subtraction: ``-``
- multiplication: ``*``
- division: ``/``

Note that all control expressions must be enclosed in parenthesis ``( )``!
Parenthsis can also be used in expressions to force non-standard
order of calculation, for example: ``(2 * (5 + 7))``.

Now, if we wanted to change the entire set of harmonic frequencies up,
we would need to change the number ``230.0`` for each of the SineSources.
We can save ourselves this work by using the value for the frequency of
one SineSource in another SineSource. The condition for this is that
we give the first SineSource a **MarSystem name**. This is how we give it
the name "base": ``base: SineSource``. Its frequency control is then
accessible with a **control path** ``/base/frequency``::

  Series {
    -> Parallel {
      -> Series {
          -> base: SineSource { frequency = (360.0) }
          -> Gain { gain = 1 }
      }
      -> Series {
          -> SineSource { frequency = (3 * /base/frequency) }
          -> Gain { gain = (1 / 3.0) }
      }
      -> Series {
          -> SineSource { frequency = (5 * /base/frequency) }
          -> Gain { gain = (1 / 5.0) }
      }
    }
    -> MixToMono
    -> AudioSink
  }

As you can hear, whatever frequency value we give to the "base" SineSource,
others will compute their frequency values from the "base" one.

We could further improve this by **add controls** to MarSystems which will act
as temporary value placeholders. We can add controls to *any* MarSystem,
including the composits. This is done by adding the ``+`` sign
in front of the control value assignment: ``+ <new control name> = <value>``.
For example, we could add two controls to the top-level Series, and use
their value throughout the network: we refer to controls of the root MarSystem
by ``/<control name>``::

  Series {
    + frequency = 360.0
    + amplitude = 0.1
    -> Parallel {
      -> Series {
          -> SineSource { frequency = /frequency }
          -> Gain { gain = (amplitude / 1) }
      }
      -> Series {
          -> h1: SineSource { frequency = (3 * /frequency) }
          -> Gain { gain = (/amplitude / 3) }
      }
      -> Series {
          -> SineSource { frequency = (5 * /frequency) }
          -> Gain { gain = (/amplitude / 5) }
      }
    }
    -> MixToMono
    -> AudioSink
  }

Controls can also be set on command-line, when running ``marsyas-run``,
using the option ``-c <control name>=<value>``, which will override
existing control values. For example, assuming that we save the above
script into "harmonics.mrs" we could run
it with the base frequency 670Hz like this::

    marsyas-run harmonics.mrs -c frequency=670

Likewise, we can make a script that can play any sound file, specified
on command line. Here is the script, which we save into "play.mrs"... ::

  Series {
    -> input: SoundFileSource
    -> AudioSink
    + done = (input/hasData == false)
  }

...and here is the command to play our beloved sound::

  marsyas-run test.mrs -c input/filename="cool/sound.wav"


Control links
-------------

So far we have only used controls to, ehm, control operation of MarSystems.
What else could they possibly be used for? There is more to controls:
some MarSystems will report information by changing the values of their
controls over time, and this can even be used for controlling other
MarSystems!

We can convert any data stream into a change of a control value using
the MarSystem **FlowToControl**. This MarSystem has a control named "value",
which is set to the value of the first element of each input slice as it
is processed. We can use the value of this control in an expression for
another control. This creates a **control link** so that whenever one of
the linked controls changes, the other one is automatically updated.

For example, the following code places a FlowToControl named ``energy``
after the Rms that computes the root-mean-square energy of its
input. The ``energy/value`` control belonging to the FlowToControl is
used in the expression for the ``gain`` control of the Gain that
attenuates the NoiseSource::

  Series {
    -> Parallel {
      -> Series {
        -> input: SoundFileSource {filename="sound.wav"}
        -> Rms
        -> energy: FlowToControl
      }
      -> Series {
          -> NoiseSource
          -> Gain {gain = (energy/value * 0.5)}
          -> AudioSink
      }
    }
    + done = (input/hasData == false)
  }

If you run this script on a rather rhythmical sound file, you will hear
noise which follows the sound energy contour of the sound file.


Controlling the termination of a script
---------------------------------------

There is one special control name that has appeared in every code example
that uses SoundFileSource: "done". This is a mechanism for a Marsyas script
to report its own termination. Before ``marsyas-run`` starts running a script,
it looks whether the root MarSystem has a control named "done" of boolean
type. If such control is found it is being monitored. As soon as its value
becomes ``true``, ``marsyas-run`` stops executing.

In our examples, we sometimes added this control explicitely to the root
MarSystem and defined its
value with the expression ``(input/hasData == false)``, where ``input``
is the name of a SoundFileSource. Now, SoundFileSource has a boolean control
named ``hasData`` that is ``true`` as long as there is more data to be read from
the sound file. When the end of the sound file is reached, this control
becomes ``false``. This in turn triggers re-evaluation of the root ``done``
control, which now evaluates to ``true``, and the script stops executing.



Advanced data flow management
=============================

ShiftInput
-----------

...

Accumulator
-----------

...

Shredder
--------

...

Memory
------

...

Transpose
---------

...





Where to go from here
=====================

marsyas-info:
  The ``marsyas-info`` command-line program provides information about features
  available in your installation of Marsyas.

  All Marsystem types are listed using the following command::

      marsyas-info list marsystems

  All controls of a MarSystem type are listed using the following command while
  replacing ``<marsystem type>`` with the name of the MarSystem type::

      marsyas-info list controls <marsystem type>

Manual:
  Further information about Marsyas and its features is available in
  `the manual <http://marsyas.info/doc/manual/marsyas-user/index.html>`__.
  Please note that some information in the manual is out of date.

C++ Library Reference:
  Detailed description of Marsystem types is provided in
  `the C++ library reference <http://marsyas.info/doc/sourceDoc/html/index.html>`__.
  Each MarSystem type is a C++ class deriving from the "MarSystem" base class.
  The names of MarSystem types used in Marsyas Script are identical to the
  names of the C++ classes.
  The C++ documentation often displays control names prefixed with
  their control type and a slash (for example "mrs_real/frequency").
  In Marsyas Script, disregard this and use control names without their type.

Marsyas Script Reference:
  Detailed description of the Marsyas Script language syntax and semantics
  is provided in
  `the language reference <https://github.com/marsyas/marsyas/wiki/Scripting-Language>`__.
