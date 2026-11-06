# The Synaptics Hydra vector coprocessor

Hydra is a vector arithmetic accelerator that works as a coprocessor attached to
a small MCU in a small embedded chip.

Hydra was designed at [Synaptics, Inc.](https://www.synaptics.com), where it has appeared in a variety of
touch controller, touchscreen controller, and fingerprint sensing chips since 2012.
In Synaptics chips, Hydra is paired either with a commercial microcontroller core such as
SiFive's RISC-V E2 or E7, ARM Cortex-M, or Cadence/Tensilica's Xtensa,
or with Synaptics' own proprietary MCU, Chimera.

---

Until recently, Chimera and Hydra were proprietary technologies that were never described in public, even
though they have shipped billions of units and there is a good chance that you have Chimera and Hydra processors
right now inside your phone, car, or laptop. (Or soon, possibly in the fingertips of your own personal robot.)
As the market for Synaptics touch chips has broadened, and more and more
people are interested in programming Synaptics touch chips, we have decided to open up these architectures to the
general public.

Initially, the specifications and related documentation for Chimera and Hydra will appear in this github repository
and in Chimera's companion repository:

* https://github.com/synaptics-public/synaptics-chimera
* https://github.com/synaptics-public/synaptics-hydra

We hope over time to expand these repositories to include further materials, perhaps eventually including
the Chimera and Hydra cores themselves either under license or as open-source &mdash; but that will
have to wait for a future phase.

Chimera and Hydra are named after ancient Greek mythological creatures. The [Chimera](https://en.wikipedia.org/wiki/Chimera_%28mythology%29)
was a beast assembled from the parts of several animals; the Chimera CPU similarly draws from and combines the
computer architecture traditions of RISC, CISC, DSP, and MCUs. The [Hydra](https://en.wikipedia.org/wiki/Lernaean_Hydra)
was a serpent with many identical snakelike heads; the Hydra coprocessor likewise chews on many vector elements together.

<img src='doc/synaptics-chimera-image.png' alt='Chimera drawing' width='300'> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <img src='doc/synaptics-hydra-image.png' alt='Hydra drawing' width='300'>

<!-- Artwork is courtesy of ChatGPT Images. -->

---

The latest version, Hydra 4.2, has the following general properties:

* Hydra brings vector capabilities to very small embedded chips that cannot afford traditional vector facilities such as RISC-V's "V" extension or ARM's Helium, Neon, or SVE.
* Hydra works as an on-chip coprocessor operated by firmware running on a modest 32-bit host CPU such as RISC-V or Chimera.
* Vector data are located in the host CPU's main RAM; vector size is limited only by the size of the RAM.
* Hydra uses four DMA channels with interleaved banks of RAM to achieve up to 128 bits/cycle of sustained memory throughput.
* Vector operations range from simple vector arithmetic to advanced operations such as matrix multiplications, FIR convolutions, sorting and median filters, extended-precision arithmetic, cryptographic encryption and hashing, and neural networks.
* Addressing modes include linear, strided, packed, matrix, transposed matrix, circular, indexed, and pattern generation, as well as special modes to support FFTs and complex number arithmetic.
* Data types include 8-, 16-, and 32-bit integers and fixed-point numbers, IEEE standard single- and half-precision floating-point, BFLOAT16, and Posits (an alternative floating-point format that packs wide range and good precision into fewer bits). Vector data can be packed with _K_ bits per element for any _K_ &le; 32.
* Hydra is compact: Hydra 4.2 is 60K-110K gates depending on its configuration. (Like any processor, it grows somewhat larger when synthesized to very high clock speeds.)
* Hydra performs one 32-bit fused multiply-add or up to 4 byte-integer multiply-adds per cycle in its arithmetic operations; it achieves this sustained rate even in advanced operations such as large matrix multiplications and 2D convolutions.
* Hydra can perform vector operations one-by-one under firmware control, or autonomously under control of a stored program of vector instructions.

---

This repository is still in preparation, but it will shortly contain at least these primary Hydra documents:

* The _Hydra 4.2 User's Guide_, an MS Word (or PDF) document of ~800 pages.
* The _Hydra 4.2 Architecture Overview_ presentation, an MS PowerPoint (or PDF) deck of ~200 slides.

Also:

* Dave Gillespie's presentation at Embedded World 2026, which described how we used Hydra to accelerate a simple neural network in Synaptics touch screen controllers.

Questions, inquiries, and comments are always welcome!

Thank you,

Dave Gillespie  
Synaptics Fellow  
daveg@synaptics.com
