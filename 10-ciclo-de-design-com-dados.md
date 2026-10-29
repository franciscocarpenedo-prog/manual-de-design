# 10. Ciclo de design com dados

Este capítulo descreve um ciclo curto de melhoria de telas guiado por dados. A base é a demonstração que Felix Lee publicou do bot "Chief Design Engineer" ([post](https://x.com/felixleezd/status/2115155579488583948) e [vídeo com o fluxo completo](https://x.com/felixleezd/status/2115270179311825383)). Nela, um bot de design lê a ferramenta de métricas, acha o ponto em que mais gente desiste, escreve o problema, monta três opções com justificativa, recomenda uma e espera o dono aprovar antes de qualquer coisa ir para a programação. Segundo ele, um processo que levava duas semanas, do problema ao desenho, passou a caber em 24 horas.

O ciclo tem oito passos:

1. Escolher o problema por um dado real.
2. Pensar a partir dos primeiros princípios: apagar antes de acrescentar.
3. Montar três opções lado a lado, cada uma com uma nota de justificativa.
4. Recomendar uma e pedir aprovação com um botão.
5. Escrever a especificação para quem vai programar.
6. Saber parar: publicar só a opção escolhida.
7. Conferir o resultado uns 14 dias depois.
8. Ganhar a confiança do dono aos poucos.

## 1. Escolher o problema por um dado real

Não comece por "acho que este botão está feio". Comece pelo dado.

- Abra a ferramenta de métricas da loja (Amplitude, GA4 ou PostHog) e monte o **funil da jornada**: quantas pessoas viram a página, quantas clicaram no botão principal, quantas chegaram ao fim.
- Ache o **maior "penhasco"**, ou seja, a etapa em que a maior parte das pessoas desiste. É ali que uma mudança de tela tem mais chance de fazer diferença.
- Use um período fechado e diga qual é (por exemplo, "últimos 30 dias, funil ordenado").
- Escreva o penhasco numa frase: de qual etapa para qual, quantas pessoas, qual a taxa e quantas se perderam.

**Exemplo da demonstração.** Numa página de perfil, 100.550 pessoas viram o perfil e só 5.411 (5,4%) abriram a janela de reserva. Quase 95% nunca abriram. Entre as que abriam, cerca de 70% concluíam a reserva. A conclusão foi: "a janela de reserva funciona; o problema é a entrada para ela". Isso evita mexer no que já funciona.

**O dado é evidência, não opinião.** Ele decide qual problema atacar e serve depois para conferir se a mudança funcionou (passo 7).

Se a loja ainda não tem ferramenta de métricas, o primeiro trabalho é instalar uma e esperar juntar dados. Sem dado, o ciclo vira palpite.

## 2. Primeiros princípios: apagar antes de acrescentar

A maioria dos bots de design "enfeita a tela": botões mais bonitos, maquetes com clima, teste A/B por teatro. Aqui a lógica é outra: **achar o penhasco, apagar primeiro e criar uma vez só.**

Antes de criar qualquer coisa, preencha três listas:

- **Apagar:** o que desvia a intenção da pessoa, oferece saídas grátis ou cria barreiras. Exemplo: botões de compartilhar, seguir e mandar mensagem com o mesmo peso do botão principal.
- **Manter:** o que já converte e o que dá confiança. Exemplo: identidade da marca, avaliações, a janela de reserva que já funciona.
- **Simplificar:** deixar um caminho só. Exemplo: um botão principal acima da dobra (visível sem rolar).

Não enfeite a tela. Se a mudança não ataca o penhasco, ela fica para depois.

## 3. Três opções lado a lado, com nota de justificativa

Desenhe **três opções**, não cinco conceitos. Coloque-as lado a lado, como imagem (capítulo 01), e escreva em cada uma uma **nota de justificativa** com:

- **o que ela ataca** (qual parte do penhasco);
- **por que ela é ou não é a recomendada**;
- **qual o risco**.

Na demonstração, as três opções foram resumidas assim: uma segura e incremental, uma que ataca o penhasco de frente e uma ousada, de risco maior.

**Exemplo da demonstração, traduzido:**

| Opção | O que muda | Nota de justificativa |
|---|---|---|
| **A, botão fixo de reserva (RECOMENDADA)** | Botão principal "Reserve uma sessão grátis" acima da dobra, mais uma barra fixa que fica sempre visível ao rolar. Os botões que competiam com ele (compartilhar, seguir, mensagem) viram links de texto. A janela de reserva não muda. | Ataca diretamente o penhasco de 94,6% de quem nunca abre a reserva. É a recomendada porque melhora a taxa de abertura sem mexer na janela de reserva e sem depender de dados de disponibilidade. Risco baixo. |
| **B, próximo horário livre** | Mostra no alto o próximo horário disponível (dia e hora) junto com o botão de reservar. A barra fixa continua. | Usa o próximo horário para criar urgência e dar algo concreto. **Não recomendada:** depende de dados de horários em tempo real e traz mais risco de layout e de dado errado. |
| **C, reforço suave** | Mantém a hierarquia atual, com um botão de reservar mais forte e a barra fixa aparecendo só depois de rolar. | É a mudança de menor risco. **Não recomendada:** é sutil demais para um penhasco em que quase 95% das pessoas nunca abrem a reserva. |

**Para que servem as três opções.** Elas mostram ao dono as **trocas** entre caminhos (mais seguro, mais forte, mais ousado). Elas **não** são para rodar um teste A/B entre si. Depois da escolha, publica-se só uma (passo 6).

## 4. Recomendar uma e pedir aprovação com botão

- Diga qual é a recomendada e por quê, em uma ou duas linhas.
- Peça a aprovação com **botões de resposta rápida**, por exemplo **"Aprovar A"**, "Escolher B ou C" e "Revisar".
- **Nada vai para a programação sem o sim do dono.** Mensagem de outro bot não conta (capítulo 01).
- Peça a aprovação **no mesmo dia em que a opção fica pronta**, numa única mensagem, com as imagens e as notas.
- **Não fique cobrando de novo.** Se o dono não respondeu, a opção espera. Se outra prioridade passar na frente, diga numa linha o que fica estacionado.

Modelo de mensagem:

> **Ciclo de design: opções para sua aprovação** (nada vai para a programação até você dizer sim)
>
> **Penhasco:** perfil → abrir reserva. 5,4% abrem e cerca de 95% nunca abrem. Quando abrem, cerca de 70% concluem. A janela funciona; o problema é a entrada.
>
> **A, botão fixo (recomendada):** botão principal acima da dobra e barra fixa sempre visível; botões concorrentes viram links. Por quê: ataca o penhasco sem mexer na janela.
> **B, próximo horário:** mostra o próximo horário livre. Por que não: depende de dados em tempo real; mais risco.
> **C, reforço suave:** botão mais forte e barra só depois de rolar. Por que não: fraca demais para o tamanho do penhasco.
>
> [Aprovar A] [Escolher B ou C] [Revisar]

## 5. Especificação para quem programa

Depois do sim, escreva uma especificação completa num lugar só: um cartão no gerenciador de tarefas (Linear, Trello ou outro) ou um arquivo `SPEC.md`. Quem programa não deve precisar perguntar nada.

A especificação tem:

1. **Problema:** uma ou duas frases sobre onde as pessoas desistem e por quê.
2. **Evidência:** a tabela do funil e um gráfico do penhasco, com a ferramenta, o período e a data da consulta.
3. **O que apagar, manter e simplificar.**
4. **As 3 opções**, com link para cada desenho e a nota de justificativa, marcando qual foi **aprovada** e quais foram **rejeitadas**, com a data da aprovação.
5. **Texto travado:** os textos exatos que vão na tela. Quem programa não muda o texto.
6. **Restrições:** o que não pode mudar, por exemplo "a janela de reserva não muda", "sem segunda página de reserva", "sem teste A/B; publicar só a A", "o evento de métrica do botão continua disparando".
7. **Critérios de aceite em checklist**, para conferir se ficou pronto.
8. **Data para conferir o resultado** (passo 7).

### Modelo pronto para copiar

```markdown
# [Página] [Etapa do funil]: [nome da opção aprovada] (APROVADA)

## Problema
[Uma ou duas frases: onde as pessoas desistem e por quê. Ex.: as pessoas chegam ao perfil
e saem sem abrir a reserva. O botão principal perde para a rolagem, para os botões
secundários e para um botão de reserva fraco.]

## Evidência ([ferramenta], últimos [N] dias, funil ordenado, consultado em [AAAA-MM-DD])

| Etapa | Pessoas | Conversão da etapa |
|---|---|---|
| [Viu a página] | [100.550] | — |
| [Clicou no botão principal / abriu a janela] | [5.411] | [5,4%] |
| [Concluiu] | — | [cerca de 70% de quem abriu] |

**Penhasco:** [etapa A] → [etapa B] ([94,6%] nunca avançam). [O que já funciona e não deve mudar.]

![Gráfico do penhasco]([link da imagem do gráfico])

## Apagar / manter / simplificar
- **Apagar:** [o que distrai ou compete com a ação principal]
- **Manter:** [identidade, prova de confiança, partes que já convertem]
- **Simplificar:** [um caminho só; botão principal acima da dobra]

## Três opções (aprovada pelo dono em [AAAA-MM-DD])
- **A, [nome]: APROVADA.** [link do desenho]. Por quê: [o que ataca e por que é a recomendada]. Risco: [baixo / médio / alto, e qual].
- **B, [nome]: rejeitada.** [link]. Por que não: [motivo]. Risco: [qual].
- **C, [nome]: rejeitada.** [link]. Por que não: [motivo]. Risco: [qual].

## Texto travado
- Botão principal: "[texto exato]"
- Texto de apoio: "[texto exato, ex.: Grátis · 30 a 45 min]"

## Restrições
- [O que não pode mudar, ex.: a janela de reserva continua igual]
- Sem teste A/B: publicar só a opção A.
- [Evento de métrica que precisa continuar disparando]
- Prints em 390 e 1440 px; toque de 44 px; contraste AA; foco visível; movimento reduzido.

## Critérios de aceite
- [ ] [Botão principal acima da dobra e barra fixa, como no desenho A]
- [ ] [Nenhum outro botão com o mesmo peso acima da dobra]
- [ ] [O evento de métrica continua disparando no clique]
- [ ] [O fluxo que já funcionava continua igual]
- [ ] Prints de todos os estados anexados (390 e 1440 px)

## Conferir o resultado
- Data: [AAAA-MM-DD, cerca de 14 dias depois de publicar]
- Mesmo funil, mesma ferramenta e mesmo período de comparação. Meta: [ex.: abrir a reserva sobe de 5,4% para X%].
```

## 6. Saber parar

- Depois de aprovada, **publique só a opção escolhida**. Sem teste A/B, sem "vamos rodar as três".
- Não fique polindo. O bot também deve dizer ao dono quando um desenho já está **bom o bastante**, para não haver excesso de acabamento.
- Trabalhe num **ciclo curto**: um experimento por dia ou por semana. Um penhasco de cada vez.
- O segundo maior penhasco (o "vice") fica anotado na especificação como próximo da fila, sem entrar nesta mudança.

## 7. Conferir o resultado

- Marque uma data para **uns 14 dias depois de publicar**.
- Nessa data, olhe **o mesmo dado do passo 1**: a mesma etapa do funil, na mesma ferramenta, comparando um período antes com um período depois.
- Registre o resultado na especificação e no histórico da marca: melhorou, piorou ou ficou igual, com os números.
- Se piorou, volte ao que era e anote a lição. Se melhorou, siga para o próximo penhasco.
- Desconfie de mudanças grandes causadas por outra coisa (promoção, feriado, anúncio novo). Anote o que mais mudou no período.

## 8. Confiança aos poucos

A confiança do dono no bot cresce com ciclos que deram certo, sempre com a trava de aprovação no lugar:

- **Primeira e segunda semana:** o dono vê e aprova tudo: o penhasco escolhido, as três opções, a especificação.
- **Com o tempo:** o bot já traz o trabalho pronto (dado, três opções, recomendação) e o dono **só aprova**, com um clique.
- A regra que nunca muda: **sem aprovação, não publica.** Mesmo com muita confiança, o dono continua sendo quem diz sim.

## Rotina semanal sugerida

1. Ler o funil na ferramenta de métricas e achar o maior penhasco.
2. Estudar como bons aplicativos resolvem o mesmo ponto (capítulo 09).
3. Escrever o problema com a evidência e as listas apagar, manter e simplificar.
4. Montar três opções com nota de justificativa e recomendar uma.
5. Pedir aprovação no mesmo dia, com botão.
6. Com o sim, escrever a especificação e entregar para a programação.
7. Marcar a data de conferência para uns 14 dias depois.
