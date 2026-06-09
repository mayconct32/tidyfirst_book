# *Resumo do livro "TidyFirst?"*
###
<img src="/tidyfirst.jpg" alt="" width="550px" height="650px">

## Apresentação
Código bagunçado é um transtorno. É preciso fazer o "tidy" do código para que fique mais legível, e isso exige dividi-lo em seções gerenciáveis. Neste guia prático, o autor Kent Beck, criador da Extreme Programming e pioneiro dos padrões de software, sugere quando e onde podemos aplicar as tidyings a fim de melhorar o código, nunca se esquecendo da estrutura geral do sistema. 

## Parte Ⅰ
###
### Tidyings
"Tidyings são um subconjunto de refatorações. Tidyings são pequenas e adoráveis refatorações sutis, que ninguém poderia desaprovar."(pág 23 7-11)
### 1. Cláusulas de guarda
"Cláusulas de guarda se comportam como blocos condicionais ou verificações prévias que avaliam determinadas condições, antes de permitir que o algoritmo no código execute uma ação. Se a condicão for verdadeira, o algoritmo prossegue normalmente. Se a condicao for falsa, a cláusula de guarda direciona o algoritmo para outro 'caminho'. Muitas pessoas conhecem esse conceito como pré-condição."

Antes:
```python
if (condição):
    if (outra condicão):
        ...todo o resto do código da rotina...
```
Aplicando cláusulas de guarda:
```python
if (não atender a condição): return
if (outra condicão): return
...restante do código da rotina...
```

Fica mais fácil analisar o código com cláusulas de guarda porque as precondicoes sao explícitas.

