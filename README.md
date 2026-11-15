# Template de monografia da UEMA

Este repositório é um modelo em LaTeX para escrever uma monografia. Os arquivos estão separados por parte do trabalho e as configurações de formatação já ficam prontas para você se concentrar no conteúdo.

> **Importante:** os textos que já vêm no template são exemplos e instruções. Troque-os pelo conteúdo do seu trabalho antes de entregar a versão final.

## 1. O que você precisa

- Uma distribuição LaTeX instalada:
  - **Windows:** MiKTeX ou TeX Live;
  - **macOS:** MacTeX;
  - **Linux:** TeX Live.
- Os pacotes `abntex2` e `latexmk`. Se a compilação indicar que outro pacote está faltando, instale-o pela distribuição LaTeX escolhida.
- Um editor de texto. O Visual Studio Code com a extensão **LaTeX Workshop** é uma opção; também é possível compilar pelo terminal.

## 2. Comece por aqui

1. Abra a pasta inteira do projeto no editor. Não mova os arquivos para fora de suas pastas: o documento depende desses caminhos.
2. Abra [`info_documento.tex`](info_documento.tex) e substitua os dados de exemplo pelos dados do seu trabalho:
   - título, autores, cidade e ano;
   - orientador;
   - instituição e curso;
   - tipo do trabalho e texto de apresentação.
3. Abra os arquivos da pasta [`textuais/`](textuais/) e substitua os textos de exemplo pelos capítulos da monografia.
4. Revise os elementos pré-textuais em [`pre-textuais/`](pre-textuais/), como resumo, folha de aprovação e agradecimentos.
5. Atualize as referências em [`bib/referencias.bib`](bib/referencias.bib). O arquivo contém referências de demonstração: remova-as e cadastre as fontes realmente citadas no trabalho.
6. Compile o documento e confira o PDF. Corrija mensagens de erro e compile novamente depois de alterar citações, referências ou a estrutura.

## 3. Como compilar

Abra um terminal na pasta do projeto e execute:

```bash
latexmk -pdf main.tex
```

O arquivo final será [`main.pdf`](main.pdf). O `latexmk` pode compilar mais de uma vez automaticamente para atualizar o sumário, as referências cruzadas e a bibliografia.

Se você não tiver o `latexmk`, use esta sequência:

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

É normal precisar compilar mais de uma vez após mudanças. Arquivos como `.aux`, `.log` e `.toc` são auxiliares gerados durante a compilação; não edite esses arquivos.

## 4. Onde editar cada parte

| Pasta ou arquivo | O que contém |
| --- | --- |
| [`main.tex`](main.tex) | Arquivo principal: escolhe a ordem das partes e reúne todo o documento. |
| [`info_documento.tex`](info_documento.tex) | Dados usados na capa, folha de rosto e folha de aprovação. |
| [`pre-textuais/`](pre-textuais/) | Resumo, abstract, dedicatória, agradecimentos, epígrafe, listas e folha de aprovação. |
| [`textuais/`](textuais/) | Capítulos do conteúdo principal. |
| [`pos-textuais/`](pos-textuais/) | Apêndices e anexos. |
| [`bib/referencias.bib`](bib/referencias.bib) | Referências bibliográficas usadas nas citações. |
| [`configs/`](configs/) | Regras de formatação, capa, listas, sumário, apêndices, anexos e siglas. |
| [`img/`](img/) | Imagens usadas no documento. |
| [`pdfs/`](pdfs/) | PDFs incluídos no documento, como a ficha catalográfica. |

O [`main.tex`](main.tex) inclui `pdfs/ficha_catalografica.pdf` diretamente. Substitua esse arquivo pela ficha catalográfica do seu trabalho, mantendo o mesmo nome e caminho. Se a ficha ainda não estiver disponível, comente temporariamente a linha `\includepdf` no arquivo principal; lembre-se de reativá-la quando tiver o PDF.

O arquivo [`main.tex`](main.tex) já inclui os elementos na ordem do modelo. Se um elemento opcional não fizer parte do seu trabalho, comente a linha correspondente usando `%` no início da linha. Por exemplo:

```latex
% \include{pre-textuais/epigrafe}
```

Para incluir novamente esse elemento, retire o `%`. Faça isso com cuidado: não remova as configurações nem os elementos exigidos pela orientação do seu curso.

## 5. Escrever capítulos e seções

Os capítulos e seções são criados com comandos LaTeX. Por exemplo:

```latex
\chapter{INTRODUÇÃO}

Texto do capítulo.

\section{Objetivos}

Texto da seção.

\subsection{Objetivo geral}

Texto da subseção.
```

Cada capítulo textual tem seu próprio arquivo em [`textuais/`](textuais/). O [`main.tex`](main.tex) os chama com `\include{...}`. Para criar um novo capítulo, crie um arquivo `.tex` nessa pasta e acrescente uma linha `\include{textuais/nome-do-arquivo}` no lugar adequado do arquivo principal.

Não escreva a extensão `.tex` dentro de `\include`.

