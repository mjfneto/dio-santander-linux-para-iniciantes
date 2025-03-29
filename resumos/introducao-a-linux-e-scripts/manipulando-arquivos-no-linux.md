# Manipulando Arquivos no Linux

## Trabalhando com arquivos

### Terminal Linux – Apresentação

```
mjfneto@servidor1:~$
```

- `mjfneto` indica o usuário logado na máquina;
- `@servidor1` indica a máquina em que o usuário está logado;
- `~` indica que se está na pasta do usuário;
- `$` indica que o usuário não é um superusuário, é um usuário com restrições.
  - `#` indicaria um superusuário (root).

---

> Para todos os comandos no Linux, são respeitadas letras minúsculas e maiúsculas.

### Navegando pelo sistema de arquivos

- _print working directory_

  ```bash
  pwd
  ```

- _change directory_

  ```bash
  cd /
  ```

  O comando acima faz navegar para a pasta raiz (`/`).

---

> **(Gemini 2.0 Flash)**
>
> A pasta raiz, representada por `/`, é a base do sistema de arquivos no Linux, similar a um diretório principal. Todos os outros diretórios e arquivos do sistema são organizados dentro dela.
>
> A pasta raiz é essencial para o funcionamento do sistema operacional, pois contém arquivos de inicialização, configurações do sistema, bibliotecas compartilhadas e outros arquivos importantes. É importante ter cuidado ao modificar arquivos na pasta raiz, pois isso pode afetar a estabilidade do sistema.

---

- Voltar para o diretório anterior:
  ```bash
  cd ..
  ```
  - `..` indica o diretório imediatamente anterior;
  - `.` indica o diretório atual.

### Filtrando a exibição de arquivos

- Se tenho uma lista grande de arquivos, e não posso usar a barra de rolagem, uma opção é usar o comando `more`:

  ```bash
  ls | more
  ```

  - Apertando `Enter` você "rola" pelos arquivos, um a um;
  - `Ctrl` + `C` para sair da exibição.

- Se quero listar todos os arquivos que começam com a letra `p`:

  ```bash
  ls p*
  ```

  - Uma vantagem dessa abordagem é que, se o diretório tiver conteúdo, ele mostra o que há nele.

- Se quero um arquivo que tenha a letra `m` na primeira posição, qualquer caractere na segunda posição, a letra `g` na terceira posição, e que tenha qualquer terminação:

  ```bash
  ls m?g*
  ```

- Se quero listar somente os `arquivo`s de 1 a 3, independente da terminação:

  ```bash
  ls arquivo[1-3]*
  ```

  - Para ignorar os `arquivo`s de 1 a 3, seria:

  ```bash
  ls arquivo[^1-3]*
  ```

- Se quero listar somente os `arquivo`s 2 e 5, independente da terminação:
  ```bash
  ls arquivo[2,5]*
  ```
  - Para ignorar os `arquivo`s 2 e 5, seria:
    ```bash
    ls arquivo[^2,5]*
    ```

### Localizando arquivos

- Se quero encontrar um arquivo específico (`-name`) a partir do diretório atual:
  ```bash
  find -name arquivo
  ```

### Criando diretórios

- Para criar o diretório `Documentos`:

  ```bash
  mkdir Documentos
  ```

[Atalhos de teclado úteis (prompt do terminal no Linux)](/anexos/atalhos-de-teclado-uteis-prompt-linux.md)

- Para criar um arquivo contendo espaços em branco, use aspas simples:
  ```bash
  mkdir 'Meus Documentos'
  ```

### Excluindo arquivos e diretórios

- Para excluir diretórios:

  ```bash
  rmdir diretorio
  ```

  - Não exclui se o diretório tiver conteúdo.

- Para excluir qualquer diretório, mesmo que contenha arquivos:

  ```bash
  rm -rf arquivo
  ```

  - `r` significa _recursivo_, ou seja, excluirá recursivamente, de diretório a diretório, progressivamente, completamente;
  - `f` significa _force_.

### Obtendo ajuda

A grande maioria dos comandos têm a opção `--help`, que fornece informações adicionais acerca de sua execução.

```bash
ls --help
```

---

> **(Gemini 2.0 Flash)**
>
> No contexto do terminal Linux, `--help` é geralmente considerado uma **opção** (ou _option_ em inglês), embora o termo "flag" também seja usado de forma intercambiável em algumas situações.
>
> Aqui está uma explicação para esclarecer a diferença:
>
> - **Opções (Options):**
>   - Opções modificam o comportamento de um comando.
>   - Geralmente, são precedidas por um ou dois hífens (`-` ou `--`).
>   - `--help` se encaixa nessa definição, pois altera a saída do comando, fazendo com que ele exiba informações de ajuda em vez de executar sua função principal.
> - **Flags (Flags):**
>   - Flags são um tipo de opção que geralmente ativa ou desativa um recurso.
>   - Algumas pessoas usam "flag" como um termo geral para qualquer opção que modifica um comando.
>
> Portanto, embora você possa ouvir alguém se referir a `--help` como uma flag, tecnicamente é mais preciso chamá-la de opção.

---

![Lista longa de arquivos.](/imagens/VirtualBox_Linux%20Ubuntu_29_03_2025_11_46_42.png)

Na imagem acima:

- Na primeira coluna:
  - Se um arquivo começa com:
    - `d` (e.g. `drwxrwxrwt`), trata-se de um **diretório**;
    - `-`, trata-se de um **arquivo**;
    - `l`, trata-se de um **link**, um redirecionamento para outro local.
  - O restante é um representação das gráfica das permissões do arquivo:
    - `r`: _read_;
    - `w`: _write_;
    - `x`: _execute_;
