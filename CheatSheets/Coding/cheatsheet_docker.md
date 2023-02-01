## Build image
```
docker build -t <image_name> . 
```

## Run scripts after mounting test data to local folder
```
docker run -it -v <local_folder>:/data <image_name> bash
```

## Example Docker Images

Lots in [this folder](https://github.com/populationgenomics/images/tree/main/images).

* [R example](https://github.com/populationgenomics/images/blob/main/images/str-r/Dockerfile)
