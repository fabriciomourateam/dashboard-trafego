# Método de Gestão de Tráfego — Playbook do Fabricio

> Guia pra você entender o que um gestor de tráfego faz, ler seus próprios números e,
> se quiser, ir assumindo a operação com o Claude Code como copiloto.
> Escrito a partir da análise real da conta (Google Ads + CRM), ago/2026.

---

## 1. O panorama do seu negócio (pra decisão ficar com pé no chão)

- Você investe **~R$34 mil/mês** em mídia (Google ~R$28,5k + Meta ~R$6k).
- Paga **~R$20 mil/ano** (~R$1,7k/mês) ao gestor — isso é **~5% da mídia**. A taxa é barata.
- O caro não é o gestor: é a **estratégia rodando torta** sobre R$34k/mês. Um ganho de
  20% de eficiência = **~R$6,8k/mês**, que faz a mensalidade do gestor virar detalhe.

**Conclusão honesta:** o primeiro objetivo não é "demitir pra economizar R$1,7k". É
**construir visibilidade** (o painel + atribuição de venda) pra você (a) cobrar o gestor
com número de VENDA e não de lead, e (b) poder assumir depois, já entendendo as alavancas.
Dá pra você rodar sozinho — mas comece como dono informado, não como aposta no escuro.

---

## 2. Os 5 números que importam (e só esses, pra começar)

Esqueça "impressões", "cliques" e "CTR" no início. O que decide o resultado:

| Número | O que é | Onde ver | Meta saudável (seu caso) |
|--------|---------|----------|--------------------------|
| **CPL** (custo por lead) | Gasto ÷ leads reais (CRM) | painel | quanto menor, mas cuidado: barato demais = lixo |
| **Taxa lead→call** | % de leads que agendam call | CRM | quanto maior, melhor (hoje ~20%) |
| **CAC** (custo por venda) | Gasto ÷ vendas do canal | painel | < R$400 é ótimo pro seu ticket |
| **Ticket médio** | R$ por venda | CRM (`lead_sales`) | ~R$2.300 |
| **ROAS** | (vendas × ticket) ÷ gasto | painel | > 4x bom, > 6x ótimo |

**A regra de ouro:** CPL baixo NÃO é vitória. Você já provou isso — de maio pra cá o CPL
despencou (R$112→R$29) e mesmo assim a venda caiu. **Otimize por CAC e ROAS, nunca por CPL.**

---

## 3. O erro estrutural que está te custando caro

O Google Ads otimiza pelo que você **manda ele otimizar**. Hoje ele otimiza por
"conversão = preenchimento de formulário". Resultado: ele fica **excelente em achar gente
que preenche formulário de graça** — e ruim em achar gente que **compra**.

Prova nos dados: o Google contou **~11.300 "conversões"**; o CRM tem **~2.574 leads** e
**~200 vendas**. Ele está mirando um alvo 4–5x maior que o lead real.

**A correção (maior alavanca que você tem):**
1. Capturar o `gclid` (id do clique do Google) no formulário de leads.
2. Quando a venda acontece no CRM, mandar essa venda **de volta** pro Google (importação
   de conversão offline), amarrada pelo `gclid`.
3. Trocar o objetivo da campanha pra otimizar por **essa** conversão (venda), não por formulário.

Efeito: o algoritmo passa a caçar **comprador**, não formulário. É a diferença entre
"lead barato" e "cliente".

> ⚠️ Isso exige uma pequena mudança no `controle-de-pacientes` (capturar gclid/utm no form)
> e uma configuração no Google Ads. Posso implementar a parte do formulário se você me
> der acesso de escrita naquele repositório.

---

## 4. A rotina do gestor (o que fazer e quando)

### 🗓️ Diária (5 min)
- Olhar gasto do dia e se alguma campanha parou/estourou orçamento.
- Ver se entraram leads (CRM) — volume anormalmente alto ou zero = alerta.

### 🗓️ Semanal (30–45 min) — a rotina que mais rende
1. **Relatório de termos de pesquisa** (Google Ads → Palavras-chave → Termos de pesquisa):
   ler o que as pessoas *realmente* digitaram. Marcar como **negativa** tudo que não é
   cliente (convênio, grátis, emprego, curso, cidade que você não atende, app concorrente).
