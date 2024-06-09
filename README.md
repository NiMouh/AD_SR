# Trabalho Prático 2 de Segurança em Redes de Computadores

## Autores

- Ana Vidal (118408)
- Simão Andrade (118345)

## Estrutura do Relatório

1. Introdução
2. Objetivo

## Introdução

## Objetivo

Definir regras SIEM para detetar comportamentos de rede anómalos e dispositivos possivelmente comprometidos. Testar as
regras definidas num registo de dados de fluxos de tráfego IP, identificando os dispositivos comprometidos.

Tarefas a realizar:

- [x] Análise dos comportamentos não anómalos (4 valores):
    - [x] Identificar servidores/serviços internos
    - [x] Descrever e quantificar as trocas de tráfego dos utilizadores internos com os servidores internos e externos
    - [x] Descrever e quantificar trocas de tráfego dos utilizadores externos com os servidores públicos da empresa
- [ ] Definição das regras SIEM (6 valores):
    - [ ] Respetiva justificação para a deteção de atividades BotNet internas
    - [ ] Exfiltração de dados usando HTTPS e/ou DNS
    - [ ] Atividades de C&C usando DNS e utilizadores externos usando os serviços públicos empresariais de forma anómala
- [ ] Teste das regras SIEM e identificação dos dispositivos com comportamentos anómalos (6 valores).
- [ ] Relatório (4 valores)

## Conteúdo utilizado

- Datasets: `dataset3.zip`
    - Dataset não anómalo: `dataset3.parquet`
    - Dataset anómalo: `teste3.parquet`
    - Dataset de servidores externos: `servers3.parquet`
- GeoIP_DB: `GeoIP_DB.zip`
    - Base de dados para identificar o *Autonomous System* (rede de IPs de uma organização) de um IP: `GeoIP_ASNum.dat`
    - Base de dados para identificar a localização geográfica de um IP: `GeoIP.dat`

## Processo de Análise

- Inicialmente:
    - [x] Ip's de origem e destino
    - [x] Portas comuns
    - [x] Protocolos comuns
    - [x] Número de pacotes (por src_ip)
    - [x] Rácio de download/upload (por src_ip)
    - [x] Localização geográfica dos IPs (dos dst_ip para cada src_ip)
    - [ ] Domínios DNS visitados (por src_ip)
    - [ ] Fazer mais análise às comunicações internas (src_ip e dst_ip)
    - [ ] Número de conexões por ~~hora~~ (por src_ip)

- Seguidamente:
    - [ ] Detetar atividades de BotNet (número de conexões por hora)
    - [ ] Detetar exfiltração de dados (Taxas anómalas de transferência de dados)
    - [ ] Detetar atividades de C&C (número e tamanho de pacotes DNS anómalo)

- Finalmente:
    - [x] Identificar dispositivos comprometidos (identificar os IPs que violam as regras definidas)
    - [ ] Tentar identificar o tipo de comprometimento (BotNet, exfiltração de dados, C&C)
    - [ ] Justificar a identificação dos dispositivos comprometidos

## Lista da Ana

Isto não dá para fazer:

- saber se o atacante está dentro ou fora da rede(a usar tunnels);

Determinar Download e upload:

- ver quais os utilizadores enviam tamanhos grandes de informação para fora da rede;
- duração de ‘download’ e ‘upload’ são importantes;
- Broswer != Https, obter o ratio de Upload < Download;
- Maioritáriamente temos mais ‘downloads’ que ‘uploads’ por utilizador;

Dados:

- média do número de conexões, por hora, por dia e criar assim o modelo;
- Anomalias de transferência de dados, o tipo de anomalia;

DNS:

- DNS/NON-DNS, ver domínios estranhos e logs;
- DNS de https, verificar comportamentos, se temos DNS cifrado que não o nosso, então ao histórico dos logs e ver;

## Regras SIEM

Nesta secção, são definidas regras SIEM para detetar comportamentos de rede anómalos e dispositivos possivelmente
comprometidos.

As regras seguem a seguinte estrutura:

1. **Detetar**: Descrição da atividade que se pretende detetar.
2. **Justificação**: Razão pela qual a atividade é considerada anómala.
3. **Regra**: Condição que, se verificada, deteta a atividade.

### Regras Identificadas

1. **Alta percentagem de tráfego enviado por um único utilizador**
    - **Detetar**: Atividades de BotNet
    - **Justificação**: BotNet é uma rede de dispositivos infetados com malware que são controlados remotamente por um
      atacante. Estes dispositivos enviam tráfego para um servidor C&C, que pode ser detetado por uma alta percentagem
      de tráfego enviada por um único utilizador.
    - **Regra**: Se um utilizador enviar mais de 2% do tráfego total, então detetar atividades de BotNet.

### Dispositivos comprometidos (Por completar)

A lista seguinte apresenta os dispositivos e o número de regras violadas correspondente:

| IP              | # |
|-----------------|:-:|
| 192.168.103.185 | 1 |
| 192.168.103.169 | 1 |
| 192.168.103.125 | 2 |
| 192.168.103.90  | 2 |
| 192.168.103.85  | 1 |
| 192.168.103.84  | 1 |
| 192.168.103.69  | 1 |

Pode-se então concluir que os dispositivos com os IPs ` ` estão de facto comprometidos.