# Transparencias para la charla "Memorias de TFG en $\LaTeX$"
[Grabación de la charla](https://youtu.be/a197TAd7Wsw?) (a fecha del commit [4c42758](https://github.com/rajayonin/latex-thesis/commit/4c4275804aae559dc6109dd5b4ca688dce999787)).


## Pre-requisites
This presentation uses [Marp](https://marp.app/), the Markdown Presentation Ecosystem.

You can either install the [Marp CLI](https://github.com/marp-team/marp-cli) or the [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) extension.
- If you use VS Code, make sure to enable HTML (`markdown.marp.enableHtml` setting)


## Compilation

### Marp CLI
```
marp --html --pdf presentation.md --allow-local-files
```

### NPM
```
npx @marp-team/marp-cli@latest presentation.md --pdf --allow-local-files
```

## Cool info
- [C. Ayers - Unleash Your Creativity with Marp Presentation Customization](https://chris-ayers.com/2023/03/31/customizing-marp)
- [Official documentation](https://marpit.marp.app/markdown)
