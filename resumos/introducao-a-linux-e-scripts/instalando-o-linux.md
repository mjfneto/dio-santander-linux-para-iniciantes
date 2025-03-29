# Instalando o Linux

## Distribuições utilizadas no curso

Para nos acostumarmos com os comandos, vamos começar o curso usando a distribuição Ubuntu Server:

- [ubuntu.com/download/server](https://ubuntu.com/download/server)

Posteriormente, usaremos a versão Desktop.

## Realizando o download do VirtualBox

- [virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

- As máquinas virtuais são computadores de software com a mesma funcionalidade que os computadores físicos. Assim como estes, elas executam aplicativos e um sistema operacional. No entanto, as máquinas virtuais são arquivos de computador executados em um computador físico e se comportam como um.

## Instalando o VirtualBox

## Criando máquinas virtuais

### Windows: hypervisorlaunchtype

1. No Windows, abra o prompt de comandos;
2. Digite `bcdedit`;

   - Se a opção `hypervisorlaunchtype` estiver como `Auto`, digitar o seguinte comando:
     ```bash
     bcdedit /set hypervisorlaunchtype off
     ```
     Isso desabilita o Hyper-V, virtualizador padrão do Windows, permitindo a execução do VirtualBox.
   - Se a opção `hypervisorlaunchtype` não estiver listada:

     `Painel de Controle` > `Programas` > `Ativar ou desativar recursos do Windows` > habilitar `Plataforma do Hipervisor do Windows` > Reiniciar o computador > seguir as instruções acima para desligar o Hyper-V

### Instalando o Linux Ubuntu em MV

- É importante começarmos pelo Linux Server porque, com ele, estaremos praticando comandos fora de um ambiente gráfico.
- No futuro, ao trabalhar com um servidor web, por exemplo, não terá um ambiente gráfico instalado.
- Se eu criar um contêiner (Docker), precisarei entender de comandos.
- Entre outros…

---

- Para reinicializar o computar:
  ```bash
  sudo reboot
  ```

### Desligando máquina virtual – Salvar Estado

- Para desligar a máquina virtual imediatamente (tempo `0`), pela linha de comando:

  ```bash
  shutdown 0
  ```

- Para desligar a máquina virtual, **salvando o estado da máquina virtual**:
  1. Clicar no ❌ para fechar a janela da máquina virtual;
  2. Selecionar `Salvar o estado da máquina`;
     ![Close Virtual Machine dialog](/imagens/Screenshot%20from%202025-03-21%2023-43-02.png)
  3. Assim, ao inicializar a MV, recupera-se o estado anterior, sem passar pelo processo de boot.

### Criando uma conta na AWS

Outras formas de ter acesso a uma máquina virtual com Linux:

- Outros softwares de virtualização:
  - Hyper-V (Microsoft), VMWare, etc.
- Serviços de nuvem:
  - Amazon Web Services (AWS), Azure (Microsoft), Google Cloud Platform, etc.
  - [aws.amazon.com](https://www.aws.amazon.com/)

### AWS — Criando uma máquina virtual em nuvem (EC2)

- Os serviços de máquina virtual da AWS são conhecidos como **EC2**.
  - Instâncias (em execução): número de máquinas virtuais ativas.
  - Tipo de instância: `t2.micro` (qualificado para o nível gratuito).
  - Par de chaves (login): para se conectar com segurança à sua instância.
    - Nome do par de chaves
    - Tipo de par de chaves
      - RSA: par de chaves públicas e privadas criptografadas por RSA.
      - ED25519 (não compatível com instâncias do Windows)
    - Formato de arquivo de chave privada:
      - `.pem` (OpenSSH)
      - `.ppk` (PuTTY)
  - Configuração de Rede:
    - `✅ Permitir tráfego SSH de` (porque o acesso remoto é feito por esse protocolo):
      - `Qualquer lugar 0.0.0.0/0`:
        > Regras com origem `0.0.0.0/0` permitem que todos os endereços IP acessem sua instância. Recomendamos configurar regras de grupo de segurança para permitir o acesso apenas de endereços IP conhecidos.
  - `Executar instância`
- Informações da instância:
  - **Endereço IPv4 público**: importante para fazermos o acesso remoto à instância.

### Utilizando o WSL

Uma terceira de fazer a virtualização de uma máquina Linux é através do WSL, recurso do Windows 10/11.

> O Subsistema do Windows para Linux permite que os desenvolvedores executem um ambiente GNU/Linux, incluindo a maioria das ferramentas de linha de comando, utilitários e aplicativos, diretamente no Windows, sem modificações ou sem a sobrecarga de uma máquina virtual tradicional ou instalação dualboot.

<div style="background-color: orange; padding: 10px; border-left: 8px solid darkorange; margin-bottom: 16px">
    ❗ Para usar o WSL, é preciso ter a versão <strong>Pro</strong> do Windows 10/11.
</div>

- Também é necessário ter ativados alguns recursos do Windows:

  - Painel de Controle > Programas > Programas e Recursos — Ativar ou desativar recursos do Windows > `🮱 Plataforma de Máquina Virtual`, `🮱 Plataforma do Hipervisor do Windows` e `🮱 Subsistema do Windows para Linux` > Reiniciar o computador.
  - Além disso, o valor do parâmetro [`hypervisorlaunchtype`](#windows-hypervisorlaunchtype) precisa ser `Auto`. (Por isso, não é possível usar o VirtualBox e o WSL ao mesmo tempo.)

- Por fim, fazer uma atualização no Windows, seguindo estas [instruções](https://learn.microsoft.com/pt-br/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package).

  - Reiniciar o computador.

Seguidos esses passos, você pode instalar as distribuições do Linux como se fossem aplicativos, simplesmente baixando-as na Microsoft Store.
