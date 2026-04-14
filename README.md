# Como configurar o auto-update do `git_scripts`

## Resumo

Este repositório pode expor uma checagem de atualização automática para comandos interativos,
seguindo a política:

- perguntar só quando houver `TTY`
- nunca perguntar em `CI` ou scripts não interativos
- usar padrão `N`
- se o usuário aceitar, atualizar com `fetch` + `pull --ff-only`
- se o usuário recusar, continuar normalmente
- em loops com `watch`, perguntar só no início


## Arquivo de apoio

O helper para isso está em:

```bash
git_scripts_self_update.sh
```

Ele expõe a função:

```bash
git_scripts_maybe_self_update
```


## Exemplo de uso em uma função interativa

No início da função ou script interativo do `git_scripts`, carregue o helper e chame a checagem:

```bash
source "$(git rev-parse --show-toplevel)/git_scripts_self_update.sh"
git_scripts_maybe_self_update "$0" "$@"
```

Se houver versão mais nova e o terminal for interativo, o usuário verá algo como:

```bash
[git_scripts] A newer version is available. Would you like to update now? [y/N]
```

O padrão é `N`:

- se o usuário responder `y`, `yes`, `1`, `true` ou `on`, o helper executa:

```bash
git -C <repo> fetch origin <branch>
git -C <repo> pull --ff-only origin <branch>
```

e reinicia o comando atual com a versão nova

- se o usuário responder `n` ou apenas pressionar `Enter`, o comando continua normalmente sem atualizar
- se não houver `TTY`, o helper não pergunta e mantém apenas o aviso simples


## Política de execução

- A checagem só roda uma vez por processo, usando `GIT_SCRIPTS_UPDATE_ALREADY_CHECKED=1`.
- O helper grava um carimbo de tempo dentro do `.git` para não perguntar toda hora.
- O intervalo padrão é de `21600` segundos (`6` horas).
- O `fetch` rápido usa timeout padrão de `2` segundos para não atrasar o comando.


## Variáveis de ambiente

```bash
GIT_SCRIPTS_UPDATE_CHECK=0
```

Desativa a checagem.

```bash
GIT_SCRIPTS_UPDATE_CHECK_INTERVAL_SECONDS=21600
```

Define o intervalo mínimo entre checagens.

```bash
GIT_SCRIPTS_UPDATE_FETCH_TIMEOUT_SECONDS=2
```

Define o timeout do `fetch` leve.

```bash
GIT_SCRIPTS_REPO_ROOT=/caminho/do/repo
```

Permite fixar explicitamente a raiz do repositório quando necessário.
