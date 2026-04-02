---
title: Config File Structures
has_children: false
nav_order: 50
---

## Config File Structures

Many MDI tasks are accomplished by writing YAML format configuration files.
This page summarizes their barebones structures for quick reference. 
Extended documentation is provided in the respective repositories.
- In "minimal examples", only required entries are shown with example values.
- In "complete structures", all possible entries are shown.
- Items in square brackets [] list allowed values.
- Items in angled brackets \<\> must be replaced with a value.
- Similar names in different places refer to the same type of thing, e.g., a pipeline.
- Job file templates are available by calling `mdi <pipelineName> template`.
- Tool templates are available in the [mdi-suite-template](/mdi-suite-template/overview).

## Stage 1 pipeline job files

As described in detail
[here](/mdi/docs/job_config_files.html),
end users write a job file, a.k.a. data script,
to declare the inputs, options, and output paths for their specific 
work to be done by a pipeline. Pipelines can 
be called with all options defined on the command line, 
but using job files is strongly recommended for organization and 
to create a permanent record.

### Minimal example

```yml
# my-data.yml - minimal example
---
pipeline: myPipeline
do:
    my-options:
        option1: /path/to/input55
    output:
        output-dir: /path/to/my/output
        data-name:  sample55
    job-manager:
        account:    myAccount # if submitting to a job scheduler
execute:
    - do
```

### Complete structure

```yml
# my-data.yml - complete structure
---
pipeline: <toolSuiteName>/<pipelineName>:[<semanticVersion>|<gitBranch>|latest] # only pipelineName is required
variables: # for accessing common values below, in bash style
    <VAR_NAME>: <value>
shared: # options set for all relevant actions
    <optionFamily>: 
        <optionName>: <value>
        <optionName>: 
            - <value> # multiple option values queue parallel jobs
            - $<VAR_NAME>
            - ${<VAR_NAME>}
    <externalSuiteName>//<optionFamily>: 
        <optionName>: <value>
<actionName>:
    <optionFamily>: # some options are pipeline specific
        <optionName>: <value>
        <optionName>: 
            - <value>
            - $<VAR_NAME>
            - ${<VAR_NAME>}
    <externalSuiteName>//<optionFamily>: 
        <optionName>: <value>
    output: # options here to the end apply to all pipelines
        output-dir:     <dirPath> # where to put output files
        data-name:      <value>
    push: # where to push data packages
        push-server:    <externalServerDomainName>
        push-dir:       <externalServerDirPath>
        push-user:      <externalServerUser>
        push-key:       <localKeyFilePath>
    resources: # how to run the job
        runtime:        <auto|conda|direct|container|singularity>
        n-cpu:          2
        n-gpu:          0
        ram-per-cpu:    4G
        tmp-dir:        <dirPath>
        tmp-dir-large:  <dirPath>
    job-manager:
        email:          <emailAddress>
        account:        <slurmAccount>
        time-limit:     24:00:00
        partition:      <partitionName>
        exclusive:      [true|false]
execute: # actions to execute when this job file is called
    - <actionName>
```

## Stage 1 pipeline configuration files

As described in detail
[here](/mdi-suite-template/docs/pipelines/pipeline_yml.html), 
a pipeline's stucture - including it's actions, options, and program dependencies - 
are defined by developers in file 'pipeline.yml'. 

### Minimal example

```yml
# pipelines/myPipeline/pipeline.yml - minimal example
---
pipeline:
    name: myPipeline
    description: "short text description"
actions:
    do: 
        condaFamilies:
            - base
            - my-packages    
        optionFamilies:
            - my-options
        description: "short text description"    
condaFamilies:
    my-packages:
        dependencies:
            - python
optionFamilies:
    my-options:
        options:
            option1: 
                type: string
                required: true
                default: null
                description: "short text description"   
```

### Complete structure

