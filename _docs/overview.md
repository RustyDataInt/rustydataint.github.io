---
title: "Michigan Data Interface"
has_children: false
nav_order: 0
---

<!-- please do not alter the next line -->
{% include mdi-project-overview.md %}  

These pages describe the MDI project overall. Links within lead you 
to documentation for specific components, e.g., how to get started
[writing your own tool suites]({{ "/docs/project-structure/#tool-suites" | relative_url }}).

### Screenshots

{% include screenshot.html 
   image="stage1-command-line.jpg" 
   caption="Stage 1 pipelines via command line, YAML-based tool and job definition" %}
{% include screenshot.html 
   image="pipeline-runner.jpg" 
   caption="Pipeline Runner web app running Stage 1 pipelines, remote HPC access" %}
{% include screenshot.html 
   image="stage2-apps.jpg" 
   caption="Stage 2 interactive apps via an access-controlled public web server" %}

### Video Overviews

{% include kaltura_video_thumbnail.html 
   thumbnail="mdi-what-is-it-min.jpg" 
   caption="The MDI - What is it?"   
   src="https://cdnapisec.kaltura.com/p/1038472/sp/103847200/embedIframeJs/uiconf_id/46145191/partner_id/1038472?iframeembed=true&playerId=kaltura_player&entry_id=1_yabesq04&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en_US&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;flashvars[hotspots.plugin]=1&amp;flashvars[Kaltura.addCrossoriginToIframe]=true&amp;&wid=1_g7wbn1db"
   width="608"
   height="402" %}

{% include kaltura_player.html %}

### Quick Start

Many times you will start using the MDI by installing a tool suite that uses it. Otherwise,
follow these instructions to clone and install the MDI **command line interface** on an HPC server:

- [Install the MDI CLI on an HPC server](/mdi/docs/installation)

Install the **MDI Desktop**, a program that connects to a server to run MDI apps from your Windows or Mac computer:

- [Install the MDI Desktop on your PC](/mdi-desktop-app/docs/installation)

Tool developers should start by copying our **repository suite template**
and following its [documentation](/mdi-suite-template):

- [Create a new tool suite from the template](https://github.com/MiDataInt/mdi-suite-template/generate)

See the following for a barebones summary of
the structure of job, pipeline, and app **configuration files**:

- [Barebones anatomy of configuration files](/docs/barebones)

<!-- 
### Live App Demo

To try out 
[this repository's](https://github.com/MiDataInt/demo-mdi-tools)
 **live demo app server**:

- go to: <https://mdi-demo.wilsonte-umich.io/>
- enter the access key: <code>mdi-demo</code>
- click <code>Load from Server</code> and select a data package or bookmark to load 
-->

### Guiding Principles

- effective, streamlined use of modern development tools
- optimal use of scalable computation resources
- rapid collaboration, code sharing, and community building
- interactive data analysis
- standardized implementation frameworks
- maximum developer flexibility

Our goal is to help you develop and share robust
data analysis tools, or to use tools developed by others,
without placing too many requirements on the process. 

### Basic Training for Developers

Please see our 
[Basic Training](https://midataint.github.io/mdi-basic-training) tutorials 
in the link below if you need help getting started with Git, the command line, 
job schedulers, R, Shiny, etc.

### Portability and Licensing

The MDI can be used by any laboratory or organization for any data analysis 
needs under the MIT license. A few instructions are specific to the 
University of Michigan environment but the codebase is generic.

<!-- please do not alter the next line -->
{% include mdi-project-documentation.md %}
