# Copiando Arquivos e Manipulando Processos

## Manipulação de Arquivos

### Copiando arquivos

```bash
cp /dir/de/origem/arquivo /dir/de/destino/
```

> **⚠ Atenção:**
>
> Se você copiar arquivos com o mesmo nome na origem e no destino, o comando `cp` sobreporá os do diretório de destino. Mas, é possível dar segurança ao processo usando a flag `-i` (_interactive_), que pergunta, toda vez que um mesmo nome é detectado, se a sobreposição deve ser feita ou não.

### Renomeando/movendo arquivos

> **⚠ Atenção:**
>
> Se você mover arquivos com o mesmo nome na origem e no destino, o comando `mv` sobreporá os do diretório de destino. Mas, é possível dar segurança ao processo usando a flag `-i` (_interactive_), que pergunta, toda vez que um mesmo nome é detectado, se a sobreposição deve ser feita ou não.

### Iniciando, visualizando e encerrando um processo

```bash
ps
```

O comando `ps`, sem nenhuma opção ou flag, mostra somente os processos em execução no terminal do usuário que o executa. Assim, ele também não mostra os processos em execução por outros usuários, informação importante no contexto de servidores.

Sendo assim, precisamos o `ps` com outros parâmetros:

```bash
ps aux

# a - lista os processos em execução para todos os usuários logados
# u - informa os usuários associados a cada processo
# x - inclui os processos que foram executados fora do console (e.g. via ambiente gráfico)
```

Todo processo tem um número de identificação e a hora em que foi executado.

---

Podemos encerrar todos os processos com nome `chrome`, por exemplo, usando o comando `killall`:

```bash
killall chrome
```

---

O comando `w` lista todos os usuários logados:

```bash
w
```

Para vermos o PID do processo de login de cada usuário, usamos o comando `who`:

```bash
who -a
```

Com o PID do processo de login de um usuário, podemos derrubá-lo. Abaixo, por exemplo, encerramos o processo (de login) com a identificação `1229`:

```bash
kill 1229
```
