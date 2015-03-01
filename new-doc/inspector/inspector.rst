.. title: Marsyas Inspector
.. slug: inspector


Marsyas Inspector helps with inspecting the structure and monitoring and
debugging the behavior of Marsyas networks. It operates on networks defined
in Marsyas Script files.

Features:

- Visualization of the network structure.
- Tick-by-tick execution of the network.
- Display and modification of control values of MarSystems.
- Plotting of input and output data of MarSystems.
- Monitoring execution time of each MarSystem.
- Reporting any warnings and errors in the network.

Overview
########

.. image:: /images/inspector/overview-annotated.png

At the top edge of the main window are the usual **menu** and **toolbar**.

The main window consists of multiple areas that can contain different
components. There is one **central area** that always displays the main view,
and there is one **side area** at each edge of the window that can optionally
display multiple peripheral views.

The central area always displays the **Structure View**, which visualises
network structure.

The side areas can contain the following components:

- **Control View**: Displays controls for the selected MarSystem.
- **Signal View** (multiple): Plots a slice of an input or an output of
  a MarSystem.
- **Messages View**: Displays warnings, errors and other messages produced by Marsyas.
- **Statistics View**: Displays statistics of execution of each MarSystem.

Side views can be **shown** or **hidden** using the View menu. Each side view
can also be hidden using the Close button in its top-right corner. Moreover,
each side view can be **detached** from the main window using the Detach button
in its top-right corner.

Opening a Marsyas Network
#########################

A Marsyas network is loaded by opening a Marsyas Script file either using
the File menu, or the Open System toolbar button.

Processing the Network
######################

The network is processed using the Tick toolbar button.
At that moment, as many slices will be processed as the number in the
number box left of the Tick button. This number can be changed arbitrarily.

Structure View
##############

The Structure View displays the structure of the MarSystem network.

MarSystems
**********

Each MarSystem is represented with a rectangular box.
The **name** and the **type** of the MarSystem is displayed at the top of the box.

At any time, one of the MarSystems may be **selected** by clicking on its name.
Selecting a MarSystem affects other views: for example, the Control View will
show controls for the selected MarSystem.

Composite MarSystems
*********************************************

Composite MarSystems can be displayed in two modes:

- **Expanded**: Children are visible.
- **Collapsed**: Children are hidden.

Switching between expanded and collapsed mode is done by clicking the "+/-"
button next to the MarSystem's name, or by double-clicking on the name.

Children are displayed within the expanded box of their parent MarSystem,
and input-output connections between them are displayed as lines.

MarSystem inputs and outputs
****************************

The top edge of a MarSystem represents its input, and the bottom edge
its output.

**Details** about inputs and outputs of all MarSystems are displayed when the
mouse is moved over an input or output of any MarSystem. The information
is displayed in the following format:

<number of samples> x <number of observations> [ <sample rate> ]

At any time, one input or output of a MarSystem may be **selected** by
clicking onto the top or the bottom edge of the MarSystem.
Selecting a MarSystem input or output affects other views: for example, the
last selected Signal View will plot the data of the selected input or output.


Controls View
#############

The Controls View displays controls for the selected MarSystem.

By defaulte, only **public** controls are displayed. Display of **private**
controls is enabled using the "Private" toggle box in the top-right corner
of the Controls View.

The list of displayed controls can be **filtered** by entering text into the
"Filter" text box at the top edge of the Controls View.

Control values are **updated** as the network is processed.

Each cntrol value can also be **changed** by double-clicking onto it and typing
the new value into the edit-box that appears, then pressing the Return key.

Signal View
###########

A Signal View plots a slice of an input or an output of a MarSystem.

There can be **multiple** Signal Views visible at a time. New signal views
are added using the View menu.

A MarSystem input or output is **selected** for plotting in two steps:

1. Select one of the Signal Views by clicking onto its plot area.
2. Select a MarSystem input or output.

The plot is **updated** as the network is processed, always displaying the
last processed slice of the selected input or output stream.
Note that **at least 1 slice** of the network must be **processed** for a Signal View
to plot anything.

There are different **plot modes** that can be selected using the "D" button
in the top-right corner of a Signal View:

- Table
- Points
- Sticks
- Line
- Curve
- Spectrogram

The **range** of the plot can be **auto-scaled** by clicking the "S" button in
the top-right corner.

Statistics View
###############

The Statistics View displays statistics of execution of each MarSystem:

- CPU Time
- Real Time

If a reference recording of the network execution is provided, then the
following information is displayed:

- Max Dev: maximum deviation from reference within the last output slice.
- Avg Dev: average deviation from reference within the last output slice.

Messages View
#############

The Messages View displays warnings, errors and other messages produced by
Marsyas. The view will become visibile automatically on every new message.
