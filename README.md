# Git_Tips

# Comandos básicos Git e Github

## Sumário

<!--ts-->

- [Principais Comandos do Git](#-principais-comandos-do-git-)
<!--te-->

## Antes de iniciar este procedimento
## Vá até uma pasta onde deseja clonar o projeto escolhido

## 👑 Principais comandos do GIT 👑

### Definindo o nome de usuário

```bash
git config --global user.name “seu nome”
```

### Definindo o email do usuário

```bash
git config --global user.email “seu email”
```

### Clonar Repositório

```bash
git clone -b <branch> <remote_repo>
```

### Listar pastas criadas

```bash
ls
```

### Entrar na pasta criada, conforme o nome do [ Projeto Atual ]

```bash
cd <nome da pasta>
```

### Inicializa o repositório

```bash
git init
```

### Verifica se houve alterações / estado dos arquivos

```bash
git status
```

### Verifica se o diretório remoto foi instalado

```bash
git remote -v
```
### >>> Caso não retorne nenhum informação execute o comando abaixo:

### Informar a pasta remota (Via HTTPS):

(lembre-se de copiar no botão verde [ Code ] na página do projeto no GitHub)

```bash
git remote add origin <link do projeto>
```

### Puxar atualizações do Projeto > Lembrar de clicar em > Commit Behind no GitHub (Página) antes de executar o comando abaixo.

```bash
git pull origin main
```

### Coloca o arquivo em Staging > Antes de Commit

```bash
git add .
```

### Realiza o Commit

```bash
git commit -m "update <versão do projeto> <nome do projeto>"
```

### Enviar atualizações do Projeto > Lembrar de clicar em > Commit Ahead no GitHub (Página), após executar o comando abaixo.

```bash
git push origin main
```

### Informar a pasta remota (Via HTTPS):

(lembre-se de trocar o usuário no comando)

```bash
git remote add origin https://github.com/adosilva/senai-versoes-colaboracoes.git
```

### Informar a pasta remota (Via SSH):

(lembre-se de trocar o usuário no comando)

```bash
git remote add origin git@github.com:adosilva/senai-versoes-colaboracoes.git
```

### Visualizar o repositório remoto:

```bash
git remote –v
```

### Alterar o nome da branch principal de Master para Main (isso é uma boa prática atualmente recomendada)

```bash
git branch -M "main"
```

### Resolvendo o erro "fatal: refusing to merge unrelated histories"...

```bash
git pull origin main --allow-unrelated-histories
```

```bash
git pull --allow-unrelated-histories origin main
git push -u origin main
```

### Realiza o envio dos commits para o branch main

```bash
git push origin main
```

### Baixar a alteração feita no repositório remoto:

```bash
git pull
```

### Cria uma tag

```bash
git tag -a <nome da tag> -m <comentário>
```

### Realiza o envio das Tags para o repositório remoto

```bash
git push origin --tags
```

### Muda para a branch main

```bash
git checkout main
```

### Cria uma nova branch

```bash
git checkout -b nome-branch
```

### Realiza o envio dos commits para a nova branch

```bash
git push origin nome-branch
```

### Faz a mesclagem com outra branch

```bash
git merge origin nome-branch
```

