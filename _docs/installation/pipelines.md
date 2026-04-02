---
title: Stage 1 Pipelines
parent: Installation
has_children: false
nav_order: 10
---

## Stage 1 Pipeline installation

All MDI tool suites can be deployed in one of two modes,
either as a single-suite or a multi-suite installation.
Instructions below will first set up the command line
interface (CLI) for either mode.

Once the CLI is installed, you may need to then build one or more pipeline
[Conda environments](https://docs.conda.io/en/latest/)
if either your HPC server or a tool suite does not offer
Singularity/Apptainer support.

Note that Stage 1 Pipeline installation only applies
to a Linux HPC server with bash shell support.

### Single-suite installation

Many tool suites are intended to be installed independently of other tool 
suites. This is easier since the MDI frameworks and tool suite are installed 
together as a unit, but you might end up with multiple MDI installations. 
Here, the installation sequence is:

1. clone the tool suite repository
2. run the suite's <code>install.sh</code> script

Details will be provided in the documentation of the tool suite you are 
using, but the pattern is:

```bash
git clone https://github.com/<git_user>/<tool_suite_name>.git
cd <tool_suite_name>
./install.sh 1
perl alias.pl <alias_name> # optional
```

### Multi-suite installation

For a less redundant installation, you can install and run many tool 
suites from one MDI installation. Here, the installation sequence is:

1. clone to MDI repository
2. run the MDI <code>install.sh</code> script
3. add tools suites to your installation

```bash
git clone https://github.com/MiDataInt/mdi.git
cd mdi
./install.sh 1
./mdi alias --alias mdi # optional; change the alias name if you'd like 
./mdi add --suite <git_user>/<tool_suite_name>
# etc.
```

Note that `mdi add` acts by editing file '.../mdi/config/suites.yml'.
You can also manually edit this and other config files.

## Obtain or build the required runtime environments

MDI pipelines use
[Conda environments](https://docs.conda.io/en/latest/)
to provide third-party program dependencies that are explicitly versioned 
controlled. There are two ways to obtain or install the environments 
required by a pipeline in an installed tool suite.

### Use Singularity/Apptainer (if supported)

If both your HPC server and the tool suite offer support for 
Singularity containers, also called Apptainers, there may
be nothing more to do - containers carrying the built environments
will be downloaded and used automatically.

If you need to run a command on your server to make the 
`singularity` command available (other than `module load singularity`,
which will be checked automatically), communicate that command to your
MDI installation by editing file '.../mdi/config/singularity.yml'.

### Build the environments locally

If you must or choose not to use containers, e.g., when developing
code, you should build the environments locally using the CLI:

```bash
# <mdi_alias_name> <pipeline> conda --create
mdi my_pipeline conda --help
mdi my_pipeline conda --create
```

## Install your developer-forks locally

The MDI encourages 'fork-and-pull' code development, wherein you 
fork repositories you need to edit to create "developer-forks".

To can easily install your developer forks locally in parallel 
to the definitive repositories using CLI command options:

```bash
# <mdi_alias_name> install --forks
mdi install --help
mdi install --forks
```

You will find the definitive and developer-forks repositories cloned
into sub-directories of '.../mdi/suites'. Using the developer flag
`-d` on CLI calls causes code to be read from developer-forks.
