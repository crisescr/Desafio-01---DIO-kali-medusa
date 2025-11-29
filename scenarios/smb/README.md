# Ataque Password Spraying em SMB com Enumeração de Usuários

Este documento descreve o passo a passo realizado para simular um ataque **password spraying** contra o serviço **SMB** em um ambiente Metasploitable, utilizando enumeração de usuários e a ferramenta Medusa.

**AS IMAGENS DO ATAQUE ESTÃO NA PASTA IMAGENS\SMB**

---

## 1. Enumeração de Usuários no SMB

Com acesso prévio à rede (cenário exemplificando engenharia social, como phishing), iniciamos a enumeração do host alvo `192.168.56.101` utilizando **enum4linux**:

```bash
enum4linux -a 192.168.56.101 | tee enum4_output.txt
```

A saída completa é salva automaticamente no arquivo `enum4_output.txt`.

**Imagem: smb_01.png**

---

## 2. Revisando Usuários Identificados

Abrimos o arquivo gerado para inspecionar usuários reais:

```bash
less enum4_output.txt
```

O arquivo contém nomes reais de usuários presentes no sistema.

**Imagem: smb_02.png**

---

## 3. Criando a Wordlist de Usuários

Com os nomes identificados, criamos uma lista de usuários:

```bash
echo -e "user\nmsfadmin\nservice" > smb_users.txt
```

---

## 4. Criando Wordlist de Senhas

No ataque de password spraying, escolhemos **poucas senhas** e testamos contra **muitos usuários**.

Criamos uma pequena lista de senhas prováveis:

```bash
echo -e "password\n123456\nWelcome123\nmsfadmin" > senhas_spray.txt
```

**Imagem: smb_user_pass.png**

---

## 5. Executando o Password Spraying com Medusa

Agora realizamos o ataque utilizando o Medusa:

```bash
medusa -h 192.168.56.101 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50
```

* O Medusa testa todas as combinações usuário/senha.
* Se aparecer **SUCCESS / Account found**, significa que encontramos credenciais válidas.

**Imagem: smb_success.png**

---

## 6. Validando o Acesso SMB Encontrado

Com as credenciais válidas encontradas, testamos o acesso SMB:

```bash
smbclient -L //192.168.56.101 -U msfadmin
```

Se o login for aceito, teremos acesso às shares disponíveis.

**Imagem: smb_success02.png**

---

## 7. Conclusão

Realizamos com sucesso um ataque **password spraying** no serviço SMB:

* Enumeramos usuários reais.
* Criamos listas de usuários e senhas prováveis.
* Utilizamos o Medusa para testar combinações.
* Validamos credenciais e acesso efetivo ao servidor SMB.

Este processo demonstra como ataques com poucas senhas podem comprometer múltiplos usuários em sistemas mal configurados.
