## Overview

[Stockfish](https://stockfishchess.org) is a free, powerful UCI chess engine
derived from Glaurung 2.1. However, this is not the original Stockfish and doesn't
actually improve upon it in any way, unfortunately.

This is Fat Fritz 2, a Stockfish derivative that uses mostly the same code, with a few
minor changes, along with a custom neural network [made by Albert Silver for the company
ChessBase](https://www.youtube.com/watch?v=1TabPJxO84o). This is not an official GitHub
repository for Fat Fritz 2 or for Stockfish, but instead an unofficial repository to document how
[Fat Fritz 2 is a ripoff of Stockfish](https://lichess.org/blog/YCvy7xMAACIA8007/fat-fritz-2-is-a-rip-off)
and make it freely available on GitHub to anyone who is curious.

The Stockfish derivative Fat Fritz 2 is not a complete chess program, and requires a
UCI-compatible graphical user interface (GUI) (e.g. XBoard with PolyGlot, Scid, Cute Chess,
eboard, Arena, Sigma Chess, Shredder, Chess Partner or Fritz) in order to be used comfortably.
Read the documentation for your GUI of choice for information about how to use this Stockfish
derivative with it.

The Stockfish engine features two evaluation functions for chess, the classical
evaluation based on handcrafted terms, and the NNUE evaluation based on efficiently
updatable neural networks. The classical evaluation runs efficiently on almost all
CPU architectures, while the NNUE evaluation benefits from the vector
intrinsics available on most CPUs (sse2, avx2, neon, or similar).

The NNUE is the only part modified in the Fat Fritz 2 derivative of Stockfish. Everything
else is the same as an original developer build of Stockfish, [commit
0266e702970640df693a8e572dd3cb9d227cdfc6](https://github.com/official-stockfish/Stockfish/commit/0266e702970640df693a8e572dd3cb9d227cdfc6),
"Fix static_assert", which ddobbelaere authored and vondele committed on Jan 11, 2021. The
many subsequent improvements to Stockfish since that date have not been incorporated into
Fat Fritz 2 at all, so it is now much weaker than current Stockfish. Fat Fritz 2 has 2
additional files added in the /src directory compared to the original Stockfish source
code: compile.sh and FatFritz2_v1.bin. There are also a few minor changes to a few other
files to accomodate the NNUE changes and rebrand it as Fat Fritz 2.

You can find the official Stockfish repository here on [GitHub](https://github.com/official-stockfish/Stockfish),
and the official Stockfish website at [stockfishchess.org](https://stockfishchess.org). The official Fat Fritz
website is at [chessbase.com](https://en.chessbase.com/products/fat-fritz). Fat Fritz 2 is very
controversial, and was the subject of a lawsuit by the Stockfish developers against ChessBase
[which they wrote about here](https://stockfishchess.org/blog/2021/our-lawsuit-against-chessbase/), but the
Stockfish developers and ChessBase reached a settlement
[which you can read about here](https://stockfishchess.org/blog/2022/chessbase-stockfish-agreement/).

Basically ChessBase violated the GNU GPL 3 and unethically used Stockfish's work without permission, charging money
for it, and not making the source code publicly available, and a lawsuit was necessary to force them into
compliance with the GNU GPL 3. They also made deceptive claims about Fat Fritz 2 being the strongest chess engine
and about its level of originality, when, as you can see by the commit history, hardly anything was changed.

Under the terms of this settlement, ChessBase has released Fat Fritz 2 for free as open source software under
the GNU GPL 3, available for download at [foss.chessbase.com](https://foss.chessbase.com/#Stockfish). This
unofficial GitHub repository for Fat Fritz 2 exists to make it more easily available and to provide a
wider array of binaries than ChessBase has on its official website, and so people can see how little was changed
in the source code for themselves. It is being distributed for free here in accordance with the GNU GPL 3.

It should be noted that the original version of Fat Fritz was a derivative of [Leela Chess Zero](https://lczero.org/),
not Stockfish, and the original Fat Fritz used a custom neural network that was derived from actual human games for the
training data for the Leela Chess Zero chess engine, rather than using self-play like the neural networks made by the
Leela Chess Zero project. This didn't actually make it any better than Leela Chess Zero, though.

Then Fat Fritz 2, based on Stockfish, used the self-play of the original Fat Fritz based on Leela Chess Zero for
development of its neural network. The neural networks for both versions of Fat Fritz were developed by Albert Silver
for ChessBase, while the software was developed by the open-source community (Leela Chess Zero developers for the
original Fat Fritz, and Stockfish developers for Fat Fritz 2). Development of the neural network for Fat Fritz 2 took
very little work, and was done in only 2 days. It is not as good as official Stockfish.

Please support the official releases of free and open-source chess engines like Stockfish, Leela Chess Zero, and others.
This repository only exists to document how Fat Fritz 2 was initially made in violation of the GNU GPL based on
minimal code changes, and to distribute its source code and binaries freely to anyone who is interested, in accordance
with the GNU GPL 3, so that people can obtain its source code or binaries for free without having to pay any money. Also,
please do not ask the authors of Stockfish or Leela Chess Zero to incorporate anything from Fat Fritz or Fat Fritz 2,
since those were just cheap ripoffs of their work and did not actually improve on it at all, but just existed for
ChessBase to make money off other people's work in violation of the GNU GPL.


## Files

This distribution of the Stockfish derivative Fat Fritz 2 consists of the following files:

  * Readme.md, the file you are currently reading.

  * Copying.txt, a text file containing the GNU General Public License version 3.

  * src, a subdirectory containing the full source code, including a Makefile
    that can be used to compile Stockfish on Unix-like systems.

  * the file FatFritz2_v1.bin, storing the neural network for the NNUE 
    evaluation. Unlike official Stockfish, Fat Fritz 2 does not embed
    this file in a binary distribution, but has it as a separate file.

Note: to use the NNUE evaluation, the additional data file with neural network parameters
needs to be available. This file is called FatFritz2_v1.bin and should come with any distribution
of the Fat Fritz 2 derivative of Stockfish.


## UCI options

Currently, Stockfish has the following UCI options:

  * #### Threads
    The number of CPU threads used for searching a position. For best performance, set
    this equal to the number of CPU cores available.

  * #### Hash
    The size of the hash table in MB. It is recommended to set Hash after setting Threads.

  * #### Ponder
    Let Stockfish ponder its next move while the opponent is thinking.

  * #### MultiPV
    Output the N best lines (principal variations, PVs) when searching.
    Leave at 1 for best performance.

  * #### Use NNUE
    Toggle between the NNUE and classical evaluation functions. If set to "true",
    the network parameters must be available to load from file (see also EvalFile),
    if they are not embedded in the binary.

  * #### EvalFile
    The name of the file of the NNUE evaluation parameters. Depending on the GUI the
    filename might have to include the full path to the folder/directory that contains the file.
    Other locations, such as the directory that contains the binary and the working directory,
    are also searched.

  * #### UCI_AnalyseMode
    An option handled by your GUI.

  * #### UCI_Chess960
    An option handled by your GUI. If true, Stockfish will play Chess960.

  * #### UCI_ShowWDL
    If enabled, show approximate WDL statistics as part of the engine output.
    These WDL numbers model expected game outcomes for a given evaluation and
    game ply for engine self-play at fishtest LTC conditions (60+0.6s per game).

  * #### UCI_LimitStrength
    Enable weaker play aiming for an Elo rating as set by UCI_Elo. This option overrides Skill Level.

  * #### UCI_Elo
    If enabled by UCI_LimitStrength, aim for an engine strength of the given Elo.
    This Elo rating has been calibrated at a time control of 60s+0.6s and anchored to CCRL 40/4.

  * #### Skill Level
    Lower the Skill Level in order to make Stockfish play weaker (see also UCI_LimitStrength).
    Internally, MultiPV is enabled, and with a certain probability depending on the Skill Level a
    weaker move will be played.

  * #### SyzygyPath
    Path to the folders/directories storing the Syzygy tablebase files. Multiple
    directories are to be separated by ";" on Windows and by ":" on Unix-based
    operating systems. Do not use spaces around the ";" or ":".

    Example: `C:\tablebases\wdl345;C:\tablebases\wdl6;D:\tablebases\dtz345;D:\tablebases\dtz6`

    It is recommended to store .rtbw files on an SSD. There is no loss in storing
    the .rtbz files on a regular HD. It is recommended to verify all md5 checksums
    of the downloaded tablebase files (`md5sum -c checksum.md5`) as corruption will
    lead to engine crashes.

  * #### SyzygyProbeDepth
    Minimum remaining search depth for which a position is probed. Set this option
    to a higher value to probe less aggressively if you experience too much slowdown
    (in terms of nps) due to TB probing.

  * #### Syzygy50MoveRule
    Disable to let fifty-move rule draws detected by Syzygy tablebase probes count
    as wins or losses. This is useful for ICCF correspondence games.

  * #### SyzygyProbeLimit
    Limit Syzygy tablebase probing to positions with at most this many pieces left
    (including kings and pawns).

  * #### Contempt
    A positive value for contempt favors middle game positions and avoids draws,
    effective for the classical evaluation only.

  * #### Analysis Contempt
    By default, contempt is set to prefer the side to move. Set this option to "White"
    or "Black" to analyse with contempt for that side, or "Off" to disable contempt.

  * #### Move Overhead
    Assume a time delay of x ms due to network and GUI overheads. This is useful to
    avoid losses on time in those cases.

  * #### Slow Mover
    Lower values will make Stockfish take less time in games, higher values will
    make it think longer.

  * #### nodestime
    Tells the engine to use nodes searched instead of wall time to account for
    elapsed time. Useful for engine testing.

  * #### Clear Hash
    Clear the hash table.

  * #### Debug Log File
    Write all communication to and from the engine into a text file.

## A note on classical and NNUE evaluation

Both approaches assign a value to a position that is used in alpha-beta (PVS) search
to find the best move. The classical evaluation computes this value as a function
of various chess concepts, handcrafted by experts, tested and tuned using fishtest.
The NNUE evaluation computes this value with a neural network based on basic
inputs (e.g. piece positions only). The network is optimized and trained
on the evaluations of millions of positions at moderate search depth.

The NNUE evaluation was first introduced in shogi, and ported to Stockfish afterward.
It can be evaluated efficiently on CPUs, and exploits the fact that only parts
of the neural network need to be updated after a typical chess move.
[The nodchip repository](https://github.com/nodchip/Stockfish) provides additional
tools to train and develop the NNUE networks.

On CPUs supporting modern vector instructions (avx2 and similar), the NNUE evaluation
results in stronger playing strength, even if the nodes per second computed by the engine
is somewhat lower (roughly 60% of nps is typical).

Note that the NNUE evaluation depends on the Stockfish binary and the network parameter
file (see EvalFile). Not every parameter file is compatible with a given Stockfish binary.
The default value of the EvalFile UCI option is the name of a network that is guaranteed
to be compatible with that binary. In the Fat Fritz 2 Stockfish derivative, some changes
have been made to the NNUE so it will only work with the Fat Fritz 2 NNUE and not a
standard Stockfish NNUE.

## What to expect from Syzygybases?

If the engine is searching a position that is not in the tablebases (e.g.
a position with 8 pieces), it will access the tablebases during the search.
If the engine reports a very large score (typically 153.xx), this means 
it has found a winning line into a tablebase position.

If the engine is given a position to search that is in the tablebases, it
will use the tablebases at the beginning of the search to preselect all
good moves, i.e. all moves that preserve the win or preserve the draw while
taking into account the 50-move rule.
It will then perform a search only on those moves. **The engine will not move
immediately**, unless there is only a single good move. **The engine likely
will not report a mate score, even if the position is known to be won.**

It is therefore clear that this behaviour is not identical to what one might
be used to with Nalimov tablebases. There are technical reasons for this
difference, the main technical reason being that Nalimov tablebases use the
DTM metric (distance-to-mate), while Syzygybases use a variation of the
DTZ metric (distance-to-zero, zero meaning any move that resets the 50-move
counter). This special metric is one of the reasons that Syzygybases are
more compact than Nalimov tablebases, while still storing all information
needed for optimal play and in addition being able to take into account
the 50-move rule.

## Large Pages

Stockfish supports large pages on Linux and Windows. Large pages make
the hash access more efficient, improving the engine speed, especially
on large hash sizes. Typical increases are 5..10% in terms of nodes per
second, but speed increases up to 30% have been measured. The support is
automatic. Stockfish attempts to use large pages when available and
will fall back to regular memory allocation when this is not the case.

### Support on Linux

Large page support on Linux is obtained by the Linux kernel
transparent huge pages functionality. Typically, transparent huge pages
are already enabled, and no configuration is needed.

### Support on Windows

The use of large pages requires "Lock Pages in Memory" privilege. See
[Enable the Lock Pages in Memory Option (Windows)](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/enable-the-lock-pages-in-memory-option-windows)
on how to enable this privilege, then run [RAMMap](https://docs.microsoft.com/en-us/sysinternals/downloads/rammap)
to double-check that large pages are used. We suggest that you reboot
your computer after you have enabled large pages, because long Windows
sessions suffer from memory fragmentation, which may prevent Stockfish
from getting large pages: a fresh session is better in this regard.

## Compiling Stockfish yourself from the sources

Stockfish has support for 32 or 64-bit CPUs, certain hardware
instructions, big-endian machines such as Power PC, and other platforms.

On Unix-like systems, it should be easy to compile Stockfish
directly from the source code with the included Makefile in the folder
`src`. In general it is recommended to run `make help` to see a list of make
targets with corresponding descriptions.

```
    cd src
    make help
    make net
    make build ARCH=x86-64-modern
```

When not using the Makefile to compile (for instance, with Microsoft MSVC) you
need to manually set/unset some switches in the compiler command line; see
file *types.h* for a quick reference.

When reporting an issue or a bug, please tell us which version and
compiler you used to create your executable. These informations can
be found by typing the following commands in a console:

```
    ./stockfish compiler
```

## Understanding the code base and participating in the project

Stockfish's improvement over the last couple of years has been a great
community effort. There are a few ways to help contribute to its growth.

### Donating hardware

Improving Stockfish requires a massive amount of testing. You can donate
your hardware resources by installing the [Fishtest Worker](https://github.com/glinscott/fishtest/wiki/Running-the-worker:-overview)
and view the current tests on [Fishtest](https://tests.stockfishchess.org/tests).

### Improving the code

If you want to help improve the code, there are several valuable resources:

* [In this wiki,](https://www.chessprogramming.org) many techniques used in
Stockfish are explained with a lot of background information.

* [The section on Stockfish](https://www.chessprogramming.org/Stockfish)
describes many features and techniques used by Stockfish. However, it is
generic rather than being focused on Stockfish's precise implementation.
Nevertheless, a helpful resource.

* The latest source can always be found on [GitHub](https://github.com/official-stockfish/Stockfish).
Discussions about Stockfish take place in the [FishCooking](https://groups.google.com/forum/#!forum/fishcooking)
group and engine testing is done on [Fishtest](https://tests.stockfishchess.org/tests).
If you want to help improve Stockfish, please read this [guideline](https://github.com/glinscott/fishtest/wiki/Creating-my-first-test)
first, where the basics of Stockfish development are explained.


## Terms of use

Stockfish is free, and distributed under the **GNU General Public License version 3**
(GPL v3). Essentially, this means you are free to do almost exactly
what you want with the program, including distributing it among your
friends, making it available for download from your website, selling
it (either by itself or as part of some bigger software package), or
using it as the starting point for a software project of your own.

The only real limitation is that whenever you distribute Stockfish in
some way, you must always include the full source code, or a pointer
to where the source code can be found. If you make any changes to the
source code, these changes must also be made available under the GPL.

For full details, read the copy of the GPL v3 found in the file named
*Copying.txt*.
