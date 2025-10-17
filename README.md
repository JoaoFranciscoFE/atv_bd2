# 🧠 Redis Lists — Entendendo o Tipo de Dado *List*

Explore o tipo de dado mais dinâmico do Redis e aprenda a manipular coleções ordenadas de elementos com facilidade.  
As *Lists* são perfeitas para filas, pilhas, histórico de ações e muito mais.

---

## 📘 O que é o Tipo List no Redis?

As **Lists** no Redis são coleções **ordenadas de strings**, que funcionam como uma sequência encadeada.  
Elas permitem inserir e remover elementos tanto do **início (esquerda)** quanto do **fim (direita)** da lista.

Cada lista no Redis é identificada por uma **chave única**, e os elementos são armazenados na ordem em que foram inseridos.

📦 **Capacidade:** milhões de elementos por lista (limitado apenas pela memória)  
⚡ **Principais usos:** filas, pilhas, mensagens, logs e histórico de operações.

---

## 🧩 Quando Usar Lists no Redis?

### ✅ Casos de Uso Ideais

| 💡 **Cenário** | 🧠 **Descrição** |
|----------------|-----------------|
| **Filas de Processamento (Queue)** | Use `LPUSH` e `RPOP` para implementar uma fila FIFO. |
| **Pilhas (Stack)** | Use `LPUSH` e `LPOP` para criar uma estrutura LIFO simples. |
| **Histórico de Ações** | Armazene eventos recentes, logs ou histórico de usuários. |
| **Sistemas de Mensagens** | Gerencie mensagens entre serviços com operações atômicas. |

---

## ⚙️ Estrutura Lógica

Cada **chave** representa uma **lista ordenada de valores**.  
As operações de inserção e remoção acontecem nas extremidades — o que garante **alta performance** mesmo em listas grandes.

---

## 🔧 Principais Comandos de List

| **Comando** | **Descrição** | **Exemplo (Redis CLI)** |
|--------------|----------------|--------------------------|
| `LPUSH` | Adiciona um ou mais elementos no início (à esquerda) de uma lista. | `LPUSH tarefas_diarias "Revisar código"` |
| `RPUSH` | Adiciona um ou mais elementos no final (à direita) de uma lista. | `RPUSH tarefas_diarias "Comprar café"` |
| `LPOP` | Remove e retorna o primeiro elemento (da esquerda) de uma lista. | `LPOP tarefas_diarias` |
| `RPOP` | Remove e retorna o último elemento (da direita) de uma lista. | `RPOP tarefas_diarias` |
| `LRANGE` | Retorna um intervalo de elementos de uma lista. | `LRANGE tarefas_diarias 0 -1` |
| `LLEN` | Retorna o número de elementos em uma lista. | `LLEN tarefas_diarias` |
| `LREM` | Remove elementos de uma lista que correspondem a um valor específico. | `LREM tarefas_diarias 0 "Enviar e-mail"` |
| `LTRIM` | Reduz uma lista para que ela contenha apenas o intervalo de elementos especificado. | `LTRIM tarefas_diarias 0 0` |
| `LINDEX` | Retorna o elemento em uma posição (índice) específica de uma lista. | `LINDEX tarefas_diarias 0` |



Esses comandos formam a base das operações com **listas** no Redis,  
permitindo implementar estruturas de dados flexíveis com **alta eficiência**.

---

## 💻 Exemplos Práticos no Redis CLI

### 🧮 Exemplo 1 — Fila de Tarefas (FIFO)

# Adicionar tarefas no fim da fila
```
RPUSH fila:tarefas "Processar pedido #101"
RPUSH fila:tarefas "Processar pedido #102"
RPUSH fila:tarefas "Processar pedido #103"
```
# Ver todas as tarefas
```
LRANGE fila:tarefas 0 -1
```
# Consumir a primeira tarefa 
```
LPOP fila:tarefas
```
# Verificar quantas restam
```
LLEN fila:tarefas
```

### 🧮 Exemplo 2 — Pilha de ações (LIFO)

# Adicionar ações na pilha
```
LPUSH historico "Abrir documento"
LPUSH historico "Editar parágrafo"
LPUSH historico "Salvar alterações"
```
# Remover a última ação realizada
```
LPOP historico   # Retorna "Salvar alterações"
```
# Ver o histórico restante
```
LRANGE historico 0 -1
```

## 🧮 Exemplo 3 — Limitar o Tamanho da Lista

# Adicionar novos registros
```
LPUSH logs "Login sucesso"
LPUSH logs "Logout usuário"
LPUSH logs "Erro 404"
```
# Manter apenas os registros que estão dentro do intervalo  
```
LTRIM logs 0 1
```
# Listar logs atuais
```
LRANGE logs 0 -1
```

---

## 💡 Uso real: ideal para sistemas de métricas, páginas de produtos, monitoramento de eventos e dashboards analíticos.

Dica de Organização

Use namespaces nas chaves para organizar melhor seus dados
e facilitar operações em lote ou por domínio.
```
LPUSH fila:email "Enviar email de boas-vindas"
LPUSH fila:email "Enviar email de confirmação"
LPUSH fila:pagamentos "Processar pagamento #321"
```
## 📘 Padrão recomendado:
```
<domínio>:<entidade>
```
➡️ Exemplos:

- `fila:tarefas`
- `fila:email`
- `historico:usuarios`

## Benefícios das Lists

- ✅ Operações de inserção e remoção com complexidade O(1)
- ✅ Ideal para filas e pilhas em tempo real
- ✅ Estrutura simples e altamente eficiente
- ✅ Suporte a múltiplos produtores e consumidores

## Conclusão

- As Lists são uma ferramenta poderosa no Redis para lidar com sequências ordenadas de dados.
- Com comandos simples e operações eficientes, é possível implementar desde filas de tarefas até históricos de atividades de usuários com altíssimo desempenho.

---

📖 Referências

- 📘 Documento: "Redis — Entendendo o Tipo de Dado List"
- 🌐 Documentação oficial do Redis: https://redis.io/docs/latest/develop/data-types/lists/
