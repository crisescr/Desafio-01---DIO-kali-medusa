# Cenário: FTP (Força Bruta)

Objetivo:
Testar força bruta de credenciais FTP em VM vulnerável (apenas laboratório).

Passos realizados:
1. Enumeração: verificação de porta FTP (ex.: nmap -sV -p 21 <IP>).
2. Wordlist usada: ../../wordlists/ftp-simple.txt
3. Ferramenta: Medusa (Kali) — execução controlada.
4. Limites aplicados: máximo 5 tentativas por usuário; pausa 5s entre usuários.

Evidências:
- images/ftp/01-enum.png
- images/ftp/02-attempt.png
- scenarios/ftp/ftp-results.txt

Recomendações:
- Habilitar lockout após N tentativas.
- Forçar uso de FTP sobre TLS (FTPS) ou SFTP.
- Políticas de senha fortes e monitoramento.

Observações:
Sempre restaurar snapshot após o teste se quiser repetir do estado limpo.
