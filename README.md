# 🛡️ Mini SOC Lab  
### Auditoria, Hardening e Monitoramento de Servidores Linux

Projeto acadêmico desenvolvido na disciplina de **Segurança Cibernética**, com foco na construção de um ambiente de **Security Operations Center (SOC)** para auditoria, análise, mitigação e monitoramento contínuo de vulnerabilidades em servidores Linux.

---

## 📌 Objetivo

Implementar um laboratório prático para:

- Avaliar a postura de segurança de um servidor vulnerável
- Identificar falhas de configuração
- Aplicar hardening automatizado
- Monitorar eventos de segurança
- Validar melhorias após remediação

---

## 🏗️ Arquitetura do Ambiente

O laboratório foi estruturado com 4 máquinas virtuais conectadas em rede interna.

| Máquina | Função | IP |
|--------|------|----|
| Kali Linux | Análise ofensiva + automação | 192.168.56.10 |
| Ubuntu Server 22.04 | Servidor alvo | 192.168.56.20 |
| Wazuh | SIEM / Monitoramento | 192.168.56.30 |
| OpenVAS | Scanner de vulnerabilidades | 192.168.56.40 |

---

## 🔧 Ferramentas Utilizadas

### Auditoria e Compliance
- Lynis

### Monitoramento
- Wazuh

### Detecção
- rkhunter
- chkrootkit

### Varredura
- Nmap
- OpenVAS

### Automação
- Ansible

---

## ⚠️ Vulnerabilidades Simuladas

O servidor foi propositalmente configurado com falhas de segurança para análise:

- Configuração insegura de SSH
- Serviços desnecessários expostos
- Firewall desabilitado
- Permissões incorretas
- Logging comprometido
- Artefatos suspeitos
- Usuários inseguros

---

## 🔍 Auditoria Inicial

### Lynis

**Hardening Index:**  
`55/100`

Principais achados:

- SSH inseguro
- Serviços expostos
- Configuração fraca de autenticação
- Falhas de hardening

---

### rkhunter

**Warnings encontrados:**  
`1`

---

### Nmap

**Portas abertas:**  
`2`

Serviços identificados:

- SSH
- FTP

---

### OpenVAS

| Severidade | Quantidade |
|-----------|-----------|
| High | 0 |
| Medium | 1 |
| Low | 3 |

---

## 🚨 Monitoramento com Wazuh

Eventos simulados para validação:

- Tentativas de brute force SSH
- Modificação de arquivos críticos
- Criação de usuários
- Eventos de integridade

O Wazuh identificou os eventos e gerou alertas em tempo real.

---

## ⚙️ Hardening Automatizado

Aplicado via **Ansible Playbook**

### Correções implementadas

### SSH
- Desabilitação de root login
- Restrição de autenticação por senha
- Limitação de tentativas

### Firewall
- Ativação do UFW
- Política restritiva

### Sistema
- Correção de permissões
- Reativação de logs
- Remoção de artefatos inseguros

### Proteções adicionais
- Fail2ban
- Hardening via sysctl

---

## 📈 Resultados Pós-Hardening

| Ferramenta | Antes | Depois |
|-----------|------|--------|
| Lynis | 55/100 | 61/100 |
| rkhunter | 1 warning | 0 warnings |
| Nmap | 2 portas | 1 porta |
| OpenVAS | 0H / 1M / 3L | 0H / 0M / 2L |

---

## 🔗 Correlação entre Ferramentas

### SSH Inseguro
Detectado por:

- Lynis
- Nmap

Mitigado com:

- Ansible

---

### Alterações de Integridade

Detectadas por:

- Wazuh

Validadas por:

- Logs do sistema

---

### Exposição de Serviços

Identificada por:

- Nmap
- OpenVAS

Corrigida via:

- Hardening automatizado

---

## 📚 Competências Desenvolvidas

### Técnicas
- Hardening Linux
- Auditoria CIS
- SIEM
- Correlação de eventos
- Automação com Ansible
- Análise de vulnerabilidades

### Analíticas
- Interpretação de evidências
- Validação pós-remediação
- Investigação técnica

---

## 🚀 Melhorias Futuras

- Atualização do OpenSSH
- Política forte de senhas
- Auditoria periódica automatizada
- Regras customizadas no Wazuh
- Ampliação do playbook de hardening

---

## 📖 Aprendizados

Este projeto proporcionou experiência prática em:

- Operação básica de SOC
- Monitoramento defensivo
- Hardening automatizado
- Revalidação técnica
- Correlação entre ferramentas de segurança

---

## 👨‍💻 Autores

**Alisson F. Andrade**

**João Vitor Rodrigues chiarioni**

**Tiago Bezerra de Almeida Silva**  
Estudantes de Segurança Cibernética
