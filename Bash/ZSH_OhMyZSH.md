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

## Erros:
Se der erro no `poetry:

```bash
gedit ~/.zshrc
```

Adicione

```bash
export PATH="$HOME/.local/bin:{$PATH}”
```

Depois reinicie o terminal

```python
source ~/.zshrc
```