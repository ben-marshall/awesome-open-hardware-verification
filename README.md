# Open Hardware Verification

*A curated List of Free and Open Source hardware verification tools and frameworks.*

The aim here is to curate a (mostly) comprehensive list of available tools for verifying
the functional correctness of Free and Open Source Hardware designs. The list can
include:
- [Tools](#Tools) which contain or implement verification related functionality
- [Testbench Frameworks](#Frameworks) which make writing testbenches easier
- [Verification Guides](#Guides) and blog posts on how to actually go about verifying a hardware design
- [Conferences](#Conferences) where new work on open source hardware verification is talked about

Pull requests and submissions are encouraged!

**Some Rules:**

This list focuses on *Verification* and not *design*. While there are lots of cool new
languages and frameworks aimed at making hardware design easier (or at least, *not Verilog/VHDL*),
verification can sometimes get left out in the cold.

While some new design tools/languages claim that "our new design tool `X` makes verification
easier because it is written in high level language `Y`", it can often be much harder to find
evidence of this in terms of re-usable verification IP/frameworks/methods which are written
in "new language/tool `Y`". It might seem mean, but being a new design language which 
*theoretically* makes verification easier is not enough to merit inclusion on this list. What's
needed is *practical* demonstration of making verification easier. This can be through libraries or
IP which use "new language/tool `Y`", or in depth tutorials which explain how to use it for proper
design verification.

If you're after hardware *design* tools, these awesome lists are a good place to start:
- [awesome-hdl](https://github.com/drom/awesome-hdl)

Further, entries in this list should not only be open source themselves, but *be usable* by
people developing open source hardware using open source tools. For example, if company `X`
releases a set of re-usable verification components written using
[UVM](https://www.accellera.org/downloads/standards/uvm)
and SystemVerilog, is there an Free and Open Source SystemVerilog implementation which can make
use of them?

## Contents

**Tools:**

- [Symbiyosys](#Symbiyosys)
- [Verilator](#Verilator)
- [LibreCores CI](#LibreCores-CI)

**Frameworks:**

- [cocotb](#cocotb)
- [riscv-formal](#riscv-formal)
- [UVVM](#UVVM)
- [OSVVM](#OSVVM)
- [VUnit](#VUnit)
- [V3](#V3)

**Components / VIPs**

- [uvm_axi](#uvm_axi)

**Guides:**

- [Dan Gisselquist Formal Verification Blogs](#Dan-Gisselquist-Formal-Verification-Blogs)

**Conferences:**

- [ORCONF](#ORCONF)
- [OSDA](#OSDA)

---

## Tools:

### SymbiYosys

*"SymbiYosis a front-end driver program for Yosys-based formal hardware
verification flows. SymbiYosys provides flows for the following formal tasks:
Bounded verification of safety properties (assertions),
Unbounded verification of safety properties,
Generation of test benches from cover statements,
Verification of liveness properties"*

SymbiYosys requires [Yosys](https://github.com/YosysHQ/yosys) (an open
source synthesis tool) and one or more formal reasoning engines (listed
[here](https://symbiyosys.readthedocs.io/en/latest/quickstart.html#prerequisites)to work.

- Written In: Python
- Write Assertions In: Verilog/SystemVerilog Assertions (SVA)
- Supports: Formal verification of correctness properties.
- Link: https://symbiyosys.readthedocs.io/en/latest/

### Verilator

Verilator is  "the fastest free Verilog HDL simulator". From a verification
perspective it supports *line coverage*, *signal toggle coverage* and limited
specification of *functional coverage* using SystemVerilog Assertions.
It also allows one to write testbenches in C++ or SystemC.

- Written In: C++
- Write testbenches in: C++/SystemC
- Supports: Design simuation, *Coverage collection from simulations*.
- Link: https://www.veripool.org/projects/verilator/wiki/Intro

### LibreCores CI

*"LibreCores CI is a service, which provides Continuous Integration of projects being hosted on LibreCores. The objective of the service is to improve the contributor experience and to increase trust to projects by providing automated testing and health metrics of the projects."*

- Currently under development at the time of writing (Dec 2018)
- Aims to allow automation of testing for hardware designs. Think "Travis for hardware".
- Link: https://www.librecores.org/static/librecores-ci

## Frameworks:

### Cocotb
*"cocotb is a coroutine based cosimulation library for writing VHDL and Verilog testbenches in Python."*

- Licence: [Revised BSD License](https://github.com/potentialventures/cocotb/blob/master/LICENSE)
- Implemented in: Python
- Write Testbeches In: Python
- Link: https://github.com/potentialventures/cocotb

### riscv-formal

A re-usable formal verification framework for RISC-V CPU designs.
Uses the [Yosys/SymbiYosys](#SymbiYosys) tools.

- License: [ISC](https://github.com/SymbioticEDA/riscv-formal/blob/master/COPYING)
- Written In: Verilog
- Link: https://github.com/SymbioticEDA/riscv-formal

### UVVM

*"Open Source VHDL Verification Library and Methodology - for very efficient VHDL verification of FPGA and ASIC - resulting also in a significant quality improvement"*

- License: [MIT](https://github.com/UVVM/UVVM/blob/master/LICENSE)
- Written In: VHDL
- Write Testbenches In: VHDL
- Supports: [a bunch of stuff](https://github.com/UVVM/UVVM#main-features)
- Link: https://github.com/UVVM/UVVM

### OSVVM

*"Open Source VHDL Verification Methodology (OSVVM) provides an ASIC level VHDL verification methodology that is simple enough to use even on small FPGA projects. OSVVM offers the same capabilities as those based on other verification languages:"*

The GitHub organisation includes some AXI4 [Verification IP](https://github.com/OSVVM/VerificationIP)

- License: ?
- Written In: VHDL
- Supports: Constrained Random Test Generation, Functional Coverage Collection, [and more](https://osvvm.org/about-os-vvm)
- Link: https://osvvm.org/
- GitHub: https://github.com/OSVVM/OSVVM

### VUnit

*"VUnit is an open source unit testing framework for VHDL/SystemVerilog \[...\] It features the functionality needed to realize continuous and automated testing of your HDL code. VUnit doesn’t replace but rather complements traditional testing methodologies by supporting a “test early and often” approach through automation."*

Based partially on [OSVVM](#OSVVM)

- Written In: VHDL/Python
- Write Testbenches In: VHDL/System Verilog
- License: [Mozilla Public License, v. 2.0.](https://github.com/VUnit/vunit/blob/master/LICENSE.txt) baring OSVVM components.
- Link: https://vunit.github.io/index.html

### V3

*"V3 is a new and extensible framework for hardware verification and debugging researches on both Boolean-level and word-level designs. It is a powerful tool for users and an elaborate framework for developers as well."*

Academic project, looks unmaintained since 2014.

- Written In: C++
- Write Testbenches In: Unclear?
- License: [Non-commercial](https://github.com/chengyinwu/V3/blob/master/COPYING)
- Supports: formal methods based approaches using AGIER / SAT Solving over verilog input files. Not entirely clear how one specifies correctness properties.
- Link: https://github.com/chengyinwu/V3

## Components / VIPs

### uvm_axi

A bus functional model for ARM's AXI bus protocol. Looks like it has been written as a standard UVM Verification Package.
Being written in SystemVerilog (using all of its object orientated, behavioural modelling features) makes it hard
to re-use with the current set of FOSS simulators. It is still a good example of re-usable verification IP.

Last commit in 2013, so likely un-maintained.

- Link: https://github.com/funningboy/uvm_axi
- Written in: System Verilog
- Write Testbenches In: System Verilog
- License: GNU Lesser General Public License

## Guides:

### Dan Gisselquist Formal Verification Blogs

A set of posts on experiences using [Symbiyosys/Yosys](#Symbiyosys) for formally verifying a CPU design.
Includes lots of useful insights and guides for specific and general use cases.

- Link: https://zipcpu.com/formal/formal.html

## Conferences:

### ORCONF

*"ORConf is an annual conference for open source digital, semiconductor and embedded systems designers and users. Each year attendees are treated to an ever-impressive array of presentations from all corners of the open source hardware space."*

- Link: https://orconf.org/

### OSDA

*"Workshop on Open Source Design Automation (OSDA)"*

*"This one-day workshop aims to bring together industrial, academic, and hobbyist actors to explore, disseminate, and network over ongoing efforts for open design automation, with a view to enabling unfettered research and development, improving EDA quality, and lowering the barriers and risks to entry for industry. These aims are particularly poignant due to the recent efforts across the European Union (and beyond) that mandate 'open access' for publicly funded research to both published manuscripts as well as any code necessary for reproducing its conclusions."*

- Longer Description: https://osda.gitlab.io/motivation.html
- Link: https://osda.gitlab.io/
