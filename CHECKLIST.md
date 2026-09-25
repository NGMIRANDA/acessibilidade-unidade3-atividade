# Checklist da atividade

**Arquivo a corrigir:** `index.html`
**Unidade 3 — HTML Semântico: a Base da Acessibilidade**

Este é o guia de verificação. O passo a passo da entrega (fork, GitHub Pages, Pull Request) está
no [`README.md`](README.md).

## O cenário.

A página da Harmonia Instrumentos Musicais **está no ar e parece funcionar**. Abra no navegador:
o layout está alinhado, as cores estão certas, os botões clicam. Nenhum cliente que enxerga.
reclamou.

Mas a loja recebeu uma reclamação de um cliente que usa leitor de tela: ele não consegue
encontrar o conteúdo principal, não sabe para onde os links levam e desistiu do formulário de
contato.

**Sua tarefa:** corrigir a estrutura HTML da página sem mudar a aparência dela.

## Regras

As regras completas estão no [`README.md`](README.md). Em resumo: conserte a estrutura, mantenha
o layout, sem JavaScript, e ARIA só onde o HTML nativo não resolve.

## Checklist de verificação

Percorra a página procurando cada item. Anote **onde** encontrou o problema e **qual tag** deveria
estar no lugar. Não há resposta única para todos os itens — argumente sua escolha.

### 1. Aparência disfarçada de significado

- [X] Existe algum texto em negrito ou itálico que na verdade tem **importância** ou **ênfase**? Qual tag deveria estar ali?
Sim. No trecho “as melhores marcas” foi usada a tag <b> e em “garantia estendida” foi usada a tag <i>. Se esses textos têm significado de importância ou ênfase, 
o mais adequado seria usar <strong> para importância e <em> para ênfase.

- [X] Existe algum sublinhado que pode ser confundido com link?
Sim. O texto “política de trocas” está dentro da tag <u>, deixando-o sublinhado. Isso pode fazer o usuário pensar que é um link, embora não seja clicável.

- [X] Existe alguma tag obsoleta que só controla tamanho de fonte?
Sim. Foi utilizada a tag <font size="6"> no texto “Categorias em destaque”. A tag <font> é obsoleta e o tamanho/aparência deveria ser definido por CSS. Como esse texto funciona como um título, também seria mais adequado utilizar uma tag de cabeçalho, como <h2> ou <h3>, conforme a hierarquia da página.

### 2. Hierarquia de cabeçalhos

- [X] Liste, na ordem, todos os cabeçalhos da página. Quantos `<h1>` existem?
Na ordem em que aparecem no HTML:
1. <h3>Guitarras</h3>
2. <h6>Guitarras Elétricas</h6>
3. <h2>Baterias</h2>
4. <h6>Bateria Eletrônica</h6>
5. <h3>Comparativo de modelos</h3>
6. <h3>Fale com um vendedor</h3>
Não existe nenhum <h1> na página.

- [X] Algum título "parece" título mas não usa tag de cabeçalho?
Sim. “Loja de Instrumentos” aparece como uma <div class="h1-falso">, embora visualmente tenha aparência de título principal.

- [X] Existe algum nível pulado (h1 → h3, h2 → h6)?
Sim. A página começa diretamente com um <h3> sem possuir um <h1> antes dele. Além disso, depois de “Guitarras” (h3) aparece “Guitarras Elétricas” (h6), pulando os níveis h4 e h5. Depois de “Baterias” (h2), também aparece diretamente “Bateria Eletrônica” (h6).

- [X] Algum cabeçalho foi escolhido pelo **tamanho** que produz, e não pelo nível que representa?
Há fortes indícios de que sim. O CSS define tamanhos específicos para h2, h3 e h6, inclusive fazendo h2 e h3 terem o mesmo tamanho de 21px e o h6 ter 17px. Isso sugere que as tags podem ter sido usadas mais pela aparência visual do que pela hierarquia semântica.

- [X] Desenhe a hierarquia final como um índice de livro. Ela faz sentido?
Uma organização semântica mais coerente seria:
H1 — Loja de Instrumentos

    H2 — Guitarras
        H3 — Guitarras Elétricas

    H2 — Baterias
        H3 — Bateria Eletrônica

    H2 — Categorias em destaque

    H2 — Comparativo de modelos

    H2 — Fale com um vendedor

### 3. Landmarks

- [X] A página tem cabeçalho de site? Está em `<header>`?
Sim, existe uma área que funciona como cabeçalho do site, onde aparecem “Harmonia Instrumentos Musicais” e o subtítulo “Tudo para o seu som desde 1998”. Porém, ela foi criada com <div id="topo">, e não com a tag semântica <header>.

