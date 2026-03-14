# lab-auditoria-controle-acessp-linux
Controle de Acesso em servidor Linux

"Distro: Kali Linux (versão 2025.4)"

Em 14/03/2026 
1 - "Configuração inicial do servidor Kali para laboratório de Auditoria e Controle de Acesso";

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






