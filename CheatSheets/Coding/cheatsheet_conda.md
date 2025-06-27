# Conda

## export conda config file

```bash
conda env export > environment.yaml
```

## create env from config file

```bash
conda env create -f environment.yaml
```

## find envs location / names

`conda env list`

## conda on Garvan's HPC (Brenner)

https://github.com/annacuomo/Garvan_useful_commands/blob/main/Garvan_HPC/Setting_up_Conda.md

## create (python) environment and set up as kernel on notebook

as an example, installing scanpy

```bash
conda create -n scanpy python=3.6.3
conda activate scanpy
conda init bash
pip install scanpy
pip install notebook
pip install jupyterlab
conda install -c anaconda ipykernel
python -m ipykernel install --user --name=my_scanpy
```

## create R environment and set up as kernel on notebook

```bash
conda create --name r_env r-essentials r-base
conda activate r_env
pip install jupyterlab
conda install -n r_env r-irkernel
```

then, inside of R:

```R
install.packages("IRkernel")
IRkernel::installspec(name="ir36_native", displayname="R 3.6.0 (native)")
```