2. **Palavras que convertem** → migrar de correspondência **ampla** para **frase/exata**.
3. Ver **CAC por campanha** (cruzando com o CRM): pausar/reduzir quem tem CAC alto,
   escalar quem tem CAC baixo.
4. Conferir a **taxa lead→call** da semana. Caindo? O lead piorou (segmentação) ou o
   atendimento demorou.

### 🗓️ Mensal (1–2h)
- Fechar CAC, ROAS e ticket do mês (o painel faz isso).
- Comparar com o mês anterior. Decidir realocação de verba entre canais.
- Testar 1 coisa nova por vez (criativo, público, oferta) — nunca várias juntas.

### 🚦 Regra dos 3 dias
Mexeu em lance/orçamento/segmentação? **Espere 3–4 dias** antes de julgar. O algoritmo
reaprende. Mexer todo dia = nunca sai da fase de aprendizado.

---

## 5. Checklist de otimização (as alavancas, por ordem de impacto)

1. ✅ **Atribuição de venda** (seção 3) — antes de tudo.
2. ✅ **Podar broad match** — `nutricionista online` em ampla queimou ~R$121k. Migrar
   termos vencedores pra frase/exata.
3. ✅ **Negativas** — lista pronta no painel. Revisar toda semana.
4. ✅ **CAC por campanha** — cortar o que não paga, escalar o que paga.
5. ✅ **Ajuste por dispositivo/horário** — 92% em celular; madrugada (0–5h) tem baixa
   intenção → reduzir lance nesse período.
6. ✅ **Público** — pago converte homem 25–34; orgânico (ViralOS) mira mulher 35–44.
   Decidir se alinha os dois ou trata como funis separados.
7. ✅ **Criativo/oferta** — onde o ViralOS já te ajuda a produzir volume.

---

## 6. Como usar o Claude Code pra isso (o copiloto)

O que dá pra automatizar/apoiar aqui comigo:

- **Toda semana:** você exporta os CSVs do Google Ads, joga na pasta `csv_novos/` e me
  pede pra atualizar o painel + gerar a lista de negativas e o CAC por canal. Posso deixar
  isso rodando em rotina automática e te avisar o que mudou.
- **Análise de desperdício:** eu leio os termos de pesquisa e te entrego a lista de
  negativas pronta pra colar no Google Ads.
- **Cruzamento com venda:** eu puxo o funil real do CRM e calculo CAC/ROAS de verdade.
- **O que ainda é você (ou API):** clicar dentro do Google Ads pra aplicar as mudanças.
  Isso pode ser automatizado depois conectando a **API do Google Ads** — é um passo a mais,
  mas viável.

**Caminho sugerido de transição (60–90 dias):**
1. Mês 1: eu monto a visibilidade (feito) + você aprende a ler o painel semanalmente.
2. Mês 2: você começa a aplicar as ações (negativas, lances) com minha recomendação.
3. Mês 3: você decide — manter o gestor, trocar por um mais barato, ou assumir de vez.

---

## 7. Correções de dados pendentes no CRM (pra relatório parar de mentir)

Achados na análise que precisam de ajuste no `controle-de-pacientes`:

- **`origem` fragmentada:** `indicação` / `indicacao` / `Indicação` são a mesma coisa
  contadas separado; idem `google forms` / `google_forms`. → normalizar para valores fixos.
- **Faturamento não lançado:** 48 das 78 vendas de julho e 25 de 25 de agosto estão sem
  `gross_value`. → preencher, e idealmente tornar o campo obrigatório no fechamento.
- **Sem `gclid`/`utm` nos leads:** impossível saber qual campanha gera venda (seção 3).
  → capturar no formulário.

> Essas três correções são o que separa "achismo" de "decisão com dado". As duas primeiras
> são rápidas; a terceira é a de maior retorno.

---

*Dúvida em qualquer ponto: me chama aqui no Claude Code que eu detalho ou executo.*
