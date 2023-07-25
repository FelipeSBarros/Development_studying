# instalando
```
docker pull orfeotoolbox/otb
```
# Usando

Para usar o CLI, basta executar o docker image::

`docker run -it orfeotoolbox/otb`

Caso queira usar a GUI, deve-se executar o docker imagem com os seguintes argumentos:

`docker run -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ --device=/dev/dri:/dev/dri orfeotoolbox/otb:8.1.1 monteverdi`
