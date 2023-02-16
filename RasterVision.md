![](https://docs.rastervision.io/en/stable/_images/raster-vision-logo-index.png)

**Raster Vision** é uma biblioteca e framework aberta para desenvolvedores Python desenvolverem modelos de visão computacional para imagens de satélite, fotografias aéreas, e imagens de drone. Possui suporte para [[DeepLearning_chip_Classificaction]] classificação de `chip`, detecção de objeto, e segmentação semantica usando PyTorch.

![][https://docs.rastervision.io/en/stable/_images/cv-tasks.png]
:warninig: Para o estudo, utilizei a versão docker do `raster-vision`. E para que se possa usá-lo com as funcionalidades de GPU, é necessário, primeiro, configurar o [[NVIDIA container -toolkit]] .

## Instalando Raster Vision usando Docker

Para poder seguir o [quick start](https://docs.rastervision.io/en/stable/framework/quickstart.html) , vamos usar a ferramenta em [[Docker]], conforme indicado [aqui](https://docs.rastervision.io/en/stable/setup/index.html#docker-images) .

```
docker pull quay.io/azavea/raster-vision:pytorch-latest rastervision
```

> é importante a informação da versão do pytorch a ser usada: `pytorch-latest`

### Configurações de pastas

É importante criar duas pastas:
1. Uma para ser a fonte dos arquivos de configuração e; 
2. Outro para os resultados gerados;

```
mkdir quickstart_code
mkdir quickstart_output
```
3. Definindo variáveis de ambiente com a informação da localização dessas pastas:
```
export RV_QUICKSTART_CODE_DIR=`pwd`/code
export RV_QUICKSTART_OUT_DIR=`pwd`/output
# mkdir -p ${RV_QUICKSTART_CODE_DIR} ${RV_QUICKSTART_OUT_DIR}
```

### Executando o container e acessando o `bash`

Para executar o docker com o `Raster Vision`, basta usar o comando a seguir:

```
docker run --rm -it \
    -v ${RV_QUICKSTART_CODE_DIR}:/opt/src/code  \
    -v ${RV_QUICKSTART_OUT_DIR}:/opt/data/output \
    quay.io/azavea/raster-vision:pytorch-latest /bin/bash
```

A flag `-v` monta um volume usando as variáveis de ambiente configuradas anteriormente, definindo-as para esse volume montado (`/opt/src/...`).

:warning: Caso seja necessário usar as funcionalidades dos processamentos usando GPU e, ao executar o comando anterior, o seguinte aviso for apresentado:

>WARNING: The NVIDIA Driver was not detected.  GPU functionality will not be available.
   Use the NVIDIA Container Toolkit to start this container with GPU support; see
   https://docs.nvidia.com/datacenter/cloud-native/ .

É que será necessário usar o [NVIDIA container tool kit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#setting-up-nvidia-container-toolkit) . Para um guia de instalação, ver nota [[NVIDIA container -toolkit]] .

Em seguida, basta rodar o seguinte código:

```
docker run --runtime=nvidia --rm -it \
    -v ${RV_QUICKSTART_CODE_DIR}:/opt/src/code  \
    -v ${RV_QUICKSTART_OUT_DIR}:/opt/data/output \
    quay.io/azavea/raster-vision:pytorch-latest /bin/bash
```

Percebam que, agora estamos com a flag `--runtime=nvidia`, indicando a necessidade de uso de GPU.

:warning: A definição dos caminhos às pastas como variáveis de ambiente não persistem após reinicialização do sistema.