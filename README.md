# lab-auditoria-controle-acessp-linux
## Controle de Acesso em servidor Linux

"Distro: Kali Linux (versão 2025.4)"

Em 14/03/2026 
## 1 - "Configuração inicial do servidor Kali para laboratório de Auditoria e Controle de Acesso";

No Kali Linux:
Atualizei e fiz upgrade no SO
_sudo apt update && sudo apt upgrade -y_

Verifiquei se o serviço SSH estava disponível
_sudo systemctl status ssh_
Se não
_sudo apt install openssh-server -y_

Depois:
_sudo systemctl enable ssh_
_sudo systemctl start ssh_

Para saber o IP da máquina na rede
_ip a_

Daí já consegui acessar do meu dispositivo Win11 através do SSH
ssh usuario@ip_do_kali

UM PONTO IMPORTANTE NA ÁREA DE SEGURANÇA DA INFORMAÇÃO (EVITAR O ACESSO DO root VIA SSH)

Alterei o arquivo sshd_config, através do comando "sudo nano /etc/ssh/sshd_config" para DESABILITAR O LOGIN DO root via SSH, assim aumetando a dificuldade de acesso por BRUTAL FORCE

Encontre a linha #PermitRootLogin prohibit-password ou PermitRootLogin yes.

Troque/adicione para:

PermitRootLogin no

Logo após isso restartei o serviço ssh 
_sudo systemctl restart ssh_ 

## 2 - Gestão de usuários e grupos (RBAC no servidor Linux)

Este laboratório simula um ambiente com papéis bem definidos para estudo de Auditoria e Controle de Acesso:

- admin: administração do servidor, gestão de usuários, serviços e configurações críticas.
- dev: desenvolvimento e manutenção de aplicações no servidor, sem acesso administrativo completo.
- analista: foco em leitura de logs e geração de relatórios de auditoria, sem poder alterar configuração do sistema.
- guest: acesso extremamente limitado, apenas para testes pontuais.

O objetivo é aplicar o princípio do menor privilégio, concedendo a cada papel apenas o acesso necessário para suas funções.

 
### 2.1 Usuários e grupos (implementando RBAC)

Para representar os papéis definidos, foram criados os seguintes grupos de sistema:

- admin
- dev
- analista
- guest

Em seguida, foram criados usuários de laboratório e associados a esses grupos:

- adminuser → grupo admin
- devuser → grupo dev
- analystuser → grupo analista
- guestuser → grupo guest

Comandos principais utilizados:

```bash
# criação de grupos
groupadd admin
groupadd dev
groupadd analista
groupadd guest

# exemplo de criação de usuário do papel admin
useradd -m -s /bin/bash adminuser
passwd adminuser
usermod -aG admin adminuser
```

Esse texto mostra claramente que você sabe aplicar grupos como mecanismo de RBAC.

***

## 3. Configurando sudo com mínimo privilégio

### 3.1. Dar sudo só ao grupo `admin`

Modelo simples: só quem está no grupo `admin` pode usar sudo.

1) Entrar com `sudo visudo` (modo seguro de editar sudoers).

2) Adicionar essa linha (se não existir algo semelhante):

```text
%admin ALL=(ALL) ALL

```


## 4. Primeiros passos de auditoria (logins e sudo)

Vamos aproveitar o que já existe no sistema, sem instalar nada extra ainda.

### 4.1. Comandos para coletar informações

1) Visualizar logins recentes:
```bash
# histórico de logins
last

# usuários logados no momento
who

```






