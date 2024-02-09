### eCodeOrama, an educational interactive flow visualization tool for mit scratch programs

#### Brief explanation

The project will create a interactive tool to extract, visualize graphically and edit (to improve the presentation of) the layout of the flow of code in blocks / scripts in a mit scratch program and their interaction with any messages or other external events. The tool will use rules to decide on many layout parameters (e.g. the position of the code blocks in the layout, the colors used, etc) but the user will be able to overwrite the default choices. The presentation will be compatible with the codeOrama code layout specification.
The tool will also promote code understanding, especially to young students that use scratch, and will include debugging aids.
The students can use this flow to better visualize and understand their program, to explain it to others, to debug it and to design extensions and modifications.

#### Why is it important

Programming with visual / blockly languages
([`scratch`](https://scratch.mit.edu), [makecode](https://makecode.microbit.org/), etc)
is quite common in the young ages.
This tool will be specific to ([`scratch`](https://scratch.mit.edu) and will later be extended to handle more languages and visualizations.

An intuitive approach to this kind of programming is the creation of many threads/*scripts* that communicate through *messages*.
Yet, in many cases the resulting execution flow is tricky to follow,
but would be very useful from an educational perspective (and for debugging too).

We will make an interactive tool to parse a computer program and reveal this flow,
mainly the inter-thread communication.
The input programming language will be processed as `json` structures.
Communication among different threads and components will be shown explicitly.

#### Github of the project
git@github.com:sarantos40/eCodeOrama.git

#### Expected Results

A tool to visualize and edit the layout of the event based script flow of a scratch program, keeping it compatible with the codeOrama code layout specification.

#### Knowledge Prerequisites

python, mit scratch, gui development

#### Related bibliography

  * Ladias, A., Mikropoulos, Ar., Ladias, D. & Bellou, I.  «*CodeOrama: A two-dimensional visualization tool for Scratch code to assist young learners' understanding of computer programming*».  Themes in eLearning, Vol 14 (2021).  <http://earthlab.uoi.gr/tel/index.php/themeselearn/article/view/32/18>

  * Λαδιάς Αν., Λαδιάς Δημ.  «**Η αναπαράσταση του αλγορίθμου με τη βοήθεια του κωδικΟράματος σε περιβάλλοντα οπτικού προγραμματισμού**».  Περιοδικό «*Θέματα Επιστημών και Τεχνολογίας στην Εκπαίδευση*», τόμος 9(2), (σελ. 103-117), 2016, ISSN: 1792-8796.  <http://earthlab.uoi.gr/thete/index.php/thete/article/view/265/141>

#### Related Links for codeOrama and tools

  * [Related student notes](https://www.dropbox.com/s/dk2n4plqjsnzago/2015%20Special%20programming%20topics%20in%20Scratch.pdf?e=1&dl=0)
  * https://eproceedings.epublishing.ekt.gr/index.php/cetpe/article/view/3690
  * https://github.com/dgmid/CodeOverview
  * https://blog.ouseful.info/2016/02/18/blockpy-python-blockly-environment/
  * https://scratch.mit.edu/
  * https://mindplus.cc/en.html
  * https://pictoblox.ai/
  * https://developers.google.com/blockly/
  * https://en.wikipedia.org/wiki/DOT_(graph_description_language)
  * https://www.graphviz.org/
  * [Description of *codeOrama* and links by Tassos Ladias](TassosLadias.html)
  * [Other material in Greek](GreekRef)

#### About the flow

The *primary flow* is, in most cases, the set of threads that run concurrently.
In `python` we can create threads, but this is not very common.
We usually start only *main*. 
Other languages, like MIT [`scratch`](https://scratch.mit.edu) are based on threads and events.
The [`scratch`](https://scratch.mit.edu) programming language will be processed as `json` structures.

The actual [`scratch`](https://scratch.mit.edu) code is stored in `json` (inside a `zip` file),
which make the parsing code easier,
and we can concentrate on the visualization.

We will use [`scratch`](https://scratch.mit.edu), where
every object (called *sprite*) can create its own threads (executing code in code blocks thay are called *scripts*),
that start with their `When ...` conditonal command (which appears first in the *script*) is triggered by an *event*.

*Events* can have a variety of sources (such as the keyboard, the mouse or other devices).
Any *script* can also trigger (software) *events* using `broadcast` with a message.
They usually trigger one or more *scripts* that start with `When I receive message X`, to initiate more threads.
Sometimes the broadcaster will wait for their completion (using the command `broadcast message X and wait`).
Each *event* or message can initiate many concurrent threads.
This is the flow that I consider primary, and we should start from that.

#### CodeOrama

A common way to demonstrate the flow of a scratch program is `CodeOrama`.

[Here](Examples) and [Here](https://sarantos.no-ip.org/eCodeOrama/Examples) are also some *codeOrama* examples - there is more material available, but it is in Greek.
Nevertheless, the output layout of *codeOrama*s is quite clear.
Our output does not have to be exaclty the same, but has to be compatible, beautiful and clear.

The Layout of a `CodeOrama` mainly consists of a table where:

  * Each column represents a *sprite*
  * Each rows represents an *event*
      * *events* are
          * messages from (the same or other) *sprites*
          * user interface events (mouse clicks, keystrokes, ...)
  * Each cell contains (zero or more) *scripts* (code blocks)
      * the cell contains the any *scripts* of the *sprite* that are called on the *event*
      * all *sprite* *scripts* are put into the appropriate rows
      * all *event* inititated *scripts* are put into the appropriate column
  * We include a header row and a header column that describe them (with texts and icons)
  * Arrows connect the code line that triggers an *event* with the cell / *script* that handles it
      * also creation of *sprite* clones
      * maybe also calls to user defined functions
      * and the return to the flow of the code

`CodeOrama` is constructed manually so far.
Here we will develop *eCodeOrama*, an interactive tool that will help the user to create a compatible `CodeOrama` layout, and similar text reports / outputs about a [`scratch`](https://scratch.mit.edu) program.

#### MIT scratch

The visualization can be a graph, or a some text-based layout
(with pieces of code and the appropriate edges with arrows).
We can use a graph tool / library to handle the graph layout issues.

One such visualization in common use is *codeOrama*.
The *codeOrama* is often used to provide a higher level of code description,
but it is constructed manually.
The idea is to make a tool to create *codeOrama*s (as export / printing operation).

### Getting Started

The student must be already familiar
with the programming language and the main tools that he intents to use.

During the discussion period the user should deepen his knowledge
to the specifics of the problem, such as the `json` format and tools
and the parsing of [`scratch`](https://scratch.mit.edu) input,
to identify the significant available data, as
*sprites*, *events*, *scripts* and commands of interest (that broadcast messages or handle *events*).

This way, he will be able to write in detail the description of the milestones,
especially the first ones.

### Proposed initial implementation steps

The proposal should define the expected results / milestones
for each short period of time (e.g. each week).
that should gradually demonstrate parts of the developed functionality.

Here is an example of such a sequence of milestones:
 1. Week 1
      * Parse `scratch` v3 input, identify main entities and produce simple text lists and reports
 1. Week 2
      * Create a graphical output displaying the *scripts* as graphical nodes on appropriate row (*event*) and column (*sprite*) and the edges that connect them.
 1. Week 3
      * Make an (interactive) graphical application, with basic interaction and configuration (colors, order) and save / load the configuration.
 1. Week 4
      * Implement interactive editing / relocating of *sprites*, *events*, *scripts* and edges.
 1. Week 5
      * Export the layout to `pdf`, `json`, generic `xml`, `xlsx`, `ods`.
      * Parse `scratch` v2 input
 1. Week 6
      * Prepare and test an initial standalone first version, ready to be used by users.
 1. Week 7
      * Display `scratch` comments and use them to pass special presentation directives
 1. Week 8
      * Identify and implement rules for better placement of nodes and edges, and provide options for their selection.
 1. Week 9
      * identify additional required interactive functionality, ...
 1. Week 10
      * ...
    
### More about *codeorama*

### More about this project

[Here](Ideas.html) are some more technical details and implementation ideas / discussion, that one can adopt to his proposal.

Throughout this project, we will monitor and discuss the progress of the project. Tassos Ladias, one of the *codeOrama* designers, participates in the support of this project.
 
For easier code mainenance, `python` is preferred but not required.

Each proposal will specify the implementation language, environment, tools, application model, firsti steps, milestones, ...

You can ask general questions on the forum, and we can discuss specific parts of your proposal on private messages.
