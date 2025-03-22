# Acesso Remoto a Máquinas Linux

### Acesso remoto via Windows

Vamos simular um acesso remoto à uma máquina Linux, imaginando, por exemplo, que esse servidor está em outra cidade. Como o acessamos para poder utilizá-lo?

1. Saber o IP da máquina;

   ```bash
   ip a
   ```

   O `a` significa "exibir todos os IPs disponíveis neste computador".

   Buscar pelo valor do parâmetro `inet`.

2. Usar um software chamado **PuTTY** para fazer o acesso remoto através de SSH no Windows.

   - Acessar [putty.org](https://putty.org/)
   - Fazer o download do `putty.exe`
   - Posteriormente, usaremos o `puttygen.exe` (utilitário para geração de chaves RSA e DSA)

3. Checar se o PuTTY e o servidor estão na mesma **faixa de IP**.
   - servidor: 10.0.0.103 / cliente: 10.0.0.191
4. No nosso caso, para que a conexão seja possível, e como não havíamos configurado o servidor para conexões SSH, é preciso ter o `openssh-server` instalado no servidor Linux:
   ```bash
   sudo apt-get install openssh-server
   ```

### Acesso remoto via Linux

Através do pacote `ssh` é possível acessar máquinas Linux remotamente.

```bash
ssh nome_de_usuario@endereco_do_servidor
```

### Acessando uma máquina virtual em nuvem (PuTTY)

- Para acessar a instância da máquina virtual em execução no AWS com o PuTTY, precisamos de um certificado (arquivo `.ppk` [Windows]).

  (Este certificado foi baixado na criação da máquina virtual. E o PuTTY não trabalha com o formato `.pem` (Linux).)

- Agora, usaremos o [`puttygen.exe`](#acesso-remoto-via-windows) (PuTTY Key Generator).

### Acessando uma máquina virtual em nuvem (ssh)

- Aqui, usa-se o certificado em formato `.pem` (Linux).

```bash
ssh -i Ubuntu-AWS.pem nome_de_usuario@endereco_do_servidor
```

Caso aconteça um erro, dizendo que o arquivo `.pem` não está protegido:

```bash
sudo chmod 600 Ubuntu-AWS.pem
```

### Excluindo uma instância na AWS

Se não for mais de seu interesse usar a instância, o ideal é excluí-la para evitar cobranças.

Essa é a base de utilização de um serviço em nuvem, paga-se de acordo com a utilização, então, é normal excluir instâncias em execução.
