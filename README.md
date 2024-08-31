#Dotfile

##Aplicativos instalados

**Lazygit**

Uma interface de terminal simples para comandos git

`brew install jesseduffield/lazygit/lazygit`



![commit_and_push-compressed](/home/edius/Projetos/dotfile/imagens/commit_and_push-compressed.gif)

Como usar:

`lazygit`

**pfetch-rs**

Informação do sistema escrita em Rust

`brew install pfetch-rs`

Como usar:

`pfetch`

**Nerd-fonts**

Nerd Fonts é um projeto que corrige fontes direcionadas a desenvolvedores com um alto número de glifos (ícones). Especificamente para adicionar um alto número de glifos extras de 'fontes icônicas' populares, como Font Awesome, Devicons, Octicons e outras.

```shell
cd ~/.local/share/fonts && curl -fLO https://github.com/ryanoasis/nerd-fonts/raw/HEAD/patched-fonts/DroidSansMono/DroidSansMNerdFont-Regular.otf
```

**ripgrep (rg)**

ripgrep é uma ferramenta de pesquisa orientada a linhas que busca recursivamente a corrente diretório para um padrão regex. Por padrão, o ripgrep respeitará as regras do gitignore e automaticamente pular arquivos ocultos/diretórios e arquivos binários. (Para desativar toda a filtragem automática por padrão, use `rg -uuu`.) ripgrep tem primeira classe suporte em Windows, macOS e Linux.

`brew install ripgrep`

**fd**

