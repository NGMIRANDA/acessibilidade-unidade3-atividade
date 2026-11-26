# Harmonia Instrumentos Musicais — Acessibilidade e responsividade

Projeto acadêmico em HTML5 e CSS3, desenvolvido a partir da primeira versão da Unidade 3.

## Implementações e branches

| Branch | Implementação |
|---|---|
| correcao | HTML semântico, cabeçalhos, landmarks, listas, tabela e formulário |
| skip-link | Atalho de teclado para o conteúdo principal |
| prefers-color-scheme | Tema claro/escuro automático e melhorias de acessibilidade |
| prefers-reduced-motion | Transições somente quando o usuário não solicita movimento reduzido |
| formulario-cadastro | Campos rotulados, obrigatoriedade e validação nativa de e-mail e senha |
| responsividade | Layout flexível, navegação adaptável e tabela com rolagem localizada |

## Responsividade

Desktop: a partir de 1024 px, conteúdo e barra lateral lado a lado. Tablet: 768–1023 px, coluna única. Celular: até 767 px, espaçamentos e botões adaptados. A tabela mantém sua estrutura semântica.

## Executar

Abra index.html no navegador ou acesse https://ngmiranda.github.io/acessibilidade-unidade3-atividade/ após a publicação da main.

## Validação

Testar em 320, 375, 768, 1024 e 1440 px; navegar por Tab e ativar o skip link; emular tema escuro e movimento reduzido no DevTools; testar cadastro vazio, e-mail inválido e senha curta. Executar Lighthouse em Accessibility no Chrome, desktop e mobile. Registrar a pontuação real após a execução; meta de 80 a 100.

## Limitações

Demonstração estática, sem backend, sem JavaScript e sem armazenamento de cadastro. Usar dados fictícios. A validação HTML usa o navegador; somente a preferência de turno pode aparecer na URL. Compras estão desabilitadas. Algumas páginas e PDF do enunciado original não foram fornecidos e seus links são demonstrativos. Nenhuma conformidade WCAG integral ou pontuação Lighthouse foi certificada.

## Referências

- https://www.w3.org/TR/WCAG21/
- https://developer.mozilla.org/pt-BR/
- https://developer.chrome.com/docs/lighthouse/accessibility/
