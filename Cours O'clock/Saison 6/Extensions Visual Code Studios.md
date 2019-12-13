# Extensions Visual Studio Code

Les extensions (ou _plugins_) pour VS Code sont disponibles dans la [Marketplace](https://marketplace.visualstudio.com/).

> [Rappel](./README.md) : la commande `code` est à remplacer par `code-insiders` selon la version installée chez vous (si l'icône de votre programme est bleue = `code` ; si elle est verte = `code-insiders`).

## Base

- [Traduire l'interface en français](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-fr) `code --install-extension MS-CEINTL.vscode-language-pack-fr`
- [_Live Share_](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare), pour l'édition collaborative temps-réel (équivalent de _Teletype_ sur Atom) `code --install-extension ms-vsliveshare.vsliveshare`
- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) `code --install-extension EditorConfig.EditorConfig`

## MarkDown

- [Preview à la GitHub](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-preview-github-styles) avec [Ctrl+Maj+V](https://code.visualstudio.com/Docs/languages/markdown#_markdown-preview) `code --install-extension bierner.markdown-preview-github-styles`
- Linter [Markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) `code --install-extension DavidAnson.vscode-markdownlint`
- Utilitaire Markdown : Markdown All in One `code --install-extension yzhang.markdown-all-in-one`

## HTML

- Linter [HTMLHint](https://marketplace.visualstudio.com/items?itemName=mkaufman.HTMLHint) — attention, il faut installer le programme `htmlhint` en plus de l'extension pour VS Code `code --install-extension mkaufman.HTMLHint`

## CSS

- Linter [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint) — attention, il faut installer le programme `stylelint` en plus de l'extension pour VS Code, et Stylelint travaille avec un fichier de configuration par projet, cf. [la documentation](https://stylelint.io/user-guide/configuration/) `code --install-extension shinnn.stylelint`
- Si l'extension [stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint) ne fonctionne pas (après redémarrage de VSCode), il faut lui ajouter l'extension [`stylelint-fix`](https://marketplace.visualstudio.com/items?itemName=calvinhong.stylelint-fix)
- [IntelliSense for CSS](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion) `code --install-extension Zignd.html-css-class-completion`
- [colorize](https://marketplace.visualstudio.com/items?itemName=kamikillerto.vscode-colorize) `code --install-extension kamikillerto.vscode-colorize`

## JS

- Linter [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) — attention, il faut installer le programme `eslint` en plus de l'extension pour VS Code (cf. [fiche-récap](https://github.com/O-clock-Alumni/fiches-recap/blob/master/js/eslint.md#visual-studio-code)) `code --install-extension dbaeumer.vscode-eslint`
- Pour la coloration syntaxique, avec Babel `code --install-extension dzannotti.vscode-babel-coloring`

## PHP

- [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client) `code --install-extension bmewburn.vscode-intelephense-client` (préférée à la plus populaire mais moins performante extension [PHP IntelliSense](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-intellisense))
- [PHP CS Fixer](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer) `code --install-extension junstyle.php-cs-fixer`
- [PHP DocBlocker](https://marketplace.visualstudio.com/items?itemName=neilbrayfield.php-docblocker) `code --install-extension neilbrayfield.php-docblocker`
- [PHP Getters & Setters](https://marketplace.visualstudio.com/items?itemName=phproberto.vscode-php-getters-setters) `code --install-extension phproberto.vscode-php-getters-setters`

## Symfony

- [Twig](https://marketplace.visualstudio.com/items?itemName=whatwedo.twig) `code --install-extension whatwedo.twig`

## Bonus

- [file-icons](https://marketplace.visualstudio.com/items?itemName=file-icons.file-icons), pour avoir des icônes en fonction du type de fichier dans l'arborescence `code --install-extension file-icons.file-icons`
- [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) `code --install-extension CoenraadS.bracket-pair-colorizer`
- Pour appliquer au code vos propres règles (espaces, tabulations...) `code --install-extension HookyQR.beautify`
- [TODO Highlight](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) `code --install-extension wayou.vscode-todo-highlight`
- [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments), propose une coloration syntaxique spécifique dans les commentaires, par exemple une ligne de commentaire commençant par un `?` ou un `!` sera mise en évidence par le plugin `code --install-extension aaron-bond.better-comments`

## Avancé

- Gérez vos Todo-list avec [Todo+](https://marketplace.visualstudio.com/items?itemName=fabiospampinato.vscode-todo-plus)
- Activez le mode [`vi`](https://fr.wikipedia.org/wiki/Vi) avec l'émulation [Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)