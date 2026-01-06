# 🛒 Segmentação de Clientes com K-Means & RFM

> **Status:** Concluído ✅  
> **Área:** Data Science / Marketing Analytics  
> **Tecnologias:** Python, Scikit-learn, Pandas, Plotly, PyGWalker

## 💼 O Problema de Negócio
Uma empresa de varejo precisava otimizar suas campanhas de marketing. O envio massivo de e-mails genéricos estava gerando baixo engajamento e alto custo. 

O objetivo deste projeto foi abandonar a intuição e utilizar **Machine Learning não-supervisionado** para segmentar a base de clientes automaticamente, permitindo ações personalizadas para:
1.  Reter os melhores clientes (VIPs).
2.  Recuperar clientes que pararam de comprar (Churn).
3.  Identificar novos potenciais (Promissores).

---

## 🛠️ Metodologia e Decisão Técnica

### 1. Engenharia de Atributos (RFM)
Transformei dados transacionais brutos em comportamento de compra:
* **Recency (R):** Dias desde a última compra.
* **Frequency (F):** Quantidade total de compras.
* **Monetary (M):** Total gasto na história.

### 2. Definição do Número de Clusters (Elbow Method)
Para não "chutar" o número de grupos, utilizei o **Método do Cotovelo (Elbow Method)**. O gráfico abaixo mostra que a inércia (erro) diminui drasticamente até **K=4**, indicando que 4 é o número matemático ideal de segmentos para esta base.

![Gráfico Elbow Method](Metodo-cotovelo.png)

---

## 🔍 Resultados e Insight de Negócio

O algoritmo identificou 4 perfis distintos. Porém, a maior descoberta veio na análise pós-modelagem.

### O Fenômeno "Churned VIP"
Identificamos clientes matematicamente classificados como VIPs (alto gasto histórico), mas que não compravam há mais de 1 ano. 
Aplicamos uma **Regra de Negócio** corretiva:
* **Regra:** Se `Cluster == VIP` e `Recency > 90 dias` ➔ Reclassificar para **"Churned VIP"**.
* **Impacto:** Apenas 3.5% dos VIPs demoram mais de 90 dias para voltar. Quem passa desse prazo é um risco crítico.

O gráfico abaixo mostra essa separação: os pontos em **Vermelho** são ex-VIPs que precisam de contato telefônico imediato, separados dos VIPs ativos (Dourado).

![Segmentação 2D com Churned VIP](Segmentacao-final-novo-cluster.png)

| Cluster Final | Perfil Comportamental | Ação Recomendada |
| :--- | :--- | :--- |
| **Champions (VIP)** | Compram a cada 12 dias, gastam 15x mais. | *Fidelidade e Atendimento Exclusivo.* |
| **Churned VIP** | Ex-VIPs inativos há >90 dias. | *Ligação pessoal (Resgate).* |
| **Novos / Promissores** | Recência baixa, mas poucas compras. | *Onboarding e Cross-sell.* |
| **Fiéis (Loyal)** | Boa frequência, gasto intermediário. | *Incentivos para aumentar Ticket Médio.* |
| **Perdidos (Lost)** | Inativos há > 6 meses. | *Campanhas de reativação massiva.* |

---

## 📊 Visualização 3D dos Clusters

Para entender a separação espacial das três variáveis (R, F, M) simultaneamente, geramos uma visualização tridimensional. 
Note como o grupo **VIP (Laranja)** se descola da massa no topo do eixo vertical (Monetário) e à esquerda (Recência zero).

![Cubo 3D RFM](separacao-espacial-RFM.png)

---

## 📦 Como Executar este Projeto

1. Clone o repositório:
   ```bash
   git clone https://github.com/lioradopacio/segmentacao-avancada-clientes-rfm-kmeans.git
