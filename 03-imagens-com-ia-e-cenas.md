# 03. Imagens com IA e cenas

Cenas de ambiente (o produto numa sala, cozinha, banheiro) e cenas de uso com pessoas vendem muito, mas são onde a IA mais erra. Este capítulo reúne o que foi testado, o que foi reprovado e o que funcionou.

## A regra de ouro

O produto na imagem precisa ser **o produto real**, com a forma, a proporção e os detalhes da foto. O ambiente pode ser criado; o produto, não.

## Comparação de métodos para cenas de ambiente

Foram testados cinco métodos para colocar o produto num cômodo. O resultado:

| Método | Como funciona | Resultado |
|---|---|---|
| Expandir a foto (outpainting) | A IA "continua" a foto para os lados, criando o cômodo. | Reprovado: a IA refaz o desenho do produto (exemplo 02). |
| **Editar a foto real e trocar só o fundo** | A IA recebe a foto real de perto e muda apenas o que está atrás do produto. | **Vencedor** (exemplo 04). |
| Colagem com nova iluminação | O recorte do produto é colado num fundo gerado e a luz é ajustada. | Reprovado: continua com cara de adesivo (exemplo 03). |
| Colagem com passada de harmonização pela IA | Igual ao anterior, com uma passada final da IA para "unir" as partes. | Reprovado: a IA refaz o desenho do produto nessa passada. |
| Gerar com a foto como referência | A IA cria a cena inteira olhando a foto. | Resultado variável; às vezes bom, às vezes errado. |

### Lições

- **Colar a foto do produto num fundo gerado fica com cara de adesivo** e foi reprovado. O que funcionou foi editar a foto real de perto trocando só o fundo, com luz e sombra integradas, ou fazer um render 3D do arquivo real (capítulo 04).
- **Plano fechado funciona, plano aberto entrega a montagem.** Com o produto nítido e o cômodo desfocado, a cena convence. Num plano aberto, a diferença de luz e de nitidez entre produto e fundo aparece.
- **No prompt, descreva só o ambiente e a luz, nunca o produto.** Quando o prompt descreve o produto, a IA tende a redesenhá-lo.
- O modelo **Flux Kontext** foi o mais fiel para manter o produto e mudar a cena.
- Ferramentas de "reiluminação" (como IC-Light) lavam a textura do produto. Se usar, devolva a textura com separação de frequências (transferir o detalhe fino da foto original para o resultado).
- Para escalar (muitas cenas de um mesmo produto), o caminho é treinar um **LoRA do objeto** com 10 a 20 fotos reais.

## Erros típicos da IA que foram reprovados

- **Proporção errada:** laterais finas demais, peça mais estreita do que a real, botões com cara de falsos (exemplo 05). As frases do dono foram "estão muito finos" e "os botões estão muito falsos". A correção foi refazer usando a foto real como base.
- **Peça "fechada":** botões que parecem pinos soltos colados numa placa, sem o furo por onde saem (exemplo 01).
- **Cor saturada demais:** uma cor de parede ou de produto mais forte do que a real.
- **Objetos que não parecem do material:** uma toalha que parecia azulejo ou feltro (exemplo 08). Se um objeto de cena não convence de perto, tire-o da cena.
- **Cômodos iguais:** a mesma parede com outra cor não é outro cômodo. Cada ambiente precisa de móveis, entorno e luz próprios.

## Prompt no estilo de fotógrafo

Pedir "ultra realista 8k" piora o resultado. Funciona melhor descrever **como a foto foi tirada**:

- **Condições de captura:** câmera (por exemplo, celular comum ou câmera com lente de 35 mm), abertura, ISO, hora do dia, altura dos olhos.
- Peça **"foto comum, sem edição, ruído leve"**.
- Coloque **1 ou 2 imperfeições no ambiente** (um fio de rodapé, uma marca leve na parede), **nunca no produto**.
- Inclua uma lista do que **não** quer: sem CGI, sem brilho exagerado (glow), sem HDR, sem desfoque exagerado de fundo.

