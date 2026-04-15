# CLAUDE.md

Este arquivo orienta o Claude Code ao trabalhar neste repositório.

## Visão Geral do Projeto

Este projeto é uma SPA em arquivo único, usada como guia interno de suporte para o sistema **Squalus Gestão**.

Pasta do projeto:
`C:\Fminds\projeto-apoio-config-sagres`

Arquivos principais:
- `index.html` → guia principal exibido no navegador / GitHub Pages
- `calibrate.html` → ferramenta interna para calibrar as áreas dos campos nos prints
- `prints/` → imagens das telas usadas no guia e na calibração

Não há build, dependências externas nem servidor. Basta abrir os arquivos HTML no navegador.

## Arquitetura

A maior parte da lógica está no `index.html`, organizada em três blocos principais:

1. `<style>` — CSS completo em tema escuro, usando variáveis em `:root`.
2. `<body>` — seções da página em `<section class="page-section" id="...">`.
3. `<script>` — controla navegação, busca, modal de imagem, destaque de campos e comportamento visual.

O `calibrate.html` é a ferramenta auxiliar usada para:
- listar as imagens disponíveis
- listar os campos de cada tela
- marcar canto superior esquerdo e canto inferior direito
- gerar o bloco de coordenadas para uso no `index.html`

## Objetivo Principal

Quando eu enviar:
1. o caminho da tela no sistema
2. um print da tela de configuração

você deve:
- identificar e mapear os campos visíveis
- criar a nova estrutura no `index.html`
- adicionar a mesma tela no `calibrate.html`
- manter consistência total entre nomes, ids e arquivos
- deixar o projeto pronto para calibração
- preservar o funcionamento correto do botão **Exibir na tela**

## Fluxo Operacional Obrigatório

### Etapa 1 — Ler o pedido
Sempre identificar:
- caminho da tela no sistema
- nome da tela
- melhor id para a seção
- nome padronizado do arquivo de print
- campos visíveis
- agrupamentos de campos
- tipo de campo: seleção, texto, número, data, etc.

### Etapa 2 — Atualizar o `index.html`
Ao criar uma nova tela, atualizar:
1. o item da sidebar
2. o card da home, quando fizer sentido
3. uma nova `<section>` com:
   - `id` único
   - `data-section-img="prints/NOME_DO_ARQUIVO.png"`
   - breadcrumb
   - título
   - descrição curta
   - bloco de print com placeholder
   - note-box com caminho de acesso
   - uma ou mais tabelas em `fields-card`
4. a estrutura de coordenadas correspondente usada pelo projeto

### Etapa 3 — Atualizar o `calibrate.html`
Sempre adicionar:
- a nova imagem na lista de imagens
- o label da nova tela
- os grupos de campos
- exatamente os mesmos nomes de campos usados no `index.html`

### Etapa 4 — Preparar para calibração
Depois da estrutura HTML criada:
- o print deve ser esperado dentro de `prints/NOME_DO_ARQUIVO.png`
- a tela deve aparecer no `calibrate.html`
- o usuário deve conseguir abrir a calibração e marcar os campos
- após a calibração, as coordenadas geradas devem corresponder exatamente aos nomes dos campos

## Regras Críticas de Consistência

Este projeto depende fortemente de correspondência exata de texto.

Os itens abaixo devem permanecer consistentes entre si:
- `id` da seção
- `data-section-img`
- nome do arquivo em `prints/`
- nome do campo exibido no `index.html`
- nome do campo registrado no `calibrate.html`
- chaves e labels usados na estrutura de coordenadas

Se um nome for alterado de forma inconsistente, o botão **Exibir na tela** pode:
- parar de funcionar
- abrir o print errado
- destacar a área errada

## Regras de Nomenclatura

### Nome dos prints
Sempre usar nomes curtos, em `snake_case`, sem espaços.

Exemplos:
- `prints/cfg_gerais.png`
- `prints/contas_pagar_nf_compra.png`

### IDs das seções
Sempre usar `kebab-case`.

Exemplos:
- `cfg-gerais`
- `cfg-contas-pagar-nf`

### Nome dos campos
O nome do campo deve ser idêntico em todos os pontos do projeto.

Não resumir, não simplificar, não trocar aspas, não alterar acentuação e não “melhorar” o texto por conta própria.

## Como Adicionar uma Nova Tela de Configuração

1. Criar uma nova `<section class="page-section" id="cfg-xxxx" data-section-img="prints/xxxx.png">`
2. Adicionar o item correspondente na sidebar
3. Adicionar o card na home, quando fizer sentido
4. Adicionar a definição correspondente no `calibrate.html`
5. Garantir que o print esperado esteja em `prints/xxxx.png`
6. Garantir que os nomes dos campos sejam exatamente iguais entre os arquivos

## Tags de Tipo de Campo

Usar as classes existentes do projeto de forma consistente:
- `tag-sim` — campos booleanos Sim/Não
- `tag-nao` — campos desabilitados, não aplicáveis ou marcados como Não
- `tag-opt` — campos de seleção / lista / dropdown
- `tag-text` ou a classe equivalente já existente no projeto — campos de texto livre

Sempre respeitar o padrão já usado no próprio código.

## Regras de Edição

- Não refatorar partes não relacionadas da página
- Não reescrever CSS sem necessidade
- Não alterar seções antigas sem motivo claro
- Não mudar estilo visual sem necessidade
- Não mexer na lógica de busca, navegação, modal ou destaque se não for necessário
- Fazer a menor alteração segura possível
- Preservar o padrão visual dark atual
- Preservar a estrutura já funcional do projeto

## Formato Esperado da Resposta

Ao concluir uma tarefa, responder sempre nesta estrutura:

### 1. O que foi adicionado
- item de menu
- card da home
- nova seção
- campos mapeados
- nome esperado do print
- estrutura pronta para calibração

### 2. Arquivos alterados
Listar exatamente quais arquivos foram alterados.

### 3. Próximo passo operacional
Explicar de forma objetiva o que eu preciso fazer em seguida, por exemplo:
- salvar o print em `prints/...`
- abrir o `calibrate.html`
- selecionar a nova tela
- marcar os campos
- copiar o bloco gerado
- substituir o bloco correspondente no `index.html`

## Quando eu enviar apenas o print + caminho da tela

Assuma que a tarefa é:
- mapear os campos
- criar a nova seção
- atualizar o `index.html`
- atualizar o `calibrate.html`
- deixar tudo pronto para calibração

## Quando eu disser que o “Exibir na tela” está errado

Verificar nesta ordem:
1. se o nome do campo está idêntico entre os arquivos
2. se o caminho do print está correto
3. se o `data-section-img` bate com o arquivo esperado
4. se a estrutura de coordenadas está consistente
5. se a tela foi adicionada corretamente também no `calibrate.html`

## Prioridade

Neste repositório, consistência e confiabilidade operacional são mais importantes do que criatividade.

Prefira exatidão, padronização e compatibilidade com o fluxo existente.