
# Some toughts and text highlights:
> "Neural networks don't require us to build features to predict something on machine learning algorithm. They build them for us!"

> "We don't give it features, we ask it to learn features."

_D. Zeiler and Rob Fergus: Each weight find different features. Like, one to identify diagonal adges;_

> Deep Learning means that we can take those features and combine them to create more advanced features.

> Regardless were you are at, the most important thing is to expriment.

> The fact that neural networks are so flexible means that, in practice, they are often a suitable kind of model, and you can focus your effort on the process of training them—that is, of finding good weight assignments.

>One could imagine that you might need to find a new "mechanism" for automatically updating weights for every problem. ... This is called _stochastic gradient descent_ (SGD). 

>- The functional form of the _model_ is called its _architecture_ (but be careful—sometimes people use _model_ as a synonym of _architecture_, so this can get confusing).
>- The _weights_ are called _parameters_.
>- The _predictions_ are calculated from the _independent variable_, which is the _data_ not including the _labels_.
>- The _results_ of the model are called _predictions_.
>- The measure of _performance_ is called the _loss_.
>- The loss depends not only on the predictions, but also the correct _labels_ (also known as _targets_ or the _dependent variable_); e.g., "dog" or "cat."

> _overfitting_: (i.e., you have actually observed the validation accuracy getting worse during training)

> `epochs`: how many times to look at each image;

> [DeepLearning] model has learned to create feature detectors that look for corners, repeating lines, circles, and other simple patterns. These are built from the basic building blocks developed in the first layer.

> Growing the layer of networks it start being able to identify and match with higher-level semantic components, such as car wheels, text, and flower petals. Using these components, layers four and five can identify even higher-level concepts

> _Machine learning_ is a discipline where we define a program not by writing it entirely ourselves, but by learning from data. _Deep learning_ is a specialty within machine learning that uses _neural networks_ with multiple _layers_.

> training data is fully exposed, the validation data is less exposed, and test data is totally hidden.

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

* `ImageDataLoaders`
* `SegmentationDataLoader`
* `TabularDataLoader`
* `CollabDataLoaders`
## `learner()`
Combina **modelos** (redes neurais) que estaremos trabalhando, e os **dados** que usaremos para treinar o modelo. 
Recebe: `DataLoader` object, e  o modelo.
Possui como parâmetro `metrics`:
* The concept of a metric may remind you of _loss_, but there is an important distinction. The entire purpose of loss is to define a "measure of performance" that the training system can use to update weights automatically.
* `error_rate`, which is a function provided by fastai that does just what it says: tells you what percentage of images in the validation set are being classified incorrectly. Another common metric for classification is `accuracy` (which is just `1.0 - error_rate`). fastai provides many more, which will be discussed throughout this book.
`rasnet18`

São poucos os tipos de modelo que servem para quase todas as aplicações.

[`Pytorch Image Models`](https://github.com/huggingface/pytorch-image-models)  (timm): A  maior coleção de visão computacional do mundo. E o [fast.ai](https://timm.fast.ai/) está integrado com tais modelos. 

> When using a pretrained model, `vision_learner` will remove the last layer, since that is always specifically customized to the original training task (i.e. ImageNet dataset classification), and replace it with one or more new layers with randomized weights, of an appropriate size for the dataset you are working with. This last part of the model is known as the _head_.

>Using a pretrained model for a task different to what it was originally trained for is known as _transfer learning_.

### `finetune()` / `fit()` method
> "It takes those pre-trained wieghts downloaded from models and ajust them in a relly carefully way t teach the model the differences between your dataset and what it was trained for -> `finetuning`"

> Fine-tuning: A transfer learning technique where the parameters of a pretrained model are updated by training for additional epochs using a different task to that used for pretraining.
### `predict()` method

* `loss`: number that says how good were the results.

### `fit_one_cycle`
`fit_one_cycle`, the most commonly used method for training fastai models _from scratch_ (i.e. without transfer learning);