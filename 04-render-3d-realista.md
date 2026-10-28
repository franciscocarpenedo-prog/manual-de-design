# 04. Render 3D realista

Quando a marca tem o arquivo 3D do produto (por exemplo, o arquivo usado na impressão 3D), o render no Blender é a forma mais fiel de mostrar o produto em ambientes: a geometria é a real, e a luz e a sombra são físicas, não inventadas.

Este capítulo resume o método que chegou ao resultado aprovado, com as armadilhas encontradas no caminho.

## Quando usar render em vez de IA

- Quando a proporção e os detalhes mecânicos importam (botões, encaixes, furos).
- Quando é preciso mostrar o mesmo produto em vários ambientes e cores com consistência.
- Quando a montagem com IA ficou com cara de adesivo (capítulo 03).

## 1. Geometria real

- Use a geometria real do arquivo GLB ou STL, na **escala real** (em metros).
- Arquivos GLB comprimidos (meshopt) precisam ser descomprimidos antes. A ferramenta `gltf-transform` faz isso.
- Não invente detalhes. Por exemplo, um furo que só existia nas peças de teste não deve aparecer no produto final.

## 2. Materiais que parecem de verdade

### Plástico impresso em 3D

- **As camadas da impressão vão no relevo (bump), não na cor.** Use uma textura de ondas (Wave) com camadas de cerca de 0,2 mm, na direção em que a peça foi impressa.
- **Armadilha das coordenadas:** usar as coordenadas do objeto herdou a escala embutida no GLB e deixou as camadas do tamanho errado. A correção foi usar a posição da geometria em metros (Geometry > Position), na escala real.
- Face com acabamento texturizado (como a placa PEI da impressora) leva um grão de Voronoi.
- Para tirar a perfeição de "plástico de computador": variação leve de tom de lote, manchas de rugosidade e poeira rara.
- Exemplo de acabamento seda bronze: metálico 0,65 e rugosidade 0,38.

### Paredes e azulejos

- Parede: textura de reboco gratuita (licença CC0, do Poly Haven), mais "casca de laranja" de tinta e uma variação de ±2% de rolo.
- **Azulejo:** o esmalte é brilhante e o rejunte é fosco e afundado. Um erro trocou os dois (esmalte fosco e rejunte saltado) e ficou falso.

### Tecidos

- Toalha com simulação de tecido e pilhas dobradas ficaram com cara de feltro ou espuma (exemplo 08). A solução foi **tirar a toalha da cena**. Se um objeto não convence de perto, é melhor não ter.

## 3. Cenário completo, em escala real

- Cada cômodo é um cenário 3D completo e em escala: peça na altura real (por exemplo, 1,10 m do chão), piso, teto, rodapé, batente de porta.
- **Cada cômodo com móveis e luz diferentes.** Mudar só a cor da parede não é um novo ambiente.
- Exemplo aprovado de cômodo diferente de verdade: exemplo 07.

## 4. Luz de interior

- Uma luz de área grande fazendo o papel de **janela**, com temperatura de cor definida, mais um HDRI fraco para o preenchimento.
- Exemplos de combinação: janela 4600 K com abajur 2700 K; janela 6000 K com LED 3400 K.
- Para o fundo do produto em sombra, use o "shadow catcher", que recebe só a sombra e permite colocar o produto sobre outro fundo com sombra física correta.

## 5. Câmera

| Plano | Lente | Abertura | Enquadramento |
|---|---|---|---|
| Aberto | 28 mm | f/4 | Peça ocupando 15% a 25% da altura do quadro. |
| Médio | 50 mm | f/2,8 a f/3,2 | Girar a câmera 32° a 40° para mostrar a fresta dos botões. |

## 6. Peças que se mexem precisam parecer funcionais

- O botão sai de um **furo aberto, com folga**, mostrando a haste e a fresta escura (exemplo 06, foto real e render lado a lado).
- **A fresta não recebe luz própria (emissão).** Com emissão, a peça ficou com cara de "acesa" ou "fechada". O escuro do furo vem só da sombra natural (oclusão).
- A cor da fresta é **a cor da frente escurecida** (cerca de 35% a 55% da luminosidade), nunca branca e nunca preta pura.
- Botão basculante (tecla que gira num eixo): ele percorre um arco em torno do pivô (cerca de 8°), com deslocamento de 44% a 50% do diâmetro do botão.

## 7. Cor fiel ao produto

- Use o mapeamento de cor **AgX** com o contraste "Medium High Contrast".
- **Armadilha:** o AgX tira saturação de cores fortes perto do branco. Um laranja virou salmão.
- Correção: um pequeno laço automático que renderiza, mede a cor da face da peça, corrige o código de cor e a exposição e renderiza de novo, até bater com a cor real. Some a isso um balanço de branco de câmera feito contra uma parede de cor conhecida, com força de cerca de 0,7.

## 8. Configuração de render

- Cycles na CPU, cerca de 200 amostras adaptativas e o removedor de ruído OIDN.

## 9. Pós-produção de "foto de celular"

1. Distorção de barril leve (cerca de 0,012).
2. Aberração cromática de cerca de 0,07%.
3. Vinheta de 10%.
4. Ruído de sensor, mais forte nas sombras.
5. Nitidez no estilo da câmera de celular.
6. JPG com qualidade 93.

## 10. Confira contra a foto real

Antes de mostrar, coloque **foto real e render lado a lado**, de perto, no mesmo ângulo (exemplo 06). Confira proporção, cor, folga dos botões, textura das camadas e o escuro do furo.
