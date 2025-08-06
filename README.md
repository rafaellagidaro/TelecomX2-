# ðŸ“Š AnÃ¡lise Preditiva de Rotatividade de Clientes

## ðŸš€ VisÃ£o Geral
Este projeto implementa uma soluÃ§Ã£o completa de machine learning para previsÃ£o de rotatividade de clientes (churn) utilizando dados histÃ³ricos. O sistema identifica clientes com risco de abandono e fornece insights acionÃ¡veis para estratÃ©gias de retenÃ§Ã£o.


## ðŸ”§ Tecnologias Utilizadas
**Linguagens e Frameworks:**
- ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
- ![Scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
- ![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
- ![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)

**Ferramentas:**
- ![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
- ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)
- ![Markdown](https://img.shields.io/badge/markdown-%23000000.svg?style=for-the-badge&logo=markdown&logoColor=white)

**TÃ©cnicas AvanÃ§adas:**
- SMOTE para balanceamento de classes
- OtimizaÃ§Ã£o de hiperparÃ¢metros com GridSearchCV
- ValidaÃ§Ã£o cruzada (5 folds)
- MÃ©tricas de avaliaÃ§Ã£o multicritÃ©rio

## ðŸ“‚ Estrutura do Projeto
```bash
â”œâ”€â”€ dados/                   # Pasta com conjuntos de dados
â”‚   â””â”€â”€ dados_df.csv         # Dataset principal
â”œâ”€â”€ notebooks/               # Jupyter notebooks
â”‚   â””â”€â”€ Challenge_TeleconX_Parte2.ipynb  # Notebook principal
â”œâ”€â”€ relatorios/              # RelatÃ³rios e visualizaÃ§Ãµes
â”‚   â”œâ”€â”€ metricas_modelos.png # Comparativo de mÃ©tricas
â”‚   â””â”€â”€ curva_roc.png        # Curva ROC comparativa
â”œâ”€â”€ README.md                # DocumentaÃ§Ã£o do projeto
â””â”€â”€ requirements.txt         # DependÃªncias do projeto
```

## âš™ï¸ ImplementaÃ§Ã£o

### ðŸ”„ Fluxo de Processamento
```mermaid
graph TD
    A[Carregamento de Dados] --> B[AnÃ¡lise ExploratÃ³ria]
    B --> C[PrÃ©-processamento]
    C --> D[DivisÃ£o Treino/Teste]
    D --> E[Balanceamento SMOTE]
    E --> F[Modelagem]
    F --> G[OtimizaÃ§Ã£o]
    G --> H[AvaliaÃ§Ã£o]
    H --> I[Deploy]
```

### ðŸ”‘ Componentes Chave
1. **PrÃ©-processamento Inteligente**
   - CodificaÃ§Ã£o de variÃ¡veis categÃ³ricas (One-Hot Encoding)
   - NormalizaÃ§Ã£o de features numÃ©ricas
   - Tratamento de dados ausentes

2. **Balanceamento EstratÃ©gico**
   ```python
   smote = SMOTE(random_state=42)
   X_train_res, y_train_res = smote.fit_resample(X_train, y_train)
   ```

3. **OtimizaÃ§Ã£o Rigorosa**
   ```python
   grid_search = GridSearchCV(
       pipeline,
       param_grid=params,
       cv=5,
       scoring='roc_auc',
       n_jobs=-1,
       verbose=1
   )
   ```

4. **AvaliaÃ§Ã£o Abrangente**
   ```python
   print(classification_report(y_test, y_pred))
   plot_confusion_matrix(model, X_test, y_test)
   ```

## ðŸ“ˆ Resultados e ConclusÃµes

### ComparaÃ§Ã£o de Modelos
| Modelo           | AUC Score | PrecisÃ£o (Churn) | Recall (Churn) | F1-Score (Churn) |
|------------------|-----------|------------------|----------------|------------------|
| Random Forest    | 0.8387    | 0.55             | 0.69           | 0.61             |
| Gradient Boosting| 0.8438    | 0.60             | 0.72           | 0.65             |

### Insights Principais
1. ðŸŽ¯ **Gradient Boosting** apresentou melhor desempenho geral (AUC = 0.8438)
2. âš–ï¸ EstratÃ©gia de SMOTE eficaz para lidar com desbalanceamento
3. ðŸ“‰ Modelos apresentam melhor performance na classe majoritÃ¡ria
4. â±ï¸ Features como `Charges.Total` e `EstÃ¡gio` sÃ£o altamente preditivas

## ðŸš€ RecomendaÃ§Ãµes para ProduÃ§Ã£o

### ImplementaÃ§Ã£o
```python
# Exemplo de API Flask para deploy
from flask import Flask, request, jsonify
import joblib

app = Flask(__name__)
model = joblib.load('melhor_modelo.pkl')

@app.route('/predict', methods=['POST'])
def predict():
    data = request.json
    prediction = model.predict_proba([data['features']])
    return jsonify({'churn_probability': prediction[0][1]})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### EstratÃ©gias de AÃ§Ã£o
1. **SegmentaÃ§Ã£o de Clientes**
   - Priorizar clientes com probabilidade >70% de churn
   - Oferecer planos personalizados

2. **Monitoramento ContÃ­nuo**
   - Recalibrar modelos trimestralmente
   - Acompanhar mudanÃ§as no perfil dos clientes

3. **IntegraÃ§Ã£o com CRM**
   ```mermaid
   sequenceDiagram
       Sistema ML->>CRM: Alertas de risco de churn
       CRM->>Agentes: NotificaÃ§Ãµes prioritÃ¡rias
       Agentes->>Cliente: Ofertas personalizadas
   ```

4. **KPI de Sucesso**
   - ReduÃ§Ã£o de 15% na taxa de churn em 6 meses
   - Aumento de 10% na receita por cliente

## ðŸ‘¨â€ðŸ’» Autor
**Jefferson Ferreira**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jefferson-ferreira-ds/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/francaferreira/)

**Principais ContribuiÃ§Ãµes:**
- ðŸ” AnÃ¡lise exploratÃ³ria de dados
- ðŸ¤– Desenvolvimento da pipeline de ML
- ðŸ“Š VisualizaÃ§Ã£o de resultados
- ðŸš€ ImplementaÃ§Ã£o da soluÃ§Ã£o

**PrÃ³ximos Passos:**
1. Desenvolver dashboard de monitoramento
2. Implementar sistema de alertas em tempo real
3. Testar tÃ©cnicas de deep learning
4. Expandir para previsÃ£o de lifetime value

---
