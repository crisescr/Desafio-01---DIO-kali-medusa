# Cenário: SMB — Enumeração e Password Spraying (Laboratório)

## Objetivo
Executar, de forma controlada, enumeração de serviço SMB e um teste de password-spraying limitado para entender riscos e mitigação em ambiente isolado.

## Requisitos do lab
- VM alvo com serviço SMB ativo (ex.: Metasploitable2 ou outra VM de testes).
- Kali Linux na mesma rede host-only.
- Snapshot das VMs antes dos testes.

## Wordlists
- `../../wordlists/smb-spray.txt` — lista curta de senhas.
- `../../wordlists/smb-users.txt` — lista curta de nomes de usuário (ex.: admin, user, test).

## Procedimento (passos)
1. **Enumeração**
   - Identifique portas SMB (ex.: `nmap -p 139,445 --script smb-os-discovery <IP>`).
   - Enumere compartilhamentos visíveis (`smbclient -L //<IP> -N` ou ferramentas de enumeração).
   - Documente banners e versões do serviço.
2. **Preparar lista de alvos**
   - Use uma lista curta de usuários (não mais que 5–10 nomes) para limitar o escopo.
3. **Password spraying controlado**
   - Para cada senha da lista curta, tente autenticar contra cada usuário, mas **máx. 1–2 tentativas por conta** antes de pausar. Ex.: tente `Password1` contra `user1`, `user2`, …; depois aguarde 60–120s; em seguida prossiga com a próxima senha.
   - Registre resultados em `scenarios/smb/smb-results.txt`.
4. **Validação**
   - Se houver sucesso, documente (screenshot do comando com saída, ou log salvo).
   - Salve evidências em `images/smb/`.

## Exemplos (alto-nível)
- Enumeração básica:
  - `nmap -p 139,445 --script smb-enum-shares,smb-os-discovery <IP>`
- Autenticação teste (exemplo de ferramenta): o uso de ferramentas como `smbclient` para testar credenciais de forma individual.
- **ATENÇÃO:** Não execute brute force massivo. Use apenas password-spraying com limites e pausas.

## Evidências esperadas
- `images/smb/01-nmap.png` — resultado da enumeração (portas / serviços).
- `images/smb/02-sharelist.png` — lista de shares visíveis.
- `images/smb/03-attempt.png` — tentativa de autenticação (terminal).
- `scenarios/smb/smb-results.txt` — resumo com timestamps e resultados.

## O que limitei / Por que
- Limitei número de usuários e senhas testadas e incluí pausas para evitar lockouts e comportamento de negação acidental. Em ambientes reais, password spraying funciona explorando contas com senhas fracas distribuídas — aqui queremos demonstrar o conceito sem causar danos.

## Recomendações de mitigação
- Implementar lockout progressivo e detecção de tentativas distribuídas.
- Forçar autenticação multi-factor (MFA) para recursos sensíveis.
- Revisar e reforçar políticas de senhas (expiração, complexidade) e proibindo senhas padrão.
- Monitoramento centralizado de autenticações e alertas para padrões de spray.
- Restringir acesso SMB por rede e segmentação adequada.

## Observações finais
- Registre sempre horário (UTC ou local) ao salvar resultados.
- Não deixe listas de usuários/senhas em repositórios públicos em produção — para o laboratório, mantenha apenas listas educacionais e curtas.
