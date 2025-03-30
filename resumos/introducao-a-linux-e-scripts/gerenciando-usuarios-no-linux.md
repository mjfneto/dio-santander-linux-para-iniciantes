# Gerenciando Usuários no Linux

## Trabalhando com Usuários

### Criando e excluindo usuários

- Para criar o usuário `joao.silva`.

  ```bash
  useradd joao.silva
  ```

- Para remover, forçosamente, o usuário `joao.silva`:

  ```bash
  userdel -f joao.silva
  ```

- Para criar o usuário `joao.silva` com um comentário (no caso, seu nome completo) e definindo a shell na qual ele se logará ao terminal:

  ```bash
  useradd -m -c "João da Silva" -s /bin/bash joao.silva
  ```

  - `-m` ou `--create-home`
  - `-c` ou `--comment`

  - Para criar (ou alterar) a senha para o usuário `joao.silva`:
    ```bash
    passwd joao.silva
    ```
  - Para definir que a shell do usuário `joao.silva` é a padrão, ou seja, bash:

    ```bash
    chsh -s /bin/bash joao.silva
    ```

- Para remover forçosamente o usuário `joao.silva`, removendo também seu diretório HOME:
  ```bash
  userdel -fr joao.silva
  ```

### Editando informações do usuário

- Para definir uma data de expiração para a conta do usuário no momento da sua criação:

  ```bash
  useradd guest -c "Convidado" -m -e 30/03/2025
  ```

  - `-e` ou `--expiredate`

- Para fazer alterações na conta do usuário:

  ```bash
  usermod
  ```

- Para forçar que o usuário troque sua senha no próximo login:
  ```bash
  passwd joao.silva -e
  ```
  - Se fosse passada uma data de expiração, o usuário precisaria trocar a senha na data especificada, mas, como aquela não foi passada, o usuário precisa mudar a senha no próximo acesso.

Para verificar quais usuários estão cadastrados no sistema e algumas de suas informações, consultamos o arquivo `/etc/passwd`:

```bash
cat /etc/passwd
```

### Shell Script – Criando usuários em lote

- Para criar o usuário `joao.silva` com os principais parâmetros, incluindo a senha:

  ```bash
  useradd joao.silva -m -c "João da Silva" -s /bin/bash -p $(openssl passwd -crypt Senha123)
  ```

  - No caso, a senha precisa estar criptografada, por isso usamos o resultado do comando `openssl` com a opção `-crypt` ⚠ (ler caixa de informação abaixo).
  - Para criar o usuário `joao.silva` com a senha criptografada usando o algoritmo de hash SHA-256:
    ```bash
    useradd joao.silva -m -c "João da Silva" -s /bin/bash -p $(openssl passwd -5 Senha123)
    ```

> **(Gemini 2.0 Flash)**
>
> **O comando openssl passwd não possui a opção `-crypt`.** Essa opção foi substituída por outras opções que especificam o algoritmo de hash a ser usado para gerar a senha criptografada.
>
> **Como usar o comando openssl passwd**
>
> O comando `openssl passwd` é usado para gerar senhas criptografadas usando diferentes algoritmos de hash. A sintaxe básica do comando é a seguinte:
>
> ```bash
> openssl passwd [options] [password]
> ```
>
> **Opções do comando openssl passwd**
>
> As opções mais comuns do comando openssl passwd são:
>
> - `-1`: usa o algoritmo de hash MD5.
> - `-salt`: especifica o salt a ser usado na criptografia da senha.
> - `-in`: lê a senha a ser criptografada de um arquivo.
> - `-out`: grava a senha criptografada em um arquivo.
>
> **Exemplos de uso do comando openssl passwd**
>
> Aqui estão alguns exemplos de como usar o comando openssl passwd:
>
> Para gerar uma senha criptografada usando o algoritmo de hash MD5:
>
> ```bash
> openssl passwd -1 senha
> ```
>
> Para gerar uma senha criptografada usando o algoritmo de hash SHA-256:
>
> ```bash
> openssl passwd -salt senha
> ```
>
> Para ler a senha a ser criptografada de um arquivo:
>
> ```bash
> openssl passwd -in senha.txt
> ```
>
> Para gravar a senha criptografada em um arquivo:
>
> ```bash
> openssl passwd -out senha.txt senha
> ```
>
> **Observações**
>
> - O comando openssl passwd é uma ferramenta poderosa para gerar senhas criptografadas. No entanto, é importante observar que o algoritmo de hash MD5 é considerado inseguro e não deve ser usado para gerar senhas para sistemas críticos.
> - O algoritmo de hash SHA-256 é considerado mais seguro que o MD5 e é recomendado para uso em sistemas críticos.

