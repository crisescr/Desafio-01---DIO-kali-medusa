# Rules of Engagement

- Objetivo: atividades educativas em ambiente controlado.
- Alvo: apenas VMs locais configuradas (Kali, Metasploitable2, DVWA).
- Rede: usar Host-Only / Internal Network; **não** conectar as VMs à Internet.
- Snapshots: tirar snapshot antes de cada cenário.
- Limites: usar wordlists curtas; limitar tentativas por usuário; pausar entre tentativas.
- Evidências: salvar screenshots, outputs e gerar hash SHA256 para arquivos críticos.
- Ética: não executar testes contra sistemas que você não possui/tem autorização.

- # Rules of Engagement (Regras de Engajamento)

**Projeto:** Força Bruta com Kali + Medusa  
**Autor:** Seu Nome  
**Data:** YYYY-MM-DD  
**Propósito:** Atividade educacional dentro do curso DIO para aprender técnicas de auditoria em ambiente controlado.

## Escopo
- Alvos autorizados: VMs locais importadas para o lab — `Kali` (atacante), `Metasploitable2` e `DVWA` (alvos).
- Rede: VirtualBox Host-Only / Internal Network (sem conexão com Internet).

## Autorizações
- Testes autorizados pelo autor do repositório/ambiente (Só executar em VMs que você controla).
- Não executar contra ativos de terceiros sem autorização explícita por escrito.

## Limites e controles
- Wordlists curtas e educativas; **máximo 5 tentativas** por usuário por senha (ajustável por cenário).
- Pausa mínima entre blocos de tentativas: **5–60 segundos** conforme cenário.
- Não realizar ataques massivos ou paralelos que gerem flood no host.
- Não utilizar listas públicas massivas (rockyou etc.) neste repositório público.

## Snapshots e backups
- Tirar snapshot das VMs antes de cada cenário. Se algo falhar, restaurar snapshot para estado limpo.

## Coleta de evidências
- Evidências: screenshots, arquivos de saída (.txt) e hashes SHA256 dos arquivos de evidência.
- Não incluir senhas sensíveis em repositório público — use apenas senhas de teste curtas ou placeholders.

## Contingência
- Em caso de comportamento inesperado do host (ex.: travamento), restaurar snapshot e documentar o incidente em `incidents.md`.
- Se houver erro de configuração de rede ou impacto fora do lab, encerrar VMs imediatamente.

## Responsável / Contato
- Nome: CHRISTIE SOARES WALDEMAR
- E-mail: christiecwb@gmail.com
## Versões
- v1.0 — 02/11/2025 — Documento inicial.


add RULES and initial structure
