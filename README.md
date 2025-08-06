!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>Análise Preditiva de Rotatividade de Clientes</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 2rem;
      background-color: #f9f9f9;
      color: #333;
    }
    h1, h2, h3, h4 {
      color: #2c3e50;
    }
    code {
      background-color: #eee;
      padding: 3px 5px;
      border-radius: 4px;
    }
    pre {
      background-color: #eee;
      padding: 10px;
      border-radius: 6px;
      overflow-x: auto;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 1rem 0;
    }
    th, td {
      border: 1px solid #aaa;
      padding: 8px;
      text-align: center;
    }
    th {
      background-color: #ddd;
    }
    .badge {
      display: inline-block;
      margin-right: 5px;
    }
    a {
      color: #2980b9;
      text-decoration: none;
    }
  </style>
</head>
<body>

  <h1>📚 Análise Preditiva de Rotatividade de Clientes</h1>

  <h2>🚀 Visão Geral</h2>
  <p>Este projeto implementa uma solução completa de <em>machine learning</em> para previsão de rotatividade de clientes (churn) utilizando dados históricos. O sistema identifica clientes com risco de abandono e fornece insights acionáveis para estratégias de retenção.</p>

  <h2>🔧 Tecnologias Utilizadas</h2>
  <h3>Linguagens e Frameworks:</h3>
  <span class="badge">Python</span>
  <span class="badge">Scikit-learn</span>
  <span class="badge">Pandas</span>
  <span class="badge">Matplotlib</span>

  <h3>Ferramentas:</h3>
  <span class="badge">Jupyter Notebook</span>
  <span class="badge">Git</span>
  <span class="badge">Markdown</span>

  <h3>Técnicas Avançadas:</h3>
  <ul>
    <li>SMOTE para balanceamento de classes</li>
    <li>Otimização de hiperparâmetros com GridSearchCV</li>
    <li>Validação cruzada (5 folds)</li>
    <li>Métricas de avaliação multicritério</li>
  </ul>

  <h2>📂 Estrutura do Projeto</h2>
  <pre>
├── dados/
│   └── dados_df.csv
├── notebooks/
│   └── Challenge_TeleconX_Parte2.ipynb
├── relatorios/
│   ├── metricas_modelos.png
│   └── curva_roc.png
├── README.md
└── requirements.txt
  </pre>

  <h2>⚙️ Implementação</h2>
  <h3>🔧 Fluxo de Processamento</h3>
  <p><em>Ver gráfico de fluxo no README.md original com Mermaid</em></p>

  <h3>🔍 Componentes Chave</h3>
  <h4>1. Pré-processamento Inteligente</h4>
  <ul>
    <li>Codificação One-Hot</li>
    <li>Normalização</li>
    <li>Tratamento de nulos</li>
  </ul>

  <h4>2. Balanceamento com SMOTE</h4>
  <pre><code>smote = SMOTE(random_state=42)
X_train_res, y_train_res = smote.fit_resample(X_train, y_train)</code></pre>

  <h4>3. Otimização com GridSearch</h4>
  <pre><code>grid_search = GridSearchCV(
    pipeline,
    param_grid=params,
    cv=5,
    scoring='roc_auc',
    n_jobs=-1,
    verbose=1
)</code></pre>

  <h4>4. Avaliação</h4>
  <pre><code>print(classification_report(y_test, y_pred))
plot_confusion_matrix(model, X_test, y_test)</code></pre>

  <h2>📈 Resultados e Conclusões</h2>
  <h3>📊 Comparação de Modelos</h3>
  <table>
    <tr>
      <th>Modelo</th>
      <th>AUC Score</th>
      <th>Precisão</th>
      <th>Recall</th>
      <th>F1-Score</th>
    </tr>
    <tr>
      <td>Random Forest</td>
      <td>0.8387</td>
      <td>0.55</td>
      <td>0.69</td>
      <td>0.61</td>
    </tr>
    <tr>
      <td>Gradient Boosting</td>
      <td>0.8438</td>
      <td>0.60</td>
      <td>0.72</td>
      <td>0.65</td>
    </tr>
  </table>

  <h3>🔎 Insights</h3>
  <ul>
    <li>🎯 Gradient Boosting teve o melhor desempenho geral</li>
    <li>⚖️ SMOTE ajudou a melhorar o equilíbrio</li>
    <li>📎 Classe majoritária tem maior acurácia</li>
    <li>📌 Features mais preditivas: <code>Charges.Total</code> e <code>Estágio</code></li>
  </ul>

  <h2>🚀 Deploy e Estratégias</h2>
  <h3>API Flask (Exemplo)</h3>
  <pre><code>
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
  </code></pre>

  <h3>🎯 Estratégias de Ação</h3>
  <ul>
    <li>Segmentar clientes com risco > 70%</li>
    <li>Recalibrar modelo trimestralmente</li>
    <li>Enviar alertas ao CRM com prioridade</li>
    <li>Métricas: reduzir churn em 15%, aumentar receita em 10%</li>
  </ul>

  <h2>👩‍💻 Autora</h2>
  <p><strong>Bruna Rafaela Gidaro</strong></p>
  <p>

  <h3>Principais Contribuições:</h3>
  <ul>
    <li>🔍 Análise exploratória</li>
    <li>🤖 Desenvolvimento do pipeline</li>
    <li>📊 Visualização</li>
    <li>🚀 Implementação</li>
  </ul>

  <h3>Próximos Passos:</h3>
  <ul>
    <li>Dashboard de monitoramento</li>
    <li>Alertas em tempo real</li>
    <li>Testar Deep Learning</li>
    <li>Previsão de Lifetime Value</li>
  </ul>

</body>
</html>
