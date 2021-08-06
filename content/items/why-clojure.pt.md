---
title: "Por que Clojure?"
author: ["Wanderson Ferreira"]
date: 2021-08-02T14:29:00-03:00
tags: ["clojure"]
draft: false
---

Nos últimos 5 anos eu precisei responder essa pergunta diversas vezes e eu
sempre dei uma resposta ruim. Vou tentar novamente, vamos iniciar com o porque
eu não consigo responder essa pergunta direito.

<!--more-->

---


## Contexto {#contexto}

Eu venho do meio acadêmico e assim que eu iniciei no desenvolvimento de software
eu percebi que **Opiniões pessoais são muitas vezes decisivas no processo de
tomada de decisões importantes**

Curioso porque eu não posso escolher minha explicação favorita para a teoria de
Tectônica de Placas em Geofísica, claramente você pode discordar com a teoria
vigente, porém precisa criar uma teoria bem sólida, dados para comprovar sua
teoria nova e esperar que diversos pesquisadores ao redor do mundo comprovem o
que você sugeriu. Logo, você deve esperar que isso não aconteça com muita
frequência quando falamos de "conceitos fundamentais".

Até mesmo para os conceitos menos prioritários nós tinhamos sempre um ótimo
decisor para julgar se a nova teoria era boa ou não: O Planeta Terra.

Se você jogar uma onda elétrica no solo e criar um mecanismo novo para medir a
resistividade, você pode facilmente testar se funcionou ou não pegando uma
amostra da rocha em profundidade e medindo a resistividade no seu laboratório.E
esse tipo de abordagem não é exclusivo para pesquisadores em universidades, se
você trabalha em empresas como a ExxonMobil ou Petrobras, você vai ter os mesmos
problemas e o planeta Terra vai continuar sendo o seu arbitro.

Mas agora, quais são os conceitos fundamentais do desenvolvimento de software?
Eles são facilmente mensuráveis? Melhor ainda, como esses conceitos impactam
empresas pequenas construindo sistemas para 1000 usuários no melhor cenário?

Eu nunca frequentei universidade de Ciência da Computação, mas eu imagino que
temos boas respostas para essas perguntas por lá, porém quando entramos no mundo
corporativo nós rapidamente nos apoiamos em "melhores práticas" do mercado que é
basicamente uma pilha de conselhos genéricos que a maioria da industria acordou
serem boas ideias.

E por que isso? É esquisito que os conceitos teóricos não façam parte do
dia-a-dia do programador. Talvez nós estamos mais próximo da teoria quando
pensamos em "estruturas de dados", "tempo de execução de algoritmos", etc. Porém
para todo o resto estamos a deriva.

O quão úteis são os conselhos de melhores práticas? Na minha opinião, não muito!

Se eu te falar "evite complexidade", o que isso significa? Certamente eu quero
evitar complexidade, mas como? e mais importante ainda, como eu posso evitar
dada as circunstancias especificas do meu projeto, da minha empresa, do meu
time, de quanto eu tenho disponível para gastar, do meu tempo disponível, e das
minhas habilidades?

Eu não sei, só evite complexidade.

Vamos adicionar a natureza do desenho de sistemas dentro dessa bola de
incertezas: Existem incontáveis formas de grudar um código um no outro para
fazer algo acontecer. Como nós dividimos o nosso problema em pedaços menores?
Como esses pedaços vão interagir? Como vamos levar em consideração que o futuro
pode mudar? Quais são as possíveis natureza dessas mudanças? Como elas se
manifestam dentro da empresa?

Impossível.

A quantidade de questões abertas é abismal.


## As opções {#as-opções}

Eu posso facilmente entender o porque um **time** escolhe Java/C# para criar seus
produtos. Nós temos muitas coisas para pensar e o Java/C# já existe por gerações
e simplesmente funciona. Google, Amazon, Netflix, e muitas outras empresas tem
muito código Java (e muito dinheiro também) rodando por ai. Podemos encontrar
respostas para as nossas dúvidas técnicas com facilidade online e temos um
vocabulário compartilhado para falar sobre algumas das "melhores práticas"
dentro da comunidade.

