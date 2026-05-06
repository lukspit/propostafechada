# Proposta Fechada

Sistema Claude Code que gera propostas comerciais em formato de página de venda — persuasivas, com design profissional, criadas do zero com IA para cada cliente.

Não é um template. É um agente que entende o seu contexto e gera uma proposta única, com copy estratégica e visual que parece agência.

---

## O que está incluído

```
CLAUDE.md                          ← cérebro do sistema (lido automaticamente pelo Claude Code)
.claude/
  commands/
    proposta.md                    ← comando /proposta
  skills/
    copywriting.md                 ← copy persuasiva
    humanizacao.md                 ← texto que soa humano, não IA
    estrutura-proposta.md          ← anatomia da proposta vencedora
    gatilhos-conversao.md          ← Cialdini aplicado a propostas
    ui-ux.md                       ← design que vende antes de ler
```

---

## Pré-requisitos

- [Claude Code](https://claude.ai/code) instalado
- Assinatura ativa do Claude (Pro ou superior)

---

## Como usar

**1. Clone o repositório**
```bash
git clone https://github.com/lukspit/propostafechada.git
cd propostafechada
```

**2. Abra no Claude Code**
```bash
claude .
```

**3. Rode o comando**
```
/proposta
```

O agente vai conduzir a conversa, criar uma pasta para o cliente, coletar o contexto necessário e gerar a proposta como arquivo HTML pronto para abrir no navegador ou enviar pelo WhatsApp.

---

## Como funciona

1. Você informa o nome do cliente → o sistema cria a pasta `propostas/nome-do-cliente/`
2. Adiciona os arquivos que tiver (logo, briefing, transcrição de reunião) — tudo opcional
3. Responde algumas perguntas estratégicas sobre o projeto
4. Informa as cores da sua marca e qualquer referência visual
5. O sistema gera `proposta.html` na pasta do cliente — abre direto no navegador, funciona no mobile

---

## Output

Uma página HTML completa, autocontida, mobile-first. Sem dependências externas. Abre no navegador com dois cliques ou envia pelo WhatsApp como link.
