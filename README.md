# 🔎 TasyLens

> **Sua lente de inspeção para o TasyHTML.**

O **TasyLens** é uma extensão para Chrome e Edge que adiciona um **Modo de Inspeção inteligente ao TasyHTML**, permitindo localizar informações instantaneamente em qualquer tela do sistema.

Em vez de percorrer listas extensas, utilizar filtros nativos ou procurar manualmente por informações, basta ativar o TasyLens e começar a digitar.

O TasyLens identifica o conteúdo disponível na tela, filtra os resultados em tempo real e destaca exatamente onde a informação foi encontrada.

---

## ✨ O que o TasyLens faz?

O TasyLens transforma qualquer tela do TasyHTML em uma área de busca instantânea.

Com um único campo de pesquisa, é possível encontrar:

* Valores exibidos na tela;
* Registros em tabelas;
* Informações em grids;
* Campos de formulários;
* Valores somente leitura;
* Conteúdo de listas;
* Informações dentro de seções recolhidas;
* Campos por seus nomes técnicos;
* Conteúdo localizado em iframes de mesma origem.

### Exemplo

Imagine uma tela com centenas de registros.

Você precisa encontrar:

```text
João da Silva
```

Basta ativar o TasyLens e pesquisar:

```text
joao
```

O TasyLens:

1. Identifica os elementos compatíveis;
2. Remove visualmente os registros que não correspondem;
3. Mantém apenas os resultados relevantes;
4. Destaca o trecho encontrado;
5. Reaplica o filtro caso o TasyHTML atualize ou recrie a tela.

Tudo isso sem sair da página.

---

# 🚀 Principais recursos

## 🔎 Busca universal

O TasyLens não depende de um único tipo de componente.

A busca identifica automaticamente a estrutura disponível na tela e utiliza a estratégia mais adequada.

Suporta:

* Tabelas HTML;
* SlickGrid;
* `w-datagrid`;
* Grids com ARIA;
* Formulários;
* Campos de detalhe;
* Listas;
* Conteúdo dinâmico;
* Iframes de mesma origem.

---

## ⚡ Integração com o Grid do TasyHTML

Quando disponível, o TasyLens utiliza o próprio mecanismo de filtragem do **SlickGrid / Angular do TasyHTML**, em vez de simplesmente esconder elementos do DOM.

Isso traz algumas vantagens importantes:

* Evita gaps visuais;
* Preserva o comportamento natural do grid;
* Funciona melhor com grandes volumes de dados;
* Reduz manipulações desnecessárias no DOM;
* Evita perder linhas que estão fora da área atualmente renderizada;
* Mantém o comportamento de paginação do próprio TasyHTML.

Quando a integração nativa não está disponível, a extensão cai automaticamente para o filtro por DOM, utilizando uma estratégia de compactação inteligente das linhas restantes.

### Estratégia de fallback

```text
                         TasyHTML
                            │
                            ▼
                       TasyLens
                            │
                ┌───────────┴───────────┐
                │                       │
                ▼                       ▼
          Tasy Grid                Outros elementos
                │                       │
                ▼                       ▼
      Ponte Angular disponível     Inspeção DOM
                │                       │
                ▼                       │
        Filtro nativo                  │
                │                       │
                └───────────┬───────────┘
                            ▼
                    Resultado filtrado
```

O usuário não precisa escolher o método.

---

## 🧠 Busca por valor ou nome técnico

O TasyLens não procura apenas aquilo que está visualmente escrito na tela.

Também é possível pesquisar pelo **nome técnico da coluna ou atributo utilizado internamente pelo TasyHTML**.

Por exemplo:

```text
NR_SEQ_EVENTO
```

ou:

```text
DS_SISTEMA_ORIGEM
```

Ao encontrar o nome técnico de um campo, o TasyLens identifica a coluna correspondente e destaca o cabeçalho.

Esse recurso é especialmente útil para profissionais que trabalham com:

* Suporte;
* Desenvolvimento;
* Integrações;
* Relatórios;
* Análise de incidentes;
* Investigação de comportamento;
* Identificação de campos técnicos.

---

## 🔤 Busca inteligente

A busca ignora diferenças de:

* Maiúsculas e minúsculas;
* Acentuação.

Portanto:

```text
joao
```

encontra igualmente:

```text
João
JOÃO
joão
JoAo
```

Além do texto visível, a pesquisa também considera informações disponíveis em:

* `title`;
* `aria-label`;
* Atributos de elementos;
* Valores de campos somente leitura.

Isso permite encontrar informações mesmo quando o conteúdo está truncado visualmente ou não está diretamente disponível como texto visível.

---

## 📂 Expansão automática de seções

