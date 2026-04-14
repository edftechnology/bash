::: {#title .cell .markdown}
# Como configurar o bash e o autocompletar no `linux ubuntu`

## Resumo

Este guia apresenta o procedimento para instalar e configurar o `bash` e
o seu sistema de autocompletar (`ble.sh`) no `linux ubuntu`.
:::

::: {#installation .cell .markdown}
## Instruções de instalação

1.  Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ``` bash
    Ctrl + Alt + T
    ```

2.  Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`.
    Especificamente, ele remove todos os arquivos de pacotes (`.deb`)
    baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`.
    Digite o seguinte comando: `bash  sudo apt clean`

    2.2 Remover pacotes `.deb` antigos ou duplicados do `cache` local. É
    útil para liberar espaço, pois remove apenas os pacotes que não
    podem mais ser baixados (ou seja, versões antigas de pacotes que
    foram atualizados). Digite o seguinte comando:
    `bash  sudo apt autoclean`

    2.3 Remover pacotes que foram automaticamente instalados para
    satisfazer as dependências de outros pacotes e que não são mais
    necessários. Digite o seguinte comando:
    `bash  sudo apt autoremove -y`

    2.4 Buscar as atualizações disponíveis para os pacotes que estão
    instalados em seu sistema. Digite o seguinte comando e pressione
    `Enter`: `bash  sudo apt update`

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de
    pacotes disponíveis e tentará corrigir pacotes quebrados ou com
    dependências ausentes: `bash  sudo apt --fix-broken install`

    2.6 Limpar o `cache` do gerenciador de pacotes `apt` novamente:
    `bash  sudo apt clean`

    2.7 Para ver a lista de pacotes a serem atualizados, digite o
    seguinte comando e pressione `Enter`:
    `bash  sudo apt list --upgradable`

    2.8 Realmente atualizar os pacotes instalados para as suas versões
    mais recentes, com base na última vez que você executou
    `sudo apt update`. Digite o seguinte comando e pressione `Enter`:
    `bash  sudo apt full-upgrade -y`
:::

::: {#full_code .cell .markdown}
## 1.1 Código completo para configurar/instalar/usar {#11-código-completo-para-configurarinstalarusar}

Para configurar/instalar/usar o `bash` e o autocompletar no
`linux ubuntu` sem precisar digitar linha por linha, você pode seguir
estas etapas:

1.  Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ``` bash
    Ctrl + Alt + T
    ```

2.  Digite o seguinte comando e pressione `Enter`:

    \`\`\`bash sudo apt clean sudo apt autoclean sudo apt autoremove -y
    sudo apt update sudo apt \--fix-broken install sudo apt clean sudo
    apt list \--upgradable sudo apt full-upgrade -y git clone
    \--recursive <https://github.com/akinomyoga/ble.sh.git> \~/ble.sh
    make -C \~/ble.sh cat \<\< \'EOF\' \>\> \~/.bashrc

# \-\-- Autocompletar do bash \-\-- {#----autocompletar-do-bash----}

\[ -f /etc/bash_completion \] && . /etc/bash_completion source
\~/ble.sh/out/ble.sh bleopt complete_auto_complete=1 bleopt
prompt_ps1_final=1 bleopt complete_auto_history=1 EOF source \~/.bashrc
\`\`\`
:::

::: {#references .cell .markdown}
## Referências

\[1\] OPENAI. **Instalar o `bash` no `linux ubuntu` pelo
`terminal emulator`**. Disponível em:
<https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/69de8097-5798-83e9-ae8e-6757cf2f0859>.
ChatGPT. Acessado em: 14/04/2026.
:::
