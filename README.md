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
- [AAPG (Automated Assembly Program Generator)](#AAPG)
- [riscv-dv](#riscv-dv)
- [covered](#covered)
- [svlint](#svlint)
- [sv-parser](#sv-parser)
- [Surelog](#surelog-system-verilog-2017-pre-processor-parser)
- [rggen](#rggen) (Code generation tool for configuration and status registers)
- [EBMC / CBMC](#ebmc--cbmc) (Model checker for C/C++ and hardware designs)

**Frameworks:**

- [cocotb](#cocotb)
- [riscv-formal](#riscv-formal)
- [UVVM](#UVVM)
- [OSVVM](#OSVVM)
- [VUnit](#VUnit)
- [V3](#V3)

**Components / VIPs**

- [uvm_axi](#uvm_axi)
- [AXI Bus Formal VIP](#axi-bus-formal-vip)
- [AXI Bus Functional Model tvip-axi](#AXI-Bus-Functional-Model---tvip-axi)
- [APB Bus Functional Model tvip-apb](#APB-Bus-Functional-Model---tvip-apb)

**Guides:**

- [Dan Gisselquist Formal Verification Blogs](#Dan-Gisselquist-Formal-Verification-Blogs)

**Conferences:**

- [ORCONF](#ORCONF)
- [OSDA](#OSDA)
- [CHIPS Alliance Workshop on Open Source Design Verification](#CHIPS-Alliance-Workshop-on-Open-Source-Design-Verification)

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

## AAPG

*"Automated Assembly Program Generator (aapg) is a tool that is intended to generate random RISC-V programs to test RISC-V cores."*

From the [Shakti](https://gitlab.com/shaktiproject) RISC-V core project.
Acts as a way to generate random stimulus for a RISC-V core.
Output of the programs can then be checked between DUT and a GRM.

- Link: https://gitlab.com/shaktiproject/tools/aapg
- License: BSD 3-clause
- Written In: Python

## riscv-dv

Similar to [AAPG](#AAPG), but this time from Google. 
Generates randomised RISC-V programs which can 
then be run by the DUT and A GRM and checked for equivilence. 
It has knowledge of interesting features like page tables, CSR access and
trap/interrupt handling.
Can generate randomised instruction streams with features like loops
and function calls etc.

This project cannot be used with current free open source HDL simulators
since it relies on the object orientated parts of UVM. It is still a
useful piece of Verification IP though, and serves as a guide for other
similar projects.

- Link: https://github.com/google/riscv-dv
- License: Apache-2.0
- Written In: SystemVerilog + UVM

### covered

*"Covered is a Verilog code coverage analysis tool that can be useful for determining how well a diagnostic test suite is covering the design under test."* ... *"Covered reads in the Verilog design files and a VCD, LXT or FST formatted dumpfile from a diagnostic run and generates a database file called a Coverage Description Database (CDD) file"* ... "*Once a CDD file is created, the user can use Covered to generate various human-readable coverage reports in an ASCII format or use Covered's GUI to interactively look at coverage results*".

- Link: https://github.com/anders-code/verilog-covered
- License: GPL-2.0
- Written In: C

### svlint

An open source, MIT licensed SystemVerilog linting tool. Built on top of an open source [SystemVerilog parser](#sv-parser).

- Link: https://github.com/dalance/svlint
- License: MIT
- Written In: Rust

### sv-parser

An open source, MIT/Apache licensed SystemVerilog parser/ Useful for quickly building custom tools / checkers.

- Link: https://github.com/dalance/sv-parser
- License: MIT / Apache
- Written In: Rust

### Surelog: System Verilog 2017 Pre-processor, Parser

*"This project aims at providing a complete System Verilog 2017 front-end: 
a preprocessor, a parser, an elaborator for both design and testbench."* 

*"Linter, Simulator, Synthesis tool, Formal tools can use this front-end.
They either can be developed as plugins (linked with) or use this front-end
as an intermediate step of their compilation flows"*.

- Link: https://github.com/alainmarcel/Surelog
- License: Apache 2.0
- Written In: C++ with Python bindings.

### RgGen

"*RgGen is a code generation tool for ASIC/IP/FPGA/RTL engineers. It will
automatically generate soruce code related to configuration and status
registers (CSR), e.g. SytemVerilog RTL, UVM RAL model, Wiki documents, from
human readable register map specifications.*"

- Link: https://github.com/rggen/rggen
- License: MIT
- Written in: Ruby


### EBMC / CBMC

**EBMC:**

"*EBMC is a Model Checker for hardware designs. It includes both bounded and
unbounded analysis, i.e., it can both discover bugs and is also able to prove
the absence of bugs. It can read Netlists (ISCAS89 format), Verilog, System
Verilog and SMV files. Properties can be given in LTL or a fragment of System
Verilog Assertions.*"

- Link: http://www.cprover.org/ebmc/
- Licence: http://www.cprover.org/ebmc/download/license.txt
- Written in: _Unknown_.

Note: Only the binaries for EBMC can be downloaded, no source-code is
available.  It's included on this list because it is a powerful tool which
would otherwise not be available to the open hardware community.
For a completely free and open tool with similar capabilities,
look at [SymbiYosys](#Symbiyosys).

**CBMC:**

"*CBMC is a Bounded Model Checker for C and C++ programs.*"

"*Furthermore, it can check C and C++ for consistency with other languages,
such as Verilog. The verification is performed by unwinding the loops in the
program and passing the resulting equation to a decision procedure.*"

- Link: http://www.cprover.org/cbmc/
  - Source: https://github.com/diffblue/cbmc
- Licence: https://github.com/diffblue/cbmc/blob/develop/LICENSE
- Written in: C++.


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

There is also an accompanying library of user contributed VIPs: [UVVM_Community_VIPs](https://github.com/UVVM/UVVM_Community_VIPs).

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

### AXI Bus Formal VIP

A set of formal properties for checking for correct protocol behaviour in an AXI bus.
Used as part of a Wishbone-AXI bus bridge, but usable with any AXI bus.
There is a great blog post on it's use [here](https://zipcpu.com/formal/2018/12/28/axilite.html) from ZipCPU.
It works with SymbiYosys.

- Link: https://github.com/ZipCPU/wb2axip/blob/master/bench/formal/faxil_slave.v
- Written in: Verilog
- Write Testbenches In: Verilog
- License: None specified

### AXI Bus Functional Model - tvip-axi

Bus function model for AMBA AXI protocol.
Supports master and slave agents, AXI4 and AXI4-Lite protocols.
Configurable address/data/id widths.
Supports in/out-of-order responses, delayed responses and read interleaving.

- Link: https://github.com/taichi-ishitani/tvip-axi
- Written in: SystemVerilog and UVM
- License: Apache-2.0

### APB Bus Functional Model - tvip-apb

Bus function model for AMBA APB protocol

- Link: https://github.com/taichi-ishitani/tvip-apb
- Written in: SystemVerilog and UVM
- License: Apache-2.0


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

### CHIPS Alliance Workshop on Open Source Design Verification

*"The workshop invites contributions from industry, academia and hobbyists, either as talk or tutorial. Proposals should cover open source design simulation and verification, for example in the following categories (but not limited to):

    Open source simulation tools
    Open source design verification tools
    Open source rapid prototyping tools and methodologies
    Open source libraries for design verification
    Open source standards and methodologies for design verification
    Industry case studies of usage and integration of the aforementioned

Most importantly, your submitted proposal should cover the open source aspect."*

- Link: https://chipsalliance.org/workshops-meetings/
- Date: November 14-15, 2019
- Location: Munich, Germany
