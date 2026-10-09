# Painel de Estoque e Pagamento da Dívida Pública — SEPLAN MA

Dashboard web (100% client-side) para análise do **estoque da dívida pública** e do **fluxo de pagamentos**, com **atualização por planilha Excel** direto no navegador.

> Analista & Gestor de Dívida Pública — **Jokson Muniz** · SEPLAN MA

---

## ✨ Funcionalidades

| Recurso | Descrição |
|---|---|
| **Upload de Excel** | Botão *Atualizar planilha* ou arraste-e-solte o `.xlsx`. Lê as abas `BASE ESTQ`, `BASE PGTO`, `SALDO DEVEDOR 2025` e `PROJ DIVIDA`. |
| **KPIs automáticos** | Saldo total devedor, dívida interna, externa, reestruturação, pagamentos acumulados e nº de contratos — com variação vs. mês anterior. |
| **Gráficos** | Rosca (composição por tipo), barras horizontais (credor, componente de pagamento, concentração) e séries temporais (evolução do saldo + projeção, pagamentos por ano). |
| **Filtros** | Ano, mês de competência, tipo de dívida, credor e busca livre — tudo recalcula na hora. |
| **Comparativo entre competências** | Quatro meses lado a lado: cards de resumo por competência (saldo, composição e variação), tabela contrato × competência com variação absoluta, Δ % e sparkline de tendência, e exportação do comparativo em CSV. |
| **Tabelas** | Contratos ordenáveis, paginados e com total; tabela de projeção por contrato. |
| **Exportação** | CSV dos dados filtrados e impressão / PDF do painel. |
| **Tema** | Claro e escuro, com preferência salva. |
| **Privacidade** | Nenhum dado sai do computador — todo o processamento ocorre no navegador. A base fica salva em `localStorage` para a próxima visita. |
| **Responsivo** | Adaptado para desktop, tablet e celular. |

---

## 🚀 Publicar no GitHub Pages

### Opção A — Interface web (mais simples)

1. Crie um repositório novo em <https://github.com/new> (ex.: `painel-divida-seplan`), marcando **Public**.
2. Na página do repositório, clique em **Add file → Upload files**.
3. Envie o arquivo `index.html` (e, se quiser, este `README.md`).
4. Commit em **Commit changes**.
5. Vá em **Settings → Pages**.
6. Em *Build and deployment → Source*, escolha **Deploy from a branch**.
7. Selecione a branch **main** e a pasta **/ (root)**. Clique em **Save**.
8. Aguarde ~1 minuto. O painel estará em:
   `https://<seu-usuario>.github.io/<nome-do-repositorio>/`

### Opção B — Linha de comando

```bash
git init
git add index.html README.md
git commit -m "feat: painel de estoque e pagamento da dívida pública"
git branch -M main
git remote add origin https://github.com/<seu-usuario>/<nome-do-repositorio>.git
git push -u origin main
```

Depois ative o GitHub Pages em **Settings → Pages** (branch `main`, pasta `/ (root)`).

> O painel é um **único arquivo HTML autocontido** — funciona também aberto localmente com duplo clique, sem servidor.

---

## 🔀 Comparativo entre competências

A seção **Comparativo entre competências** permite colocar **quatro meses lado a lado** (por padrão, os quatro últimos meses completos da base).

- **Seletores de competência** — escolha livremente qualquer mês da série em cada um dos quatro campos; o painel recalcula na hora.
- **Cards de resumo** — para cada competência: saldo total, variação percentual vs. mês anterior, barra de composição (interna / externa / reestruturação), valores por tipo e nº de contratos.
- **Rodapé do período** — variação acumulada entre a primeira e a última competência (R$ e %), saldo final, média mensal, máximo e mínimo.
- **Tabela contrato × competência** — uma coluna por mês, com a variação absoluta, o Δ % e uma **sparkline de tendência** por contrato. Ordenada pelos maiores movimentos de saldo.
- **Exportação CSV** — botão *CSV* no cabeçalho da seção, com os mesmos filtros aplicados.

O comparativo **respeita todos os filtros** do painel (tipo de dívida, credor e busca livre), além de acompanhar a atualização da planilha.

---

## 📋 Formato esperado da planilha

O painel localiza as abas e os cabeçalhos **automaticamente** (tolerante a variações de nome e de ordem das colunas).

| Aba | Colunas usadas | Uso no painel |
|---|---|---|
| `BASE ESTQ` | `CONTRATO`, `TIPO`, `SALDO`, `DATA` | Estoque por competência, KPIs, rosca, evolução |
| `BASE PGTO` | `CONTRATO`, `MÊS`, `ANO`, `TIPO`, `PRINCIPAL`, `JUROS`, `ENCARGOS`, `TOTAL` | Fluxo de pagamentos por ano/componente |
| `SALDO DEVEDOR 2025` | `CONTRATO` + colunas mensais | Série histórica mensal |
| `PROJ DIVIDA` | `CONTRATO`, `ACUMULADO` e `MÉDIA` (principal/juros/encargos) | Projeção por contrato |

**Regras de leitura**

- A **competência de referência** é o último mês cujo saldo representa ≥ 50 % do maior saldo da série — isso ignora automaticamente meses parciais/incompletos.
- O **credor** é derivado do nome do contrato (BNDES, Caixa Econômica, BID, Banco do Brasil, Lei 9.496/PROPAG).
- Datas aceitas: formato de data do Excel ou texto `AAAA-MM-DD` / `DD/MM/AAAA`.

---

## 🛠️ Tecnologias

- HTML + CSS + JavaScript puro (sem build, sem dependências de runtime).
- Gráficos em **SVG** desenhados sob medida.
- Leitura de `.xlsx` via [SheetJS](https://sheetjs.com/) carregado sob demanda por CDN (com 3 CDNs de fallback).

---

## 📄 Licença

Uso interno — SEPLAN MA. Ajuste conforme a política de publicação da instituição.
