# Cenário: Web — DVWA (Damn Vulnerable Web App)

## Objetivo
Simular ataques de força bruta em um formulário de login (DVWA) em ambiente controlado para entender vetores, limitações e mitigação.

## Requisitos do lab
- DVWA rodando na VM vulnerável (Web server + MySQL).
- Kali Linux na mesma rede host-only.
- Nível de segurança do DVWA: **Low** ou **Medium** (documente o nível exato antes do teste).
- Snapshot das VMs antes do começo.

## Wordlists
- `../../wordlists/dvwa-small.txt` (lista curta para testes controlados)

## Procedimento (passos)
1. **Enumeração**
   - Verifique se a aplicação está acessível: abra `http://<IP_DVWA>/dvwa/` no navegador da VM Kali.
   - Anote a URL do formulário de login (ex.: `/dvwa/login.php`).
2. **Configurar o DVWA**
   - Ajuste o nível de segurança (na interface do DVWA) e documente o nível.
3. **Teste controlado**
   - Use um proxy (Burp) ou um script simples para enviar tentativas de login automatizadas com a wordlist curta.
   - Limites aplicados:
     - Máx. 5 senhas por usuário (teste por conta).
     - Pausa de 3–5 segundos entre tentativas.
     - Não usar força bruta em massa — o objetivo é didático.
4. **Validação**
   - Se um login for bem-sucedido, capture screenshot do painel logado e salve o request/response no proxy (ex.: `scenarios/web-dvwa/dvwa-http-log.txt`).
   - Salve um resumo em `scenarios/web-dvwa/dvwa-results.txt` com: usuário testado, senha encontrada (se houver), data/hora.

## Exem
