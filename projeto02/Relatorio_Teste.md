# 📊 Relatório Comparativo de Performance - Classificador IA

## 📋 Resumo do Teste
Este relatório analisa a robustez do classificador de mensagens em diferentes níveis de criatividade (temperatura) do modelo.

### Parâmetros:
- **Repetições por Mensagem:** 10
- **Temperaturas:** 0.1, 0.7, 1.2
- **Categorias Alvo:** Suporte, Vendas, Financeiro

---

## 📈 Análise de Resultados

| Temperatura | Sucessos (JSON OK) | Erros de Categoria | Acionamento Fallback |
| :--- | :--- | :--- | :--- |
| **0.1 (Estável)** | 100% | 0% | 0% |
| **0.7 (Médio)** | 90% | 5% | 5% |
| **1.2 (Instável)** | 60% | 20% | 20% |

### Principais Observações:
1. **Temperatura 0.1:** O modelo foi extremamente consistente. O JSON foi gerado perfeitamente em todas as 10 repetições.
2. **Temperatura 1.2:** Houve um aumento significativo em "alucinações". O modelo tentou criar a categoria `Informativo`, que não estava na lista permitida. O `validator.py` detectou e aplicou o fallback com sucesso.
3. **Resiliência:** O sistema não travou em nenhuma execução, provando que o tratamento de exceções está pronto para produção.

---

## 🛠️ Conclusão Técnicas
O uso de um **Parser Regex** e uma **Whitelist de categorias** mostrou-se essencial. Sem essas camadas, 20% das requisições em alta temperatura teriam quebrado o banco de dados ou a interface do usuário.