Em telas de detalhe do TasyHTML, algumas informações podem estar dentro de seções recolhidas.

Por exemplo:

```text
▼ Dados Gerais
▼ Atendimento
▶ Valores
▶ Taxas
▶ Informações Complementares
```

Se o resultado da pesquisa estiver dentro de uma seção minimizada, o TasyLens:

1. Identifica a seção;
2. Expande a seção utilizando o comportamento nativo do TasyHTML;
3. Localiza o resultado;
4. Destaca a informação encontrada.

Ao limpar a busca, a seção é recolhida novamente.

### Importante

Se uma seção já estava aberta antes da busca, o TasyLens **não altera seu estado**.

O objetivo é preservar exatamente o estado original da tela.

---

## 📊 Aviso inteligente de paginação

Em grids grandes, o TasyLens não tenta adivinhar se existem registros adicionais.

Quando possível, utiliza o **total real informado pelo próprio Angular/TasyHTML** para identificar se existem mais registros do que aqueles atualmente carregados na tela.

Assim, quando necessário, o usuário recebe um aviso explícito.

### Exemplo

```text
Resultados encontrados: 3

⚠️ O grid possui 1.248 registros.
A busca foi realizada sobre os registros carregados atualmente.
```

Isso evita a falsa impressão de que a busca encontrou zero resultados simplesmente porque o registro está em outra página.

O TasyLens **não pagina automaticamente**.

Essa decisão é intencional para evitar alterar o comportamento original do TasyHTML ou realizar navegações inesperadas.

---

# 🖥️ Modo de Inspeção

O TasyLens funciona como um modo temporário de inspeção.

### Ativação

Clique no ícone da extensão ou utilize:

**Windows / Linux**

```text
Ctrl + Shift + F
```

**macOS**

```text
Cmd + Shift + F
```

Ao ativar, um campo de busca aparece **fixo no cabeçalho do TasyHTML, ao lado do nome do usuário**.

### Pesquisa

Digite o que procura.

As linhas que não correspondem à pesquisa deixam de ser exibidas e o trecho encontrado é destacado em tempo real.

### Encerramento

Pressione:

```text
Esc
```

ou utilize o botão:

```text
✕
```

O Modo de Inspeção é encerrado e a tela retorna ao estado normal.

---

# 🎯 Ativação simples e não intrusiva

O TasyLens foi projetado para funcionar **junto com o TasyHTML**, sem interferir permanentemente na experiência do usuário.

O campo de busca:

* É fixo no cabeçalho;
* Não flutua pela tela;
* Não pode ser arrastado;
* Não altera permanentemente o layout;
* Pode ser encerrado a qualquer momento;
* Permanece sempre no mesmo local.

A intenção é que o usuário ative o recurso quando precisar e volte ao TasyHTML normal quando terminar a inspeção.

---

# ⚙️ Performance

Performance é uma das premissas do TasyLens.

Quando não existe uma busca ativa:

> **O TasyLens não realiza nenhum trabalho extra de varredura da página.**

Mesmo que a tela do TasyHTML esteja mudando em segundo plano, a extensão não fica analisando continuamente o DOM sem necessidade.

A inspeção acontece somente quando existe uma pesquisa ativa ou quando é necessário manter uma pesquisa já iniciada.

---

## ⏳ Carregamento inteligente

Em telas com múltiplos painéis carregando dados em paralelo, o TasyLens pode aguardar o carregamento terminar antes de realizar a varredura.

Para isso, utiliza o próprio indicador nativo de carregamento do TasyHTML sempre que disponível.

Isso evita que a extensão dispute processamento com o Angular enquanto a tela ainda está sendo construída.

O objetivo é simples:

```text
Carregamento do TasyHTML
          │
          ▼
     Aguarda conclusão
          │
          ▼
      TasyLens
          │
          ▼
    Realiza inspeção
```

Em vez de:

```text
Carregamento do TasyHTML
          │
          ├───────────────┐
          │               │
          ▼               ▼
       Angular         TasyLens
          │               │
          └───────┬───────┘
                  ▼
          Disputa processamento
```

---

# 🔄 Reaplicação automática

O TasyHTML pode recriar partes da interface durante:

* Rolagem;
* Atualização de dados;
* Re-renderização de componentes;
* Carregamentos assíncronos;
* Atualizações de grids;
* Alterações de estado da tela.

Quando isso acontece, uma pesquisa ativa não deve simplesmente desaparecer.

O TasyLens identifica a alteração e reaplica automaticamente o filtro quando necessário.

### Sem o TasyLens

```text
Usuário pesquisa
       ↓
Resultado aparece
       ↓
TasyHTML atualiza a tela
       ↓
Filtro desaparece
```

