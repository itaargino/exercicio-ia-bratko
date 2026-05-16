## Exercício 21.2 - Análise Analítica (Predecessor)

O objetivo deste exercício é calcular o número exato de passos de refinamento necessários para o algoritmo MINIHYPER construir a definição do predicado recursivo `predecessor/2` a partir da hipótese inicial vazia.

### Como os Passos de Refinamento são Calculados
Cada passo de refinamento do MINIHYPER numa cláusula consiste estritamente em:
1. **Adicionar um literal de background** (BK) ao corpo da regra.
2. **Unificar duas variáveis** existentes na cláusula para criar as conexões lógicas.

#### Cláusula 1: Caso Base (`predecessor(A, B) :- parent(A, B).`)
* **Estado Inicial:** `[predecessor(X1, Y1)]`
* **Passo 1:** Adiciona o literal `parent(X3, Y3)`.
* **Passo 2:** Unifica a variável da cabeça `X1` com `X3`.
* **Passo 3:** Unifica a variável da cabeça `Y1` com `Y3`.
* *Subtotal: 3 passos.*

#### Cláusula 2: Caso Recursivo (`predecessor(C, D) :- parent(C, E), predecessor(E, D).`)
* **Estado Inicial:** `[predecessor(X2, Y2)]`
* **Passo 4:** Adiciona o literal `parent(X4, Y4)`.
* **Passo 5:** Adiciona o literal recursivo `predecessor(X5, Y5)`.
* **Passo 6:** Unifica `X2` com `X4` (conecta o início da cadeia).
* **Passo 7:** Unifica `Y4` com `X5` (passa o filho para a recursão).
* **Passo 8:** Unifica `Y5` com `Y2` (conecta o fim da cadeia ao objetivo).
* *Subtotal: 5 passos.*

---

## Resultados do Exercício 21.2

A tabela abaixo resume a contagem total de refinamentos exigida pelo interpretador:

| Cláusula Alvo | Refinamentos Aplicados | Passos Necessários | Profundidade Mínima (`MaxD`) |
| :--- | :--- | :---: | :---: |
| **Cláusula 1 (Caso Base)** | 1 Adição de Literal + 2 Unificações de Variáveis | **3** | - |
| **Cláusula 2 (Recursiva)** | 2 Adições de Literais + 3 Unificações de Variáveis | **5** | - |
| **Total Combinado** | **Transformação Completa da Hipótese** | **8** | **8** |

**Conclusão:** São necessários exatamente **8 passos de refinamento** no grafo de estados. O MINIHYPER encontraria esta solução assim que a busca por aprofundamento iterativo atingisse o nível **`MaxD = 8`**.
