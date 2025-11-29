# Boas Práticas de Segurança 

Este documento reúne medidas essenciais de mitigação baseadas **exclusivamente** nos três ataques simulados: **FTP**, **SMB** e **Formulário Web (DVWA)**.

---

## 1. FTP – Mitigação do Ataque de Brute Force

### Riscos observados no cenário simulado

* Senhas fracas e facilmente descobertas.
* Protocolo sem criptografia.
* Serviço exposto e sem limitação de tentativas.

### Boas práticas

* Substituir **FTP por SFTP ou FTPS**.
* Aplicar **políticas de senhas fortes**.
* Habilitar **bloqueio após tentativas falhas**.
* Restringir acesso ao serviço por IP ou firewall.
* Desabilitar login anônimo.
* Monitorar logs de autenticação.

---

## 2. SMB – Mitigação do Password Spraying

### Riscos observados no cenário simulado

* Enumeração de usuários via `enum4linux`.
* Várias tentativas de poucas senhas em muitos usuários.
* Acesso permitido com credenciais fracas.

### Boas práticas

* Exigir **senhas fortes e únicas** para cada usuário.
* Desabilitar **SMBv1**.
* Limitar tentativas de autenticação (lockout ou delays).
* Restringir portas **445/139** a redes confiáveis.
* Reduzir privilégios exagerados em contas SMB.
* Monitorar logs de falhas de login.

---

## 3. Formulário Web (DVWA) – Mitigação do Brute Force

### Riscos observados no cenário simulado

* Endpoint recebendo tentativas ilimitadas.
* Falta de proteções como CAPTCHA.
* Mensagem clara de falha ("Login failed").

### Boas práticas

* Implementar **CAPTCHA** após tentativas falhas.
* Aplicar **rate limiting** por IP e por usuário.
* Utilizar **HTTPS** para proteger credenciais.
* Mensagens de erro genéricas.
* Exigir senhas fortes aos usuários.
* Implementar **MFA** para contas administrativas.
* Monitorar tentativas suspeitas no `/login.php`.

---

## Conclusão

Os ataques simulados demonstram como serviços sem proteção adequada se tornam vulneráveis a brute force e password spraying. Com políticas fortes de autenticação, limitação de tentativas, protocolos seguros e monitoramento ativo, é possível mitigar de forma significativa estes riscos.
