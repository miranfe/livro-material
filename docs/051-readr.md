## O pacote readr



O pacote `readr`do tidyverse é utilizado para importar arquivos de texto, como `.txt` ou `.csv`, para o R. Para carregá-lo, rode o código:


```r
library(readr)
```

O `readr` transforma 7 tipos de arquivos de textos em `tibbles` usando as funções:

- `read_csv()`: para arquivos separados por vírgula.

- `read_tsv()`: para arquivos separados por tabulação.

- `read_delim()`: para arquivos separados por um delimitador genérico. O argumento `delim=` indica qual caracter separa cada coluna no arquivo de texto.

- `read_table()`: para arquivos de texto tabular com colunas separadas por espaço.

- `read_fwf()`: para arquivos compactos que devem ter a largura de cada coluna especificada.

- `read_log()`: para arquivos padrões de log.

Vamos mostrar na próxima seção como importar as extensões mais comuns: `.csv` e `.txt`.

### Importando arquivos de texto

Como exemplo, utilizaremos uma base de filmes do IMDB, gravada em diversos formatos. O download dos arquivos pode ser realizado a partir [deste repositório](https://github.com/curso-r/intro-programacao-em-r-mestre/tree/master/dados).

Primeiro, vamos ler a base em formato `.csv`.


```r
imdb_csv <- read_csv(file = "imdb.csv")
```



A mensagem retornada pela função indica qual classe foi atribuída para cada coluna. Repare que o argumento `file=` representa o caminho até o arquivo. Se o arquivo a ser lido não estiver no diretório de trabalho da sua sessão, você precisa especificar o caminho até o arquivo. 


```r
# Se o arquivo estiver dentro de uma pasta chamada dados.

imdb_csv <- read_csv(file = "dados/imdb.csv")
```

A maioria das funções de leitura do `readr` possuem argumentos muito úteis para resolver problemas de importação:

- `col_names=`: indica se a primeira linha da base contém ou não o nome das colunas. Também pode ser utilizado para (re)nomear colunas.

- `col_types=`: caso alguma coluna seja importada com a classe errada (uma coluna de números foi importada como texto, por exemplo), você pode usar esse argumento para especificar a classe das colunas.

- `locale=`: útil para tratar problema de *encoding*.

- `skip=`: pula linhas no começo do arquivo antes de iniciar a importação. Útil para quando o arquivo a ser importado vem com metadados ou qualquer tipo de texto nas primeiras linhas, antes da base.

- `na=`: indica quais *strings* deverão ser considaras `NA` na hora da importação.

Para ler bases com extensão `.txt` cujas colunas estão separadas por tabulação, podemos utilizar a função `read_tsv()`.


```r
imbd_tsv <- read_tsv(file = "imdb.tsv")
```

Repare que a sintaxe é igual a da função `read_csv()`. Em geral, as funções de importação do `tidyverse` terão sintaxe muito parecidas e, caso a base que você precisa importar não apresente nenhum problema^[O que, infelizmente, acontece muito raramente.], elas só precisarão do argumento `file=` para funcionar.

A seguir, vamos falar das funções `parse_()`, muito úteis para tratar problemas na classe das variáveis na hora da importação.

### Parseando valores

### Locale

### Escrevendo arquivos

Para a maioria das funções `read_`, existe uma respectiva função `write_`. Essas funções servem para salvar bases em um formato específico de arquivo. Além do caminho/nome do arquivo a ser criado, você também precisa passar o objeto que será escrito. Para o arquivo criado funcionar corretamente, você precisa especificar a extensão correta no nome do arquivo.


```r
# Arquivo .csv
write_csv(x = mtcars, path = "data/mtcars.csv")

# Base separada por tabulação
write_delim(x = mtcars, delim = "\t", path = "data/mtcars.txt")
```

Também é possível salvar qualquer tipo de objeto do R em um tipo especial de arquivos, o `.rds`. A vantagem dessa extensão é guardar a estrutura dos dados salvos, como a classe das colunas de um data.frame. Além disso, é uma boa alternativa para lidar com grandes bancos de dados, já que você pode compactar os arquivos `.rds`, deixando-os bem menores que, por exemplo, um arquivo Excel.

Para ler ou escrever arquivos `.rds`, utilize as funções `read_rds()` e `write_rds()`.


```r
imdb_rds <- read_rds(path = "imdb.rds")
write_rds(mtcars, path = "mtcars.rds")
```

#### Exercícios {-}

1. Qual a diferença entre as funções `read_csv()` e `read_csv2()`?

2. Leia o arquivo `imdb.csv` utilizando a função `read_delim()`.

3. Escreva a base mtcars em um arquivo `mtcars.csv` que não contenha o nome das colunas.
