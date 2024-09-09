> Olá!! Bem vindos ao meu projeto de portifólio. Logo abaixo você encontra 7 automações criados por mim, todos programados em Python. 
> Cada um possui uma breve descrição sobre sua função e como executa-lo em sua máquina. 
> Espero que goste 😊


## `Projeto 1: DoS Blocker`

### Descrição:
O **DoS Blocker** monitora o tráfego da rede para identificar e bloquear ataques de negação de serviço (DoS). Ele analisa a taxa de pacotes de IPs específicos e, se a taxa ultrapassar um limite definido (40 pacotes por segundo), o IP é bloqueado utilizando o `iptables`.

### Como Executar:
1. Certifique-se de ter o **Python** instalado em seu sistema, bem como as dependências necessárias:
    ```bash
    pip install scapy
    ```

2. Execute o script com privilégios de superusuário (root):
    ```bash
    sudo python3 dos_blocker.py
    ```

3. O script começará a monitorar o tráfego da rede. Quando um IP enviar pacotes além do limite, ele será bloqueado.

### Dependências:
- `scapy` (biblioteca para captura de pacotes de rede)
- `iptables` (para bloquear IPs diretamente no sistema)

### Observações:
- O limite de pacotes por segundo está configurado para 40, mas pode ser alterado modificando a constante `THESHOLD`.
- Para monitorar o tráfego de rede, é necessário acesso root.


## `Projeto 2: Mini Firewall`

### Descrição:
O **Mini Firewall** é um firewall simples que bloqueia IPs com base em listas de permissões (whitelist) e bloqueios (blacklist). Ele também detecta o worm Nimda e bloqueia IPs maliciosos. Registra eventos de bloqueio em arquivos de log.

### Como Executar:
1. Crie os arquivos de listas de IPs (`whitelist.txt` e `blacklist.txt`) com os IPs permitidos e bloqueados, respectivamente.
   
2. Instale as dependências necessárias:
    ```bash
    pip install scapy
    ```

3. Execute o script como superusuário (root):
    ```bash
    sudo python3 mini_firewall.py
    ```

4. O firewall começa a monitorar o tráfego da rede, bloqueando IPs maliciosos e registrando os eventos no diretório `logs`.

### Dependências:
- `scapy` (biblioteca para análise de pacotes de rede)
- `iptables` (para bloquear IPs no sistema)
- Listas de IPs (`whitelist.txt` e `blacklist.txt`)

### Observações:
- O script detecta o worm Nimda ao analisar o tráfego HTTP (porta 80).
- Arquivos de log são gerados automaticamente com timestamps, armazenando informações sobre os eventos de bloqueio.
- O limite de pacotes por segundo também é definido como 40, e pode ser alterado na variável `THRESHOLD`.


## `Projeto 3: Simulation`

### Descrição:
O **Simulation** é uma simulação de firewall simples que gera endereços IP aleatórios e verifica se eles correspondem às regras predefinidas de bloqueio. Se o IP estiver na lista de bloqueio, a ação será "block"; caso contrário, a ação será "allow". 

### Como Executar:
1. Simplesmente execute o script sem a necessidade de permissões especiais:
    ```bash
    python3 simulation.py
    ```

2. O script gera 12 endereços IP aleatórios dentro do intervalo `192.168.1.0 - 192.168.1.20` e verifica as regras de firewall para cada IP, imprimindo a ação correspondente.

### Dependências:
- Não há dependências externas.

### Observações:
- As regras de firewall são definidas no dicionário `firewall_rules`, que pode ser modificado conforme necessário para incluir novos IPs e ações.
- Um número aleatório entre 0 e 9999 é gerado junto com cada IP, simulando eventos variados.



## `Projeto 4: OS Fingerprinting`

### Descrição:
O **OS Fingerprinting** realiza a varredura de um host para identificar o sistema operacional e os serviços associados aos diferentes protocolos e portas. Utiliza a biblioteca `nmap` para fazer a varredura e exporta os resultados para um arquivo CSV.

