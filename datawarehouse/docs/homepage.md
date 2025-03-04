{% docs __overview__ %}

# Projeto DBT-Core para Data Warehouse de Atenção Básica no Município

Este projeto utiliza DBT (Data Build Tool) para gerenciar e transformar dados de um Data Warehouse (DW) voltado para a Atenção Básica no Município. O objetivo é criar um pipeline de dados robusto e eficiente para tratar e organizar os dados relacionados à saúde básica, como planos de saúde e movimentações dos pacientes, facilitando a análise e a geração de insights.

## Estrutura do Projeto

### Fluxo do Processo ETL

O processo de ETL (Extração, Transformação e Carga) é dividido em etapas que permitem a organização e o tratamento dos dados. A seguir, está uma explicação das fases principais desse fluxo:

1. **Carga de Dados**:
   - **Leitura do CSV**: Os dados são inicialmente carregados a partir de arquivos CSV.
   - **Transformação Inicial**: Os dados passam por uma transformação inicial para adequação ao banco de dados.
   - **Inserção no PostgreSQL**: Após a transformação, os dados são carregados no banco PostgreSQL.

2. **Staging (stg)**:
   - **Limpeza de Dados**: Nessa etapa, os dados são limpos, removendo inconsistências ou registros desnecessários.
   - **Padronização de Colunas**: Aqui, os dados são estruturados conforme um padrão predefinido para facilitar a análise posterior.

3. **Mart (vw_mart)**:
   - **Aplicação de Regras de Negócio**: As regras de negócio são aplicadas para transformar os dados em informações relevantes.
   - **Criação de Indicadores**: Indicadores de desempenho e outros KPIs são gerados para facilitar a análise.

### Quantidade de Linhas

O projeto começa com **901.944** linhas de dados, provenientes dos arquivos CSV carregados. Após a aplicação das regras de negócio e transformações, o número de linhas é reduzido para **200.520**, refletindo a filtragem e a transformação dos dados conforme as exigências do modelo de negócio.

### Models

Os **models** definem as transformações de dados usando SQL. Eles são divididos em duas camadas principais: **staging** e **datamart**.

- **Staging**: A camada de staging prepara e limpa os dados antes de carregá-los nas tabelas finais de análise. Neste projeto, não há uma camada de staging separada para movimentações, já que os dados são extraídos diretamente de um Data Lake e não requerem essa pré-transformação.

- **Datamart**: A camada de datamart armazena os dados finais para análise. Os dados transformados são carregados diretamente para esse modelo. Um exemplo disso é o modelo `dm_atencao_basica_municipio.sql`, que aplica regras de negócio para incluir dados de planos de saúde e movimentações dos pacientes a partir de 2018, criando um modelo final para análise.

### Sources

Os **sources** são as tabelas ou arquivos de origem dos dados utilizados pelo DBT para realizar as transformações.

{% enddocs %}
