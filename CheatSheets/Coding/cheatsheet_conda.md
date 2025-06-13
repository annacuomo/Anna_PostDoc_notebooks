# Conda

## export conda config file

```bash
conda env export > environment.yaml
```

## create env from config file

```bash
conda env create -f environment.yaml
```

## Conda on HPC (Brenner)

https://github.com/annacuomo/Garvan_useful_commands/blob/main/Garvan_HPC/Setting_up_Conda.md

## create environment and set up on notebook

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

## find envs location / names

`conda env list`
