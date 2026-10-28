# SARIMA — comércio varejista ampliado do Ceará

Exercício de séries temporais com a base PMC/IBGE disponibilizada pelo professor.

## Conteúdo

- `index.html`: relatório completo, com gráficos e recursos incorporados. Pode ser aberto diretamente no navegador.
- `template-exercicio-sarima.qmd`: fonte Quarto com todo o código e a discussão.
- `template-exercicio-sarima.ipynb`: notebook já executado, com os mesmos blocos de código, tabelas e figuras.
- `pyproject.toml` e `uv.lock`: dependências e versões do ambiente Python.
- `.gitignore`: exclui `.venv`, caches e arquivos temporários.
- `_quarto.yml` e `styles.css`: configuração e apresentação do relatório.
- `data/pmc_volume_uf.csv`: cópia da base original do exercício, incluindo as 27 UFs.
- `data/pmc_ceara.csv`: recorte do Ceará no formato usado pelo modelo.
- `resultados/`: gráficos, coeficientes, testes, métricas de validação, registro da execução e previsão em CSV.

## Recorte e resultados

São 266 observações mensais entre janeiro de 2004 e fevereiro de 2026, sem lacunas. A média do índice em 2022 é 100. A previsão de 24 meses cobre março de 2026 a fevereiro de 2028. Não foram incorporados dados publicados após o corte da base do professor.

O AutoARIMA selecionou SARIMA(0,1,3) × (1,1,2)[12]. O relatório discute o aviso de precisão do otimizador, uma checagem independente com a mesma estrutura, os diagnósticos de resíduos e uma validação temporal de 24 meses contra o ingênuo sazonal.

## Reproduzir

1. Instale Python 3.11 a 3.13, [uv](https://docs.astral.sh/uv/getting-started/installation/) e [Quarto](https://quarto.org/docs/get-started/).
2. Abra o terminal nesta pasta.
3. Execute:

```bash
uv sync --frozen
uv run quarto render template-exercicio-sarima.qmd --to html
```

O `uv` cria a pasta `.venv` automaticamente. Não a envie ao GitHub. O relatório é recalculado e salvo em `index.html`. A execução original usou Quarto 1.10.19; as versões Python estão em `uv.lock` e no registro de execução.

Também é possível gerar o HTML a partir dos resultados já armazenados no notebook, sem recalcular o modelo:

```bash
uv run quarto render template-exercicio-sarima.ipynb --to html --no-execute
```

## Publicar no GitHub Pages

### Criar e enviar o repositório

1. Entre na sua conta do GitHub e escolha **New repository**.
2. Nome sugerido: `sarima-ceara-pmc`. Escolha **Public** e crie o repositório vazio.
3. Extraia o ZIP deste projeto. Envie o conteúdo da pasta `sarima-ceara` para a raiz do repositório; `index.html` precisa ficar na raiz, e não dentro de outra pasta.
4. Inclua os dados, o arquivo `.qmd`, `pyproject.toml`, `uv.lock`, `_quarto.yml`, `styles.css`, `.gitignore` e os resultados. Não envie o próprio ZIP nem `.venv`.
5. Confirme o envio com um commit.

Se preferir utilizar Git localmente, substitua `SEU_USUARIO` pelo seu usuário:

```bash
git clone https://github.com/SEU_USUARIO/sarima-ceara-pmc.git
cd sarima-ceara-pmc
```

Copie o conteúdo do projeto para o repositório clonado e execute:

```bash
git add .
git commit -m "Adiciona análise SARIMA do comércio do Ceará"
git push -u origin main
```

Se o Git pedir nome e e-mail, configure os seus próprios dados de identificação de commit. A autenticação é realizada na sua conta, pelo fluxo normal do GitHub.

### Ativar o Pages

1. No repositório, abra **Settings → Pages**.
2. Em **Build and deployment**, escolha **Deploy from a branch**.
3. Selecione a branch **main** e a pasta **/ (root)**. Clique em **Save**.
4. Aguarde a publicação. Copie a URL exibida nessa página e abra-a para conferir.
5. Envie **essa URL publicada** no formulário do Blackboard. O envio no Blackboard precisa ser feito pelo aluno.

O endereço terá o formato `https://SEU_USUARIO.github.io/sarima-ceara-pmc/`. Esse é apenas um modelo de endereço: o repositório e o site ainda não foram criados na sua conta. A integração com GitHub estava desativada no ambiente de preparação.

## Antes de entregar

Confira o HTML, revise as interpretações e siga a política da disciplina sobre autoria, colaboração e uso de ferramentas. Se for necessário informar nome, turma ou matrícula no relatório, acrescente seus dados verdadeiros ao cabeçalho do `.qmd` e renderize novamente.

## Fonte

Template: https://github.com/padsInsper/202634-fa/blob/main/dinamicas/template-exercicio-sarima.qmd

Base: https://github.com/padsInsper/202634-fa/releases/download/data/pmc_volume_uf.csv
