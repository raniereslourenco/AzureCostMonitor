# Monitoramento de Custos no Azure Data Factory (ADF)
Este documento detalha as estratégias, processos e ferramentas para monitorar e otimizar os custos no Azure Data Factory.

## Visão Geral do Processo
O monitoramento de custos no ADF não é centralizado em uma única tela; por esse motivo, eis uma visão 360°.

### 1. Configuração de Tags
O primeiro passo é a etiquetagem (tagging). Sem tags, enxergamos o custo total da instância do ADF, mas teremos dificuldade em distinguir quais projetos ou áreas estão consumindo mais.

Tags sugeridas: Environment (Dev/Prod), ProjectName, CostCenter.

### 2. Azure Cost Management + Billing
É aqui que a mágica acontece em nível macro.

Vá ao portal do Azure > Cost Management.

Filtre por Resource Type: Microsoft.DataFactory/factories.

Agrupe por Resource ou Tag para ver a distribuição de gastos.

### 3. Consumption Report no ADF Studio
Para uma visão granular (nível de pipeline), utilizamos o Monitor do próprio ADF.

No ADF Studio, vá em Monitor > Pipeline Runs.

Adicione a coluna Billable Duration e utilize o ícone de consumo (moeda) ao lado de cada execução para ver o detalhamento por Integration Runtime (IR).

# Insights de Otimização
Durante a implementação, alguns padrões são cruciais para essa otimização:

## Integration Runtime (IR) Selection
O uso de Azure IR em regiões mais baratas ou o ajuste do TTL (Time to Live) no Data Flow pode economizar até 30% em jobs recorrentes.

## Pipeline Overhead
Atividades de "Lookup" e "Get Metadata" são baratas, mas se executadas em loops infinitos ou frequências de segundos, o custo de orquestração acumula.

## Data Flow Clusters
O Data Flow utiliza clusters Spark. Configure o "Quick Re-use" para evitar o tempo de cold start (5 min) que é cobrado em cada execução.
