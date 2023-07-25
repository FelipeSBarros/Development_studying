[[Docker Orfeo Toolbox]]

# [Sem docker](https://www.orfeo-toolbox.org/CookBook/Installation.html)

Algumas dependencias:
```
sudo apt install libpython3.11
pip install numpy
sudo apt install libx11-6 libxext6 libxau6 libxxf86vm1 libxdmcp6 libdrm2
sudo apt install libexpat-dev   libexpat1-dev
```

Baixar o pacote do [site](https://www.orfeo-toolbox.org/download/).
O pacote é um arquivo ao extraído. Pode-se descompromi-lo com dois cliques ou com os seguintes comandos:

```
mv ./Downloads/OTB-8.1.1-Linux64.run ./
chmod +x OTB-8.1.1-Linux64.run
./OTB-8.1.1-Linux64.run
```

**Atenção**: A instalação realizada não deverá ter sua parta modificada. Deve-se descomprimir o arquivo no diretorio final.


Executando
```
./OTB-8.1.1-Linux64/monteverdi.sh
```
