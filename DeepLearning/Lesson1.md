
# Some Toughts:
> "Neural networks don't require us to build features to predict something on machine learning algorithm. They build them for us!"


> "We don't give it features, we ask it to learn features."

_D. Zeiler and Rob Fergus: Each weight find different features. Like, one to identify diagonal adges;_

> Deep Learning means that we can take those features and combine them to create more advanced features.

> Regardless were you are at, the most important thing is to expriment.

## [DataBlock](https://docs.fast.ai/data.block.html)
High level API to quickly get your data in a `DataLoaders`;
Importante para trabalhar com diferentes tipos de dados.
Se trata de um tipo de nivel intermediário flexivel (para quase qualquer tipo de dado).
Por isso possui parâmetros que cobrem: 
* `block` (tipo de dados, tipo de output) - com isso o `fat.ai` define o melhor modelo a ser usado.
* `splitter`:  Define como criar um conjunto d dados para validação;
* `item+tfms`: Item `transforms` - `crop` ou `squish`

## [DataLoader](https://docs.fast.ai/data.core.html#dataloaders)
`DataLoader` alimenta o algoritmo de aprendizado com várias imagens ao mesmo tempo -> `batch`. 
Basic wrapper around several [`DataLoader`](https://docs.fast.ai/data.load.html#dataloader) (dls). 
`dls` contém iteradores dp pytorch que usa batch de amostras para treinamento e teste.

* `SegmentationDataLoader`
* `TabularDataLoader`
* `CollabDataLoaders`
## `learner()`
Combina **modelos** (redes neurais) que estaremos trabalhando, e os **dados** que usaremos para treinar o modelo. 
Recebe: `DataLoader` object, e  o modelo.
Possui como parâmetro `metrics`.
`rasnet18`
São poucos os tipos de modelo que servem para quase todas as aplicações.

[`Pytorch Image Models`](https://github.com/huggingface/pytorch-image-models)  (timm): A  maior coleção de visão computacional do mundo. E o [fast.ai](https://timm.fast.ai/) está integrado com tais modelos. 
### `finetune()` / `fit()` method
> "It takes those pre-trained wieghts downloaded from models and ajust them in a relly carefully way t teach the model the differences between your dataset and what it was trained for -> `finetuning`"

### `predict()` method

* `loss`: number that says how good were the results.