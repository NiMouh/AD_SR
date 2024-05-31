# Trabalho Prático 2 de Segurança em Redes de Computadores

## Autores

- Ana Vidal (118408)
- Simão Andrade (118345)

## Estrutura do Relatório

1. Introdução
2. Objetivo

## Introdução

## Objetivo

Definir regras SIEM para detetar comportamentos de rede anómalos e dispositivos possivelmente comprometidos. Testar as regras definidas num registo de dados de fluxos de tráfego IP, identificando os dispositivos comprometidos.

Tarefas a realizar:

- [ ] Análise dos comportamentos não anómalos (4 valores):
    - [ ] Identificar servidores/serviços internos
    - [ ] Descrever e quantificar as trocas de tráfego dos utilizadores internos com os servidores internos e externos
    - [ ] Descrever e quantificar trocas de tráfego dos utilizadores externos com os servidores públicos da empresa
- [ ] Definição das regras SIEM (6 valores):
    - [ ] Respetiva justificação para a deteção de atividades BotNet internas
    - [ ] Exfiltração de dados usando HTTPS e/ou DNS
    - [ ] Atividades de C&C usando DNS e utilizadores externos usando os serviços públicos empresariais de forma anómala
- [ ] Teste das regras SIEM e identificação dos dispositivos com comportamentos anómalos (6 valores).
- [ ] Relatório (4 valores)

## Conteúdo utilizado

- Datasets:
  - Dataset não anomolo: `dataset3.parquet`
  - Dataset anomalo: `teste3.parquet`
  - Dataset de servidores externos: `servers3.parquet`
- GeoIP_DB: `GeoIP_DB.zip`

## Lista de Tarefas

1º saber se o atacante está dentro ou fora da rede(a usar tunnels);
2º Ver quais os utilizadores enviam tamanhos grandes de informação para fora da rede;
Duração de download e upload são importantes;
Média do número de conexões, por hora, por dia e criar assim o modelo;
DNS/NON-DNS, ver domínios estranhos e logs;
DNS de https, verificar comportamentos, se temos DNS cifrado que não o nosso, então ao histórico dos logs e ver;
Broswer != Https,  obter o ration de Upload < Download;
Anomalias de transferência de dados, o tipo de anomalia;
Maioritária mente temos mais downloads que Uploads por utilizador;
Fazer verificações por conexões(TCP, UDP)