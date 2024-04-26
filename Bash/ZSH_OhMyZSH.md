## Instalando [ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

```bash
sudo apt install zsh
```
## Instalando [Oh My ZSH](https://ohmyz.sh/)

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Caso Oh My ZSH não esteja sendo iniciado automaticamente
[ver](https://github.com/ohmyzsh/ohmyzsh/issues/6112#issuecomment-463644808)**.

## Instalando [Powerline Fonts](https://github.com/powerline/fonts)

```bash
sudo apt-get install fonts-powerline
```

## Erros e solução de problemas:

## Se der erro no `poetry:

```bash
gedit ~/.zshrc
```

Adicione

```bash
export PATH="$HOME/.local/bin:{$PATH}"
```

Depois reinicie o terminal

```python
source ~/.zshrc
```

### Erro no `pip`

[python pip issues](https://www.golinuxcloud.com/zsh-command-not-found-pip/)

## [Plugins](https://github.com/unixorn/awesome-zsh-plugins)

* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
**Installing:**
`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`

* [git](https://kapeli.com/cheat_sheets/Oh-My-Zsh_Git.docset/Contents/Resources/Documents/index)

**.zshrc:**

```
plugins=(git
	zsh-autosuggestions)
```
