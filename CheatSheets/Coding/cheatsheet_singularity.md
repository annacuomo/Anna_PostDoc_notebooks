## Inspect info re: image

```bash
singularity inspect --deffile SAIGE-QTL.sif
```

shows you the code part of the recipe / definition file used to build the image.

```bash
singularity inspect --environment SAIGE-QTL.sif
```

same but for the environment (?).

```bash
singularity inspect /share/ScratchGeneral/anncuo/software/Demuxafy.sif
```

just shows you the version, e.g. for Demuxafy it's 2.1.0 here.

## Run Singularity on HPC

shows you the code part of the recipe / definition file used to build the image.

Usage specifically for GCP at [this link](https://github.com/annacuomo/Garvan_useful_commands/blob/main/Garvan_HPC/Setting_up_singularity.md), note that this is a private repo atm.

## Resources

* [Definition files docs](https://docs.sylabs.io/guides/latest/user-guide/definition_files.html)