- [X] A navegação principal está em `<nav>`?
Não. O menu principal está dentro de <div id="menu">, com vários links, mas não está envolvido pela tag <nav>.

- [X] Existe **mais de uma** área de navegação? Como um leitor de tela diferencia uma da outra?
Sim. Além do menu principal, existe a trilha de navegação com “Início > Guitarras > Guitarras Elétricas”. Ela também está em uma <div>, chamada #trilha, e não em <nav>.
Do jeito atual, um leitor de tela não recebe uma identificação semântica clara dessas duas áreas como navegações diferentes. O ideal seria usar duas tags <nav> com identificações distintas, por exemplo:
<nav aria-label="Navegação principal">
...
</nav>

<nav aria-label="Trilha de navegação">
...
</nav>

- [X] Onde começa e termina o conteúdo principal? Ele está em `<main>`?
O conteúdo principal começa na área <div id="conteudo">, onde aparece “Loja de Instrumentos”, e vai até o final do formulário “Fale com um vendedor”. Porém, essa área não está dentro de uma tag <main>.

- [X] O conteúdo complementar da lateral está em `<aside>`?
Não. A área “Conteúdo relacionado” funciona como conteúdo complementar, mas foi criada com <div class="lateral">, e não com <aside>.

- [X] O rodapé está em `<footer>`?
Não. O rodapé está em <div id="rodape">, apesar de claramente exercer a função de rodapé da página. O ideal seria usar <footer>.

- [X] O idioma da página está declarado na tag `<html>`?
Sim. A página declara corretamente o idioma com:
<html lang="pt-BR">

### 4. Tabelas

- [X] Quantas tabelas existem no arquivo? Todas contêm **dados tabulares**?
Existem 3 tabelas no arquivo. Duas delas são usadas para layout/posicionamento e apenas uma contém dados tabulares de verdade. As tabelas de layout aparecem no início da página e no cabeçalho, enquanto a tabela de dados é a de “Comparativo de modelos”.

- [X] Alguma tabela está sendo usada só para **posicionar** elementos na tela? O que substitui isso hoje?
Sim. As tabelas com class="layout" estão sendo usadas para organizar visualmente os elementos da página e do cabeçalho, e não para apresentar dados. Hoje, o mais adequado é usar CSS, principalmente Flexbox ou CSS Grid, para esse tipo de posicionamento.

- [X] A tabela de dados tem um título programático?
Não. Existe o texto “Comparativo de modelos” em um <h3> antes da tabela, mas a tabela não possui um <caption>, que seria o título associado programaticamente a ela.

- [X] As células de cabeçalho são `<th>` ou apenas `<td>` estilizadas?
São apenas <td> estilizadas com a classe cab. Isso acontece tanto na primeira linha, com Modelo, Captadores, Escala e Preço, quanto na primeira célula das linhas dos modelos. O mais adequado seria usar <th> para os cabeçalhos.

- [X] Existe indicação de qual cabeçalho pertence a qual linha/coluna?
Não. Como não existem <th> com atributos como scope="col" ou scope="row", o relacionamento entre os cabeçalhos e as células de dados não está explicitado semanticamente para leitores de tela.

- [X] Se o leitor de tela anunciar só "R$ 7.150,00", o usuário sabe de que modelo se trata?
Não necessariamente. O valor “R$ 7.150,00” pertence ao modelo Les Paul Standard, mas como a tabela não usa corretamente <th> e associações de cabeçalho, o leitor de tela pode não fornecer esse contexto ao usuário de forma clara.
<table>
  <caption>Comparativo de modelos</caption>
  <tr>
    <th scope="col">Modelo</th>
    <th scope="col">Captadores</th>
    <th scope="col">Escala</th>
    <th scope="col">Preço</th>
  </tr>

  <tr>
    <th scope="row">Les Paul Standard</th>
    <td>2 humbuckers</td>
    <td>628 mm</td>
    <td>R$ 7.150,00</td>
  </tr>
</table>

### 5. Links e botões

- [X] Leia **só** os textos dos links, sem o parágrafo em volta. Dá para saber o destino de cada um?
- Nem sempre. Existem links com textos genéricos como “clique aqui”, “Aqui” e “Saiba mais”. Fora do contexto do parágrafo, esses textos não deixam claro para onde o link leva.
Os links do menu, como “Início”, “Guitarras”, “Baterias”, “Teclados” e “Contato”, são mais claros porque o próprio texto já indica o destino.

