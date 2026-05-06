# Agente /proposta — Proposta Fechada

Você vai conduzir uma conversa estratégica para coletar o contexto necessário e gerar uma proposta comercial em HTML — uma página que parece um site profissional, não um documento. A proposta deve passar nos três testes do CLAUDE.md: estranho, design e humanidade.

---

## Etapa 1 — Espaço de trabalho

Pergunte o nome do cliente para quem a proposta é destinada.

Com o nome, crie imediatamente a pasta de trabalho:
```bash
mkdir -p propostas/[nome-slugificado]/
```

Exemplo: cliente "Studio Forma" → `propostas/studio-forma/`

Depois de criar a pasta, avise o usuário:

> "Criei a pasta `propostas/[nome]/`. Se quiser enriquecer a proposta, coloque dentro dela o que tiver disponível — tudo é opcional:
> - **Logo do seu negócio** (quem está mandando a proposta) — PNG ou SVG, fundo transparente de preferência
> - **Logo do cliente** — se quiser personalizar ainda mais com a marca dele
> - **Qualquer contexto adicional**: transcrição de reunião, briefing, anotações, PDF, print de conversa, o que for
>
> Quanto mais contexto, melhor a proposta. Mas se não tiver nada, também funciona — é só me avisar e a gente começa."

Aguarde a confirmação. Liste os arquivos presentes na pasta e leia todo o conteúdo disponível para absorver o contexto antes de fazer perguntas.

---

## Etapa 2 — Contexto de negócio

Conduza uma conversa para coletar o contexto. Não apresente um formulário numerado — faça as perguntas de forma natural, em grupos pequenos, adaptando conforme as respostas.

O que precisa descobrir:

**Sobre o cliente e o projeto:**
- O que o cliente faz e quem é o cliente dele (segmento, porte, contexto)
- Qual é o projeto ou problema específico que estão contratando — o que foi pedido e o que está por trás do que foi pedido
- O que o cliente vai poder fazer, ter ou sentir depois que o projeto estiver entregue (transformação concreta, não serviço)

**Sobre o negócios de quem está mandando a proposta:**
- Qual é o investimento proposto e se há prazo ou urgência relevante
- Algum cliente parecido que já atendeu, e qual foi o resultado concreto (prova social)
- Há algum diferencial ou razão específica pela qual este cliente deveria contratar você e não outro

Se os arquivos da pasta já respondem parte dessas perguntas, não pergunte de novo — use o contexto que já tem e pergunte só o que falta.

---

## Etapa 3 — Direção visual

Com o contexto de negócio coletado, pergunte sobre o design. Duas perguntas — diretas, sem forçar escolha entre categorias:

1. **Cores** — Quais são as cores do seu negócio? Hex codes se tiver, ou descreve ("azul escuro e dourado", "verde e branco", etc.). Se não souber, diz que vou interpretar a partir do contexto.

2. **Referência visual** (opcional) — Tem algum site, proposta, marca ou print que você acha visualmente bonito — não importa o setor? Me manda o link ou descreve o que te atrai nele. Se não tiver referência, tudo bem — vou tomar as decisões com base no que fizer mais sentido pro contexto do negócio.

Não ofereça opções pré-definidas de estilo. Interprete o design a partir das cores fornecidas, da referência se houver, do tom do negócio e do perfil do cliente final da proposta. A paleta de cores e o contexto do negócio já dizem muito sobre o visual certo — confie nessa leitura.

---

## Etapa 4 — Gerar a proposta

Com todo o contexto coletado, gere a proposta. Antes de começar o HTML, pense:

**Use as skills disponíveis como guia de raciocínio:**
- `estrutura-proposta` → decida quais seções incluir e em que ordem, com base no porte e tipo do projeto
- `copywriting` → escreva cada seção com o argumento certo: problema → transformação → prova → preço
- `gatilhos-conversao` → identifique quais 2 ou 3 gatilhos são mais relevantes para esse cliente e projeto específico, e os aplique com naturalidade
- `ui-ux` → tome as decisões visuais: tipografia, espaçamento, hierarquia, containers, CTA
- `humanizacao` → revise cada bloco de texto antes de fechar o HTML, eliminando qualquer padrão de IA

**Sobre a logo:** referencia a logo com caminho relativo `./[nome-do-arquivo-da-logo]`. O HTML será salvo na mesma pasta, então o navegador vai encontrar o arquivo automaticamente.

**Sobre a paleta:** use as cores informadas como identidade visual da proposta. A cor de acento principal (marca de quem envia) deve aparecer nos CTAs, destaques de número/dado, e elementos de separação. Fundo sempre claro (branco ou off-white levemente quente) salvo se o estilo escolhido for "premium e sóbrio".

**Sobre o HTML — mobile first, sem exceção:**

A maioria das propostas vai ser aberta no celular, enviada pelo WhatsApp. Mobile não é adaptação — é o design principal.

- **Estrutura mobile first:** escreva o CSS pensando primeiro em tela de 375px. Use media queries para ajustar em desktop, não o contrário.
- **Tipografia mobile:** corpo mínimo 17px, headlines proporcionais. Nada que force o usuário a pinçar para ler.
- **Layout:** coluna única no mobile. Sem grids de 2+ colunas que quebram em tela pequena.
- **CTAs:** botões com padding generoso (mínimo 16px vertical), fáceis de tocar com o polegar. Fixo na parte inferior se fizer sentido.
- **Espaçamento:** seções com padding vertical de pelo menos 48px no mobile.
- **Imagens e logos:** max-width: 100%, nunca extrapolam o container.
- **Peso:** zero dependências externas pesadas. Google Fonts permitido (1 família, máximo 2 pesos). Nenhuma lib JS. Nenhum framework CSS.
- **Desktop:** largura máxima do conteúdo 720px, centralizado. No desktop a proposta fica ainda melhor — mas mobile é a prioridade.
- **Autocontida:** todo o CSS no `<style>` do head. O arquivo HTML abre direto no navegador sem depender de nada externo.

**Salve o arquivo gerado como:**
```
propostas/[nome-slugificado]/proposta.html
```

Depois de salvar, informe o usuário onde está o arquivo e que pode abrir direto no navegador para visualizar.

---

## O padrão que não negocia

A proposta está pronta quando passa nos três testes:

1. **Estranho** — alguém que nunca ouviu falar de quem está vendendo entende em 20 segundos o problema sendo resolvido e por que essa é a pessoa certa
2. **Design** — parece trabalho de agência premium, não documento do Word
3. **Humanidade** — nenhuma frase soa como IA. Linguagem direta, específica, com personalidade real
