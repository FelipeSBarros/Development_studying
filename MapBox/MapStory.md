# Soja em Terras Indígenas

Estudando o [MapBox Story Telling](https://www.mapbox.com/solutions/interactive-storytelling) para comunicar melhor os resultados das análises espaciais. Esse estudo está recriando a apresentação feita pelo [OJoio E O Trigo](https://ojoioeotrigo.com.br) na reportagem das [lavouras de Soja](https://ojoioeotrigo.com.br/2023/07/mato-grosso-tem-lavoura-mecanizada-dentro-de-terras-indigenas/).

## Tutoriais e materiais usados
- [Tutorial do template](https://github.com/mapbox/storytelling)
* [Tutorial MapBOX](https://labs.mapbox.com/education/impact-tools/interactive-storytelling/)
* [live coding](https://www.mapbox.com/webinars/storytelling-template-live-demo)
* [10 - Setting up a Story Map with Mapbox Storytelling](https://pointsunknown.nyc/web%20mapping/mapbox/2021/07/20/11A_MapboxStorytelling.html)
* [MapBox helper](https://labs.mapbox.com/location-helper/#8.21/-14.018/-58.689/0/35)

## Resumo
Esse repo é um modelo desenvolvido para acelerar a criação de um _"scrollytelling" map story_. O texto e mapa são quebrados em sessões (`chapters`), cada uma ancorada (_hooked_) a um ponto em particular do mapa. O resultado são arquivos de _HTML_ e _JavaScript_. Esses arquivos podem ser hospedados em qualquer serviço de hopedagem, sem a necessidade de nenhuma programação ou configuração extra. 

Atenção: _embedding_ os dados de saida como um _iFrame_ em outra página não produzirão o resultado esperado. **The scroll-driven interface requires the full page.**

Para ir além, será necessário estar familiarizado com a customização de camadas com o [MapBox Studio](https://studio.mapbox.com/). 

Para configurar e publicar o seu MapStory, será necessário:

- A Mapbox [access token](https://docs.mapbox.com/help/glossary/access-token). Sign up for a free account at [mapbox.com](https://www.mapbox.com/signup/) to get one.  
- Algum sistema de hospedagem, tipo githubpages ou netfly;
- Atenção aos detalhes. **Familiariade com JSON é recomendada.**
- Para adicionar dados aos projeto é importante subí-los ao _MapBox_, exportá-lo como [tileset]() e posteriormente, criar um [style]() com todas as camadas a serem usadas. A gestão de visualização da camada será feita feito [`config.js`](#config.js).

O modelo não depende de nenhum _framework_ CSS específico. Há alguns estilos básicos no `head` do arquivo HTML que podem ser mudados. Sinta-se à vontade em adaptar-los.

## Clonando repo
```
git clone git@github.com:mapbox/storytelling.git ./MapBox_StoryMap
```

## O `config.js`
O arquivos `config.js`, que stá na pasta `src`, é onde estará as principais informações do que é apresentado: Título, subtítulo, qual estulo do mapbox se está usando, bem como define cada `chapters` e estabelece as camadas a serem apresentadas.

### Alterando as configurações do `config.js`
No repositório local, onde fizemos o clone do projeto, temos que fazer uma cópia do `config.js.template`, alterando seu nome para `config.js`, e o abra na sua IDE.

É nele que podemos definir alguns elementos básicos, como o estilo do mapa base, informar o `token` da MapBox...

#### Steps

1. **Definir o estilo do mapa base**: veja as possibilidades [aqui](https://docs.mapbox.com/api/maps/#styles](https://docs.mapbox.com/api/maps/#styles) ou use o seu próprio estilo a partir do MapBox Studio.
2. **Inserir o Mapbox access token.** Uma boa prática é criar um `token` de acesso apra cada mapa. Dessa forma pose-de identificar o fluxo de acesso de cada um deles.
3. **Defina se quer ou não apresentar um marcados (marker)** ao centro de cada mapa de localização. Caso esteja trabalhando com marcadores, pode-se alterar a cor pela propriedade `markerColor`. 
4. **Escolha um tema para o texto da história**. Pode ser `light` ou `dark`.
5. **Defina como o texto deve ser apresentado sobre o mapa**. As opções são: `center`, `left`, `right`, and `full`.

Exemplo `config.js`:
```
{
    style: 'mapbox://styles/mapbox/streets-v11',
    accessToken: 'YOUR_ACCESS_TOKEN',
    showMarkers: true,
    markerColor: '#3FB1CE',
    theme: 'light',
    use3dTerrain: false,
    title: 'The Title Text of this Story',
    subtitle: 'A descriptive and interesting subtitle to draw in the reader',
    byline: 'By a Digital Storyteller',
    footer: 'Source: source citations, etc.',
    chapters: [
        {
```
6. **adicione quantos `chapters` forem necessários.** Basta serpará-los com `,` cada seção e o final sem vírgula.  
Exemplo de um `chapter`:

```
{
            id: 'slug-style-id',
            alignment: 'left',
            hidden: false,
            title: 'Display Title',
            image: './path/to/image/source.png',
            description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.',
            location: {
                center: [-122.418398, 37.759483],
                zoom: 8.5,
                pitch: 60,
                bearing: 0
            },
            mapAnimation: 'flyTo',
            rotateAnimation: false,
            callback: '',
            onChapterEnter: [],
            onChapterExit: []
        },
```

7. **Preencha as seções como necessário.** Atribua um nome único em `id`. Essa será o ***div id**. Portanto, evite usar espaço. O `title`, `description` são opcionais. A propriedade `description` suporta tags HTML. Caso tenha alguma imagem a ser inserida nessa seção da estoria, adicione o caminho até ela na propriedade  `image`.
8. Para as propriedades de `location`, pode-se usar o `helper.html` para ajudar nessa determinação. essa ferramenta apresenta as configuraçĩes de localização do mapa apresentado na tela.
9. Repita até ter terminado   
10. Abra o `index.html`. Voila!

## MapBox Studio

### Adicionando label
[Veja tutorial](https://www.mapbox.com/blog/labels-in-studio#:~:text=Step%201%20%E2%80%94%20Go%20to%20%E2%80%9CDatasets,be%20placed%20and%20its%20shape.)

## Dados

Para subir dados precisei usar o [MapBox CLI](https://github.com/mapbox/mapbox-cli-py#datasets-list):

``
```
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install mapboxcli
```
