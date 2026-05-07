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
> - **Logo do seu negócio** (quem manda a proposta) — PNG com fundo transparente. Com fundo sólido o visual vai ficar estranho.
> - **Logo do cliente** — para personalizar com a marca dele. Mesma exigência: PNG com fundo transparente.
> - **Qualquer contexto**: transcrição de reunião, briefing, anotações, PDF, print de conversa.
>
> Quanto mais contexto, melhor a proposta. Quando estiver pronto, me avise."

Aguarde confirmação. Liste os arquivos na pasta e leia todo o conteúdo disponível antes de prosseguir.

---

## Etapa 2 — Contexto de negócio

**Antes de fazer qualquer pergunta:** leia `.claude/skills/estrutura-proposta.md` e `.claude/skills/gatilhos-conversao.md`.

Conduza uma conversa natural para coletar o contexto. Não apresente formulário numerado — perguntas em grupos de 2–3, adaptando conforme as respostas.

O que precisa descobrir:

**Sobre o cliente e o projeto:**
- O que o cliente faz e quem é o cliente dele (segmento, porte)
- Qual é o projeto ou problema específico — o que foi pedido e o que está por trás
- O que o cliente vai poder fazer, ter ou sentir depois da entrega (transformação concreta)

**Sobre quem está mandando a proposta:**
- Investimento proposto
- Prazo e cronograma de entrega — se não souber ou não tiver definido, pergunte. **Nunca invente prazo.**
- Cliente parecido que já atendeu, com resultado concreto (prova social)
- Diferencial específico: por que esse cliente deveria contratar você e não outro
- **Número do WhatsApp** para o CTA de contato (com DDD, ex: 51999998888)

Se os arquivos da pasta já respondem alguma dessas perguntas, não pergunte de novo.

**Regra absoluta:** nunca invente informação. Nenhum entregável, prazo, preço, depoimento ou dado que não foi fornecido. Se falta algo importante — especialmente prazo, investimento ou escopo — pergunte antes de gerar. Só inicia o HTML com contexto suficiente para preencher tudo de verdade.

---

## Etapa 3 — Direção visual

**Antes de perguntar:** leia `.claude/skills/ui-ux.md` e `.claude/skills/design-visual.md`.

Duas perguntas:

1. **Cores do seu negócio** — Hex codes se tiver. Se não, descreve ("azul escuro e dourado", etc.). Se não souber, diz e interpreto pelo contexto.

2. **Referência visual** (opcional) — Site, proposta ou marca que você acha bonito. Me manda o link ou descreve. Se não tiver, tudo bem.

Não ofereça opções de estilo pré-definidas. Interprete o design a partir das cores, referência e contexto do negócio.

---

## Etapa 4 — Gerar a proposta

Leia todas as skills antes de escrever qualquer linha:
- `.claude/skills/estrutura-proposta.md` — estrutura e sequência
- `.claude/skills/gatilhos-conversao.md` — gatilhos a aplicar
- `.claude/skills/copywriting.md` — como escrever cada seção
- `.claude/skills/humanizacao.md` — revisão de linguagem
- `.claude/skills/ui-ux.md` + `.claude/skills/design-visual.md` — todas as decisões visuais

---

### Estrutura e sequência

O preço raramente funciona na primeira dobra — o argumento ainda não foi construído e o número parece caro antes de fazer sentido. A sequência que geralmente converte melhor: problema → transformação → entregáveis → prova → investimento → CTA. Mas use o contexto do projeto para decidir — o que serve a esse cliente e esse momento específico.

---

### Regras de design — sem exceção

**Emojis:** proibido. Qualquer ícone ou elemento decorativo é SVG inline ou CSS shape.

**Fontes:** Google Fonts obrigatório. Font com personalidade para headlines, limpa para corpo. Nunca Arial, Helvetica ou sans-serif genérico.

**Seções:** nunca todas com o mesmo fundo. Alterne entre branco, off-white quente, e pelo menos uma seção com fundo na cor da marca.

**Elementos visuais:** separadores, ícones, formas decorativas — SVG inline ou CSS puro. Zero imagem externa para visual.