- Na segunda coluna, o número indica a quantidade de objetos dentro do arquivo;
  - Por exemplo, na imagem, o diretório `proc` contém `159` objetos.
- Nas terceira e quarta colunas, há a indicação do dono do arquivo e do grupo ao qual ele pertence;
  - Por exemplo, na imagem, o diretório `media` tem como dono o usuário `root` e pertence ao grupo `root`.
- Na quinta coluna, é dado o tamanho do arquivo, em bytes.
  - A título de curiosidade, é possível listar os arquivos em formato legível com a opção `-h` (_human-readable_):
    ```bash
    ls -lh
    ```

Também há o comando `man` (_manual_), que mostra a página do comando na documentação. Com o comando abaixo, abre-se a página do comando `ls`:

```bash
man ls
```

#### Obtendo ajuda externa

- [help.ubuntu.com](https://help.ubuntu.com/)

### Executando tarefas administrativas como root

Para que um usuário possa fazer esse tipo de tarefa, ele precisa pertencer ao grupo de administradores.

Os grupos estão no arquivo `/etc/group`.

```bash
adm:x:4:syslog,mjfneto
```

Acima, pertencem ao grupo `adm` os usuários `syslog` e `mjfneto`. No caso, ambos conseguem realizar atividades de administrador.

As configurações do comando `sudo` estão no arquivo `/etc/sudoers`.

### Logando como usuário root

> ⚠ Use o login como usuário somente para atividades administrativas, nunca fique logado diretamente como root.

No Ubuntu, para usar o usuário root, precisamos criar uma senha para ele. O comando `passwd` atribui uma senha para um usuário. No comando abaixo, estamos atribuindo uma senha para o usuário `root`:

```bash
sudo passwd root
```

Para entrar como usuário `root`:

```bash
su
```

Para entrar como outro usuário, por exemplo:

```bash
su mjfneto
```

Com o comando acima, se eu já estivesse logado como superusuário, o login seria feito como o usuário `mjfneto`.

### Liberando acesso remoto do usuário root

O arquivo de configuração do serviço de acesso remoto `sshd` está no arquivo `/etc/ssh/sshd_config`:

```bash
cat /etc/ssh/sshd_config
```

Para autorizar o acesso remoto como usuário root, é preciso retirar o comentário da linha:

```bash
#PermitRootLogin prohibit-password
# mudar para
PermiteRootLogin yes
```

Feito isso, é preciso ou fazer uma reinicialização do sistema (`reboot`) ou reinicializar o serviço `sshd`:

- Para checar a condição do serviço:
  ```bash
  systemctl status sshd
  ```
  > 💡 Esse comando é bastante importante, pois registra as tentativas de acesso ao computador.
- Para reinicializar o serviço:
  ```bash
  systemctl restart sshd
  ```

### Trabalhando com arquivos de texto

Sobre os editores de texto `vi` e `nano`.

```bash
vi README.md
```

A partir do comando acima, o comando `vi` entende duas possibilidades:

1. Se o arquivo existe, abra-o para modificação;
2. Se o arquivo não existe, abra-o para criação.

- A tecla `i`: entrar no modo de edição (`-- INSERT --`);
- A tecla `Esc`: sair de algum modo;
- A tecla `:`: abrir o menu;
  - `wq`: salvar (_write_) e fechar (_quit_) o editor;

---

O editor `nano` é um pouco mais amigável que o `vi`.

```bash
nano README.md
```

- `^O` significa `Ctrl` + `o` e, no caso, salvar o arquivo;
- `^X` significa `Ctrl`+`x` e, no caso, fecha o editor.

### Histórico de comandos

O comando `history` armazena o histórico de comandos _do usuário_.

Por padrão, ele armazena os últimos 1000 comandos utilizados. Mas, pode ser menos. O comando abaixo lista somente os 30 últimos comandos:

```bash
history 30
```

- Para executar, por exemplo, o comando de índice `303` no histórico:

  ```bash
  !303
  ```

- Para executar, por exemplo, o comando mais recente que contém `ls` em seu nome:

  ```bash
  !?ls*
  ```

- Para encontrar, por exemplo, os comandos que utilizaram o diretório `Planilhas`:

  ```bash
  history | grep "Planilhas"
  ```

Para exibir a data e a hora de cada comando apresentado no histórico, precisamos mudar uma variável de ambiente do sistema, pois é uma variável específica que determina o tipo de exibição do comando `history`.

> O nome é variáveis de ambiente é em caixa alta.

- Para que seja uma exibição completa, utiliza-se a configuração `%c`:
  ```bash
  export HISTTIMEFORMAT="%c "
  ```
  > Um espaço foi adicionado após `%c` para melhorar a visibilidade do que é exibido pelo comando.

![Lista de configurações de tempo do comando history](/imagens/Screenshot%20from%202025-03-29%2014-12-19.png)

Para que um comando não seja armazenado no histórico, é preciso mudar um parâmetro:

```bash
set +o history
```

> O comando que faz essa alteração fica armazenado no histórico, então, apesar de nenhum outro comando ser registrado após a mudança do parâmetro, ainda é possível concluir que algum usuário fez a modificação.

- Para voltar a armazenar o histórico:
  ```bash
  set -o history
  ```

Para mudar o número dos registros que são exibidos pelo `history`, editamos o arquivo de configuração `.bashrc`, encontrado no diretório do usuário (`/home/usuario`):

```
HISTSIZE=1000
```
