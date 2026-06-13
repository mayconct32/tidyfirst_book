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

Adicione parâmetros explícitos. Isso irá melhorar a legibilidade e a compreensão do código.

"É comum ver blocos de parâmetros passados em um mapeamento(dicionário). Isso dificulta ler e entender quais dados são necessários."(pág 39 6-7)

Antes:
```ts
function calcular_desconto(params){}
```

Aplicando parâmetros explícitos:
```ts
function calcular_desconto(preco: number, cupom: boolean){}
```

### 11. Segmente as instruções

"Insira uma linha em branco entre as partes."(pág 40 3)

"Essa aqui se destaca como a tidying mais simples."(pág 40 1)

### 12. Extraia o helper

Helper -> função(ou método) auxiliar criado para isolar um pedaço de lógica que estava "escondido" dentro de um método maior

"Ao notar um bloco de código dentro de uma rotina que tem propósito óbvio e interação limitada com o resto do código na rotina. Extraia o bloco como uma rotina helper. Nomeie a rotina de acordo com o propósito(não como ela funciona)."(pág 41 1-4)

### 13. Um amontoado

Amontoado -> Um código que funciona, mas está bagunçado. Não tem separação clara de ideias, tudo está meio "misturado" num lugar. 

Kent beck sugere para utilizarmos a técnica inline(substituição de chamadas de função pelo corpo da função em si, diretamente no local em que a chamada é feita), incorporando o máximo de código que puder, até que tudo fique em um grande amontoado. Fazendo o tidying a partir daquele ponto.

### 14. Explique os comentários

Se há um comentário explicando o que o trecho de código faz, transforme esse comentário em código, extraindo um método, renomeando uma variável ou reestruturando a lógica, até que o comentário se torne redundante e possa ser apagado.

Comente apenas o que não está óbvio no código. O comentário é o próprio código; se precisar explicá-lo, que seja algo útil.

### 15. Remova comentários redundantes

"Quando encontrar um comentário que diz exatamente o que o código diz, remova-o."(pág 46 1-2)

Comentário redundante:
```js
function getX(){
    // retorna X
    return x
}
```

## Parte II
###

### Gerenciamento

"Ser capaz de identificar quando uma tidying e aplicá-la não significa que você dominou a prática de tidyings. O título deste livro livro é Tidy First?, com ênfase no ponto de interrogação. Acho importante frisar que só porque pode fazer um tidy não significa que deve fazê-lo. Nesta seção, analisaremos como gerenciar tidyings e adequá-las em um fluxo de trabalho de desenvolvimento pessoal:

Quando começar a aplicar tidyings?
Quando parar de aplicar tidyings?
Como combinar tidyings, alterando a estrutura do código, com a mudaça do comportamento do sistema?"(pág 48 13-16)

### 16. Separe as tidyings

Separação de tidyings em um pull request

1. Tudo num commit só
   
- mais rápido, menos overhead (sobrecarga);
- dificulta revisão e rastreamento;
- aceitável em times pequenos com alta confiança.

2. Commits separados dentro do mesmo PR
   
- Um commit só com tidyings, outro com o comportamento;
- o revisor consegue ler separadamente, mas está tudo junto no PR;
- bom equilíbrio para a maioria dos times.

3. PRs completamente separados(é o ideal separar commits de alteração na estrutura em PRs separados)
   
- máxima clareza e separação;
- custo alto de overhead;
- vale quando o tidy é grande, arriscado, ou afeta muita gente.

Kent Beck não está prescrevendo uma regra, está pedindo para tornar visível a diferença entre estrutura e comportamento. Como você deve fazer depende do contexto.

### 17. Encadeamento

Cada tidying abre caminho para outra, conectando partes ou etapas de forma sequencial.

### 18. Tamanhos do lote

Quantas tidyings você deve fazer em cada pull request?

"Quanto mais tidyings por lote, maior será o delay antes da integração."(pág 57 10-11)

+ tidyings por lote -> Conflitos, interações, etc...
- tidyings por lote -> maior revisão

Cortar a revisão deixará a segunda opção como a melhor. Porém, funcionará apenas em times com grande confiança entre seus membros.


### 19. Ritmo

Gerencie o ritmo das tidyings.

"Dedicar mais de uma hora a uma tidying de cada vez, antes de fazer uma mudança de comportamento, provavelmente sinaliza que você perdeu a noção do conjunto mínimo de mudanças estruturais necessárias para possibilitar a mudança de comportamento desejada. Outra possibilidade, porém, é que o código esteja tão desorganizado que valha a pena dedicar horas às tidyings antes de fazer uma mudança de comportamento. Se isso é verdade, logo deixará de ser. O design de software tem forte tendência de 'pavimentar o caminho'."(pág 60 16-19 pág 61 1-4)

"Mesmo que a princípio você use muito as tidyings, logo se verá querendo fazer uma mudança de comportamento no código que já passou por tidying."(pág 61 17-19)

### 20. Descomplicando as coisas

Organizar suas ações dentro do código, sem misturar as mudanças dentro de um fluxo de trabalho.

"Quanto mais cedo perceber a necessidade de descomplicar as coisas, menos trabalho terá."(pág 63 10-11)

### 21. Primeiro, depois, mais tarde, nunca

Qual é o melhor momento para aplicar as tidyings?

**Primeiro** -> Há vantagens imediatas, quando vale a pena em termos de entendimento ou de mudanças de comportamento com custos menores. "Em geral, priorize fazer o tidy primeiro, mas tome cuidado para que o tidy não se torne o principal objetivo."(pág 68 5-6)

**Depois** -> Não encontrou lugares para fazer o tidying agora, ou não está em um contexto muito favorável para isso. Você mudará o comportamento nessa mesma área de novo? Se sim, faça logo após essa mudança, para facilitar as futuras mudanças de comportamento. O custo compensa?

**Mais tarde** -> Não tem tempo agora. Quando tiver tempo, faça. Às vezes, o contexto exige velocidade e você precisa entregar o mais rápido possível. "Há um lote enorme de tidyings para aplicar sem vantagem imediata."(pág 68 15-16)

**Nunca** -> "O melhor motivo é que não pretendemos mudar o comportamento do código nunca mais, em hipótese alguma."(pág 64 11-12)