### Adicionando usuários a grupos

Para exibir os grupos disponíveis no sistema, consultamos o arquivo `/etc/group`:

```bash
cat /etc/group
```

- Para adicionar o usuário `mariana.silva` aos grupos `adm` e `sudo`, dando a ela permissões para atividades administrativas:

  ```bash
  usermod mariana.silva -G adm,sudo
  ```

  - `-G` para adicionar `mariana.silva` a mais de um grupo suplementar.

### Criando novos grupos

- Para criar o grupo `GRP_ADM`:
  ```bash
  groupadd GRP_ADM
  ```
- Para deletar o grupo `GRP_ADM`:
  ```bash
  groupdel GRP_ADM
  ```
- Para criar o usuário `rodrigo.silva` já adicionando-o ao grupo `GRP_ADM`:

  ```bash
  useradd rodrigo.silva -c "Rodrigo da Silva" -m -s /bin/bash -p $(openssl passwd -5 Senha123) -G GRP_ADM
  ```

- Para remover o usuário `rodrigo.silva` do grupo `adm`:

  ```bash
  gpasswd -d rodrigo.silva adm
  ```

### Conhecendo o sistema de permissões

- Para listar os arquivos de um diretório com as informações sobre as permissões:

  ```bash
  ls -l
  ```

  - O primeiro caractere indica o tipo de arquivo:
    - `d` indica um diretório;
    - `-` indica um arquivo;
    - `l` indica um link.
  - A seguinte legenda descreve os demais caracteres:
    ![Sistema de permissões de arquivos no Linux](/imagens/Screenshot%20from%202025-03-30%2011-04-13.png)
    - `r` (_read_)
    - `w` (_write_)
    - `x` (_execute_)

- Para mudar o dono de um arquivo, é preciso estar logado como usuário root ou pertencer ao grupo sudo. Por exemplo, para definir o usuário `mariana` e o grupo `GRP_ADM` como novos dono e grupo do diretório `adm`, usamos o comando `chown` (_change owner_):

  ```bash
  chown mariana:GRP_ADM /adm
  ```

### Alterando as permissões de um diretório – arquivo

Para alterar as permissões dos usuários para determinado arquivo, usa-se o comando `chmod`.

O jeito mais simples de fazer as alterações é através da base numérica, que segue a seguinte tabela:

![Tabela da base numérica para permissões no chmod](/imagens/Screenshot%20from%202025-03-30%2011-43-51.png)

- Por exemplo, para dar permissão total ao dono de um arquivo, somente de leitura e execução ao grupo, e nenhuma para os demais usuários:
  ```bash
  chmod 750 file.txt
  ```
  - dono: 4 + 2 + 1 = `7`
  - grupo: 4 + 1 = `5`
  - outros: `0` (Nenhuma permissão)

### Entendendo melhor as permissões de execução para scripts

- Um arquivo executável tem a extensão `.sh`;
- Um arquivo executável deve iniciar com `#!/bin/bash`.

- Para dar permissão de execução ao dono de um arquivo executável:
  ```bash
  chmod +x arquivo.sh
  ```
