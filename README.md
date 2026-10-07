# Como configurar/instalar/usar o `bash` no `linux ubuntu`

## Resumo

Este guia apresenta o procedimento para instalar e configurar o `bash` e o seu sistema de autocompletar (`ble.sh`) no `linux ubuntu`.

## _Abstract_

_This document contains the main commands for configuring/installing/use `bash` on `Linux Ubuntu`._


## Descrição

### `shell`

Um `shell` é uma Interface de Linha de Comando (_Command Line Interface, CLI_) que permite aos usuários interagirem com um sistema operacional por meio de comandos de texto. Ele interpreta os comandos inseridos pelo usuário e os executa, facilitando a manipulação de arquivos, a execução de programas e outras tarefas do sistema. Além disso, os shells também oferecem recursos avançados, como redirecionamento de entrada e saída, expansão de comandos e controle de processos. Exemplos comuns incluem o `Bash`, o `Zsh` e o `PowerShell`.

### `bash`

`Bash`, ou `Bourne Again Shell`, é um `shell` de linha de comando amplamente utilizado em sistemas operacionais Unix e `Linux`. Ele oferece uma variedade de recursos, como expansão de comandos, redirecionamento de entrada/saída, _scripts_ de `shell` e controle de processos. O `Bash` é altamente personalizável e suporta automação de tarefas por meio de _scripts_, tornando-o uma ferramenta poderosa para usuários avançados e administradores de sistemas. Sua sintaxe simples e intuitiva o torna acessível para iniciantes, enquanto sua flexibilidade e extensibilidade o tornam uma escolha popular entre profissionais de TI.

### `bash-completion`

O `bash-completion` é o sistema oficial de autocompletar do `Bash`. Ele adiciona inteligência ao uso da tecla TAB, permitindo completar comandos, opções e argumentos específicos (como `branches` do `git`, nomes de pacotes do `apt`, _interfaces_ de rede etc.). Funciona como uma base estrutural: ele não muda a aparência do `Terminal Emulator` nem oferece sugestões automáticas em tempo real, mas fornece o “vocabulário” que outras ferramentas podem aproveitar e melhorar.

### `fzf`

O `fzf` é um buscador interativo extremamente rápido que funciona no `Terminal Emulator`. Ele permite encontrar comandos no histórico (`Ctrl + R`), arquivos (`Ctrl + T`) e diretórios (`Alt + C`) usando busca aproximada (“fuzzy search”), ou seja, você não precisa digitar o nome exato. Diferente do _autocomplete_ tradicional, ele abre um menu interativo onde você filtra resultados dinamicamente. Ele não substitui o _autocomplete_, mas complementa — é como um “super buscador” para o `Terminal Emulator`.

## `ble.sh`

O `ble.sh` é o que realmente transforma o `Bash` em algo próximo do `Zsh` moderno. Ele melhora profundamente o editor de linha do `Bash`, adicionando sugestões automáticas baseadas no histórico (igual ao `zsh-autosuggestions`), destaque de sintaxe, menus interativos e navegação avançada. Ele atua “por cima” do `Bash`, interceptando a entrada do usuário e enriquecendo a experiência. Na prática, é o componente mais importante para deixar o `Bash` com comportamento moderno.


## 1. Como configurar/instalar/usar o `oh-my-zsh` no `Linux Ubuntu` [1][3]

Para configurar/instalar/usar o `oh-my-zsh` no `Linux Ubuntu`, você pode seguir estes passos:

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando:
    ```bash
    sudo apt clean
    ```

    2.2 Remover pacotes `.deb` antigos ou duplicados do `cache` local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando:
    ```bash
    sudo apt autoclean
    ```

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando:
    ```bash
    sudo apt autoremove -y
    ```

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt update
    ```

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de pacotes disponíveis e tentará corrigir pacotes quebrados ou com dependências ausentes:
    ```bash
    sudo apt --fix-broken install
    ```

    2.6 Limpar o `cache` do gerenciador de pacotes `apt` novamente:
    ```bash
    sudo apt clean
    ```

    2.7 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt list --upgradable
    ```

    2.8 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update`. Digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt full-upgrade -y
    ```

## 2. Instruções de instalação

Para configurar/instalar/usar o `bash` em um sistema `Linux Ubuntu`, você pode seguir estes passos:

No `Bash`, a boa notícia é que ele **já vem instalado por padrão no `Linux Ubuntu`** — então, na maioria dos casos, você não precisa instalar nada.

