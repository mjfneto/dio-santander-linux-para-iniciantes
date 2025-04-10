# Servidores de Arquivos com Linux

## Servidor de Arquivos

### Introdução ao servidor de arquivos

Vamos falar da verdadeira vocação do sistema operacional Linux: trabalhar com servidores.

Servidores distribuem **serviços**.

Neste módulo, vamos trabalhar com três tipos de servidores:

- servidor de arquivos;
- servidor web;
- servidor de banco de dados.

#### O problema que um servidor de arquivos resolve

```mermaid
---
title: Empresa
---

flowchart TD
A[Ana] <--> C
B[João] <--> C
C[Servidor]
```

A vantagem de armazenar os arquivos dos usuários no servidor está na **centralização da administração**.

Isso pode ser feito localmente (e.g. data center) ou na nuvem.

> **É possível ter um servidor Linux e compartilhar arquivos do Windows?**
>
> Sim. Para isso, utiliza-se um serviço específico.
>
> **(Windows) Protocolo SMB:** Para fazer esse compartilhamento de arquivos, no servidor Linux, é preciso ter a aplicação **SAMBA**.

Outra vantagem de ter um servidor de arquivos é a geração de **logs**, registros das atividades (e.g. quem fez upload de determinado arquivo e quando) dos usuários.

Mais uma vantagem é que, ao invés de fazer backups em máquinas individualizadas, o backup é centralizado no servidor. Dessa forma, facilita-se o trabalho do administrador de sistemas e também dos usuários.

### Instalação do SAMBA e configuração inicial

- [wiki.samba.org](https://wiki.samba.org/)

```bash
apt install samba
```

---

Neste momento do curso, temos dois discos, um onde o sistema operacional está instalado, e outro, para compartilhamento de arquivos (no caso, `/disk2`).

> Não é aconselhável que o compartilhamento de arquivos esteja no mesmo disco que o sistema operacional.
>
> Imagine o compartilhamento de arquivos entre, digamos, 400 usuários, estando no mesmo disco que o sistema operacional; isso comprometeria sua execução e o acesso aos arquivos, deixando ambos lentos.
>
> Então, o ideal é que se tenha um disco para o sistema operacional e outros discos para os compartilhamentos.

- O próximo passo é criar o diretório de compartilhamento dentro do disco destinado a essa atividade. No caso, é o `/disk2/publica`. E daremos permissão total aos usuários:

  ```bash
  chmod 777 /disk2/publica
  ```

- Ajustar os parâmetros no arquivo de configuração do SAMBA (`/etc/samba/smb.conf`). Precisamos dizer ao SAMBA que a pasta `publica` estará disponível para toda a nossa rede. Fazemos isso adicionando o seguinte ao final do arquivo:

  ```
  [publica]
      path = /disk2/publica
      writable = yes
      guest ok = yes
      guest only = yes
  ```

- Precisamos reiniciar o serviço do SAMBA, que é um daemon, um serviço executado em segundo plano. Para iniciar, reiniciar e fechar daemons, usamos o `systemctl`:

  ```bash
  systemctl restart smbd
  ```

  Acima, para o comando `systemctl` o SAMBA é conhecido como `smbd`, `d` porque se trata de um daemon.

  Para checarmos se o daemon, o serviço, está de fato rodando:

  ```bash
  systemctl status smbd
  ```

  Contudo, se reiniciarmos o servidor, o serviço não subirá sozinho, então, precisamos executar o seguinte comando:

  ```bash
  systemctl enable smbd
  ```

### Configurando o acesso via máquina cliente

No Windows, acessamos o diretório compartilhado através do IP do servidor. No próprio explorador de arquivos, na barra de endereços:

```
\\10.0.0.19\publica
```

> Para acessar um servidor Linux de um computador Windows, o usuário ainda precisa estar cadastrado naquele, ou seja, precisa constar no arquivo `/etc/passwd`.