Eu posso facilmente entender o porque uma **pessoa** escolhe Java/C# para aprender
e se tornar proficiente. Temos muitas coisas para aprender sobre as linguagens,
temos que pagar nossas contas e por causa do que expliquei no paragrafo
anterior, nós também temos mais empregos dentro dessas comunidades.

---

Então, por que clojure?

Em idos de 2014 quando eu comecei a trabalhar regularmente com programação,
entrei em uma empresa que utilizava Orientação a Objetos. A quantidade de
jargões que usávamos naqueles dias eram insanos: Devemos usar um Padrão de
Factory? E Herança Multipla de X e Y? Vamos criar uma classe base Abstrata para
isso? O Padrão Visitor é útil aqui. Sim, vamos pensar se não estamos violando
LSP também. Talvez esse relacionamento não está mapeado corretamente na nossa
ORM, dai os objetos não são hidratados corretamente quando chamamos Z.

Incrível, nenhuma palavra sobre o nosso domínio de negocio. De fato, os
problemas de negocio acabavam sendo reformulados para se encaixar nessa nova
narrativa. Dai, 8 meses no futuro o mundo real nos mostrava algum cenário que
invalidava completamente alguma suposição critica que fizemos no passado para
manter o código mais "elegante".

De volta para a lousa!

Algumas vezes, de volta para re-escrever o programa inteiro.

---

Clojure é terrivelmente chato. Tem poucos construtores para serem aprendidos e
para 90% dos problemas de negocio por ai você nunca vai utilizar nenhuma
funcionalidade avançada. Um outro ponto interessante é que eu presenciei muitos
códigos bons utilizando conceitos de Orientação a Objetos escritos em Clojure o
que é bem interessante.

A maioria dos problemas de negocio atualmente estão relacionados com
processamento de informação. Basicamente, você recebe dados de uma fonte1, envia
dados pra um receptor2, coleta os resultados, modifica algum banco de dados ou
envia emails, e responde para fonte 1 com os resultados.

A comunidade Clojure também desenvolveu seus próprios conjuntos de "melhores
práticas" para desenvolver esse tipo de aplicação da forma mais simples
possível.

As consequências de ser uma linguagem pequena ficou bem claro para mim nos
ultimos trabalhos que tive: **nós eliminamos a linguagem do processo de
pensamento para solucionar problemas**

Eu nunca falo sobre Clojure quando eu discuto sobre algum problema de negocio
com meu time. Clojure é um detalhe de implementação. De fato é comum falar
coisas como: "Vamos criar um Protocolo para isso" ou "Deveriamos adicionar
validações de tipos para ter mais certeza sobre isso?" Mas de fato é muito
diferente do que esperar algum desenvolvedor senior ou arquiteto para explicar
que um conjunto especifico de classes não pode ser manipulada para executarmos X
porque no passado nós fizemos A, B, C, e D.

Claramente existem formas de programar algo de uma forma ruim, você também
precisa interagir com código existente e tomar cuidado para não quebrar nada.
Porém, não existe um conjunto de dor autoinfligida devido a relacionamentos
inventados entre as entidades de negocio no nosso sistema.

Eu concordo que as vezes é útil ter formas de restringir alguns relacionamentos
e impor invariantes no sistema. Dessa forma, existem maneiras de criar isso em
Clojure através do uso de Schemas e/ou Specs que se parecem com um "sistema de
tipagem" sob demanda.

O poder do estilo Funcional em si é algo que não dá para ignorar também. A
quantidade de carga cognitiva associada com a programação em Python (por
exemplo) é incrível, aceitamos e encorajamos isso. Mutação de dados e calls com
side-effects encoraja que você mantenha na sua cabeça alguns bons passos lógicos
do estado do seu programa em um dado instante. Tente seguir algum código das
bibliotecas SQLAlchemy ou Pandas, ou simplesmente tente entender alguns
`decoradores`, é uma maravilha. Se você consegue, eu tenho certeza que você se
sente bem esperto e deveria mesmo.

A sensação de entender algo complexo é muito boa, eu sinto bastante falta disso
para ser sincero. Talvez essa seja a explicação porque alguns projetos usam
tantos `macros` ("meta-programming") em Clojure.

---

