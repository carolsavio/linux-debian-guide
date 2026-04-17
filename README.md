# 🐧 - GUIA COMPLETO PARA INICIANTES NO LINUX DEBIAN

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Debian](https://img.shields.io/badge/Debian-D1094E?style=for-the-badge&logo=debian&logoColor=white)
![MIT License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge&logo=opensourceinitiative&logoColor=white)

Comandos, conceitos do sistema, administração básica e rotinas práticas.

> **Objetivo do material:** explicar desde os conceitos fundamentais do Linux e do Debian até os comandos mais importantes do dia a dia, sempre com foco em compreensão e prática.

Versão produzida para estudo ***introdutório.***

## Índice

- [1. O que é Linux e o que é Debian](#1-o-que-e-linux-e-o-que-e-debian)
  - [1.1 Por que aprender Debian](#11-por-que-aprender-debian)
  - [1.2 Filosofia do sistema](#12-filosofia-do-sistema)
- [2. Como o sistema é organizado](#2-como-o-sistema-e-organizado)
  - [2.1 Multiusuário e multitarefa](#21-multiusuario-e-multitarefa)
- [3. Terminal, shell e primeiros comandos](#3-terminal-shell-e-primeiros-comandos)
  - [3.1 Anatomia de um comando](#31-anatomia-de-um-comando)
  - [3.2 Ajuda embutida](#32-ajuda-embutida)
- [4. Estrutura de diretórios do Debian](#4-estrutura-de-diretorios-do-debian)
  - [4.1 Diretórios que todo iniciante deve reconhecer](#41-diretorios-que-todo-iniciante-deve-reconhecer)
- [5. Navegação e manipulação de arquivos](#5-navegacao-e-manipulacao-de-arquivos)
  - [5.1 Caminhos absolutos e relativos](#51-caminhos-absolutos-e-relativos)
  - [5.2 Visualização e busca de conteúdo](#52-visualizacao-e-busca-de-conteudo)
- [6. Permissões, usuários e grupos](#6-permissoes-usuarios-e-grupos)
  - [6.1 O superusuário root e o sudo](#61-o-superusuario-root-e-o-sudo)
  - [6.2 Usuários e grupos na prática](#62-usuarios-e-grupos-na-pratica)
- [7. Gerenciamento de pacotes com APT e DPKG](#7-gerenciamento-de-pacotes-com-apt-e-dpkg)
  - [7.1 Pesquisar pacotes](#71-pesquisar-pacotes)
  - [7.2 Repositórios e fontes](#72-repositorios-e-fontes)
- [8. Processos, serviços e systemd](#8-processos-servicos-e-systemd)
  - [8.1 Serviços com systemctl](#81-servicos-com-systemctl)
  - [8.2 Boot e metas do sistema](#82-boot-e-metas-do-sistema)
- [9. Rede, conectividade e diagnósticos](#9-rede-conectividade-e-diagnosticos)
  - [9.1 DNS, gateway e portas](#91-dns-gateway-e-portas)
  - [9.2 SSH e acesso remoto](#92-ssh-e-acesso-remoto)
- [10. Disco, partições e uso de armazenamento](#10-disco-particoes-e-uso-de-armazenamento)
  - [10.1 Sistemas de arquivos e montagem](#101-sistemas-de-arquivos-e-montagem)
  - [10.2 Quando o disco enche](#102-quando-o-disco-enche)
- [11. Logs, troubleshooting e manutenção](#11-logs-troubleshooting-e-manutencao)
  - [11.1 Roteiro de diagnóstico](#111-roteiro-de-diagnostico)
- [12. Segurança básica e boas práticas](#12-seguranca-basica-e-boas-praticas)
  - [12.1 Firewall e exposição de serviços](#121-firewall-e-exposicao-de-servicos)
  - [12.2 Backup](#122-backup)
- [13. Fluxos práticos para o dia a dia](#13-fluxos-praticos-para-o-dia-a-dia)
  - [13.1 Atualizar o sistema com segurança](#131-atualizar-o-sistema-com-seguranca)
  - [13.2 Investigar por que um serviço falhou](#132-investigar-por-que-um-servico-falhou)
  - [13.3 Encontrar um arquivo de configuração](#133-encontrar-um-arquivo-de-configuracao)
  - [13.4 Entender consumo de recursos](#134-entender-consumo-de-recursos)
  - [13.5 Criar rotina de estudo](#135-criar-rotina-de-estudo)
- [14. Glossário e referência rápida](#14-glossario-e-referencia-rapida)
- [15. Tabela de comandos essenciais](#15-tabela-de-comandos-essenciais)
- [16. Encerramento](#16-encerramento)


# 1. O que é Linux e o que é Debian

**Resumo geral:** Linux é, em sentido estrito, o kernel: a parte central do sistema operacional responsável por conversar com o hardware, gerenciar memória, processos, dispositivos, sistema de arquivos e permissões. No uso cotidiano, porém, as pessoas chamam de “Linux” todo o conjunto formado por kernel, ferramentas de usuário, bibliotecas, shell e aplicações.

Debian é uma distribuição GNU/Linux. Isso significa que ele organiza o kernel Linux com um enorme ecossistema de pacotes, políticas de manutenção, documentação e ferramentas padronizadas. Uma distribuição existe para transformar várias peças técnicas em um sistema consistente, instalável, atualizado e utilizável.

O Debian é reconhecido por estabilidade, previsibilidade e aderência a padrões. Ele costuma ser muito usado em servidores, laboratórios, ambientes acadêmicos e também por usuários que preferem um sistema sólido e com grande repositório de software.


## 1.1 Por que aprender Debian

Aprender Debian ajuda a entender melhor o funcionamento geral do mundo Linux. Muitas distribuições derivam direta ou indiretamente dele, e vários conceitos fundamentais como ***APT, arquivos de configuração, permissões POSIX, systemd e hierarquia do sistema***, que aparecem também em outros sistemas GNU/Linux.

## 1.2 Filosofia do sistema

No Debian, praticamente tudo é arquivo, processo ou serviço. Configurações ficam em arquivos de texto; programas chegam por pacotes; serviços são geridos pelo systemd; usuários e grupos definem o controle de acesso. Esse desenho torna o sistema auditável e relativamente transparente para quem quer entender o que está acontecendo.

```bash
uname -a
cat /etc/os-release
hostnamectl
```

> O que esses comandos mostram: o kernel em uso, informações da distribuição instalada e dados do host, como nome da máquina e arquitetura.


---

# 2. Como o sistema é organizado

Para usar Debian com segurança e eficiência, é importante enxergá-lo como um conjunto de camadas. Na base está o hardware. Sobre ele, o kernel controla CPU, RAM, discos, interfaces de rede e dispositivos. Acima do kernel ficam bibliotecas e utilitários. O shell oferece uma interface textual para executar comandos. Em paralelo, podem existir interface gráfica, serviços em segundo plano e aplicações instaladas pelo usuário.

| Camada | Função | Exemplos |
| --- | --- | --- |
| Hardware | Componentes físicos | CPU, RAM, SSD, placa de rede |
| Kernel | Gerência de recursos e dispositivos | Linux |
| Espaço de usuário | Comandos, bibliotecas e utilitários | coreutils, bash, glibc |
| Serviços | Rotinas em segundo plano | ssh, cron, nginx |
| Aplicações | Programas usados pelo usuário | nano, vim, firefox |

## 2.1 Multiusuário e multitarefa

O Debian é um sistema multiusuário: mais de uma conta pode existir, cada uma com seu próprio diretório pessoal, permissões e contexto. Ele também é multitarefa: diversos processos executam ao mesmo tempo, disputando CPU, memória e dispositivos sob coordenação do kernel.


---

# 3. Terminal, shell e primeiros comandos

O terminal é a janela ou console em que você digita comandos. O shell é o interpretador desses comandos, sendo o Bash um dos mais comuns no Debian. O shell recebe o texto digitado, interpreta operadores, variáveis, pipes, redirecionamentos e então executa programas.

> Terminal x Shell: terminal é a interface; shell é o programa que interpreta o que você digita.

## 3.1 Anatomia de um comando

Normalmente um comando é composto por nome do programa, opções e argumentos. Exemplo: ls -lah /etc. Nesse caso, ls é o programa, -lah são opções e /etc é o argumento que indica qual diretório listar.

```bash
pwd
ls
ls -lah
whoami
id
date
cal
```

pwd mostra o diretório atual. ls lista arquivos. whoami mostra o usuário atual. id exibe UID, GID e grupos. date informa data e hora do sistema.

## 3.2 Ajuda embutida

```bash
man ls
ls --help
apropos network
info bash
```

Um usuário iniciante cresce muito quando passa a usar as páginas de manual. O comando man abre a documentação oficial instalada localmente. O parâmetro --help costuma mostrar um resumo rápido. apropos pesquisa tópicos relacionados.

> Boa prática: não decorar tudo é normal. O mais importante no início é saber procurar, testar e interpretar a ajuda dos comandos.


---

# 4. Estrutura de diretórios do Debian

O Debian segue a hierarquia tradicional de sistemas Unix. Em vez de letras de unidade como em alguns outros sistemas operacionais, quase tudo parte de uma raiz única, representada por /. Discos, partições e mídias são montados dentro dessa árvore.

| Diretório | Papel principal |
| --- | --- |
| / | Raiz do sistema; ponto inicial da árvore de diretórios |
| /home | Diretórios pessoais dos usuários |
| /root | Diretório pessoal do superusuário root |
| /etc | Arquivos de configuração do sistema |
| /var | Dados variáveis: logs, cache, filas, bancos locais |
| /usr | Programas, bibliotecas e documentação |
| /bin e /sbin | Comandos essenciais e utilitários administrativos |
| /tmp | Arquivos temporários |
| /dev | Arquivos de dispositivos |
| /proc | Informações do kernel e processos em pseudoarquivos |
| /sys | Interface do kernel com dispositivos e subsistemas |
| /mnt e /media | Pontos de montagem |

## 4.1 Diretórios que todo iniciante deve reconhecer

Três áreas merecem atenção especial no começo: /home, porque concentra seus arquivos pessoais; /etc, porque contém a maior parte das configurações; e /var/log, porque é um dos primeiros lugares a consultar quando algo falha.


---

# 5. Navegação e manipulação de arquivos

```bash
cd /etc
cd ~
cd ..
mkdir projetos
touch anotacoes.txt
cp arquivo1.txt copia.txt
mv copia.txt backup.txt
rm backup.txt
rm -r pasta_antiga
```

cd altera o diretório atual. mkdir cria diretórios. touch cria arquivos vazios ou atualiza timestamps. cp copia. mv move ou renomeia. rm remove. O uso de rm -r exige cuidado, pois pode apagar árvores inteiras de diretórios.

## 5.1 Caminhos absolutos e relativos

Um caminho absoluto começa na raiz, como /etc/ssh/sshd_config. Um caminho relativo parte do diretório atual, como documentos/notas.txt. Saber a diferença evita erros e facilita scripts.

## 5.2 Visualização e busca de conteúdo

```bash
cat arquivo.txt
less arquivo.txt
head -n 20 arquivo.txt
tail -n 50 arquivo.txt
wc -l arquivo.txt
grep -i "erro" /var/log/syslog
find /etc -name "*.conf"
```

cat imprime o conteúdo inteiro. less permite navegação paginada. head e tail mostram começo e fim. grep filtra linhas por padrão. find percorre diretórios em busca de nomes ou critérios.

> Combinação poderosa: grep, find, sort, cut, awk e pipes formam um conjunto extremamente útil para análise textual e automação.


---

# 6. Permissões, usuários e grupos

O modelo de permissões tradicional no Linux baseia-se em usuário dono, grupo dono e outros usuários. Para cada classe, há permissões de leitura (r), escrita (w) e execução (x).

```bash
ls -l
chmod u+x script.sh
chmod 644 arquivo.txt
chmod 755 pasta_script
chown usuario:grupo arquivo.txt
```

Quando você executa ls -l, vê uma coluna como -rwxr-xr--. Ela representa o tipo do arquivo e as permissões. chmod altera permissões. chown muda dono e grupo.

## 6.1 O superusuário root e o sudo

A conta root tem poder total sobre o sistema. Em vez de permanecer logado nela o tempo todo, o mais seguro é elevar privilégios apenas quando necessário, usando sudo.

```bash
sudo -i
sudo apt update
sudo systemctl restart ssh
```

> Cuidado operacional: com privilégios de root, um erro simples pode afetar o sistema inteiro. Sempre releia comandos destrutivos antes de pressionar Enter.

## 6.2 Usuários e grupos na prática

```bash
getent passwd
getent group
sudo adduser novo_usuario
sudo usermod -aG sudo novo_usuario
groups
passwd
```

Usuários possuem identidade própria no sistema. Grupos servem para delegar acesso coletivo a arquivos, dispositivos e comandos. O grupo sudo, por exemplo, geralmente concede capacidade de execução administrativa mediante autenticação.


---

# 7. Gerenciamento de pacotes com APT e DPKG

No Debian, software é distribuído principalmente por pacotes .deb. O dpkg instala e registra pacotes locais. O APT trabalha num nível mais alto: consulta repositórios, resolve dependências, baixa pacotes e coordena instalações, atualizações e remoções.

```bash
sudo apt update
sudo apt upgrade
sudo apt full-upgrade
sudo apt install curl
sudo apt remove nano
sudo apt purge pacote
sudo apt autoremove
```

apt update atualiza a lista local de pacotes disponíveis. apt upgrade instala versões mais novas sem remover pacotes para resolver conflitos. apt full-upgrade é mais agressivo e pode adicionar ou remover pacotes para completar a atualização.

## 7.1 Pesquisar pacotes

```bash
apt search nginx
apt show openssh-server
dpkg -l | grep ssh
which python3
```

apt search procura no catálogo. apt show exibe detalhes de um pacote. dpkg -l lista pacotes instalados. which mostra o executável encontrado no PATH.

## 7.2 Repositórios e fontes

```bash
cat /etc/apt/sources.list
ls /etc/apt/sources.list.d/
```

As fontes de pacotes ficam em arquivos como /etc/apt/sources.list. É importante adicionar repositórios extras com cuidado e preferência por fontes confiáveis, porque eles influenciam diretamente a integridade do sistema.

> Princípio de estabilidade: no Debian, misturar repositórios de origens ou versões incompatíveis pode quebrar dependências. Para iniciantes, o ideal é manter uma política conservadora.


---

# 8. Processos, serviços e systemd

Todo programa em execução é um processo. Cada processo possui PID, dono, prioridade, uso de CPU, uso de memória e estado. O systemd, adotado no Debian moderno, gerencia serviços, alvos de boot, logs e muito da inicialização do sistema.

```bash
ps aux
top
htop
pgrep ssh
kill PID
kill -9 PID
```

ps exibe instantâneos de processos. top mostra atividade em tempo real. kill envia sinais a processos. O sinal 9 (SIGKILL) encerra à força e deve ser reservado para casos em que sinais mais suaves não funcionam.

## 8.1 Serviços com systemctl

```bash
systemctl status ssh
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
sudo systemctl disable ssh
systemctl list-units --type=service
```

Serviços são programas que rodam em segundo plano, geralmente iniciados no boot ou sob demanda. Com systemctl você consulta estado, inicia, para, reinicia e habilita a inicialização automática.

## 8.2 Boot e metas do sistema

O systemd organiza a inicialização em unidades e targets. Em termos simples, targets representam estados desejados do sistema, como ambiente multiusuário ou ambiente gráfico. Isso substitui parte da lógica histórica dos runlevels, ainda mencionados em muita documentação.

> Conceito importante: nem todo programa precisa virar serviço. Ferramentas interativas rodam quando chamadas, serviços ficam disponíveis continuamente ou aguardando requisições.


---

# 9. Rede, conectividade e diagnósticos

```bash
ip a
ip route
ping -c 4 8.8.8.8
ping -c 4 debian.org
ss -tulpn
hostname -I
curl ifconfig.me
```

ip a mostra interfaces e endereços IP. ip route mostra rotas. ping testa conectividade ICMP. ss exibe portas e sockets abertos. hostname -I mostra IPs locais.

## 9.1 DNS, gateway e portas

Uma máquina pode ter rede funcionando no nível IP e ainda assim falhar em resolver nomes. Por isso, ao diagnosticar internet, separe o problema em etapas: interface ativa, IP obtido, gateway padrão, rota, resolução DNS e acesso a portas de destino.

```bash
resolvectl status
cat /etc/resolv.conf
nc -zv host porta
```

## 9.2 SSH e acesso remoto

```bash
sudo apt install openssh-server
systemctl status ssh
ssh usuario@ip_do_servidor
scp arquivo.txt usuario@ip:/destino/
```

SSH é a forma padrão de acesso remoto seguro em Linux. Permite terminal remoto, cópia de arquivos, túnel de portas e automação.

> Segurança em rede: evite expor serviços desnecessários. Se usar SSH, prefira autenticação por chave, mantenha o sistema atualizado e monitore tentativas suspeitas em logs.


---

# 10. Disco, partições e uso de armazenamento

```bash
lsblk
blkid
df -h
du -sh /var/log
mount
findmnt
```

lsblk mostra discos, partições e pontos de montagem. df -h mostra espaço livre em sistemas de arquivos montados. du mede uso de diretórios. mount e findmnt mostram como volumes estão montados.

## 10.1 Sistemas de arquivos e montagem

Em Linux, armazenar dados não é apenas ter um disco, é formatar partições com um sistema de arquivos, montá-las na árvore e controlar opções de montagem. No Debian, isso costuma ser definido em /etc/fstab para volumes persistentes.

```bash
cat /etc/fstab
```

## 10.2 Quando o disco enche

Quando falta espaço, verifique primeiro grandes diretórios em /var, caches, logs, backups e arquivos pessoais. Evite apagar arquivos do sistema sem saber a função deles. O correto é medir antes, entender a origem do crescimento e só então limpar.

```bash
sudo du -xh / | sort -h | tail -n 30
```

> Atenção: esse tipo de comando pode levar tempo e deve ser usado com bom senso em sistemas grandes.


---

# 11. Logs, troubleshooting e manutenção

No Debian, boa parte do diagnóstico depende de observar mensagens do sistema. Logs ajudam a reconstruir eventos: inicialização, falhas de serviços, erros de autenticação, problemas de disco, rede ou permissões.

```bash
journalctl -xe
journalctl -u ssh
journalctl -b
sudo tail -f /var/log/syslog
```

journalctl consulta os logs do systemd. A opção -u filtra por unidade. A opção -b mostra logs do boot atual. tail -f acompanha crescimento de arquivos em tempo real.

## 11.1 Roteiro de diagnóstico

Sempre que algo der errado, um roteiro útil é: identificar o sintoma exato, reproduzir, verificar código de retorno, consultar logs, confirmar permissões, rede e espaço em disco, e isolar se o problema está no programa, na configuração, no serviço ou no ambiente.

| Situação | Primeiros passos |
| --- | --- |
| Comando não encontrado | Verificar PATH, nome correto e se o pacote está instalado |
| Permissão negada | Checar dono, grupo, chmod, diretório pai e uso de sudo |
| Serviço não sobe | Consultar systemctl status e journalctl -u |
| Sem internet | Checar ip a, rota, gateway, DNS e firewall |
| Disco cheio | Usar df -h e du para localizar consumo |


---

# 12. Segurança básica e boas práticas

Segurança em Debian para iniciantes começa por princípios simples: manter o sistema atualizado, usar senhas fortes, limitar privilégios, instalar software de fontes confiáveis, entender o que cada comando faz e evitar trabalhar como root sem necessidade.

```bash
sudo apt update && sudo apt upgrade
sudo -l
last
who
w
```

Com last, who e w você observa sessões e usuários conectados. Isso ajuda em auditoria básica e em ambientes compartilhados.

## 12.1 Firewall e exposição de serviços

Mesmo em máquinas pessoais, é prudente saber quais portas estão abertas e quais serviços realmente precisam ficar acessíveis. Em servidores, essa disciplina é ainda mais importante.

## 12.2 Backup

Nenhuma prática de segurança é completa sem backup. Segurança não é apenas impedir invasão, é também garantir recuperação após erro humano, falha de disco ou corrupção de dados.


---

# 13. Fluxos práticos para o dia a dia

## 13.1 Atualizar o sistema com segurança

```bash
sudo apt update
sudo apt upgrade
sudo apt autoremove
```

Leia a saída dos comandos. Atualizar sem observar mensagens pode esconder pacotes retidos, conflitos ou serviços que exigem reinício.

## 13.2 Investigar por que um serviço falhou

```bash
systemctl status nome_do_servico
journalctl -u nome_do_servico -n 100 --no-pager
```

Esse fluxo é suficiente para resolver uma parte significativa dos problemas iniciais de serviços em Debian.

## 13.3 Encontrar um arquivo de configuração

```bash
find /etc -iname "*ssh*"
grep -Rin "Port" /etc/ssh/
```

## 13.4 Entender consumo de recursos

```bash
top
free -h
df -h
```

CPU, memória e disco formam o trio mais importante na triagem inicial de desempenho.

## 13.5 Criar rotina de estudo

Uma boa forma de aprender é escolher um pequeno tema por vez: navegar entre diretórios, editar arquivos com nano, consultar man pages, instalar pacotes simples, ler logs e compreender permissões. Repetição com entendimento vale mais do que decorar listas.


---

# 14. Glossário e referência rápida

| Termo | Explicação |
| --- | --- |
| Kernel | núcleo do sistema operacional |
| Shell | interpretador de comandos |
| Terminal | interface textual para interação |
| Pacote | unidade de distribuição de software |
| Repositório | fonte de pacotes |
| Processo | programa em execução |
| Serviço | processo de longa duração ou gerido pelo sistema |
| Permissão | regra de acesso a arquivos e diretórios |
| Root | superusuário com privilégios totais |
| Montagem | ato de anexar um sistema de arquivos à árvore de diretórios |


---

# 15. Tabela de comandos essenciais

| Comando | Uso | Exemplo |
| --- | --- | --- |
| pwd | Mostrar diretório atual | pwd |
| ls -lah | Listar arquivos com detalhes | ls -lah /etc |
| cd | Trocar de diretório | cd /var/log |
| cp | Copiar arquivo | cp a.txt b.txt |
| mv | Mover ou renomear | mv antigo novo |
| rm | Remover | rm arquivo.txt |
| grep | Buscar texto | grep -i erro arquivo.log |
| find | Localizar arquivos | find /etc -name '*.conf' |
| apt install | Instalar pacote | sudo apt install curl |
| systemctl status | Ver estado de serviço | systemctl status ssh |
| journalctl | Consultar logs | journalctl -u ssh |
| ip a | Ver interfaces | ip a |
| df -h | Ver espaço em disco | df -h |
| du -sh | Medir tamanho de diretório | du -sh /var/log |
| chmod | Alterar permissões | chmod 644 arquivo.txt |
| chown | Alterar dono/grupo | sudo chown user:user arquivo |


---

# 16. Encerramento

> O segredo do Debian é parar de tratar comando como "receita de bolo" e começar a olhar o que cada ferramenta realmente faz. O sistema te premia se você for organizado e prestar atenção nos detalhes. Quando você entende como a engrenagem gira, para de depender de tutorial pronto e começa a resolver as coisas sozinho, do diagnóstico à administração avançada.