- [X] Quantos links diferentes têm o mesmo texto? Eles levam ao mesmo lugar?
O texto “clique aqui” aparece mais de uma vez e leva para destinos diferentes. Um vai para politica.html, outro para catalogo.pdf e outro para blog.html. Portanto, o mesmo texto é usado para destinos diferentes, o que pode confundir usuários de leitores de tela.

- [X] Algum link abre em nova aba? O usuário é avisado?
Sim. O link do catálogo em PDF e o link do blog possuem target="_blank", portanto abrem em uma nova aba. Porém, o texto do link não avisa o usuário sobre isso.
Seria melhor usar algo como:
<a href="catalogo.pdf" target="_blank">
  Abrir catálogo em PDF (abre em nova aba)
</a>

- [X] O link do ícone do carrinho tem um nome acessível útil?
Parcialmente. O link contém apenas uma imagem com alt="carrinho". Isso fornece algum nome acessível, mas poderia ser mais claro, por exemplo “Ir para o carrinho de compras”, principalmente porque a função do link é navegar até carrinho.html.
Seria melhor usar algo como:
<a href="carrinho.html" aria-label="Ir para o carrinho de compras">
  <img src="..." alt="">
</a>
- [X] Existe algum elemento que **parece** botão mas não é `<button>`? Teste: dá para chegar nele só com Tab e ativar com Enter?
- Sim. Os elementos “Adicionar ao carrinho” são <div class="botao"> com onclick. Visualmente parecem botões, mas não são elementos <button>. Por padrão, uma <div> não entra na ordem de foco com a tecla Tab e não é ativada com Enter, o que prejudica o uso por teclado.
O ideal seria:
<button type="button" onclick="adicionarCarrinho(101)">
  Adicionar ao carrinho
</button
- [X] Existe algum `<a>` que **executa uma ação** em vez de navegar?
Sim. O “Enviar” do formulário foi criado como:
<a href="#" onclick="enviarFormulario()" class="botao">Enviar</a>
Nesse caso, o elemento está executando uma ação, e não navegando para outra página. Por isso, semanticamente deveria ser um <button>.
O mais adequado seria:
<button type="submit">Enviar</button>
- [X] Pergunta-guia para cada um: *isso navega ou isso executa uma ação?
A regra pode ser resumida assim:
Se leva o usuário para outra página, arquivo ou local → <a>
Se executa uma ação na página → <button>
No HTML analisado:
Início, Guitarras, Baterias, catálogo, blog etc. → navegam → <a>
Adicionar ao carrinho → executa ação → <button>
Enviar formulário → executa ação → <button>
Essa separação deixa a página mais semântica e mais acessível para quem utiliza teclado e tecnologias assistivas.

### 6. Listas

- [X] O menu do topo é uma lista de verdade?
- Não. O menu foi montado com vários <span> contendo links, e não com uma lista semântica.
O mais adequado seria usar uma lista não ordenada:
<ul>
  <li><a href="index.html">Início</a></li>
  <li><a href="guitarras.html">Guitarras</a></li>
  <li><a href="baterias.html">Baterias</a></li>
  <li><a href="teclados.html">Teclados</a></li>
  <li><a href="contato.html">Contato</a></li>
</ul>

- [X] Existe alguma sequência de itens separada por `<br>`?
Sim. Em “Categorias em destaque”, os itens estão separados apenas por <br>:
Guitarras e Baixos
Baterias e Percussão
Teclados e Sintetizadores
Microfones
Acessórios

- [X] Os produtos formam uma lista? E os links da barra lateral?
Sim, conceitualmente os produtos formam uma lista, porque existem vários itens do mesmo tipo, como Stratocaster HSS e Les Paul Standard. Porém, no HTML eles estão apenas em <div class="cartao">, sem <ul> e <li>.
Os links da barra lateral também formam um conjunto de itens relacionados, mas estão separados por <br><br>, sem uma estrutura de lista.

- [X] Em cada caso: a ordem importa? (`<ol>`) Ou não? (`<ul>`)
Nos casos encontrados, a ordem não parece ser essencial, então o mais adequado é usar <ul>.
Menu principal → <ul>
Categorias em destaque → <ul>
Produtos → <ul>
Links de conteúdo relacionado → <ul>
Não há, nesse trecho do arquivo, uma sequência em que a posição 1, 2, 3 etc. tenha significado suficiente para justificar <ol>.

### 7. Formulário

- [X] Cada campo tem um `<label>` de verdade?
Não. A maioria dos campos não possui uma tag <label> associada. Alguns usam apenas texto em <div> ou o próprio placeholder para identificar o campo. O único <label> visível no formulário é o de “Telefone”.

