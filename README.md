# Dashboard de Projeção Eleitoral 2026

Dashboard interativo para exploração de cenários do **2º turno da eleição presidencial brasileira de 2026**.

O projeto foi desenvolvido como uma aplicação web estática, com foco em **análise de dados, lógica de negócio, modelagem estatística, validação de entradas, segurança e visualização interativa**.

> **Importante:** este projeto não é uma IA que “prevê” o resultado da eleição. É um **modelo de projeção baseado em regras, dados de pesquisas e premissas estatísticas**. Os resultados são cenários modelados e não substituem pesquisas, apuração oficial ou previsão eleitoral calibrada.

## Demonstração

**Aplicação publicada:**  
https://projecaoeleicoes2026.pages.dev/

## Como o modelo funciona

O painel combina dados de pesquisas e parâmetros configuráveis para recalcular cenários de forma dinâmica no navegador.

Entre os fatores considerados estão:

- data e período de campo das pesquisas;
- tamanho da amostra;
- margem de erro;
- efeito de desenho amostral;
- qualidade/ajuste atribuído ao instituto;
- dispersão entre institutos;
- premissas de participação, migração e comportamento eleitoral;
- dados estaduais disponíveis e estrutura observada do 1º turno.

A lógica de ponderação utiliza decaimento temporal: pesquisas mais recentes ganham maior influência e levantamentos mais antigos perdem peso gradualmente.

De forma simplificada, o peso relativo implementado no modelo segue a estrutura:

```text
peso ∝ (amostra / efeito de desenho)
       × exp(-dias / τ)
       × qualidade do instituto
       / (margem² + erro sistemático²)
```

O painel também executa **simulações de Monte Carlo** para representar incerteza dos cenários. A frequência obtida nas simulações é tratada no próprio sistema como uma medida interna do modelo e **não como probabilidade eleitoral calibrada**.

## Tecnologias

- **HTML5** — estrutura da aplicação;
- **CSS3** — layout responsivo, temas e componentes visuais;
- **JavaScript (Vanilla)** — regras de negócio, cálculos, simulações, manipulação do DOM e interatividade;
- **JSON** — estrutura e atualização de dados;
- **Web Storage / localStorage** — persistência local de preferências e dados importados;
- **Git / GitHub** — versionamento e código-fonte;
- **Cloudflare Pages** — deploy e hospedagem da aplicação estática.

## Funcionalidades

- recálculo automático dos cenários após alteração de parâmetros;
- visualização nacional e por UF;
- gráficos atualizados dinamicamente;
- importação e validação de pesquisas;
- tratamento de pesquisas nacionais e estaduais;
- substituição de rodadas antigas do mesmo instituto por dados mais recentes quando aplicável;
- armazenamento local de configurações;
- interface responsiva;
- suporte a **Português, Inglês e Espanhol**;
- modo claro e escuro;
- validação de URLs, JSON e arquivos importados;
- controles para reduzir entrada de dados inválidos ou incompatíveis.

## Segurança

O projeto utiliza cabeçalhos de segurança no Cloudflare Pages, incluindo:

- **Content Security Policy (CSP)**;
- **HSTS**;
- **X-Content-Type-Options**;
- **X-Frame-Options**;
- **Referrer-Policy**;
- **Permissions-Policy**;
- restrições de origem para scripts, conexões, frames e outros recursos.

Também há validações no JavaScript para conteúdo externo e dados importados.

## Arquitetura

A aplicação foi propositalmente mantida como um projeto estático: os cálculos e a maior parte da lógica são executados diretamente no navegador.

```text
GitHub
   │
   ▼
Cloudflare Pages
   │
   ▼
index.html
   ├── HTML
   ├── CSS
   ├── JavaScript
   ├── modelo estatístico
   ├── validações
   └── visualizações
```

O arquivo `pesquisas-atualizadas.json` funciona como fonte externa versionada para atualizações de pesquisas sem alterar a estrutura principal da aplicação.

## Por que o GitHub mostra 100% HTML?

O GitHub classifica a linguagem principalmente pela extensão dos arquivos.

Neste projeto, uma parte relevante do **CSS e do JavaScript está incorporada ao próprio `index.html`**. Por isso o GitHub pode exibir o repositório como 100% HTML, mesmo com grande parte da lógica, dos cálculos e das interações implementada em JavaScript e a apresentação construída em CSS.

## Objetivo técnico

Este projeto foi desenvolvido aplicando conhecimentos de **Análise e Desenvolvimento de Sistemas**, passando por diferentes etapas de uma solução real:

**levantamento do problema → definição de regras → modelagem dos dados → implementação → validação → testes → segurança → versionamento → deploy.**

Além da interface, o foco do projeto está principalmente na lógica que transforma dados e premissas em cenários reproduzíveis e auditáveis.

## Aviso metodológico

Este é um projeto independente e exploratório. Uma projeção modelada não representa resultado oficial e não deve ser interpretada como garantia de resultado eleitoral.

Fontes, registros e metadados das pesquisas utilizadas podem ser consultados diretamente no próprio painel.
