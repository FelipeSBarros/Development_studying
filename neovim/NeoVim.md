Segundo [repositório](https://github.com/neovim/neovim/wiki/Installing-Neovim#linux):

```
# faz download
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage

# permite execução
chmod u+x nvim.appimage

#executa
./nvim.appimage
```

Adicionando alias ao [[ZSH_OhMyZSH]]:

```
alias nvim=~/nvim.appimage
```

### Adicionando `pynvim`
A biblioteca pynvim é necessária para o Neovim conseguir utilizar o Python da forma que ele precisa. Para instalar a biblioteca pynvim, use o comando:

```
pip install pynvim
```

## Arquivo de configuração

Quando instalamos o Vim e o Neovim, temos que criar os arquivos de configuração. Os arquivos **não são criados automaticamente**, então é necessário criá-los manualmente nas pastas corretas.

No Linux temos que colocar em `~/.config/nvim/init.vim`. Temos então que criar uma pasta chamada **_nvim_** na pasta _~/.config_ e dentro dela criar um arquivo chamado **_init.vim_**.
`~/.config/nvim/init.vim`

### Configurações globais

A primeira coisa a se fazer é realizar as configurações globais.
Seguindo a configuração básica [desse tutorial](https://www.manualdocodigo.com.br/vim-basico/#:~:text=Para%20o%20Neovim%20%C3%A9%20poss%C3%ADvel,que%20possue%20bem%20mais%20recursos.):
```
" Global Sets """""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
syntax on            " Enable syntax highlight
set nu               " Enable line numbers
set tabstop=4        " Show existing tab with 4 spaces width

...

filetype on          " Detect and set the filetype option and trigger the FileType Event
filetype plugin on   " Load the plugin file for the file type, if any
filetype indent on   " Load the indent file for the file type, if any
```

## Plugings (Plug)

Vamos usar o [Plug](https://github.com/junegunn/vim-plug) para neovim. Outra possibilidade é usar o `packer`.
Instalando Plug:
```
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```
Tendo instalado o Plug, devemos adicionar ao início de `init.vim`, o espaço para carregar os pugins:
```
call plug#begin()
" Plugins aqui
call plug#end()
```

### Temas
* [Github topic](https://github.com/topics/neovim-theme) com várias possibilidades;
* [sonokai](https://github.com/sainnhe/sonokai)

```
call plug#begin()
Plug 'sainnhe/sonokai'
call plug#end()
```
Reinicie o vim/neovim e rode o comando _PlugInstall_ para que o Sonokai seja instalado. Esse padrão se aplica para todos os outros plugins.

Acionando e configurando o tema. Neste caso, vamos configurar para usar o `andromeda`, e adicionar algumas opções:
```
" Themes """"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
if exists('+termguicolors')
  let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
  let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
  set termguicolors
endif

let g:sonokai_style = 'andromeda'
let g:sonokai_enable_italic = 1
let g:sonokai_disable_italic_comment = 0
let g:sonokai_diagnostic_line_highlight = 1
let g:sonokai_current_word = 'bold'
colorscheme sonokai
```

### Airline
[Airline](https://github.com/vim-airline/vim-airline) adiciona uma barra na parte de baixo do nvim com informações úteis;

Para instalar, basta adicionar aos plugins, atualuzar e instalar.:

```
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

### highlight de sintaxe
O Polyglot adiciona syntax highlighting pra várias linguagens. Basta adiciona o plugin:

`Plug 'sheerun/vim-polyglot'`

### nerdtree
Com o [NerdTree](- [https://github.com/preservim/nerdtree](https://github.com/preservim/nerdtree)) podemos manipular e navegar pelas pastas e arquivos, de forma facilitada. 
`Plug 'preservim/nerdtree`

o site do NerdTree tem muitos exemplos de configurações e autocmds disponíveis. 
Com o seguinte remap, poderemos usar `Ctrl+a` para abrir e fechar o painel.

`nmap <C-a> :NERDTreeToggle<CR>`

Podemos adicionar também atalhos para navegar pelos paineis:
```
" Shortcuts for split navigation
map <C-h> <C-w>h
map <C-j> <C-w>j
map <C-k> <C-w>k
map <C-l> <C-w>l
```

### FUZZY FINDER

O [Telescope](https://github.com/nvim-telescope/telescope.nvim) é um fuzzy finder, que serve para buscar arquivos e strings dentro do projeto.

```
Plug 'nvim-lua/plenary.nvim'
Plug 'nvim-telescope/telescope.nvim'
```
É preciso instalar o [`ripgrep`](https://github.com/BurntSushi/ripgrep) e o [`fd`](https://github.com/sharkdp/fd), para conseguirmos fazer as buscas por palavras. 