Exemplo de trecho de prompt (adaptar):

> Foto tirada com celular, luz natural de janela à esquerda, fim de tarde, câmera na altura do objeto, foto comum sem edição, ruído leve. Parede de reboco com pequena irregularidade perto do rodapé. Sem CGI, sem glow, sem HDR, sem bokeh exagerado.

### Estilo de foto em JSON

Uma técnica útil: extraia o estilo de fotos já aprovadas (luz, temperatura de cor, contraste, grão, lente, enquadramento) num pequeno arquivo JSON e cole esse JSON nas gerações seguintes. Isso mantém a mesma "cara" entre imagens.

## Pós-produção para tirar a "cara de IA"

Depois de gerar, uma passada leve ajuda a imagem a parecer foto:

1. Nitidez mais suave (a IA costuma exagerar no contorno).
2. Aberração cromática leve (franja de cor quase invisível nas bordas).
3. Saturação reduzida em cerca de 8%.
4. Pretos levemente levantados (sem preto absoluto).
5. Vinheta discreta.
6. Grão fino.
7. Exportar em JPG com qualidade em torno de 86.

Se a imagem foi ampliada, misture cerca de 15% de uma ampliação simples (bicúbica) com a ampliação por IA (por exemplo, Real-ESRGAN) para reduzir o aspecto "pintado".

### Ordem certa ao montar camadas

Quando juntar o produto real com um fundo, siga esta ordem:

1. Ponto de preto (igualar o preto mais escuro das duas partes).
2. Balanço de branco.
3. Nitidez e profundidade de campo compatíveis.
4. Aberração cromática.
5. Sombra de contato (logo embaixo do produto) e sombra projetada.
6. Por último, **um único** grão e **uma única** vinheta sobre a imagem já achatada. Grão aplicado separado em cada camada denuncia a montagem.

Para alinhar uma peça real por cima de uma gerada pela IA, use registro automático de imagem (por exemplo, o método ECC do OpenCV).

## Recoloração da foto real

Para mostrar o produto em outras cores a partir de uma única foto:

- Separe cada parte do produto com uma máscara.
- Calcule em luz linear: **resultado = cor desejada × sombreamento da foto real**, parte por parte. Isso mantém as sombras, os reflexos e a textura de verdade.
- Uma alternativa é trabalhar em LAB no "modo luminosidade", com um corte suave nos claros que preserva o tom.
- Confira se a cor chega até a emenda entre as partes, sem faixa clara.
- Resultado aprovado no seletor de cores: exemplo 10.

## Cenas com pessoas

Cenas de uso com pessoas podem ser feitas com IA, num estilo semirrealista, **desde que o produto seja o real**. Antes de mostrar, confira:

- **Mãos e dedos.** Conte. Foram reprovadas imagens com 3 mãos e com mão de 3 dedos. Aprovada: polegar e 4 dedos, mão segurando de forma natural (exemplo 09).
- **Proporção do produto.** Meça a razão altura/diâmetro do produto na imagem e compare com a real. Uma foto de referência achatada gerou um produto magro; a correção foi esticar a referência na proporção certa (no caso, ×1,19) ou fazer uma deformação local.
- **Gravações e logotipos.** A IA refaz o desenho e eles saem ilegíveis. Corrija repintando a área (inpaint) e reaplicando o relevo original.
- **Pixels reais colados** ficam fiéis, mas com cara de colados. A cena da IA fica mais natural. Use pixels reais só para detalhes pequenos.
- Marque como **"imagem ilustrativa"** até chegarem fotos reais.

## Harmonização: o que já foi pesquisado

- IC-Light não roda bem sem placa de vídeo.
- PCT-Net funciona para igualar cor e luz entre produto e fundo.
- Harmonizer tem licença não comercial; não use em peças de venda.
- Mapa de normais (para reiluminar) ajuda pouco em peças planas.
- A única opção fisicamente correta de luz e sombra é o render 3D com "shadow catcher" (capítulo 04).
