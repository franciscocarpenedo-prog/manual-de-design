# 08. Processo e ferramentas

## Passo a passo de qualquer trabalho

1. **Leia o que já existe:** briefing, referências e o que foi aprovado para a marca (capítulo 01).
2. **Consulte referências** antes de montar opções (capítulo 09).
3. **Crie 2 ou 3 opções** e mostre como imagem, numa prancha.
4. **Revise contra a foto real** e contra o checklist.
5. **Entregue pelo link do Drive**, com versões leves para o celular.
6. **Espere a aprovação do dono**, com as palavras dele.
7. **Registre:** guarde a versão datada, o que foi aprovado e o que foi reprovado, com o motivo.
8. Só então passe para implementação.

## Processo para funcionalidades complexas

Para telas com muitos estados (personalizador, jogo, fluxo de compra), siga este roteiro, adaptado do artigo "How I Design with AI (pt 2)" (link no capítulo 09):

1. **Entenda o produto** primeiro: o que ele faz, para quem, qual o problema.
2. **Deixe o agente construir uma versão que funciona**, mesmo feia.
3. **Tire print de cada estado de cada tela** e liste os defeitos (uma "varredura de interface").
4. **Corte o excesso:** tudo o que não ajuda a pessoa a comprar ou usar sai.
5. **Dê acabamento só nas telas cruciais.**
6. **Refine com o retorno do dono** e publique.

## Fluxo em 4 fases com habilidades de design

Para telas e sites, um fluxo que funcionou, cada fase com suas habilidades (skills) de agente:

1. **Direção:** frontend-design, ui-ux-pro-max, create-design-md (define estilo, paleta, fontes e o arquivo de design da marca).
2. **Construção:** emil-design-eng, mobile-native (constrói as telas com cuidado de detalhe e de celular).
3. **Revisão:** impeccable, review-animations, break-ui, web-design-guidelines (procura defeitos, tenta "quebrar" a tela, confere animações e boas práticas).
4. **Teste:** Playwright (prints automáticos em 390 e 1440 px e conferência dos estados).

Links das habilidades no capítulo 09.

## Ferramentas por tarefa

| Tarefa | Ferramenta |
|---|---|
| Peças e telas em HTML/CSS, com prints automáticos | Claude Code ou Grok Build, com Playwright |
| Troca de fundo em foto real e cenas | IA de imagem (Grok Imagine, Krea; modelo Flux Kontext para manter o produto) |
| Cenas com pessoas | IA de imagem (por exemplo, Flux 2 Klein no Krea), com conferência de mãos e proporção |
| Render do arquivo 3D real | Blender com Cycles e mapeamento de cor AgX |
| Pós-produção, recoloração, redimensionamento, pranchas | Python com PIL (e OpenCV para alinhamento) |
| Ampliação de imagem | Real-ESRGAN (realesr-general-x4v3), misturado com ampliação simples |
| Entrega para o celular | Google Drive (link) |

**Insista em usar um agente de código (Claude Code ou Grok Build) em vez de fazer à mão.** Ele é mais rápido, repetível e deixa o trabalho documentado.

## Prompt base para um agente de código montar telas

Adapte e cole:

> Leia o arquivo de design da marca (2 cores e 2 fontes) e o que já foi aprovado. Monte 3 opções da tela X em HTML/CSS, realmente diferentes entre si. Use a foto real do produto; não invente produto, medida, preço nem dado de cliente; marque montagens como "imagem ilustrativa". Respeite: hero sem rolar em 1366 × 768, toque de 44 px, contraste AA, foco visível, movimento reduzido. Evite os sinais de "cara de IA" (lista do capítulo 06). Tire prints em 390 e 1440 px de cada estado com Playwright e junte numa prancha com rótulos A, B e C.
