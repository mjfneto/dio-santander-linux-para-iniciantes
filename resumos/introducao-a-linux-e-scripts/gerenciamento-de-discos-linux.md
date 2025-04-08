# Gerenciamento de Discos Linux

## Gerenciamento de Discos

### Discos, sistemas de arquivos e partições

#### Sistemas de arquivos

Um sistema de arquivos é um padrão, uma forma de controle que o sistema operacional tem sobre o armazenamento e a recuperação de dados.

| Sistema operacional | Sistema de arquivos |
| :-----------------: | :-----------------: |
|        MacOS        |         HFS         |
|     Unix/Linux      |   Ext3, Ext4, XFS   |
|       Windows       |     FAT32, NTFS     |

#### Particionamento

De modo geral, o particionamento é a divisão de um disco em partes. Cada parte ou partição é independente da outra. Cada partição pode ter um sistema de arquivos diferente.

### Adicionando um novo disco

```bash
lsblk
```

```bash
fdisk -l
```

### Particionando e formatando discos via terminal

#### Particionando

```bash
fdisk /dev/sdb
```

Inicializada a configuração do `fdisk` com o comando acima, passamos às etapas de configuração da tabela de partição:

1. `n` para criar uma nova partição;
2. `p` para criar uma partição primária;
3. `1` para definir o número da partição;
4. `Enter` para selecionar o padrão para o primeiro setor;
5. `Enter` para selecionar o padrão para o setor final;
6. `w` para salvar as mudanças em disco e sair.

#### Formatando

Para formatar o disco, é preciso indicar qual sistema de arquivos você utilizará.

Abaixo, por exemplo, usa-se o comando `mkfs`, passando a extensão `ext4`:

```bash
mkfs.ext4 /dev/sdb
```

> **⚠ Atenção:**
>
> A formatação remove todos os dados existentes da partição.

### Montando e desmontando discos

- Para que o disco esteja disponível para utilização, ele precisa estar montado.
- Para montar um disco, é preciso indicar o diretório onde ele será montado.

  - Normalmente, existe um diretório específico para isso, o `/mnt`.

    - Neste diretório, podemos criar um diretório, por exemplo, `disco2`, e, nele, montamos o disco desejado:

      ```bash
      # /mnt

      mount /dev/sdb /mnt/disco2/
      ```

- Para desmontar um disco, usamos o comando `umount`:
  ```bash
  umount /dev/sdb
  ```

### Montando discos automaticamente

> O comando `lsblk` lista todos discos disponíveis e, em sua tabela, há os "pontos de montagem" (`MOUNTPOINTS`); ou seja, podemos usar esse comando quando queremos saber onde um disco está montado.

Sem uma configuração adequada, é preciso sempre montar o disco ao inicializar o computador.

Para fazer a montagem automaticamente, editamos o arquivo `/etc/fstab`:

```bash
nano /etc/fstab
```

E adicionamos a seguinte linha ao documento:

```bash
/dev/sdb /disk2 ext4 defaults 0 0
```

No exemplo acima, estamos indicando que queremos montar o disco `/dev/sdb` na ponto de montagem `/disk2` com o sistema de arquivos `ext4`, o sistema que escolhemos anteriormente.