**Animações obrigatórias:**
```css
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.reveal.visible { opacity: 1; transform: translateY(0); }
```
```javascript
const observer = new IntersectionObserver(
  (entries) => entries.forEach(e => e.isIntersecting && e.target.classList.add('visible')),
  { threshold: 0.15 }
);
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```
Hero: animação de carga direta (`animation: fadeInUp 0.8s ease forwards`), sem observer.

---

### Logos — regras específicas

**Logo do remetente:**
- Aparece UMA VEZ, no header/topo. Nunca duplicada em outra seção.
- Tamanho mínimo: altura 100px, largura automática
- Se o hero tiver layout 2 colunas (desktop), a coluna direita recebe um elemento visual criado em código — número de destaque, SVG decorativo, grid de ícones — NUNCA a mesma logo repetida.

**Logo do cliente:**
- Se presente na pasta, aparece na seção de abertura (ex: "Proposta preparada para [cliente]")
- Mesma exigência de fundo transparente
- Tamanho visual similar ao da logo do remetente

---

### CTA com WhatsApp

O botão principal de contato abre o WhatsApp com mensagem pré-escrita. Use o número coletado na etapa 2.

Formato:
```
https://wa.me/55[número sem espaço ou traço]?text=[mensagem url-encoded]
```

A mensagem deve ser contextual e facilitar o fechamento. Exemplo base (adapte para o projeto específico):
```
Olá! Vi a proposta e tenho interesse em avançar. Podemos conversar?
```

Versão url-encoded: `Ol%C3%A1%21+Vi+a+proposta+e+tenho+interesse+em+avan%C3%A7ar.+Podemos+conversar%3F`

Escreva uma mensagem específica para o projeto — não genérica. Se for proposta de identidade visual: "Vi a proposta de identidade visual e quero dar andamento." O link já coloca o cliente um passo mais perto do sim.

---

### Layout — desktop e mobile

**Mobile first.** CSS base para 375px. Media queries expandem para desktop.

**Desktop (min-width: 768px):**
- Max-width conteúdo: **900px**, centralizado
- Fundos coloridos: full-width, conteúdo interno em 900px
- Hero: 2 colunas bem-vindo (texto esquerda, visual direita)
- Nunca coluna fina no centro de tela larga

**Mobile:**
- Coluna única, headline 36–44px, corpo 17px mínimo
- CTAs: padding vertical 16px mínimo
- Padding de seção: 60px vertical

**Autocontida:** CSS no `<style>` do head. Zero dependências além de Google Fonts.

---

### Salvar e abrir

Salve como:
```
propostas/[nome-slugificado]/proposta.html
```

Depois de salvar, abra automaticamente no navegador:
```bash
open propostas/[nome-slugificado]/proposta.html
```

Informe o usuário que a proposta foi aberta no navegador e que pode testar no mobile enviando o arquivo pelo WhatsApp.

---

## Etapa 5 — Deploy no GitHub Pages

Após o usuário aprovar a proposta, pergunte se quer publicar como link para enviar ao cliente.

Se sim, execute:

```bash
cd propostas/[nome-slugificado]/
cp proposta.html index.html
git init
git add index.html
git commit -m "proposta [nome-do-cliente]"
gh repo create proposta-[nome-slugificado] --public --source=. --push
```

Depois ative o GitHub Pages:
```bash
gh api -X PUT repos/$(gh api user --jq .login)/proposta-[nome-slugificado]/pages \
  --field source='{"branch":"main","path":"/"}'
```

Aguarde 30–60 segundos e informe a URL final:
```
https://[username].github.io/proposta-[nome-slugificado]/
```

Essa é a URL que o usuário envia para o cliente — abre direto no navegador, funciona no mobile, sem precisar abrir arquivo.

---

## O padrão que não negocia

1. **Estranho** — entende em 20 segundos o problema e por que essa é a pessoa certa
2. **Design** — parece agência premium, não documento do Word ou geração padrão de IA
3. **Humanidade** — nenhuma frase soa como IA. Direto, específico, com personalidade real
