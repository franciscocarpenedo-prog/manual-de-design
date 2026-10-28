# 05. Site, telas e personalizador

Regras para telas de loja virtual: página inicial, página de produto, seletor de cores, personalizador, compra rápida e página de instalação.

## Regras gerais de tela

- O primeiro bloco da página (o "hero") precisa **caber sem rolar numa tela de 1366 × 768**.
- Áreas de toque com **pelo menos 44 px**.
- Contraste de texto no padrão AA, foco visível no teclado e respeito à preferência de "movimento reduzido" do sistema.
- Tire prints em **390 px** (celular) e **1440 px** (computador) de cada tela e de cada estado.
- Animações só com movimento (transform) e transparência (opacity). O movimento deve ser físico: a peça se move de um lugar para outro, **nunca** um cruzamento de imagens entre duas posições. Sempre com suporte a `prefers-reduced-motion`.
- Montagens e imagens de IA levam o selo **"imagem ilustrativa"**.
- Animações que revelam conteúdo ao rolar precisam de alternativa: sem isso, o print da página inteira sai em branco.
- Corrija transbordamento lateral em 390 px (nada pode "vazar" para os lados).

## Seletor de cores

- Use a **foto real recolorida** (cada cor gerada a partir da foto real). Foi aprovado (exemplo 10).
- No celular, a peça tem de ser **pequena o bastante para caber inteira na tela junto com as cores**. Exemplo de altura da foto que funcionou: `clamp(190px, calc(100svh - 410px), 380px)`, com a foto fixa no topo ao rolar e as amostras de cor numa linha só.
- Quando a junção das cores importa (peças de várias partes), mostre também as laterais.

## Personalizador

- A **foto real é o padrão**.
- O giro em 3D aparece **só enquanto a pessoa arrasta** e volta para a foto 1,5 segundo depois de soltar.
- Das opções testadas para mostrar as laterais (miniaturas, desenho em escala, giro 3D ao arrastar), a recomendada foi o giro 3D ao arrastar mais as miniaturas.
- Uma imagem do produto **na parede ou em uso vende**. Inclua sempre que possível.

## Página de compra e compra rápida

- Na compra rápida: cartões com as cores padrão e um botão "Customize o seu" que abre uma gaveta ou janela.
- Na página de compra: primeiro "Personalizar", depois as variações de cor inteira. O cliente escolhe só o que precisa (por exemplo, a quantidade de botões); o resto é pré-configurado.

## Página "como instalar"

Estilo aprovado (exemplo 11):

- Render em tons pastel com contorno (traço de desenho), sem cara de foto.
- Estrutura: rótulo pequeno, título, subtítulo, **vista explodida** (as peças separadas mostrando a ordem de montagem), um bloco "Antes de começar" com o **guia de medidas**, e depois **10 passos** em cartões.
- Cartões com cantos arredondados (por exemplo, raio de 28 px).

## Lições de estudo de sites de referência

- Uma mensagem por bloco.
- Alterne foto de estilo de vida com bloco de produto.
- Interface monocromática, com a cor vindo das fotos.
- Prova social só com números reais.
- Fundos neutros nos blocos de produto.
- Evite páginas longas demais.

## Jogos e interações divertidas

- O dono adorou controle direto com um dedo e arte plana com charme.
- Não gostou de arrastar e soltar com controle complexo, nem de arte sem charme.

## Pacote de entrega para quem vai implementar

Quando a tela foi aprovada, entregue um pacote com:

- um arquivo de variáveis de estilo (cores, fontes, espaçamentos, raios) em JSON e em CSS;
- pasta `telas/` com os prints de cada estado em 390 e 1440 px;
- pasta `assets/` com imagens e ícones finais;
- um `SPEC.md` com os estados de cada componente, as regras de acessibilidade e os **critérios de aceite** (o que precisa estar funcionando para considerar pronto).