`fd` é um programa para encontrar entradas em seu sistema de arquivos. É uma alternativa simples, rápida e fácil de usar para [`find`](https://www.gnu.org/software/findutils/). 

![screencast](/home/edius/Projetos/dotfile/imagens/screencast.svg)

`apt-get install fd-find`

Note que o binário é chamado `fdfind` como o nome binário `fd` já é usado por outro pacote. Recomenda-se que, após a instalação, você adicione um link para `fd` executando o comando `ln -s $(which fdfind) ~/.local/bin/fd`, para usar `fd` da mesma forma que nesta documentação. Certifique-se de que `$HOME/.local/bin` está em seu `$PATH`.

**lazy.nvim**

Existem várias maneiras de instalar **preguiçoso.nvim**. O **Configuração Estruturada** é a maneira recomendada, mas você também pode usar o **Configuração de Arquivo Único** se você preferir manter tudo em seu `init.lua`.

> No que se segue `~/.config/nvim` é o seu diretório de configuração Neovim. No Windows, isso geralmente acontece `~\AppData\Local\nvim`. Para saber o caminho correto para o seu sistema, execute `:echo stdpath('config')`.

```bash
nano ~/.config/nvim/init.lua
```

```lua
require("config.lazy")
```

```bash
nano ~/.config/nvim/lua/config/lazy.lua
```

```lua
-- Bootstrap lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  local lazyrepo = "https://github.com/folke/lazy.nvim.git"
  local out = vim.fn.system({ "git", "clone", "--filter=blob:none", "--branch=stable", lazyrepo, lazypath })
  if vim.v.shell_error ~= 0 then
    vim.api.nvim_echo({
      { "Failed to clone lazy.nvim:\n", "ErrorMsg" },
      { out, "WarningMsg" },
      { "\nPress any key to exit..." },
    }, true, {})
    vim.fn.getchar()
    os.exit(1)
  end
end
vim.opt.rtp:prepend(lazypath)

-- Make sure to setup `mapleader` and `maplocalleader` before
-- loading lazy.nvim so that mappings are correct.
-- This is also a good place to setup other settings (vim.opt)
vim.g.mapleader = " "
vim.g.maplocalleader = "\\"

-- Setup lazy.nvim
require("lazy").setup({
  spec = {
    -- import your plugins
    { import = "plugins" },
  },
  -- Configure any other settings here. See the documentation for more details.
  -- colorscheme that will be used when installing plugins.
  install = { colorscheme = { "habamax" } },
  -- automatically check for plugin updates
  checker = { enabled = true },
})

```

Você pode então criar suas especificações de plugin em `~/.config/nvim/lua/plugins/`. Cada arquivo deve retornar uma tabela com os plugins que você deseja instalar.



![lazy_vim](/home/edius/Projetos/dotfile/imagens/lazy_vim.png)

**Plugins Lazyvim**

Alguns usuários podem querer dividir suas especificações de plug-in em vários arquivos. Em vez de passar uma tabela de especificações para `setup()`, você pode usar um módulo Lua. As especificações do **módulo** e qualquer nível superior **sub-módulos** serão fundidos juntos na especificação final, e portanto, não é necessário adicionar `require` chamadas em seu arquivo de plugin principal para os outros arquivos.

Os benefícios de usar esta abordagem:

- Simples para **adicionar** novas especificações de plugin. Basta criar um novo arquivo em seu módulo de plugins.
- Permite **cache** de todas as suas especificações de plugin. Isso se torna importante se você tiver muitas especificações de plug-in menores.
- As alterações de especificação serão automaticamente **recarregado** quando eles são atualizados, então o `:Lazy` A interface do usuário está sempre atualizada.

Exemplo:

- `~/.config/nvim/init.lua`

```lua
require("lazy").setup("plugins")
```



- `~/.config/nvim/lua/plugins.lua` ou `~/.config/nvim/lua/plugins/init.lua` ***(este arquivo é opcional)\***

```lua
return {
  "folke/neodev.nvim",
  "folke/which-key.nvim",
  { "folke/neoconf.nvim", cmd = "Neoconf" },
}
```



- Qualquer arquivo lua em `~/.config/nvim/lua/plugins/*.lua` será automaticamente mesclado na especificação principal do plugin.

**Astrovim**

**Requisitos**

- Nerd Fontes  

​	vide (nerd fontes instalação acima)

- Neovim v0.9.5

  instalação via `apt install neovim`

- Tree-sitter CLI 

  instalação via `cargo install tree-sitter-cli`

- Uma ferramenta de área de transferência é necessária para a integração com a área de transferência do sistema (consulte [`:help clipboard-tool`](https://neovim.io/doc/user/provider.html#clipboard-tool) para soluções suportadas)

- Terminal com suporte a cores verdadeiras (para o tema padrão, caso contrário, depende do tema que você está usando) [[2\]](https://docs.astronvim.com/#2)

- Requisitos Opcionais:

  - **ripgrep**

    vide instalação ripgrep

  - **lazygit** 

    vide instalação lazygit

  - **go DiskUsage()**

    instalação `apt install gdu`

  - **bottom**

    instalação `brew install bottom` ou `cargo install bottom --locked`

  - **Node** 

    instalação `brew install node@20`



## 🧰 Instalação

1. **Faça um backup de sua configuração nvim atual** *(se existir)*

   Janela terminal

   ```
   mv ~/.config/nvim ~/.config/nvim.bak
   ```

2. **Limpe pastas neovim** *(Opcional, mas recomendado)*

   Janela terminal

   ```
   mv ~/.local/share/nvim ~/.local/share/nvim.bak
   
   mv ~/.local/state/nvim ~/.local/state/nvim.bak
   
   mv ~/.cache/nvim ~/.cache/nvim.bak
   ```

3. **Clone o repositório**

   Janela terminal

   ```
   git clone --depth 1 https://github.com/AstroNvim/template ~/.config/nvim
   
   # remove template's git connection to set up your own later
   
   rm -rf ~/.config/nvim/.git
   
   nvim
   ```

## 📦 Configuração

- **Instale o LSP**

  Entrar `:LspInstall` seguido pelo nome do servidor que você deseja instalar

  > Exemplo: `:LspInstall pyright`

- **Instalar analisador de idioma**

  Entrar `:TSInstall` seguido pelo nome do idioma que você deseja instalar

  > Exemplo: `:TSInstall python`

- **Instalar o Debugger**

  Entrar `:DapInstall` seguido pelo nome do depurador que você deseja instalar

  > Exemplo: `:DapInstall python`

- **Gerenciar plugins**

  - Rodar `:Lazy check` (`<Leader>pu`) para verificar se há atualizações de plug-in
  - Rodar `:Lazy update` (`<Leader>pU`) para aplicar quaisquer atualizações de plug-in pendentes
  - Rodar `:Lazy sync` (`<Leader>pS`) para atualizar e limpar plugins
  - Rodar `:Lazy clean` para remover quaisquer plugins desativados ou não utilizados

- **Atualizar pacotes e plugins Mason**

  Rodar `:AstroUpdate` (`<Leader>pa`) para atualizar os plugins Neovim e os pacotes Mason

- **Verificar a versão AstroNvim**

  Rodar `:AstroVersion` para exibir a versão AstroNvim instalada atualmente

- **Recarregar AstroNvim** (*EXPERIMENTAL*)

  Rodar `:AstroReload` para recarregar a configuração do AstroNvim e quaisquer novas alterações de configuração do usuário sem reiniciar. Este é atualmente um recurso experimental e pode levar à instabilidade até a próxima reinicialização.

