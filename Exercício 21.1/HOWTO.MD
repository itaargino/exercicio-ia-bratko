# Segundo Trabalho de IA - Programação Lógica Indutiva (ILP)

Este repositório contém os experimentos práticos realizados com o algoritmo **MINIHYPER** para indução lógica do predicado `has_daughter/1`.

## Como Executar

Para rodar os testes, abra o terminal na pasta do projeto, inicie o SWI-Prolog com o comando `swipl` e execute as instruções de acordo com o cenário desejado:

### Caso 1: Controle (Base Original)
```prolog
?- [mini_hyper, teste_1].
?- induce(H).
```
### Caso 2: Ausência Total de Contraexemplos(Certifique-se de que o arquivo possui a diretiva 
```prolog
?- [mini_hyper, teste_2].
?- induce(H).
```
### Caso 3: Amostra Positiva Incompleta (Sem a Pat)
```prolog
?- [mini_hyper, teste_3].
?- induce(H).
```
### Caso 3 Modificado: Amostra Incompleta com Overfitting
```prolog
?- [mini_hyper, teste_3_modificado].
?- induce(H).
```

### Caso 4: Conjunto Mínimo com Atalho Estrutural
```prolog
?- [mini_hyper, teste_4].
?- induce(H).
```

## Resultados
A tabela abaixo resume o comportamento do algoritmo e as regras geradas em cada um dos cenários discutidos:

| Caso de Teste | Alteração nos Dados | Profundidade (MaxD) | Hipótese Gerada (H) | Comportamento Lógico |
|---|---|---|---|---|
| 1. Controle | Dados originais da árvore | 4 | `[parent(A, B), female(B)]` | Convergência perfeita para a regra alvo real. |
| 2. Sem Negativos | Remoção de todos os `nex/1` | 0 | `[has_daughter(A)]` | Supergeneralização: assumiu por vacuidade que todos têm filhas. |
| 3. Sem Pat | Redução simples de exemplos positivos | 4 | `[parent(A, B), female(B)]` | Achou a regra geral correta por ser estruturalmente mais simples. |
| 3. Modificado | Pat movida para os negativos | 6 | `[parent(A, B), female(B), male(A)]` | Superespecificidade (overfitting): deduziu erroneamente que apenas homens têm filhas. |
| 4. Mínimo | Apenas Pat (E+) e Pam (E−) | 2 | `[parent(B, A)]` | “Atalho estrutural”: inverteu a lógica, definindo que ter filha é igual a ter pais. |
