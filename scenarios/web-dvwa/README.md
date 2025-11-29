# Cenário: Web — DVWA (Damn Vulnerable Web App)

## Objetivo
Simular ataques de força bruta em um formulário de login (DVWA) em ambiente controlado para entender vetores, limitações e mitigação.

## Requisitos do lab
- DVWA rodando na VM vulnerável.
- Kali Linux na mesma rede host-only.
- Nível de segurança do DVWA: **Low** ou **Medium** (documente o nível exato antes do teste).
- Snapshot das VMs antes do começo.

**AS IMAGENS DO ATAQUE AO DVWA ESTAO NA PASTA IMAGENS\DVWA**

# Ataque a Formulários Web (DVWA)

Este documento descreve o passo a passo realizado para simular um ataque de força bruta contra o formulário de login do **DVWA (Damn Vulnerable Web Application)** utilizando o Medusa.

---

## 1. Acessando o Formulário Web Alvo

No navegador, acessamos o endereço do formulário que será atacado:

```
192.168.56.101/dvwa/login.php
```

**Imagem: pagina_dvwa.png**

---

## 2. Analisando o Tráfego via Ferramentas de Desenvolvedor

Abrimos o painel de desenvolvedor do navegador (DevTools) e acessamos a aba **Network**.

Nesta seção é possível analisar:

* O que o navegador **envia** ao servidor.
* O que o navegador **recebe** de resposta.

Em seguida, realizamos uma tentativa de login com qualquer credencial para capturar a requisição.

**Imagem: pagina_dvwa_developer.png**

---

## 3. Preparando as Worklists de Usuários e Senhas

Para realizar o brute force, devemos ter dois arquivos:

* `users.txt` → lista de usuários
* `pass.txt` → lista de senhas

Essas listas serão usadas pelo Medusa para testar combinações.

---

## 4. Executando o Ataque ao Formulário com Medusa

Com base nas informações capturadas na aba Network, executamos o comando do Medusa ajustado ao formulário DVWA:

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M http \
  -m MODULE:POST \
  -m FORM: 'username=^USERS^&password=^PASS^&Login=Login' \
  -m FAILURE: 'Login failed' \
  -m PATH: '/dvwa/login.php' \
  -t 6 \
  -f
```

* `FORM` define como os dados são enviados ao formulário.
* `FAILURE` define o texto retornado quando a tentativa falha.
* `PATH` aponta para o endpoint do login.

**Imagem: dvwa_success.png**

---

## 5. Validando Credenciais Encontradas

Após o Medusa retornar **SUCCESS**, validamos manualmente no navegador:

1. Digite novamente o endereço: `192.168.56.101/dvwa/login.php`.
2. Insira o usuário e senha que retornaram **SUCCESS**.

Se o login for aceito, o ataque foi bem-sucedido.

**Imagem: dvwa_success02.png**

---

## 6. Conclusão

Neste processo, demonstramos:

* Como identificar parâmetros de requisições web via DevTools.
* Como preparar listas de usuários e senhas.
* Como usar Medusa para bruteforce em formulários HTTP.
* Como validar o acesso obtido.

Este método é útil para entender vulnerabilidades em aplicações web inseguras como o DVWA.