O recurso matador do Clojure na minha opinião é que um grupo pequeno de pessoas
pode colaborar igualmente em diferentes níveis do projeto. Devido ao Clojure não
ter nenhum recurso super complicado na linguagem, o time pode focar sua atenção
em outros pontos:

-   entendimento compartilhado sobre a arquitetura (alto nivel)
-   entendimento compartilhado das capacidades atuais do sistema
-   melhorias em entendimento do código
-   melhorias em automações
-   melhorias em teste
-   melhorias em eficiência (baixo nivel e truques isolados)

E todo mundo consegue acompanhar.


## E o Python, Ruby, etc? {#e-o-python-ruby-etc}

Linguagens como o Python receberam uma atenção enorme nos últimos anos devido a
"facilidade" e a velocidade em desenvolver um bom protótipo de uma ideia. Além
disso, o Python ficou ainda mais relevante devido ao crescimento dos times de
Ciência de Dados.

Eu só posso falar sobre o Python nessa categoria porque não tenho experiencia
nas demais. É sem dúvida uma grande linguagem e eu nunca recomendaria para
alguem iniciando um time de Ciencia de Dados que começasse com Clojure ou
Elixir. Contudo, se você está criando um time de engenharia, eu consideraria
outra coisa.

-   Python é ótimo para prototipar, mas é bem difícil de entregar consistência entre times
    -   possibilita o uso de diversos estilos
    -   dependendo das suas experiencias prévias, você pode escrever algo que o time nunca tenha visto
    -   torna mais complicado de uma pessoa trafegar entre sistemas
-   Desperdício de recursos
    -   benchmarks variados indo de 30x até 200x mais lento que Java
    -   em um time grande, essa diferença implica em mais gastos com servidores
-   Falta de um bom suporte para problemas concorrentes
    -   Estamos em 2021, isso deve ser cada vez mais demandado
-   Estabilidade
    -   a linguagem em si recebe diversas funcionalidades novas a cada lançamento
    -   a comunidade não tem a mentalidade de manter retro compatibilidade com software existente
    -   clojure tem um núcleo da linguagem muito pequeno
        -   qualquer funcionalidade pode ser feita via bibliotecas
        -   vide o caso do `core.async` e `specs` como exemplos
    -   as bibliotecas em java são bem estáveis e testadas em produção por muitos anos

Esses são alguns aspectos do Python que importam para **mim**, logo você deve ter
os seus próprios motivos, certo? E como estamos em um mundo onde tudo é pessoal,
eu tenho certeza que você tem melhores formas de lidar com cada um dos pontos
que eu mencionei acima; por favor faça isso.

Um dos principais pontos atrativos do Python é que o gasto com servidores é
barato e o tempo para codificar qualquer coisa em Java é muito custoso, assim a
gente joga fora toda a fundação robusta e impressionante do Java (JVM) em nome
de velocidade ("produtividade"). Dai quando nosso produto se tornar um sucesso
nós vamos pensar no que fazer.

Para ser bem honesto, toda a premissa de que programadores Java/C# demoram mais
para desenvolver pode ser contestada quando comparamos a quantidade de dinheiro
que é investido por empresas gigantes na produção de melhores ferramentas para
os desenvolvedores.

Minha posição nisso tudo é que o Clojure me entrega o melhor dos dois mundos: Eu
posso usar toda a robustez do Java e JVM enquanto eu mantenho a mesma
produtividade de um programador Python.


## E no final, ... {#e-no-final-dot-dot-dot}

Mas, Clojure é a única resposta?

Definitivamente não. Se eu me juntar a uma empresa com experiencia em Microsoft,
eu nunca vou propor que joguem tudo fora e abracem o Clojure/JVM/Java. Contudo,
eu definitivamente sugeriria o uso do F#.

Eu escolheria a linguagem funcional alternativa à seja lá qual linguagem
convencional estejam utilizando no local.

No final, como isso nos ajuda a melhorar o cenário "opinionado" que encontramos
na industria de desenvolvimento de software? Não ajuda em nada!

Clojure tem suas próprias crenças e seus seguidores da mesma forma que qualquer
outra linguagem.

Esse é o principal motivo pelo qual minhas resposta são sempre ruins e o porque
você deveria continuar fazendo o que você quiser.