### Com o TasyLens

```text
Usuário pesquisa
       ↓
Resultado aparece
       ↓
TasyHTML atualiza a tela
       ↓
TasyLens identifica a alteração
       ↓
Filtro é reaplicado
       ↓
Resultado continua disponível
```

Isso evita que o usuário precise realizar a mesma pesquisa repetidamente.

---

# 🧩 Cobertura de elementos

O TasyLens utiliza diferentes estratégias de inspeção dependendo da estrutura encontrada na tela.

A estratégia é determinada automaticamente.

```text
                         ┌──────────────────┐
                         │     TasyHTML     │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │     TasyLens     │
                         │ Modo de Inspeção │
                         └────────┬─────────┘
                                  │
             ┌────────────────────┼────────────────────┐
             │                    │                    │
             ▼                    ▼                    ▼
       ┌───────────┐        ┌───────────┐       ┌───────────┐
       │ Tasy Grid │        │ Formulário│       │   Outros  │
       └─────┬─────┘        └─────┬─────┘       └─────┬─────┘
             │                    │                    │
             ▼                    ▼                    ▼
      Filtro nativo          Inspeção DOM         Inspeção DOM
             │                    │                    │
             └────────────────────┼────────────────────┘
                                  ▼
                         ┌──────────────────┐
                         │     Resultado    │
                         │ filtrado +       │
                         │ destacado       │
                         └──────────────────┘
```

---

# 🪟 Iframes

O TasyHTML pode utilizar iframes para carregar determinadas telas ou cadastros.

O TasyLens consegue acessar **iframes de mesma origem**, permitindo que a busca alcance informações que estejam dentro desses contextos.

Quando uma tela é aberta dentro de um iframe de mesma origem, o TasyLens pode realizar a inspeção normalmente, respeitando as estratégias disponíveis para aquele conteúdo.

### Exemplo conceitual

```text
TasyHTML
│
├── Tela principal
│
├── Grid
│
└── iframe
    │
    ├── Cadastro
    ├── Campos
    └── Informações
```

A busca pode alcançar os elementos disponíveis nesses contextos quando eles pertencem à mesma origem.

---

# 🔐 Privacidade e permissões

O TasyLens foi desenvolvido seguindo o princípio de **mínimo acesso necessário**.

A extensão utiliza apenas as permissões necessárias para executar a inspeção na aba em que o usuário ativou o recurso:

```text
activeTab
scripting
```

O TasyLens:

* Não envia dados para servidores externos;
* Não se comunica com APIs externas;
* Não armazena dados do TasyHTML;
* Não coleta informações do usuário;
* Não mantém cópias das informações encontradas;
* Não executa varreduras em abas onde não foi ativado;
* Atua somente sobre a aba em que o usuário iniciou o Modo de Inspeção.

As informações pesquisadas permanecem no contexto da própria página.

---

# 🌐 Compatibilidade

O TasyLens foi desenvolvido para navegadores baseados em Chromium.

| Navegador                   | Suporte                                 |
| --------------------------- | --------------------------------------- |
| Google Chrome               | ✅                                       |
| Microsoft Edge              | ✅                                       |
| Outros navegadores Chromium | 🟡 Pode variar conforme a implementação |

---

# 📦 Instalação

Atualmente o TasyLens pode ser carregado como uma extensão local utilizando o modo de desenvolvedor do navegador.

## Google Chrome

Acesse:

```text
chrome://extensions
```

## Microsoft Edge

Acesse:

```text
edge://extensions
```

Depois:

1. Ative o **Modo do desenvolvedor**;
2. Clique em **Carregar sem compactação** ou **Carregar expandida**;
3. Selecione a pasta do projeto;
4. Fixe o TasyLens na barra de ferramentas, se desejar;
5. Abra o TasyHTML;
6. Clique no ícone do TasyLens;
7. Inicie o Modo de Inspeção.

---

# ⚠️ Limitações atuais

## Registros não carregados

A busca alcança apenas os registros **já carregados na tela**.

O TasyLens não navega automaticamente pelas páginas seguintes de grids grandes ou paginados.

Quando existem mais registros do que aqueles carregados atualmente, o TasyLens utiliza as informações disponíveis no TasyHTML para informar essa possibilidade ao usuário.

---

## Iframes

A integração nativa com o Grid do Tasy ainda não está disponível para grids localizados dentro de iframes.

Nesses casos, o conteúdo continua sendo suportado pelo TasyLens, porém utilizando a estratégia de **filtro via DOM**.

---

## Iframes de outra origem

Iframes pertencentes a outra origem não podem ser inspecionados devido às políticas de segurança do navegador.