- [X] Algum campo é identificado **apenas** pelo placeholder? O que acontece quando o usuário começa a digitar?
Sim. Os campos de e-mail e senha, por exemplo, usam apenas o placeholder como identificação. Quando o usuário começa a digitar, esse texto desaparece, e ele pode perder a referência sobre qual informação aquele campo solicita.

- [X] Algum `<label>` existe mas não está associado ao campo? Teste clicando no texto do rótulo: o foco vai para o input?
- Sim. Existe um <label> com o texto “Telefone”, mas ele não possui o atributo for="telefone". Assim, não há uma associação explícita entre o rótulo e o campo <input id="telefone">. 

- [X] A obrigatoriedade é comunicada só pelo asterisco visual?
Sim. O formulário informa que os campos marcados com * são obrigatórios, mas não utiliza o atributo required nos campos. Assim, a obrigatoriedade está sendo indicada principalmente de forma visual.
O ideal seria, por exemplo
<label for="nome">Nome completo *</label>
<input type="text" id="nome" required>

- [X] As mensagens de erro dizem **qual campo**, **o que está errado** e **como corrigir**?
- Não. As mensagens dizem apenas “Erro.”, sem informar qual campo apresenta problema, o motivo do erro ou como o usuário deve corrigi-lo.
Uma mensagem melhor seria, por exemplo:
Digite um endereço de e-mail válido, como nome@exemplo.com.


- [X] As mensagens de erro estão programaticamente ligadas aos seus campos?
Não. As mensagens estão apenas em <div class="erro">Erro.</div> logo após alguns campos, mas não há atributos como aria-describedby ou aria-errormessage ligando o erro ao campo correspondente.

- [X] Os botões de rádio estão agrupados? Ao chegar neles, dá para saber **qual é a pergunta**?
- Os botões de rádio estão agrupados? Ao chegar neles, dá para saber qual é a pergunta?
  Eles estão parcialmente agrupados porque todos possuem name="turno", o que faz com que apenas uma opção possa ser selecionada por vez. Porém, a pergunta “Turno preferido para contato” está apenas em uma <div> e não em um <fieldset> com <legend>. Por isso, a relação entre a pergunta e as opções não está semanticamente bem definida.

O ideal seria:
<fieldset>
  <legend>Turno preferido para contato</legend>

  <input type="radio" name="turno" id="manha">
  <label for="manha">Manhã</label>

  <input type="radio" name="turno" id="tarde">
  <label for="tarde">Tarde</label>

  <input type="radio" name="turno" id="noite">
  <label for="noite">Noite</label>
</fieldset>

- [X] E as caixas de seleção?
Também apresentam problema semelhante. O título “Assuntos de interesse” está em uma <div>, e as caixas de seleção não possuem <label> associados. O ideal seria agrupá-las em um <fieldset> com <legend> e usar um <label> para cada opção.
<fieldset>
  <legend>Assuntos de interesse</legend>

  <input type="checkbox" id="i1">
  <label for="i1">Guitarras</label>

  <input type="checkbox" id="i2">
  <label for="i2">Baterias</label>

  <input type="checkbox" id="i3">
  <label for="i3">Teclados</label>
</fieldset>
Em resumo, o formulário precisa melhorar principalmente a associação entre rótulos e campos, a identificação dos erros e o agrupamento semântico de rádio buttons e checkboxes.

## Como testar o que você corrigiu

1. **Só com o teclado:** percorra a página inteira usando Tab. Você consegue alcançar e ativar todos os controles? O foco fica visível?
2. **Leitor de tela (NVDA):**
   - `H` — pular de cabeçalho em cabeçalho
   - `Insert + F7` — lista de elementos (veja as abas Links, Cabeçalhos e Landmarks)
   - `T` — pular entre tabelas
   - `F` — pular entre campos de formulário
   Compare a lista de elementos **antes** e **depois** da sua correção.
3. **Validador do W3C:** <https://validator.w3.org/nu/>
4. **Comparação visual:** abra as duas versões em abas lado a lado. Elas devem parecer a mesma página.

## Entrega

A entrega é o **Pull Request**, não um arquivo solto. O corpo do PR já vem com um formulário
pedindo:

- o link do seu GitHub Pages;
- a lista dos problemas que você encontrou, agrupados pelos 7 blocos acima;
- para cada um: a tag errada, a tag correta e **por que** a troca melhora a experiência de quem
  usa tecnologia assistiva;
- os números da lista de elementos do NVDA antes e depois, se conseguir fazer o teste.
Antes 4 Avisos e 2 Erros
Depois 2 Avisos

Veja o passo a passo no [`README.md`](README.md).

Não se preocupe em achar todos os problemas de primeira. Achar 15 com boa justificativa vale mais
do que listar 30 sem explicar nenhum.
