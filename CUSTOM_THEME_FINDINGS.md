# Custom Theme Findings

Neste levantamento, analisamos os componentes do Carbon Design System e
identificamos as áreas que precisam ser modificadas para aplicar o novo tema
visual mais moderno, focado em bordas arredondadas, line-height maior, inputs
transparentes com outline, sombras de elevação e botões dinâmicos.

## 1. Bordas Arredondadas (Border Radius)

Os componentes do Carbon, em sua maioria, utilizam `border-radius: 0` ou bordas
levemente arredondadas (como botões e tags). O novo padrão será baseado em 3
variáveis:

- `sm`: 2px
- `md`: 4px (Padrão)
- `lg`: 8px

**Componentes afetados:**

- **Buttons**: Precisam adotar o radius `md`.
- **Inputs** (TextInput, NumberInput, Search, Select, TextArea): Passarão de
  borda reta para o radius `md`.
- **Containers e Superfícies** (Tiles, Modals, Popovers, Dropdowns, Accordions,
  Notifications): Utilizarão o radius `md` ou `lg` dependendo da área de
  superfície.
- **Outros Elementos UI** (Tags, Tooltips, Checkboxes, Toggle): Precisam de
  ajustes pontuais para manter a harmonia.

## 2. Line-height

O line-height atual da tipografia base do Carbon (ex: `body-01`, `body-02`, etc)
varia de `1.2857` a `1.5`. Para melhor leitura mobile, o padrão deve ser
ligeiramente aumentado. **Ações:**

- Sobrescrever os tokens de tipografia (arquivos de tokens em `packages/styles`
  ou equivalente) para que o line-height global receba um incremento (ex: `1.5`
  ou `1.6` para corpo de texto).

## 3. Inputs (Estilo Outline e Fundo Transparente)

O estilo "flat" do Carbon usa fundo preenchido (`$field`) e apenas uma borda
inferior. **Ações:**

- Remover a cor de fundo (`background-color: transparent`) no estado `normal`.
  Manter fundo apenas se estiver `disabled` ou `readonly`.
- Remover a borda inferior exclusiva e aplicar uma borda completa (4 lados) com
  o `$border-strong` ou `$border-subtle`.
- No estado de `focus`, a borda deve engrossar e talvez receber um outline com a
  cor de foco para realçar a área.
- **Componentes afetados**: TextInput, NumberInput, Search, Select, ComboBox,
  TextArea, DatePicker.

## 4. Sombras (Elevação)

O design atual flat raramente usa sombras, dependendo mais de bordas e mudanças
de cor de fundo. Introduziremos 5 níveis de `elevation` (0 a 5) usando
propriedades de `box-shadow`. **Componentes que receberão elevação:**

- **Elevation 1-2**: Tiles interativos, Cards, e botões secundários (opcional).
- **Elevation 3-4**: Menus suspensos (Dropdown, ComboBox list), Popovers,
  Tooltips.
- **Elevation 5**: Modais, Toast Notifications, Sticky Headers.

## 5. Botões Dinâmicos (Paddings e Centralização)

Os botões do Carbon utilizam larguras e alturas fixas ou baseadas em layouts
rígidos (ex: `block-size: layout.size('height')`). **Ações:**

- Remover os valores fixos de `height` ou `block-size` dos estilos base dos
  botões.
- Configurar variações de tamanho (`sm`, `md`, `lg`) usando exclusivamente
  `padding`.
- Garantir `display: flex`, `align-items: center` e `justify-content: center`
  para que o conteúdo (texto/ícone) fique sempre alinhado ao centro.

---

### Arquivos Chave Identificados para Modificação

- **Tokens/Theme Globais**: `packages/styles/scss/theme/_theme.scss`,
  `packages/themes/...`, `packages/styles/scss/utilities/_box-shadow.scss`
- **Buttons**: `packages/styles/scss/components/button/_button.scss` e
  `_mixins.scss`
- **Inputs**: `packages/styles/scss/components/text-input/_text-input.scss` e
  afins.
- **Tipografia**: `packages/styles/scss/type/...` ou tokens de tipografia
  global.