## 6. Formatação do texto

No LaTeX, comandos começam com uma barra invertida (`\`). O texto a ser formatado geralmente fica entre chaves `{ }`.

| O que fazer | Comando | Exemplo |
| --- | --- | --- |
| Negrito | `\textbf{texto}` | `\textbf{Requisito funcional}` |
| Itálico | `\textit{texto}` | `\textit{machine learning}` |
| Ênfase | `\emph{texto}` | `\emph{termo importante}` |
| Código ou texto monoespaçado | `\texttt{texto}` | `\texttt{arquivo.tex}` |
| Nota de rodapé | `\footnote{texto da nota}` | `Uma observação\footnote{Detalhe complementar.}` |

Use negrito e itálico com moderação e conforme as regras do seu curso. `\emph{...}` destaca uma expressão; use-o para ênfase, não como substituto automático do itálico. Para nomes de tecnologias ou expressões estrangeiras, siga a orientação acadêmica recebida.

Para parágrafos, deixe uma linha em branco entre eles no arquivo `.tex`. Não use `\\` para separar parágrafos: esse comando serve para uma quebra de linha pontual, como dentro de um endereço ou de uma célula da tabela.

Caracteres com significado especial no LaTeX precisam ser escritos com comandos:

| Caractere que você quer mostrar | Como escrever |
| --- | --- |
| `%` | `\%` |
| `$` | `\$` |
| `&` | `\&` |
| `_` | `\_` |
| `#` | `\#` |
| `{` e `}` | `\{` e `\}` |
| `\` | `\textbackslash{}` |

Por exemplo, escreva `C\&C` para exibir “C&C” e `90\%` para exibir “90%”. O caractere `%` inicia um comentário: tudo o que estiver depois dele na mesma linha é ignorado na compilação.

## 7. Listas, citações diretas e links

Para alíneas e listas com marcadores, use os ambientes já preparados para o padrão do template. `uemaenum` cria alíneas (a), b), c)); `uemaball` cria marcadores:

```latex
\begin{uemaenum}
    \item Primeiro passo
    \item Segundo passo
\end{uemaenum}

\begin{uemaball}
    \item Primeiro item
    \item Segundo item
\end{uemaball}
```

Cada `\item` cria um item. Deixe o conteúdo dentro do ambiente e não apague `\begin{...}` ou `\end{...}`. Para listas com subitens, use `itemize` dentro de um item somente se a estrutura for realmente necessária e confira o resultado no PDF.

Para uma citação direta em bloco, use o ambiente `citacao`, já utilizado no capítulo de fundamentação. A opção entre colchetes de `\cite` permite informar página ou outro detalhe da chamada:

```latex
\begin{citacao}
Texto copiado fielmente da fonte, com a chamada de citação.
\cite[p. 25]{silva2024}
\end{citacao}
```

Informe a página da citação direta quando disponível. Citações diretas curtas no meio do parágrafo devem seguir as regras da instituição; não use aspas ou formatação para substituir a indicação da fonte. Nunca apresente texto de outra pessoa como se fosse seu.

Para inserir um endereço clicável, use `\url{...}`:

```latex
\url{https://www.exemplo.org}
```

Endereços consultados como fonte também devem ser referenciados adequadamente no texto e na bibliografia, conforme a orientação do curso.

## 8. Citações e referências

Cadastre cada fonte em [`bib/referencias.bib`](bib/referencias.bib), usando uma chave única. Exemplo:

```bibtex
@book{silva2024,
  author    = {Silva, Maria},
  title     = {Título do livro},
  year      = {2024},
  publisher = {Editora Exemplo}
}

@article{souza2025,
  author  = {Souza, João},
  title   = {Título do artigo},
  journal = {Revista Exemplo},
  year    = {2025},
  volume  = {10},
  number  = {2},
  pages   = {15--30}
}
```

Use o tipo adequado à fonte, como `@book` para livro, `@article` para artigo de periódico e `@inproceedings` para trabalho publicado em evento. Cada entrada começa com uma chave única (`silva2024`, `souza2025`), e os campos são separados por vírgulas. Em intervalos de páginas, use dois hífens, como `15--30`.

No texto, cite usando a mesma chave:

```latex
Uma citação indireta no fim da frase \cite{silva2024}.

\citeonline{silva2024} apresenta a ideia no corpo da frase.
```

`\cite{...}` coloca a chamada de citação entre parênteses; `\citeonline{...}` usa o nome do autor no corpo da frase. A chave (`silva2024`) diferencia maiúsculas de minúsculas e deve ser idêntica no `.bib` e no comando. Para informar página, use, por exemplo, `\cite[p. 25]{silva2024}`. As referências são geradas a partir das citações. A bibliografia de exemplo deve ser substituída pelas fontes do seu trabalho. Se uma citação não aparecer ou a lista de referências não atualizar, compile novamente; com `latexmk`, rode o mesmo comando outra vez.

## 9. Figuras, tabelas e referências cruzadas

Coloque suas imagens na pasta [`img/`](img/) e informe o caminho relativo a partir da pasta do projeto. Exemplo de figura:

```latex
\begin{figure}[htb]
    \centering
    \caption{\label{fig:arquitetura}Arquitetura do sistema}
    \includegraphics[width=0.85\linewidth]{img/arquitetura.png}
    \fonte{Elaborado pelo autor (2026).}
\end{figure}
```

Mencione a figura no texto com `Figura \ref{fig:arquitetura}`. A mesma ideia vale para tabelas:

```latex
\begin{table}[htb]
    \centering
    \caption{\label{tab:resultados}Resultados da avaliação}
    \begin{tabular}{lc}
        \hline
        Item & Resultado \\
        \hline
        Exemplo & 10 \\
        \hline
    \end{tabular}
    \fonte{Dados da pesquisa (2026).}
\end{table}
```

Em `\begin{tabular}{lc}`, cada letra define o alinhamento de uma coluna: `l` à esquerda, `c` centralizado e `r` à direita. O `&` separa colunas e `\\` encerra uma linha. `\hline` desenha uma linha horizontal. Ajuste a quantidade de letras e de células em cada linha para que todas as linhas tenham o mesmo número de colunas. Use tabelas para apresentar dados; não use espaços repetidos para tentar alinhar texto.

Use uma chave diferente para cada `\label` e a mesma chave no `\ref`. Compile novamente para atualizar os números e as listas de figuras e tabelas.

Para uma equação curta dentro do parágrafo, coloque a expressão entre cifrões. Para uma equação destacada, use `\[...\]`:

```latex
A média é calculada por $M = \frac{\sum_{i=1}^{n} x_i}{n}$.

\[
M = \frac{\sum_{i=1}^{n} x_i}{n}
\]
```

No modo matemático, `_` indica índice inferior (por exemplo, `x_i`) e `^` indica expoente (por exemplo, `x^2`). Agrupe expressões maiores com chaves, como `x_{i+1}`. Explique os símbolos e variáveis no texto e numere/referencie equações quando necessário segundo as regras do trabalho. Não use `$` para formatar texto comum.

## 10. Siglas e listas

As siglas do template são cadastradas em [`configs/uema-acronyms.tex`](configs/uema-acronyms.tex). Para adicionar uma, copie o formato abaixo e troque a chave, a sigla e o significado:

```latex
\DeclareAcronym{api}{
  short = API,
  long = Interface de Programação de Aplicações
}
```

Use a chave no texto:

```latex
\ac{api}   % primeira ocorrência por extenso e forma abreviada; depois, forma abreviada
\acs{api}  % somente a forma abreviada
\acl{api}  % somente o significado por extenso
```

As listas de siglas e abreviaturas são editadas em [`pre-textuais/siglas.tex`](pre-textuais/siglas.tex) e [`pre-textuais/abreviaturas.tex`](pre-textuais/abreviaturas.tex). Para listas no conteúdo, o template também oferece:

```latex
\begin{uemaenum}
    \item Primeiro item
    \item Segundo item
\end{uemaenum}

\begin{uemaball}
    \item Primeiro item
    \item Segundo item
\end{uemaball}
```

## 11. Resumo, apêndices e anexos

- Edite o resumo em português em [`pre-textuais/resumo.tex`](pre-textuais/resumo.tex) e a versão em inglês em [`pre-textuais/abstract.tex`](pre-textuais/abstract.tex). Os textos atuais incluem orientações e exemplos; substitua-os pelo resumo do trabalho.
- Apêndices são materiais elaborados por você; edite [`pos-textuais/apendices.tex`](pos-textuais/apendices.tex).
- Anexos são materiais de outras fontes incluídos para complementar o trabalho; edite [`pos-textuais/anexos.tex`](pos-textuais/anexos.tex).
- Se não usar apêndices ou anexos, comente as linhas correspondentes no [`main.tex`](main.tex).

## 12. Ajustes de formatação

As configurações de formatação ficam na pasta [`configs/`](configs/). Por exemplo, [`configs/uema-style.sty`](configs/uema-style.sty) define margens, espaçamento, citações e opções de cabeçalho; os demais arquivos dessa pasta cuidam de partes específicas, como capa e sumário.

Em geral, escreva seu conteúdo nos arquivos de texto e evite alterar os arquivos de configuração. Se precisar mudar a formatação, confirme primeiro as regras com seu orientador ou com o curso.

## Dicas rápidas

- Preserve os nomes e caminhos das pastas usados em `\include`, `\input` e `\includegraphics`.
- Chaves de citação e rótulos (`\label`) não podem se repetir.
- Quando uma imagem não aparecer, confira se o nome e a extensão estão corretos e se o arquivo está na pasta indicada.
- Quando aparecer `??` em uma citação cruzada, compile novamente e confira se a chave existe.
- Leia a primeira mensagem de erro da compilação: erros seguintes podem ser apenas consequência do primeiro.
- O template ajuda com a formatação, mas confirme com seu orientador se os elementos e as normas estão adequados ao seu curso.
