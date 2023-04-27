# Git_Tips

# Comandos básicos Git e Github

## Sumário

<!--ts-->

- [Principais Comandos do Git](#-principais-comandos-do-git-)
<!--te-->

## 👑 Principais comandos do GIT 👑

### Defini o nome de usuário

```bash
git config --global user.name “seu nome”
```

### Defini o email do usuário

```bash
git config --global user.email “seu email”
```

### Clonar Repositório

```bash
git clone -b <branch> <remote_repo>
```

### Inicializa o repositório

```bash
git init
```

### Verifica se houve alterações / estado dos arquivos

```bash
git status
```

### Coloca o arquivo em Staging

```bash
git add NomeDoArquivo.txt
```

### Realiza o Commit

```bash
git commit -m "meu commit aqui"
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

