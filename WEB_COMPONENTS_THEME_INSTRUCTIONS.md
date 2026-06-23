# Como aplicar o Tema Customizado no Storybook de Web Components

Este repositório utiliza o Yarn Workspaces (monorepo). Como os web-components
importam os estilos SCSS do pacote `@carbon/styles`, você **não deve rodar \`npm
install\` dentro da pasta \`packages/web-components\`**, pois isso quebra os
links do workspace e baixa a versão pública do NPM (sem o nosso tema
customizado).

Siga os passos abaixo na raiz do projeto para refletir as alterações de estilo:

1. **Faça o build dos estilos (scss):** \`\`\`bash yarn workspace @carbon/styles
   run build \`\`\` _(Isso garante que as novas variáveis e mixins que criamos
   no `_theme.scss` sejam propagadas)._

2. **Faça o build do pacote Web Components:** \`\`\`bash yarn workspace
   @carbon/web-components run build \`\`\` _(Os web components do Carbon
   convertem arquivos SCSS locais em arquivos JavaScript `.css.js` injetados no
   Shadow DOM. Este comando irá forçar a recompilação destes arquivos com os
   novos paddings, bordas e shadows)._

3. **Inicie ou faça o build do Storybook:** Para rodar o Storybook em modo de
   desenvolvimento (com hot-reload): \`\`\`bash yarn workspace
   @carbon/web-components run storybook \`\`\` Para gerar os arquivos estáticos
   de build: \`\`\`bash yarn workspace @carbon/web-components run
   storybook:build \`\`\`

## O que foi alterado?

- Variáveis no \`packages/styles/scss/theme/\_theme.scss\` (Border-radius,
  shadows, e inputs transparentes).
- Mixins de botão e line-height global que impactam diretamente na compilação.
- O Storybook do Web Components deve agora refletir automaticamente as bordas
  arredondadas (Modal, Popover), inputs apenas com outline (\`background-color:
  transparent\`), e botões centralizados com padding dinâmico.
