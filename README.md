# *Resumo do livro "TidyFirst?"*
###
<img src="/tidyfirst.jpg" alt="" width="440px" height="570px">


## Apresentação
Código bagunçado é um transtorno. É preciso fazer o "tidy" do código para que fique mais legível, e isso exige dividi-lo em seções gerenciáveis. Neste guia prático, o autor Kent Beck, criador da Extreme Programming e pioneiro dos padrões de software, sugere quando e onde podemos aplicar as tidyings a fim de melhorar o código, nunca se esquecendo da estrutura geral do sistema. 


## Parte Ⅰ
###

### Tidyings
"Tidyings são um subconjunto de refatorações. Tidyings são pequenas e adoráveis refatorações sutis, que ninguém poderia desaprovar."(pág 23 7-11)

### 1. Cláusulas de guarda
"Cláusulas de guarda se comportam como blocos condicionais ou verificações prévias que avaliam determinadas condições, antes de permitir que o algoritmo no código execute uma ação. Se a condição for verdadeira, o algoritmo prossegue normalmente. Se a condicao for falsa, a cláusula de guarda direciona o algoritmo para outro 'caminho'. Muitas pessoas conhecem esse conceito como pré-condição."(pág 24 N.T)

Antes:
```js
if (condição){
    if (outra condição){
        ...todo o resto do código da rotina...
    }
}
```

Aplicando cláusulas de guarda:
```js
if (não atender a condição) return
if (outra condição) return
...restante do código da rotina...
```

Fica mais fácil analisar o código com cláusulas de guarda porque as precondições são explícitas.

### 2. Código morto

"Código morto [dead code] se refere a trechos do código-fonte que nunca são executados e não impactam o funcionamento de um programa"(pág 26 N.T)

"Remova. É sobre isso. Se o código não for executado, basta deletá-lo."(pág 26 1)

### 3. Normalize simetrias

Escolha um único padrão e aplique de forma consistente no projeto. Usar padrões de forma intercambiável, gera confusão e dificulta a manutenção.

"As coisas ficam confusas quando dois ou mais padrões são usados de maneira intercambiável"(pág 28 18-19)

### 4. Interface nova, implementação antiga

Seu projeto contém uma interface confusa, complicada ou difícil de usar? Basta implementar a nova interface chamando a interface antiga. O código existente continua funcionando da mesma forma, enquanto você melhora, muda ou incrementa a interface pela qual as outras partes do sistema interagem com ele.

### 5. Ordem de leitura

"Reordene o código no arquivo na ordem em que um reader preferiria encontrá-lo"(pág 31 5-6)

### 6. Ordem de coesão

Ordene o código, agrupando elementos que estão relacionados. Quando for modificá-los, será mais fácil caso precise fazer alterações, corrigir algum problema ou até mesmo implementar uma nova funcionalidade.

### 7. Mova declaração e inicialização juntas

"O nome de uma variável fornece uma dica sobre seu papel no processo de cálculo."(pág 34 1-2)

"Ao se deparar com um código que separa a declaração(com um tipo possível) e a inicialização, fica mais difícil de lê-lo."(pág 34 3-5)

Antes:
```js
function example(){
    int a
    //...algum código que não usa a variável "a"
    a = ...
    int b
    //...um pouco mais de código, talvez use "a" mas não use "b"
    b = ...a...
    //...algum código que usa "b"
}
```

Movendo declarações e inicializações juntas
```js
function example(){
    int a = ...
    //...algum código que não usa a variável "a"
    //...um pouco mais de código, talvez use "a" mas não use "b"
    int b = ...a...
    //...algum código que usa "b"
}
```

### 8. Explique as variáveis

Nomeie variáveis descrevendo seus valores. Extraia expressões em nomes autoexplicativos.

### 9. Explique as constantes

Crie uma constante simbólica. Substitua os usos da constante literal pelo símbolo.

Antes:
```js 
if (response.status_code === 404)
```

Explicando a constante:
```js 
if (response.status_code === 404_PAGE_NOT_FOUND)
```

### 10. Parâmetros explícitos
... 



