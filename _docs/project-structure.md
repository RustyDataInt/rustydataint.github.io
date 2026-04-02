---
title: Project Structure
has_children: false
nav_order: 20
---

## Project Structure

The MDI codebase is organized into modular GitHub repositories
that separate functions to allow users to access 
&ndash; and developers to work on &ndash; 
the tools most relevant to them.

{% include figure.html file="project-structure.png" %}

### Installation and Management Utilities

The MDI Manager is an R package that provides commands to 
`install()` pipelines and apps and `run()` the web interface. 
The concept is similar to the BiocManager utility of the 
[Bioconductor project](https://www.bioconductor.org/),
although users rarely load and run the MDI manager directly.

The MDI Installer/Command Line Interface (CLI) is a wrapper that makes 
it easier to run the manager utility. It also provides a streamlined, 
non-R installation for people who will only use Stage 1 pipelines on an HPC server. 

The MDI Desktop is an Electron app that helps users connect to HPC servers 
via SSH and to install and run both Stage 1 Pipelines and Stage 2 Apps, all
from a convenient desktop program. The Desktop is often the best way access 
MDI tools, whether locally or remotely.

- <https://github.com/MiDataInt/mdi> 
([documentation](/mdi))
- <https://github.com/MiDataInt/mdi-manager> 
([documentation](/mdi-manager))
- <https://github.com/MiDataInt/mdi-desktop-app> 
([documentation](/mdi-desktop-app))

### Frameworks

The MDI framework repositories help run Stage 1 Pipelines and Stage 2 Apps by 
providing code and functions that are common and useful across many tools. 
They are the building blocks that make it easy to quickly 
develop new tools. There are two separate frameworks, one for Stage 1 pipelines 
and one for Stage 2 apps. 

Most users will implicitly install the frameworks using the installer or desktop 
app and not think about them further.

For developers, the frameworks are maintained by the MDI as open-source projects 
you are welcome to help improve. 

- <https://github.com/MiDataInt/mdi-pipelines-framework> 
([documentation](/mdi-pipelines-framework))
- <https://github.com/MiDataInt/mdi-apps-framework> 
([documentation](/mdi-apps-framework))

### Tool Suites

The code that does the specific work of a pipeline or app is found in a 
tool suite repository. Anyone can develop a tools suite. We encourage you 
to make your suite repositories public as open-source code, which makes it 
easy to publish work performed with them. However, you can develop and use 
private suites if you provide a token that allows access to the repositories. 

A suite, i.e., repository, might hold only one pipeline or app, or combine 
related tools into a single suite as makes sense for your activities. For example, 
a research laboratory might combine its machine learning tools into a single suite.
Creating suites also makes it easy to share modular code between tools. 

It is easy to build your own tool suites using the following template repository, 
emulating the demo tool suite derived from it:

- <https://github.com/MiDataInt/mdi-suite-template> 
([documentation](/mdi-suite-template))
- <https://github.com/MiDataInt/demo-mdi-tools>

### Command Line Utility

End users run Stage 1 Pipelines using the `mdi` command line utility. 
This single wrapper utility provides a 
[unified method of executing and monitoring pipelines]({{ "/assets/images/screenshots/stage1-command-line.jpg" | relative_url }}). 
It is one of the many advantages of wrapping your pipeline in an MDI suite.

In remote usage modes, Stage 1 Pipelines can also be run in the 
[web interface's Pipeline Runner app]({{ "/assets/images/screenshots/pipeline-runner.jpg" | relative_url }}), 
which calls `mdi` on your behalf. 

### Documentation

The MDI helps developers maintain robust, standardized documentation for all 
project-associated code using GitHub features including README.md files and 
[GitHub Pages](https://pages.github.com/).
The following are the repositories for this documentation site,
our basic training tutorials, and the MDI 
[Jekyll](https://jekyllrb.com/)
documentation themes and templates. 
The latter are also built into the suite template, above.

- <https://github.com/MiDataInt/midataint.github.io.git>
- <https://github.com/MiDataInt/mdi-basic-training.git>
- <https://github.com/MiDataInt/mdi-documentation-template.git>
- <https://github.com/MiDataInt/just-the-docs-mdi.git>

### Public Server Support

The MDI runs equally well on many computer infrastructures.
The following repositories help you quickly create a publicly addressable 
MDI server installation using 
[Amazon Web Services](https://aws.amazon.com/) (AWS). 

- <https://github.com/MiDataInt/mdi-web-server.git>
- <https://github.com/MiDataInt/mdi-aws-ami.git>

Full public web server documentation is provided here:
- <https://midataint.github.io/mdi-aws-ami>

### End User Assistance

The recommended method for describing data to be analyzed
and other options for Stage 1 pipelines is to write YAML-format data
scripts, a.k.a. job files. A final simple 
template repository helps end users organize collections
of data scripts in their own git repositories and archive 
them using GitHub. 

- <https://github.com/MiDataInt/mdi-data-scripts-template>
