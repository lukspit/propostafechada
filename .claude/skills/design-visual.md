# Design Visual — Páginas que Impressionam Antes de Ler

Baseado na skill oficial de frontend design da Anthropic. O objetivo é criar páginas que se destacam do que qualquer IA gera por padrão. Se o resultado parece genérico, está errado.

## Antes de qualquer decisão visual

Responda três perguntas:
1. O que o usuário vai lembrar dessa página depois de fechar?
2. Qual é a emoção que o design precisa transmitir (confiança, ambição, clareza, premium)?
3. O que diferencia visualmente essa proposta de qualquer outra que o cliente já recebeu?

Se não conseguir responder as três, o design não tem direção. Defina antes de começar.

---

## Tipografia — a primeira impressão antes do conteúdo

Nunca use fontes padrão (Arial, Helvetica, Times). Toda proposta precisa de pelo menos uma fonte com personalidade.

**Pares que funcionam:**
- Display bold + body clean: `Playfair Display` (headlines) + `Inter` ou `DM Sans` (corpo)
- Moderna + humanista: `Syne` ou `Space Grotesk` (headlines) + `Plus Jakarta Sans` (corpo)
- Sóbria premium: `Cormorant Garamond` (headlines) + `Jost` (corpo)
- Técnica forte: `Cabinet Grotesk` ou `Clash Display` (headlines) + `Satoshi` (corpo)

Tamanhos: headline principal 52–72px desktop / 36–48px mobile. Corpo mínimo 17px. Line-height corpo: 1.7.

Peso extremo funciona: headlines em 800–900 weight chamam atenção. Subtítulos em 400–500.

---

## Cor — sistema com dominância, não distribuição igual

Paleta com hierarquia clara:
- 1 cor dominante (fundo de seções, background principal)
- 1 cor de acento forte (CTAs, números, elementos de destaque) — usada com parcimônia, nunca em blocos grandes
- 1 neutro escuro para texto (#111 ou #0f0f0f, nunca #000 puro)
- 1 neutro suave para seções alternadas (off-white levemente quente: #fafaf8, #f7f6f3)

Cores tímidas em distribuição igual = resultado genérico. Acento usado em tudo perde o impacto.

---

## Composição — fuja do layout previsível

Não é uma lista de seções empilhadas com o mesmo padrão. Use:

**Seções hero (abertura):** fundo com cor ou gradiente sutil, headline grande ocupando mais de 60% da largura, sem timidez. No desktop, pode ter layout de 2 colunas com elemento visual à direita.

**Alternância de fundo:** nunca todas as seções com o mesmo fundo. Alterne: branco → off-white levemente tintado → branco → seção com acento da marca como fundo.

**Assimetria estratégica:** não tudo centralizado. Texto alinhado à esquerda, elemento visual à direita (desktop). Citações de depoimento em blockquote com borda lateral colorida.

**Espaço negativo:** seções generosas (padding 80–120px vertical desktop, 60–80px mobile). Respiração comunica qualidade.

---

## Elementos visuais — código puro, nunca emoji

**Proibido:** emojis como substituto de ícone ou elemento visual. São amadores em contexto profissional.

**Obrigatório:** todos os elementos visuais são feitos em código — SVG inline ou CSS shapes.

**SVG icons inline:** crie ícones simples direto no HTML. Um checkmark, uma seta, um círculo com linha — em SVG, sem dependência externa. Exemplo:
```html
<svg width="24" height="24" viewBox="0 0 24 24" fill="none">
  <path d="M20 6L9 17L4 12" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
</svg>
```

**CSS shapes como decoração:** bordas com gradiente, linhas decorativas, separadores com `border-image`, círculos de fundo sutis com `::before`/`::after`. Esses elementos adicionam profundidade sem peso.

**Separadores entre seções:** não use `<hr>` padrão. Use linha fina colorida com acento da marca, ou transição de fundo suave, ou elemento decorativo em SVG.

---

## Atmosfera e profundidade

Fundo liso único em todas as seções = página sem vida.

Técnicas que adicionam profundidade sem peso:
- **Gradient sutil no hero:** `background: linear-gradient(135deg, #ffffff 0%, #f5f0ff 100%)` (adapte para as cores da marca)
- **Círculo decorativo de fundo:** elemento `::before` com círculo grande, muito opaco (5–10%), posicionado fora do centro para assimetria
- **Borda com gradiente:** `border-image: linear-gradient(to right, var(--accent), transparent) 1`
- **Card com sombra elegante:** `box-shadow: 0 2px 40px rgba(0,0,0,0.06)` — suave, não dramático

---

## Animações — página com vida, não página estática

Toda proposta deve ter animações de entrada. Não pesadas, não chamativas — apenas presença.

**Padrão de animação CSS + Intersection Observer (vanilla JS, ~15 linhas):**

```css
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => e.isIntersecting && e.target.classList.add('visible'));
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

Aplique a classe `.reveal` em: cada seção, cards de entregáveis, depoimentos, o bloco de preço. Stagger entre elementos no mesmo grupo: adicione `transition-delay: 0.1s`, `0.2s`, `0.3s` progressivamente.

**Hero:** a headline principal pode ter animação de entrada na carga da página (sem Intersection Observer — direto com `animation: fadeInUp 0.8s ease forwards`).

Princípio: a animação existe para guiar o olho e dar sensação de qualidade. Se remover a animação e ficar igual, estava fraco.

---

## Desktop — usa o espaço, não desperdiça

Largura máxima de conteúdo: **900px** no desktop. Nunca 600px ou menos — desperdiça tela.

Seções com fundo colorido: o fundo vai full-width (`width: 100%`), mas o conteúdo interno fica em container centralizado com max-width.

Hero desktop: considere layout 2 colunas. Coluna esquerda com headline + CTA, coluna direita com elemento visual (SVG decorativo, número grande em destaque, ou grid de logos de clientes).

Nunca uma única coluna estreita flutuando no centro de uma tela larga. É o design mais genérico possível.
