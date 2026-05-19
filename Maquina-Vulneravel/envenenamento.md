# envenenamento.md

ubuntu:ubuntu
root:root

---

# 1. Configuração insegura do SSH

### Alterações realizadas

```
sudo nano /etc/ssh/sshd_config
```

Configurações aplicadas:

```
PermitRootLogin yes
PasswordAuthentication yes
MaxAuthTries 100
```

Validação e reinício:

```
sudo sshd -t
sudo systemctl restart ssh
```

### Vulnerabilidades introduzidas

* Login direto como **root permitido**
* Autenticação por senha habilitada (mais suscetível a brute force)
* Número excessivo de tentativas de login (facilita ataques automatizados)

---

# 2. Criação de usuários com credenciais fracas

### Comandos utilizados

```
sudo useradd -m user1
sudo useradd -m user2

echo "user1:admin123" | sudo chpasswd
echo "user2:123456" | sudo chpasswd

sudo usermod -s /bin/bash user1
sudo usermod -s /bin/bash user2
```

### Vulnerabilidades introduzidas

* Senhas extremamente fracas e previsíveis
* Usuários comuns com shell ativo (possível exploração pós-comprometimento)

---

# 3. Exposição de serviços inseguros

### Comandos utilizados

```
sudo apt install vsftpd openbsd-inetd

sudo systemctl enable vsftpd
sudo systemctl enable openbsd-inetd
```

### Vulnerabilidades introduzidas

* Serviço FTP (vsftpd) potencialmente exposto (tráfego não criptografado)
* Serviço Telnet via inetd (transmissão de credenciais em texto plano)
* Ampliação da superfície de ataque

---

# 4. Firewall desativado

### Comando utilizado

```
sudo ufw disable
```

### Vulnerabilidades introduzidas

* Nenhuma filtragem de tráfego
* Todas as portas potencialmente expostas
* Facilita varredura e exploração remota

---

# 5. Permissões incorretas em arquivos críticos

### Comandos utilizados

```
sudo chmod 777 /etc/passwd
sudo chmod 777 /etc/shadow
sudo chmod 777 /etc/cron.d

ls -l /etc/passwd
ls -l /etc/shadow
ls -ld /etc/cron.d
```

### Vulnerabilidades introduzidas

* `/etc/passwd`

  * Qualquer usuário pode modificar contas do sistema
* `/etc/shadow`

  * Hashes de senha expostos para leitura e escrita
* `/etc/cron.d`

  * Qualquer usuário pode criar tarefas executadas como root

---

# 6. Desativação de logs do sistema

### Comando utilizado

```
sudo systemctl disable --now rsyslog
```

### Vulnerabilidades introduzidas

* Ausência de logs de auditoria
* Dificuldade extrema em detectar invasões
* Impossibilidade de investigação forense

---

# 7. Desativação de proteções do kernel (sysctl)

### Comandos utilizados

```
sudo nano /etc/sysctl.conf
```

Conteúdo adicionado:

```
net.ipv4.conf.all.rp_filter = 0
net.ipv4.conf.default.rp_filter = 0
kernel.randomize_va_space = 0
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
```

Aplicação:

```
sudo sysctl -p
```

### Vulnerabilidades introduzidas

* `rp_filter = 0`

  * Permite spoofing de IP
* `kernel.randomize_va_space = 0`

  * Desativa ASLR (facilita exploração de memória)
* `accept_redirects = 0`

  * Embora pareça seguro, combinado com outras falhas pode facilitar manipulação de tráfego

---

# 🔴 Resumo Geral das Falhas

* Acesso root remoto permitido
* Senhas fracas e previsíveis
* Serviços inseguros expostos (FTP/Telnet)
* Firewall desativado
* Arquivos críticos com permissões 777
* Logs desativados
* Proteções do kernel desabilitadas