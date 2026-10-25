# TaskTracker - Bootcamp II

Aplicação de linha de comando em Python para cadastrar e listar tarefas. Esta versão corresponde à fase final do bootcamp: o código da fase 2 foi empacotado em uma imagem Docker e pode ser executado em um contêiner interativo.

## Funcionalidades

- Cadastrar tarefa com título, descrição, prioridade e data limite.
- Validar título obrigatório e prioridade (`Alta`, `Média` ou `Baixa`).
- Criar a tarefa com status inicial `Pendente`.
- Listar tarefas cadastradas durante a execução.

As tarefas ficam em memória e são perdidas ao encerrar o programa. A persistência de dados não faz parte desta versão.

## Estrutura

```text
tasktracker-projeto/
├── .gitignore
├── .dockerignore
├── docs/
│   └── planejamento_logico.pdf
├── src/
│   └── main.py
├── Dockerfile
├── docker-compose.yml
└── README.md
```

O planejamento lógico da fase 1 e o código da fase 2 permanecem no repositório para rastreabilidade.

## Executar com Python

Na raiz do repositório, use `python src/main.py` (ou `python3 src/main.py` em sistemas onde esse é o comando instalado).

## Executar com Docker

Instale e inicie o Docker Desktop ou outro ambiente com Docker Engine. No terminal, entre na raiz deste repositório.

### Construir a imagem

```bash
docker build -t tasktracker-app .
```

### Executar o contêiner interativo

```bash
docker run -it --rm tasktracker-app
```

O parâmetro `-it` conecta a entrada do teclado e o terminal ao menu. `--rm` remove o contêiner ao sair.

### Executar com Docker Compose

```bash
docker compose run --rm tasktracker-app
```

O serviço define `stdin_open: true` e `tty: true`, necessários para o `input()` do programa. O Compose constrói a imagem a partir do `Dockerfile` caso ela ainda não exista.

## Demonstração sugerida

No menu, escolha `2` para mostrar a lista vazia. Depois escolha `1`, tente um título vazio e uma prioridade inválida para mostrar as validações, cadastre uma tarefa válida e escolha `2` novamente para exibi-la. Por fim, escolha `3` para sair.

## Arquivos de containerização

- `Dockerfile`: usa `python:3.11-slim`, define `/app` como diretório de trabalho, ativa logs sem buffer, copia `src/` e inicia `src/main.py`.
- `docker-compose.yml`: constrói a imagem e habilita a interação com o terminal.
- `.dockerignore`: exclui arquivos desnecessários do contexto de build.