```yml
# pipelines/<pipelineName>/pipeline.yml - complete structure
---
pipeline: # pipeline metadata
    name: <pipelineName>
    description: "short text description"
    version: <semanticVersion>
suiteVersions: # external tool suite dependencies
    <externalSuiteName>: [<semanticVersion>|<gitBranch>|latest]
actions: # pipeline action definition
    _global: # entries applied to all actions 
        environment: <environmentName>
        condaFamilies: # dependencies of the conda environment
            - <condaFamilyName>       
        optionFamilies: # options exposed to users
            - <optionsFamilyName> 
    <actionName>: # an action defined by this tool suite
        order: 1
        # thread: <threadName>
        # environment: <environmentName>
        condaFamilies:
            - <condaFamilyName>      
        optionFamilies:
            - <optionsFamilyName> 
        resources:
            required:
                total-ram: 2G
            recommended: 
                n-cpu: 1
                ram-per-cpu: 2G
        job-manager:
            recommended:
                time-limit: 1:00:00
        description: "short text description"    
    <actionName>: # an action defined by an external tool suite
        order: 2
        module: <externalSuiteName>//<sharedModuleName>
        env-vars: # variables passed to configure the shared module
            <environmentVariableName>: <value>
condaFamilies: # conda family definitions
    <condaFamilyName>:
        channels:
            - <channelName>
        dependencies:
            - <packageName>
optionFamilies: # option family definitions   
    <optionsFamilyName>:
        options:
            <optionName>: 
                order: 1
                short: <singleCharacterOption>
                type: [string|integer|double|boolean]
                required: [true|false]
                default: [null|<defaultValue>]
                # directory:
                #     must-exist: [true|false]
                #     bind-mount: [true|false]
                description: "short text description"   
package: # configure the data package to write for use by associated apps
    <actionName>: 
        uploadType: <uploadTypeName>
        files:
            <fileTypeName>:
                file: <filePath>
container: # support for singularity containers via a registry
    supported: [true|false]
    registry:  <containerRegistryDomain>
    owner:     <registryUserName>
    installer: apt-get
```

## Stage 2 app configuration files

As described in detail
[here](/mdi-suite-template/shiny/apps/README.html), 
an app's top-level stucture - including it's data inputs and app step modules - 
are defined by developers in file 'config.yml'.

### Minimal example

```yml
# shiny/apps/myApp/config.yml - minimal example
---
name: myApp
description: "short text description"
uploadTypes:
    myPackageType: 
        contentFileTypes:
            myFileType:  
                required: true
appSteps: 
    upload:
        module: sourceFileUpload
    tables:
        module: makeTables
```

### Complete structure

```yml
# shiny/apps/<appName>/config.yml - complete structure
---
name: <appName> # app metadata
description: "short text description"
version: <semanticVersion>
suiteVersions: # external tool suite dependencies
    <externalSuiteName>: [<semanticVersion>|<gitBranch>|latest]
uploadTypes: # to match 'package' in pipelines
    <uploadTypeName>: 
        contentFileTypes:
            <fileTypeName>:  
                required: [true|false]
appSteps: 
    upload: # the first step of most apps
        module: sourceFileUpload
    <appStepName>:
        module: <appStepModule>
        options:
            <optionName>:
                # as required by appStepModule
```

## Stage 2 appStep module configuration files

An app step module is defined by its 'ui.R' and 'server.R' scripts
and in config file 'module.yml'.

### Minimal example

```yml
# modules/appSteps/makeTables/module.yml - minimal example
shortLabel:       "Make Tables" 
shortDescription: "Show various summary tables of the input data."
longLabel:        "Make summary tables"
types: 
    - tables
sourceTypes: 
    - upload
```

### Complete structure

```yml
# modules/appSteps/<appStepName>/module.yml - complete structure
shortLabel:       "Tab Label" 
shortDescription: "Short text description."
longLabel:        "App step header text"
types: 
    - <moduleType>
sourceTypes: 
    - <parentModuleType> # as declared by the source module's 'types'
packages: # R packages to be installed by 'install'
    R: 
        - <rPackageName>
    Bioconductor: 
        - <bioconductorPackageName>
settings: # settings exposed in the appStep's top-level settings icon
    <Settings_Tab_Name>:
        <Setting_Name>:
            type: selectInput
            choices:
                - <choiceName>
            value: <choiceName>   
        <Setting_Name>:
            type: radioButtons
            choices:
                - <choiceName>
            value: <choiceName>       
        <Setting_Name>:
            type: checkboxGroupInput
            choices:
                - <choiceName>
            value: <choiceName>   
        <Setting_Name>:
            type: checkboxInput
            value: [true|false] 
        <Setting_Name>:
            type: textInput
            value: <defaultValue> 
        <Setting_Name>:
            type: numericInput
            value: <defaultValue>    
            min:  <minValue>
            max:  <maxValue>
            step: <stepIncrement>
        <Setting_Name>:
            type:   fileInput
            accept: 
                - .<fileExtension>
```
