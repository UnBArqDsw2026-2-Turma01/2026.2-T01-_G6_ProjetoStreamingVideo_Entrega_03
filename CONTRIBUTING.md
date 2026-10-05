# Como contribuir

1. Consulte a [introdução](docs/Introducao.md) e o [checklist](docs/Checklist.md) da Entrega 03.
2. Crie uma branch com um nome descritivo, por exemplo `docs/subequipe-01-relatorio`.
3. Atualize o relatório da sua subequipe em `docs/Base/Relatórios/`. Guarde imagens e fontes UML junto ao relatório, em uma pasta `assets/` criada quando necessário.
4. Registre as fontes consultadas, autoria, revisão, elos com artefatos anteriores e links de evidências. Atualize o histórico do relatório e o quadro de participações com contribuições efetivamente realizadas.
5. Escreva seu próprio relato de lições aprendidas e avaliação crítica de IA Generativa. Informe também quando não houver uso de IA.
6. Abra um pull request descrevendo a alteração e os participantes. Após a revisão e integração em `main`, o Pages será atualizado.

## Links no site

Nos arquivos de `docs/`, os links internos do Docsify partem da raiz da documentação, por exemplo `[Introdução](/Introducao.md)`. Não use o prefixo `/docs/`. Na raiz do repositório, use caminhos relativos como `docs/Introducao.md`.

Para citar entregas anteriores, use o endereço completo do respectivo GitHub Pages. Referências e comprobatórios devem apontar para páginas, arquivos, commits ou vídeos específicos.

## Revisão antes de publicar

- Confira a navegação com `python3 -m http.server 8000 --directory docs`.
- Verifique a leitura de tabelas, imagens e diagramas.
- Confira os links de código, execução e vídeo, quando incluídos.
- Não substitua campos pendentes por realizações, avaliações ou autoria sem evidência.
- Atualize `docs/_sidebar.md` quando criar uma página que deva aparecer no menu.
