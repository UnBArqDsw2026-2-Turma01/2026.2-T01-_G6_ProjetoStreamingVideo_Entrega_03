# Plataforma de Streaming de Vídeo — Entrega 03

Repositório do **Grupo 06, Turma 01**, da disciplina **FGA0208 — Arquitetura e Desenho de Software**, Universidade de Brasília, semestre **2026.2**.

Esta etapa trata do **Desenho de Software (Padrões de Projeto)**, em continuidade à modelagem da Entrega 02. A estrutura inicial contém a apresentação do projeto, os integrantes e os espaços para os relatórios das três subequipes.

- **Documentação:** [GitHub Pages da Entrega 03](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_03/)
- **Etapa anterior:** [GitHub Pages da Entrega 02](https://unbarqdsw2026-2-turma01.github.io/2026.2-T01-_G6_ProjetoStreamingVideo_Entrega_02/)

## Organização

| Subequipe | Foco | Relatório |
| --- | --- | --- |
| SubEquipe_01 | GoFs Criacionais + IA Generativa | [1.1.1. SubEquipe_01](docs/Base/Relatórios/1.1.1.SubEquipe_01/README.md) |
| SubEquipe_02 | GoFs Estruturais + IA Generativa | [1.1.2. SubEquipe_02](docs/Base/Relatórios/1.1.2.SubEquipe_02/README.md) |
| SubEquipe_03 | GoFs Comportamentais + IA Generativa | [1.1.3. SubEquipe_03](docs/Base/Relatórios/1.1.3.SubEquipe_03/README.md) |

```text
docs/
├── README.md                     # Página inicial e integrantes
├── Introducao.md                 # Contexto e organização das subequipes
├── Checklist.md                  # Pendências da entrega
├── index.html                    # Configuração do Docsify
├── _sidebar.md                   # Navegação do site
├── Base/
│   ├── 1.PadroesDeProjeto.md
│   ├── Relatórios/
│   │   ├── 1.1.1.SubEquipe_01/
│   │   ├── 1.1.2.SubEquipe_02/
│   │   └── 1.1.3.SubEquipe_03/
│   ├── 1.2.ParticipacoesPadroesDeProjeto.md
│   └── 1.3.IniciativasExtras.md
└── Projeto/
    ├── Projeto.md
    └── Atas/
        ├── README.md
        └── TEMPLATE.md
```

## Visualização local

O site usa [Docsify](https://docsify.js.org/) e arquivos Markdown. Na raiz do repositório, execute:

```bash
python3 -m http.server 8000 --directory docs
```

Acesse `http://localhost:8000`. O tema e o Docsify são carregados de um CDN e precisam de conexão com a internet.

## Publicação

O GitHub Pages publica a pasta **`/docs` da branch `main`**. Alterações enviadas para essa branch atualizam o site automaticamente. O arquivo `docs/.nojekyll` mantém a publicação dos arquivos de documentação, incluindo `_sidebar.md`.

## Como preencher

Consulte [CONTRIBUTING.md](CONTRIBUTING.md). Cada subequipe deve acrescentar seu padrão escolhido, modelagem UML, código, manual de execução, vídeo e registros individuais. Os campos **A preencher**, **A definir** e **Pendente** identificam trabalho ainda não realizado.
