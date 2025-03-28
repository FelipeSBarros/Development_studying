# instalando
```
docker pull orfeotoolbox/otb
```
# Usando

Para usar o CLI, basta executar o docker image::

```
docker run -it orfeotoolbox/otb
```
If you need to process images, mount a volume with your local data:

```
docker run -it --rm -v /path/to/data:/data orfeotoolbox/otb:8.1.1 bash
```
