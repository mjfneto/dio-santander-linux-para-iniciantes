# Gerenciamento de Pacotes Linux (UBUNTU-DEBIAN)

## Gerenciamento de Pacotes

### Gerenciamento de Pacotes (UBUNTU-DEBIAN)

Um pacote pode ser:

- um software novo;
- um driver (para um hardware que você tenha instalado em seu computador);
- um codec de um vídeo, por exemplo;
- etc.

A atualização de pacotes no Linux requer o pedido através de um comando, diferentemente do Windows, que a faz automaticamente.

Nas distribuições Ubuntu-Debian serão usados sempre os mesmos comandos.

```bash
apt-get
```

```bash
apt # mais moderno
```

### Atualização do sistema operacional

> ⚠ Se você tem um sistema em produção, o ideal é criar um ambiente de teste para confirmar se tudo funciona bem com a atualização.
>
> - É possível duplicar uma máquina virtual para fazer isso;
> - Também é possível fazer uma screenshot do estado do sistema, para onde seja possível regressar no caso de algum problema;
>
> Resumindo, somente atualize o sistema se você testou antes em outras ambientes.

1. Fazer uma atualização da lista de pacotes disponíveis:
   ```bash
   apt update
   ```
2. Fazer, de fato, a atualização:
   ```bash
   apt upgrade
   ```

### Instalação de pacotes no ambiente Desktop

### Gerenciamento de pacotes (FEDORA RED HAT CenTOS)

#### Red Hat

```bash
dnf
```

```bash
yum
```

### Realizando a instalação de arquivos DEB

No Debian, os arquivos executáveis para instalação possuem a extensão `.deb`.

> Para Fedora/openSUSE, a extensão é `.rpm`.

```bash
apt install arquivo.deb
```
