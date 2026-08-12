💻 **Como visualizar o painel**

Você pode interagir com o painel publicado através do link abaixo:
🔗 (https://app.powerbi.com/view?r=eyJrIjoiOTI2YTE2MjAtMGYxMC00OGY1LThjYzgtNmUwYjAyZWEzZDY4IiwidCI6IjhlYjI5MjAxLWEyN2QtNDMwMi04NDczLWM5ODJlYjViZTkzNSJ9)

📌 **Sobre o Projeto**

Este projeto é um painel interativo de People Analytics e Business Intelligence desenvolvido no Power BI, focado em mensurar a aderência da liderança (Supervisão, Gerência e Diretoria) à cultura organizacional de uma empresa multinacional. 

O objetivo principal deste dashboard é ir além da simples exibição de dados de RH, extraindo insights profundos que auxiliam na tomada de decisão da Diretoria Global. Ele diagnostica se os líderes estão focados apenas no compliance básico ou se estão atingindo níveis de Alta Performance, tudo isso encapsulado em uma interface UI/UX corporativa, limpa e responsiva, inspirada em sistemas de gestão de alto nível.

📊 **Telas, Funcionalidades e Soluções**

**1. Visão Geral (Big Numbers) e Saúde Cultural**
Uma visão macro da liderança, focada nos grandes KPIs de cultura e metas corporativas.
* **Métricas:** Quantidade de Líderes, % Aderência em Walking Management, % Compliance em Treinamentos, % Idioma (>= B2), % Performance (CPM) e % Recompensa (Bônus).
* 🎯 **Problemas Resolvidos (Business Questions):**
    * **Diagnóstico de Alta Performance:** A liderança entrega apenas a rotina reativa (treinamentos) ou realmente atinge a excelência esperada pela companhia?
    * **Comunicação Global:** Temos uma barreira linguística? O painel revela se o volume de líderes com inglês fluente é suficiente para sustentar operações globais.

**2. Tendências e Comportamento Operacional (Séries Temporais)**
Análise de evolução histórica para identificar a consistência das rotinas gerenciais ao longo do ano.
* **Métricas:** Aderência ao Walking Management por Mês (Gráfico de Linha).
* 🎯 **Problemas Resolvidos (Business Questions):**
    * **Constância vs. Sazonalidade:** Os líderes abandonam as rotinas de acompanhamento de equipe em meses de pico operacional? O painel identifica quedas bruscas de aderência (ex: meio do ano), permitindo intervenções preventivas do RH.

**3. Desempenho Tático e Análise Hierárquica**
Raio-X técnico cruzando os pilares de cultura com os níveis de cargo da liderança.
* **Métricas:** Indicadores de Idioma, Performance e Recompensa segmentados por Diretor, Gerente e Supervisor (Gráfico de Colunas Agrupadas).
* 🎯 **Problemas Resolvidos (Business Questions):**
    * **Mapeamento de Gargalos:** Onde o RH deve investir o orçamento de desenvolvimento? O visual revela se os problemas de performance e idioma estão concentrados na base da pirâmide (Supervisores) ou na alta gestão.

**4. Matriz de Ação e Feedback (Farol de Status)**
Tabela detalhada para ação tática imediata, focada no nível individual de cada colaborador.
* **Métricas:** Status binário (Aderente/Não Aderente) por líder em cada pilar, utilizando formatação condicional de ícones (✔️ e ❌).
* 🎯 **Problemas Resolvidos (Business Questions):**
    * **Gestão à Vista e Agilidade:** Como um Diretor sabe quem cobrar sem precisar exportar planilhas? A matriz permite identificar visualmente, em segundos, qual líder precisa de feedback e em qual pilar específico ele está falhando.

🧮 **Dicionário de Medidas DAX**

* **Qtd Lideres** = `COUNTROWS('dColaborador')`
* **% Aderencia WM** = `DIVIDE(SUM('fHistoricoWM'[Indicador WM]), [Qtd Lideres], 0)`
* **% Compliance Treinamentos** = `DIVIDE(SUM('dColaborador'[Indicador Treinamentos]), [Qtd Lideres], 0)`
* **% Indicador Idioma** = `DIVIDE(SUM('dColaborador'[Indicador Idioma]), [Qtd Lideres], 0)`
* **% Indicador Performance** = `DIVIDE(SUM('dColaborador'[Indicador Performance]), [Qtd Lideres], 0)`
* **% Indicador Recompensa** = `DIVIDE(SUM('dColaborador'[Indicador Recompensa]), [Qtd Lideres], 0)`

🛠️ **Modelagem e Arquitetura de Dados**

* **Engenharia de Features (ETL Avançado):** Transformação das regras de negócio em "Flags Binárias" (1 = Compliance, 0 = Não Compliance) diretamente no Power Query (M). Metas complexas (ex: Bônus > 60%) foram pré-calculadas na base para reduzir a carga de processamento do painel.
* **Lógica de Exclusão (Merge):** Cruzamento inteligente de dados para automatizar o status de treinamentos, onde IDs ausentes na lista de pendências receberam status positivo automaticamente.
* **Time Intelligence e Unpivot:** Reestruturação de bases matriciais (meses em colunas) para o formato tabular, permitindo a análise cronológica perfeita do Walking Management.
* **Star Schema:** Separação estrutural entre Tabela Dimensão (Colaboradores/Cargos) e Tabelas Fato (Treinamentos, Histórico Operacional), garantindo alta performance de filtragem.
* **Prevenção de Erros:** Uso de tratamentos para remoção de matrículas nulas/zeradas e utilização exclusiva da função `DIVIDE` no DAX para blindar o relatório contra erros de divisão por zero.
* **Design Nativo com Formatação Condicional:** Aplicação de regras visuais (Ícones Customizados) baseadas nos dados transformados no ETL, criando um sistema intuitivo de semáforo ("Farol") sem o uso de recursos externos pesados.
Prevenção de Erros: Uso de tratamentos para remoção de matrículas nulas/zeradas e utilização exclusiva da função DIVIDE no DAX para blindar o relatório contra erros de divisão por zero.

Design Nativo com Formatação Condicional: Aplicação de regras visuais (Ícones Customizados) baseadas nos dados transformados no ETL, criando um sistema intuitivo de semáforo ("Farol") sem o uso de recursos externos pesados.
