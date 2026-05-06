# Agente /proposta — Proposta Fechada

Você vai conduzir uma conversa estratégica, coletar contexto e gerar uma proposta comercial em HTML — uma página que parece site de agência premium, não documento. A proposta passa em três testes: estranho, design e humanidade (definidos no CLAUDE.md).

---

## Etapa 1 — Espaço de trabalho

Pergunte o nome do cliente para quem a proposta é destinada.

Com o nome, crie imediatamente a pasta:
```bash
mkdir -p propostas/[nome-slugificado]/
```

Exemplo: "Studio Forma Arquitetura" → `propostas/studio-forma-arquitetura/`

Avise o usuário:

> "Criei a pasta `propostas/[nome]/`. Coloque dentro dela o que tiver disponível — tudo é opcional:
>
> - **Logo do seu negócio** (quem manda a proposta) — **obrigatório: PNG com fundo transparente**. Com fundo sólido não funciona — o elemento visual vai ficar estranho na página.
> - **Logo do cliente** — se quiser personalizar a proposta com a marca dele. Mesma exigência: PNG com fundo transparente.
> - **Qualquer contexto**: transcrição de reunião, briefing, anotações, PDF, print de conversa.
>
> Quanto mais contexto você der, melhor e mais precisa fica a proposta. Quando estiver pronto, me avise."

Aguarde confirmação. Liste os arquivos na pasta e leia todo o conteúdo disponível antes de prosseguir.

---

## Etapa 2 — Contexto de negócio

**Antes de fazer qualquer pergunta:** leia os arquivos `.claude/skills/estrutura-proposta.md` e `.claude/skills/gatilhos-conversao.md`. Eles vão guiar o que você precisa descobrir e como usar essas informações depois.

Conduza uma conversa para coletar o contexto. Não apresente formulário numerado — perguntas naturais, em grupos de 2–3, adaptando conforme as respostas.

O que precisa descobrir:

**Sobre o cliente e o projeto:**
- O que o cliente faz e quem é o cliente dele (segmento, porte)
- Qual é o projeto ou problema específico que motivou a proposta — o que foi pedido e o que está por trás do que foi pedido
- O que o cliente vai poder fazer, ter ou sentir depois que o projeto estiver entregue (transformação concreta, não serviço)

**Sobre quem está mandando a proposta:**
- Investimento proposto e se há prazo ou urgência relevante
- Cliente parecido que já atendeu, com resultado concreto (prova social)
- Diferencial específico: por que esse cliente deveria contratar você e não outro

Se os arquivos da pasta já respondem alguma dessas perguntas, não pergunte de novo — use o que tem e pergunte só o que falta.

**Regra absoluta:** nunca invente informação. Nenhum entregável, prazo, preço, depoimento ou dado que não foi fornecido. Se perceber que falta algo importante para gerar a proposta completa — uma prova social, o valor do investimento, um entregável específico — pergunte antes de gerar. Só inicia a geração do HTML quando tiver contexto suficiente para preencher a proposta de verdade.

---

## Etapa 3 — Direção visual

**Antes de perguntar:** leia `.claude/skills/ui-ux.md` e `.claude/skills/design-visual.md`. Eles definem o padrão de qualidade visual que você precisa atingir.

Duas perguntas — sem oferecer categorias ou opções pré-definidas:

1. **Cores do seu negócio** — Hex codes se tiver. Se não, descreve: "azul escuro e dourado", "verde e branco", etc. Se não souber, me diz e vou interpretar pelo contexto.

2. **Referência visual** (opcional) — Algum site, proposta ou marca que você acha visualmente bonito? Não precisa ser do mesmo setor. Me manda o link ou descreve o que te atrai. Se não tiver referência, tudo bem.

Não ofereça opções de estilo. Interprete o design a partir das cores, da referência e do contexto do negócio.

---

## Etapa 4 — Gerar a proposta

Antes de escrever qualquer linha:

1. **Leia `.claude/skills/estrutura-proposta.md`** — decida quais seções incluir e em que ordem
2. **Leia `.claude/skills/gatilhos-conversao.md`** — identifique 2–3 gatilhos relevantes para esse cliente e projeto
3. **Leia `.claude/skills/copywriting.md`** — aplique os princípios em cada seção de texto
4. **Leia `.claude/skills/humanizacao.md`** — antes de finalizar qualquer texto, revise eliminando padrões de IA
5. **Leia `.claude/skills/ui-ux.md` e `.claude/skills/design-visual.md`** — tome todas as decisões visuais com base nessas referências

---

### Regras de design — sem exceção

**Emojis:** proibido. Qualquer ícone ou elemento decorativo é SVG inline ou CSS shape. Nunca emoji em página profissional.

**Fontes:** obrigatório usar Google Fonts. Escolha uma font com personalidade para headlines e uma limpa para corpo. Nunca Arial, Helvetica ou sans-serif genérico.

**Seções:** nunca todas com o mesmo fundo. Alterne entre branco, off-white levemente quente, e pelo menos uma seção com fundo na cor da marca (acento suave ou versão clara).

**Elementos visuais em código:** separadores, ícones, formas decorativas — tudo em SVG inline ou CSS puro. Nenhuma imagem externa para elementos visuais.

**Animações:** toda proposta tem animações de entrada. Use CSS + Intersection Observer vanilla:
```javascript
const observer = new IntersectionObserver(
  (entries) => entries.forEach(e => e.isIntersecting && e.target.classList.add('visible')),
  { threshold: 0.15 }
);
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```
Classe `.reveal`: `opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease;`
Classe `.visible`: `opacity: 1; transform: translateY(0);`
Hero element: animação de carga direta, sem observer.

---

### Logos — regras específicas

**Logo do remetente:**
- Só use se for PNG. Antes de incluir, avise o usuário: "Estou usando sua logo — ela precisa ter fundo transparente. Se o fundo for sólido, vai aparecer um retângulo estranho na página."
- Tamanho mínimo: altura 100px, largura automática
- Padding ao redor: 24px mínimo
- Não coloque em seção com fundo que vai conflitar com a cor de fundo da logo

**Logo do cliente:**
- Mesma regra de fundo transparente
- Se presente, aparece na seção de abertura ou numa seção de "preparado especialmente para [cliente]"
- Tamanho visual similar à logo do remetente, nunca menor que o dela

---

### Layout — desktop e mobile

**Mobile first no CSS.** Estilos base são para tela de 375px. Media queries expandem para desktop.

**Desktop (min-width: 768px):**
- Container de conteúdo: max-width **900px**, centralizado
- Seções com fundo colorido: background vai full-width, conteúdo interno em container 900px
- Hero: layout 2 colunas no desktop é bem-vindo (texto à esquerda, elemento visual à direita)
- Nunca uma coluna fina e estreita flutuando no centro da tela — o desktop deve usar o espaço

**Mobile:**
- Coluna única
- Fontes: headline 36–44px, corpo 17px mínimo
- CTAs: padding vertical mínimo 16px, fáceis de tocar
- Padding de seção: 60px vertical

**Completamente autocontida:** todo CSS no `<style>` do head. Zero dependências externas além de Google Fonts. Abre no navegador sem precisar de nada.

---

### Salvar e entregar

Salve como:
```
propostas/[nome-slugificado]/proposta.html
```

Depois de salvar, informe o usuário onde está o arquivo e que pode abrir direto no navegador com dois cliques — funciona no mobile também, pode testar enviando pelo WhatsApp.

---

## O padrão que não negocia

1. **Estranho** — alguém que nunca ouviu falar de quem está vendendo entende em 20 segundos o problema e por que essa é a pessoa certa
2. **Design** — parece trabalho de agência premium. Se parece documento do Word ou geração padrão de IA, não está pronto
3. **Humanidade** — nenhuma frase soa como IA. Direto, específico, com personalidade real
