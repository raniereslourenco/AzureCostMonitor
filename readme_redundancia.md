# Redundância de Dados no Azure Storage
A redundância no Azure replica seus dados para protegê-los contra eventos planejados e não planejados, desde falhas transitórias de hardware até interrupções catastróficas.

## 1. Opções de Redundância
Ao configurar uma conta de armazenamento, você deve escolher o nível de resiliência necessário:

Opção,Sigla,Descrição,Escopo de Falha
Locally-redundant,LRS,Três cópias em um único data center.,Falha de disco/rack
Zone-redundant,ZRS,Três cópias em três zonas de disponibilidade distintas.,Falha de data center
Geo-redundant,GRS,Cópia síncrona (LRS) + cópia assíncrona em região secundária.,Falha regional
Geo-zone-redundant,GZRS,Cópia síncrona (ZRS) + cópia assíncrona em região secundária.,Falha regional + zona

## 2. Processo de Configuração
O processo de definição ocorre geralmente na criação do Storage Account, mas pode ser alterado posteriormente (com algumas limitações).

Passo a Passo no Portal:
Acesse o Portal do Azure e vá em "Storage Accounts".
Clique em Create.
Na aba Redundancy, selecione o modelo desejado.

Para opções Geo-redundantes, você pode habilitar o Read-access (RA-GRS), permitindo leitura na região secundária mesmo se a principal estiver online.

## 3. Insights e Melhores Práticas
Latência vs. Resiliência
LRS oferece a menor latência e o menor custo, sendo ideal para ambientes de desenvolvimento ou dados temporários.

ZRS é o "sweet spot" para alta disponibilidade dentro de uma região, protegendo contra incêndios ou quedas de energia em um prédio específico sem o custo da replicação geográfica.

RPO e RTO na Replicação Geo
No GRS e GZRS, a replicação para a região secundária é assíncrona.

RPO (Recovery Point Objective): Geralmente inferior a 15 minutos, mas não há SLA oficial para a defasagem de replicação.

Failover: Em caso de desastre regional, você pode iniciar um failover gerenciado pelo cliente, o que transforma a região secundária na primária.

## 4. Possibilidades Avançadas
Object Replication: Para maior granularidade, você pode configurar a replicação de blobs específicos entre diferentes contas de armazenamento (mesmo em regiões diferentes) sem precisar de GRS no nível da conta.

Immutability Policies: Combine redundância com políticas de imutabilidade (WORM) para proteger contra exclusões acidentais ou ataques de Ransomware, garantindo que as cópias replicadas também estejam protegidas.