### Como Executar:
1. Instale a biblioteca `nmap`:
    ```bash
    pip install python-nmap
    ```

2. Execute o script como superusuário (root):
    ```bash
    sudo python3 os_fingerprinting.py <host> -p <ports> -o <output_file.csv>
    ```

    - **host**: O endereço IP do host alvo.
    - **ports**: As portas que deseja escanear (exemplo: "22,80,443").
    - **output_file**: Arquivo CSV para salvar os resultados. Se não for especificado, o padrão será `scan_results.csv`.

### Dependências:
- `python-nmap` (interface Python para o Nmap)
- `nmap` (deve estar instalado no sistema)


## `Projeto 5: Ping Sweeper`

### Descrição:
O **Ping Sweeper** realiza uma varredura de ping em uma rede para identificar hosts que estão online. Ele utiliza o protocolo ICMP para enviar pacotes e verificar se os hosts respondem.

### Como Executar:
1. Instale as dependências necessárias:
    ```bash
    pip install scapy netaddr
    ```

2. Execute o script:
    ```bash
    python3 ping_sweeper.py <network> <netmask>
    ```

    - **network**: O endereço da rede alvo (ex: `192.168.1.0`).
    - **netmask**: A máscara de rede (ex: `24` para `255.255.255.0`).

3. O script irá escanear a rede e listar os hosts que estão online.

### Dependências:
- `scapy` (biblioteca para manipulação de pacotes de rede)
- `netaddr` (para trabalhar com endereços IP e sub-redes)


## `Projeto 6: Port Scanner`

### Descrição:
O **Port Scanner** varre uma rede para identificar hosts ativos e verifica as portas abertas em cada host. Utiliza `scapy` para enviar pacotes TCP e realiza a varredura de portas de maneira paralela.

### Como Executar:
1. Instale as dependências necessárias:
    ```bash
    pip install scapy
    ```

2. Execute o script:
    ```bash
    python3 port_scanner.py <network> <netmask>
    ```

    - **network**: O endereço da rede alvo (ex: `192.168.1.0`).
    - **netmask**: A máscara de rede (ex: `24` para `255.255.255.0`).

3. O script irá identificar os hosts ativos e listar as portas abertas para cada um deles.

### Dependências:
- `scapy` (biblioteca para manipulação de pacotes de rede)

### Observações:
- O número de threads usados no scan é baseado no número de CPUs disponíveis no sistema.
- O escopo da varredura de portas é de 1 a 1023, mas pode ser ajustado no código.


## `Projeto 7: Service Fingerprinting`

### Descrição:
O **Service Fingerprinting** realiza uma varredura para identificar banners de serviços que estão rodando em portas específicas de um host. Ele tenta se conectar a um serviço e retorna o banner da aplicação, útil para detectar versões de software.

### Como Executar:
1. Execute o script:
    ```bash
    python3 service_fingerprinting.py <ip> -p <ports>
    ```

    - **ip**: O endereço IP do host alvo.
    - **ports**: Lista de portas a serem escaneadas, separadas por vírgula (ex: "22,80,443").

2. O script irá retornar os banners dos serviços identificados nas portas especificadas.

### Dependências:
- Não há dependências externas.

### Observações:
- Se o serviço não retornar um banner, o script informará que nenhum banner foi encontrado.

---
Este projeto reúne ferramentas essenciais para a segurança de redes, permitindo desde a detecção de hosts até a identificação detalhada de sistemas e serviços. Com o uso de `scapy` e `nmap`, ele automatiza a busca por vulnerabilidades e fortalece a capacidade de resposta a possíveis ameaças. Essas soluções tornam o processo mais ágil e preciso, ajudando a proteger infraestruturas críticas contra ataques. Como resultado, o projeto se torna um recurso valioso na defesa de redes.