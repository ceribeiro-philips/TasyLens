# TasyFinderField

**Modo Inspeção para o Tasy Web** — busca instantânea e destaque em tempo real em qualquer tela do sistema.

Extensão de navegador (Chrome/Edge) que adiciona um campo de busca fixo ao Tasy Web. Ao ativar, você filtra e encontra qualquer informação em tela na hora — sem rolar listas longas, sem depender de filtros nativos limitados e sem sair da página.

## Como funciona

1. Clique no ícone da extensão (ou pressione **Ctrl+Shift+F** / **Cmd+Shift+F** no Mac).
2. Um campo de busca aparece **fixo no cabeçalho**, ao lado do seu nome de usuário.
3. Digite o que procura — as linhas que não combinam somem da tela, e o trecho encontrado é destacado.
4. **Esc** ou o botão **✕** encerram o Modo Inspeção a qualquer momento, restaurando a tela ao normal.

## Recursos

### Busca universal, em qualquer tela
Reconhece e filtra, ao mesmo tempo:
- Tabelas HTML comuns;
- O **grid nativo do Tasy** (SlickGrid / `w-datagrid`);
- Grids ARIA genéricos;
- Campos de formulários de detalhe/cadastro (cada campo rótulo + valor vira uma linha filtrável);
- Listas simples, quando nada mais específico existe na tela;
- Telas dentro de **iframes de mesma origem** (comum no Tasy, que abre cada cadastro em um iframe).

### Integração nativa com o grid do Tasy
Sempre que possível, o filtro usa o **próprio mecanismo do SlickGrid** (via uma ponte com o Angular da página), em vez de esconder linhas manualmente. Isso evita gaps visuais e o risco de "perder" linhas fora da área visível em grids grandes ou paginados. Quando essa ponte não está disponível, a extensão cai automaticamente para o filtro por DOM, com compactação inteligente das linhas restantes.

### Busca por valor ou por nome técnico do campo
Além do que está visível na tela (ex.: "João", "Cancelado"), também é possível buscar pelo **nome técnico da coluna/atributo** usado internamente pelo Tasy (ex.: `NR_SEQ_EVENTO`, `DS_SISTEMA_ORIGEM`) — útil para quem conhece o campo pelo nome usado em relatórios e integrações. Ao encontrar, o cabeçalho da coluna correspondente é destacado.

### Ignora acentuação e maiúsculas/minúsculas
`joao`, `JOAO` e `João` encontram o mesmo resultado. A busca também alcança o valor de campos somente-leitura e atributos de `title`/`aria-label` (usados em células truncadas) — não só o texto visível diretamente.

### Expansão automática de seções recolhidas
Se o resultado estiver dentro de uma seção minimizada da tela de detalhe (ex.: "Valores", "Taxas"), a extensão a expande automaticamente — do jeito nativo do Tasy, sem forçar exibição por CSS — e a recolhe de novo ao limpar a busca. Seções que já estavam abertas antes nunca são mexidas.

### Aviso inteligente de paginação
Em grids grandes, a extensão sabe (usando o total real informado pelo próprio Angular do Tasy) se pode haver mais registros do que os já carregados na tela, e avisa explicitamente — sem tentar adivinhar ou paginar sozinha por conta própria.

### Desempenho: nunca compete com o Tasy
- Enquanto não há busca ativa, a extensão **não faz nenhum trabalho extra** de varredura, mesmo com a tela mudando sozinha em segundo plano.
- Em telas com múltiplos painéis carregando dados em paralelo, a extensão **espera o carregamento terminar** (detectando o próprio indicador nativo de carregamento do Tasy) antes de varrer a tela — em vez de competir com o Angular pelo processador no meio do carregamento.
- O filtro se **reaplica automaticamente** quando o Tasy recria a tela (rolagem, atualização de dados), sem nunca "sumir" silenciosamente.

### Ativação simples e não intrusiva
Um clique no ícone (ou atalho de teclado, customizável em **Opções**) liga/desliga o modo. O campo nunca flutua nem pode ser arrastado — fica sempre ancorado no mesmo lugar do cabeçalho.

## Privacidade e permissões

- Usa apenas as permissões `activeTab` e `scripting`: só age na aba onde você clicar no ícone.
- Não envia nem lê dados de fora da aba atual, não se comunica com nenhum servidor externo e não fica rodando em segundo plano em abas onde não foi ativada.

## Instalação (modo desenvolvedor)

1. Abra `chrome://extensions` (Chrome) ou `edge://extensions` (Edge).
2. Ative o **Modo do desenvolvedor**.
3. Clique em **Carregar sem compactação / Carregar expandida** e selecione a pasta do projeto.
4. Fixe o ícone na barra de ferramentas, se desejar.
5. Abra o Tasy Web e clique no ícone para começar a inspecionar.

## Limitações atuais (v1.0)

- A busca alcança apenas os registros **já carregados** na tela — não navega sozinha pelas páginas seguintes de grids grandes/paginados.
- A integração nativa com o grid ainda não alcança grids dentro de **iframes** (esses continuam funcionando, mas apenas com o filtro por DOM).
- **Iframes de outra origem** não são suportados (limitação de segurança do navegador).

---

*TasyFinderField é um ponto de partida — em evolução constante.*