Mas vamos fazer isso do jeito correto (verificar, reinstalar e garantir que está funcionando).

### 2.1 Verificar se o `Bash` já está instalado

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Shift + T 
    ```

2. Execute:

    ```bash
    bash --version
    ```

    Se aparecer algo como:

    ```bash
    GNU bash, version 5.x.x
    ```

    Então está tudo certo — o `Bash` já está instalado.

### 2.2 Reinstalar o `Bash` (caso esteja com problema)

1. Se quiser garantir uma instalação limpa:

    ```bash
    sudo apt install --reinstall bash -y
    ```


### 2.3 Definir o `Bash` como _shell_ padrão

1. Para garantir que o sistema use o `Bash` como _shell_ principal:

    ```bash
    chsh -s /bin/bash
    ```

    Depois:

    ```bash
    exec bash
    ```



### 2.4 Verificar se o `Bash` está sendo usado

1. Para verificar se o `Bash` está sendo usado:

    ```bash
    echo $SHELL
    ```

    Deve retornar:

    ```bash
    /bin/bash
    ```



### 2.5 Caso o `Bash` não esteja instalado (raro)

1. Se por algum motivo ele foi removido:

    ```bash
    sudo apt install bash -y
    ```

**Observação importante**

O `Linux Ubuntu` usa o `Bash` como _shell_ padrão tradicionalmente, mas em alguns _setups_ (principalmente com `Zsh` ou ambientes customizados), ele pode não ser o _shell_ ativo, apenas instalado.

## 1.1 Código completo para configurar/instalar/usar

Para configurar/instalar/usar o `bash` e o autocompletar no `linux ubuntu` sem precisar digitar linha por linha, você pode seguir estas etapas:

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Digite o seguinte comando e pressione `Enter`:

    ```bash
    sudo apt clean
    sudo apt autoclean
    sudo apt autoremove -y
    sudo apt update
    sudo apt --fix-broken install
    sudo apt clean
    sudo apt list --upgradable
    sudo apt full-upgrade -y
    sudo apt install bash -y
    ```


```python
## 3. Alterar a exibição de caminho completo (ou relativo ao `$HOME`) oara somente a última pasta (`basename`)

Para alterar a exibição de caminho completo (ou relativo ao `$HOME`) oara somente a última pasta (`basename`), execute:

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. **Editar o `~/.bashrc`**
    
    ```bash
    nano ~/.bashrc
    ```

3. **Procurar pela linha do `PS1`**: Use dentro do `nano`:

    ```bash
    Ctrl + W
    PS1
    ```

    Você vai encontrar algo como:

    ```bash
    PS1='\u@\h:\w\$ '
    ```

4. **Trocar `\w` por `\W`**: Você deve usar \W nos dois casos::

    ```bash
    if [ "$color_prompt" = yes ]; then
        PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\W\[\033[00m\]\$ '
    else
        PS1='${debian_chroot:+($debian_chroot)}\u@\h:\W\$ '
    fi
    unset color_prompt force_color_prompt
    ```

5. **Recarregar**:

    ```bash
    source ~/.bashrc
    ```
```

## 4. Configurar o autocompletar `ble` para o `bash` e o `zsh`:

from numpy import source
from pexpect import EOF
from typer import echo


1. **Clonar o `ble.sh`**: Você pode clonar em qualquer lugar, mas existem boas práticas. Sendo assim, a opção recomendada (padrão profissional) é clonar dentro da sua pasta pessoal:

    ```bash
    cd ~
    git clone --recursive https://github.com/akinomyoga/ble.sh.git
    ```

    Isso vai criar:

    ```bash
    ~/ble.sh
    ```

2. **Depois disso**: Entre na pasta e compile:

    ```bash
    cd ~/ble.sh
    make
    ```

3. **Ativar no Bash**: Adicione ao seu `~/.bashrc`:

    ```bash
    cat << 'EOF' >> ~/.bashrc
    # --- Autocompletar do bash ---
    [ -f /etc/bash_completion ] && . /etc/bash_completion
    source ~/ble.sh/out/ble.sh
    bleopt complete_auto_complete=1
    bleopt prompt_ps1_final=1
    bleopt complete_auto_history=1
    EOF
    ```

4. Recarregue:

    ```bash
    source ~/.bashrc
    ```

## Referências

[1] OPENAI. **Instalar o `bash` no `linux ubuntu` pelo `terminal emulator`**. Disponível em: <https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/69de8097-5798-83e9-ae8e-6757cf2f0859>. ChatGPT. Acessado em: 14/04/2026.

