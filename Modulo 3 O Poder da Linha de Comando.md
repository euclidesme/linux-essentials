# Módulo 3: O Poder da Linha de Comando

## Índice

1. [Arquivando Arquivos na Linha de Comando](#arquivando-arquivos-na-linha-de-comando)
   - [Introdução](#introdução)
   - [Por que compactar e arquivar arquivos?](#por-que-compactar-e-arquivar-arquivos)
   - [Ferramentas de Compressão](#ferramentas-de-compressão)
     - [gzip - Compressão Rápida e Comum](#gzip---compressão-rápida-e-comum)
     - [bzip2 - Melhor Compressão, Mais Lento](#bzip2---melhor-compressão-mais-lento)
     - [xz - Compressão Moderna e Eficiente](#xz---compressão-moderna-e-eficiente)
   - [Ferramentas de Arquivamento](#ferramentas-de-arquivamento)
     - [tar - O Arquivador Padrão do Linux](#tar---o-arquivador-padrão-do-linux)
     - [Exemplos Práticos com tar](#exemplos-práticos-com-tar)
   - [Gerenciando Arquivos ZIP](#gerenciando-arquivos-zip)
     - [Criando Arquivos ZIP](#criando-arquivos-zip)
     - [Extraindo Arquivos ZIP](#extraindo-arquivos-zip)
     - [Quando Usar ZIP em vez de tar](#quando-usar-zip-em-vez-de-tar)
   - [Dicas e Boas Práticas](#dicas-e-boas-práticas)

2. [Pesquisando e Extraindo Dados de Arquivos](#pesquisando-e-extraindo-dados-de-arquivos)
   - [Introdução](#introdução-1)
   - [Por que precisamos dessas ferramentas?](#por-que-precisamos-dessas-ferramentas)
   - [Ferramentas Básicas de Busca](#ferramentas-básicas-de-busca)
     - [grep - O Buscador de Padrões](#grep---o-buscador-de-padrões)
     - [Expressões Regulares com grep](#expressões-regulares-com-grep)
   - [Ferramentas de Processamento de Texto](#ferramentas-de-processamento-de-texto)
     - [cat - Concatenar e Exibir Arquivos](#cat---concatenar-e-exibir-arquivos)
     - [head e tail - Visualizando Partes de Arquivos](#head-e-tail---visualizando-partes-de-arquivos)
     - [sort - Ordenando Dados](#sort---ordenando-dados)
     - [uniq - Removendo ou Contando Duplicatas](#uniq---removendo-ou-contando-duplicatas)
   - [Ferramentas de Corte e Junção](#ferramentas-de-corte-e-junção)
   - [Ferramentas de Fluxo e Redirecionamento](#ferramentas-de-fluxo-e-redirecionamento)
   - [Exemplos Práticos Combinados](#exemplos-práticos-combinados)

3. [Transformando Comandos em Scripts](#transformando-comandos-em-scripts)
   - [Introdução](#introdução-2)
   - [O que é um script de shell?](#o-que-é-um-script-de-shell)
   - [Criando seu Primeiro Script](#criando-seu-primeiro-script)
   - [Variáveis em Scripts](#variáveis-em-scripts)
   - [Entrada do Usuário](#entrada-do-usuário)
   - [Estruturas de Controle](#estruturas-de-controle)
   - [Funções](#funções)
   - [Exemplos Práticos](#exemplos-práticos)
   - [Dicas e Boas Práticas](#dicas-e-boas-práticas-1)
   - [Depurando Scripts](#depurando-scripts)
# Módulo 3: O Poder da Linha de Comando

# Arquivando Arquivos na Linha de Comando

## Introdução

Quando trabalhamos com arquivos no Linux, frequentemente precisamos compactar, agrupar ou arquivar arquivos para economizar espaço, facilitar transferências ou criar backups. Nesta seção, vamos aprender sobre as ferramentas que o Linux oferece para essas tarefas.

### Por que compactar e arquivar arquivos?

Existem várias razões para compactar e arquivar arquivos:

- **Economizar espaço em disco**: Arquivos compactados ocupam menos espaço
- **Facilitar transferências**: É mais rápido transferir um único arquivo compactado do que muitos arquivos separados
- **Criar backups**: Manter cópias organizadas de arquivos importantes
- **Distribuir software**: Muitos programas são distribuídos como arquivos compactados

**Analogia:**
Compactar arquivos é como usar uma mala a vácuo para guardar roupas - você consegue colocar mais itens no mesmo espaço, e fica mais fácil transportar tudo junto.

## Ferramentas de Compressão

O Linux oferece várias ferramentas para compressão de arquivos, cada uma com suas próprias características.

### gzip - Compressão Rápida e Comum

O `gzip` é uma das ferramentas de compressão mais comuns no Linux:

```
gzip arquivo.txt
```

Este comando comprime o arquivo original e o substitui por uma versão compactada chamada `arquivo.txt.gz`.

Para descompactar:
```
gunzip arquivo.txt.gz
```

**Características do gzip:**
- Extensão: `.gz`
- Bom equilíbrio entre velocidade e taxa de compressão
- Preserva permissões e timestamps dos arquivos
- Comprime apenas arquivos individuais (não diretórios)

**Opções úteis:**
- `gzip -1` até `gzip -9`: Controla o nível de compressão (1=mais rápido, 9=melhor compressão)
- `gzip -k`: Mantém o arquivo original (não o exclui)
- `gzip -v`: Modo verbose, mostra detalhes da compressão

### bzip2 - Melhor Compressão, Mais Lento

O `bzip2` oferece melhor taxa de compressão que o `gzip`, mas é mais lento:

```
bzip2 arquivo.txt
```

Para descompactar:
```
bunzip2 arquivo.txt.bz2
```

**Características do bzip2:**
- Extensão: `.bz2`
- Melhor taxa de compressão que o gzip
- Mais lento que o gzip
- Também comprime apenas arquivos individuais

### xz - Compressão Moderna e Eficiente

O `xz` é uma ferramenta mais recente que oferece excelente compressão:

```
xz arquivo.txt
```

Para descompactar:
```
unxz arquivo.txt.xz
```

**Características do xz:**
- Extensão: `.xz`
- Excelente taxa de compressão
- Mais lento que gzip e bzip2
- Usado em muitas distribuições Linux modernas

### Comparando as Ferramentas de Compressão

| Ferramenta | Velocidade | Taxa de Compressão | Uso de Memória | Extensão |
|------------|------------|-------------------|----------------|----------|
| gzip       | Rápida     | Boa               | Baixo          | .gz      |
| bzip2      | Média      | Melhor            | Médio          | .bz2     |
| xz         | Lenta      | Excelente         | Alto           | .xz      |

**Dica prática:** Para arquivos pequenos ou quando a velocidade é importante, use `gzip`. Para arquivos grandes que você vai armazenar por muito tempo, use `xz`.

## Ferramentas de Arquivamento

Enquanto as ferramentas de compressão trabalham com arquivos individuais, as ferramentas de arquivamento permitem agrupar vários arquivos e diretórios em um único arquivo.

### tar - O Arquivador Padrão do Linux

O `tar` (Tape Archive) é a ferramenta padrão para arquivamento no Linux:

```
tar -cf arquivo.tar diretorio/
```

Este comando cria um arquivo chamado `arquivo.tar` contendo todo o conteúdo do diretório.

Para extrair:
```
tar -xf arquivo.tar
```

**Opções principais do tar:**
- `c`: Cria um novo arquivo
- `x`: Extrai arquivos
- `f`: Especifica o nome do arquivo
- `v`: Modo verbose (mostra o que está acontecendo)
- `t`: Lista o conteúdo sem extrair

**Combinando tar com compressão:**

O `tar` por si só apenas agrupa arquivos, sem compressão. Mas ele pode ser combinado com ferramentas de compressão:

```
# Usando gzip
tar -czf arquivo.tar.gz diretorio/

# Usando bzip2
tar -cjf arquivo.tar.bz2 diretorio/

# Usando xz
tar -cJf arquivo.tar.xz diretorio/
```

Para extrair arquivos compactados:
```
# Extraindo gzip
tar -xzf arquivo.tar.gz

# Extraindo bzip2
tar -xjf arquivo.tar.bz2

# Extraindo xz
tar -xJf arquivo.tar.xz
```

**Analogia:**
O `tar` é como uma caixa onde você coloca vários itens. As ferramentas de compressão são como máquinas de vácuo que reduzem o tamanho da caixa.

### Exemplos Práticos com tar

**Criando um backup de documentos:**
```
tar -czf backup_documentos.tar.gz ~/Documentos/
```

**Extraindo apenas arquivos específicos:**
```
tar -xzf backup.tar.gz arquivo1.txt arquivo2.txt
```

**Listando o conteúdo sem extrair:**
```
tar -tf arquivo.tar
```

**Adicionando arquivos a um arquivo tar existente:**
```
tar -rf arquivo.tar novos_arquivos/
```

**Extraindo para um diretório diferente:**
```
tar -xzf arquivo.tar.gz -C /caminho/para/diretorio/
```

## Gerenciando Arquivos ZIP

O formato ZIP é muito comum, especialmente para compartilhar arquivos com usuários de Windows e macOS.

### Criando Arquivos ZIP

Para criar um arquivo ZIP, use o comando `zip`:

```
zip -r arquivo.zip diretorio/
```

A opção `-r` é para incluir subdiretórios recursivamente.

### Extraindo Arquivos ZIP

Para extrair um arquivo ZIP, use o comando `unzip`:

```
unzip arquivo.zip
```

**Opções úteis do unzip:**
- `unzip -l arquivo.zip`: Lista o conteúdo sem extrair
- `unzip arquivo.zip -d diretorio/`: Extrai para um diretório específico
- `unzip -j arquivo.zip`: Extrai sem preservar a estrutura de diretórios

### Quando Usar ZIP em vez de tar

O formato ZIP é preferível quando:
- Você precisa compartilhar arquivos com usuários de Windows ou macOS
- Você quer extrair apenas arquivos específicos facilmente
- Você precisa que o arquivo seja facilmente aberto em qualquer sistema operacional

## Dicas e Boas Práticas

1. **Nomeie seus arquivos de forma descritiva:**
   ```
   backup_fotos_2023-05-21.tar.gz
   ```

2. **Use a compressão adequada para cada situação:**
   - Para backups de longo prazo: xz (melhor compressão)
   - Para uso diário: gzip (bom equilíbrio)
   - Para compartilhar com outros sistemas: zip

3. **Verifique a integridade dos arquivos após compressão:**
   ```
   # Para arquivos tar
   tar -tf arquivo.tar.gz > /dev/null
   
   # Para arquivos zip
   unzip -t arquivo.zip
   ```

4. **Adicione comentários em arquivos zip:**
   ```
   zip -z arquivo.zip
   ```
   (Isso abrirá um editor onde você pode adicionar comentários)

5. **Use compressão paralela para arquivos grandes:**
   ```
   # Se disponível no seu sistema
   tar -I "pigz -9" -cf arquivo.tar.gz diretorio/
   ```

## Resumo

O Linux oferece várias ferramentas poderosas para compactar e arquivar arquivos:

- **Ferramentas de compressão** (gzip, bzip2, xz) reduzem o tamanho de arquivos individuais
- **Ferramentas de arquivamento** (tar) agrupam múltiplos arquivos e diretórios
- **Formatos combinados** (tar.gz, tar.bz2, tar.xz) oferecem o melhor dos dois mundos
- **ZIP** é útil para compatibilidade com outros sistemas operacionais

Dominar essas ferramentas permite gerenciar arquivos de forma eficiente, economizar espaço em disco e facilitar o compartilhamento e backup de dados.
# Pesquisando e Extraindo Dados de Arquivos

## Introdução

Uma das tarefas mais comuns no Linux é encontrar informações específicas dentro de arquivos. O sistema oferece ferramentas poderosas para buscar, filtrar e manipular dados em arquivos de texto, permitindo que você encontre exatamente o que precisa, mesmo em grandes volumes de informação.

### Por que precisamos dessas ferramentas?

Imagine que você tenha:
- Um arquivo de log com milhares de linhas e precise encontrar erros específicos
- Uma lista de contatos e queira extrair apenas os emails
- Um documento grande e precise localizar todas as menções a um determinado termo
- Vários arquivos de configuração e precise verificar configurações específicas

**Analogia:**
Essas ferramentas são como ter uma lupa e um conjunto de filtros para examinar documentos. Em vez de ler página por página, você pode rapidamente encontrar e extrair exatamente o que procura.

## Ferramentas Básicas de Busca

### grep - O Buscador de Padrões

O `grep` é uma das ferramentas mais poderosas e versáteis do Linux. Seu nome vem de "Global Regular Expression Print" e ele permite buscar padrões de texto em arquivos.

**Uso básico:**
```
grep "termo" arquivo.txt
```

Este comando mostra todas as linhas de `arquivo.txt` que contêm a palavra "termo".

**Opções úteis do grep:**
- `grep -i`: Ignora diferenças entre maiúsculas e minúsculas
- `grep -v`: Inverte a busca (mostra linhas que NÃO contêm o padrão)
- `grep -n`: Mostra os números das linhas nos resultados
- `grep -r`: Busca recursivamente em diretórios
- `grep -l`: Mostra apenas os nomes dos arquivos que contêm o padrão
- `grep -c`: Conta quantas linhas correspondem ao padrão

**Exemplos práticos:**

Buscar por erros em arquivos de log:
```
grep "ERROR" /var/log/aplicacao.log
```

Buscar por emails em um documento:
```
grep -i "@gmail.com" contatos.txt
```

Buscar recursivamente em um diretório:
```
grep -r "configuração" /etc/
```

Contar quantas vezes uma palavra aparece:
```
grep -c "Linux" documento.txt
```

### Expressões Regulares com grep

O `grep` se torna ainda mais poderoso quando usado com expressões regulares, que são padrões especiais para descrever texto.

**Alguns caracteres especiais:**
- `.` - Qualquer caractere único
- `^` - Início da linha
- `$` - Fim da linha
- `*` - Zero ou mais ocorrências do caractere anterior
- `[]` - Qualquer caractere dentro dos colchetes
- `[^]` - Qualquer caractere EXCETO os que estão dentro dos colchetes

**Exemplos:**
```
grep "^Olá" arquivo.txt          # Linhas que começam com "Olá"
grep "mundo$" arquivo.txt        # Linhas que terminam com "mundo"
grep "ca[rs]a" arquivo.txt       # Encontra "casa" ou "cara"
grep "[0-9]" arquivo.txt         # Linhas que contêm dígitos
grep "^$" arquivo.txt            # Linhas vazias
```

**Analogia:**
Expressões regulares são como um idioma especial para descrever padrões de texto - em vez de dizer "procure a palavra exata", você pode dizer "procure qualquer palavra que comece com A, tenha um número no meio e termine com vogal".

## Ferramentas de Processamento de Texto

### cat - Concatenar e Exibir Arquivos

O comando `cat` (abreviação de "concatenate") é usado para exibir o conteúdo de arquivos:

```
cat arquivo.txt
```

Você também pode combinar vários arquivos:
```
cat arquivo1.txt arquivo2.txt > combinado.txt
```

### head e tail - Visualizando Partes de Arquivos

O `head` mostra as primeiras linhas de um arquivo:
```
head arquivo.txt        # Mostra as primeiras 10 linhas
head -n 5 arquivo.txt   # Mostra as primeiras 5 linhas
```

O `tail` mostra as últimas linhas:
```
tail arquivo.txt        # Mostra as últimas 10 linhas
tail -n 20 arquivo.txt  # Mostra as últimas 20 linhas
```

O `tail` tem um modo especial para monitorar arquivos em tempo real:
```
tail -f /var/log/syslog  # Mostra as últimas linhas e continua mostrando atualizações
```

Isso é extremamente útil para acompanhar logs em tempo real.

### sort - Ordenando Dados

O comando `sort` organiza as linhas de um arquivo em ordem alfabética:

```
sort lista.txt
```

**Opções úteis:**
- `sort -r`: Ordem reversa
- `sort -n`: Ordenação numérica (2 vem antes de 10)
- `sort -k2`: Ordena pela segunda coluna
- `sort -u`: Remove duplicatas após ordenar

**Exemplo prático:**
```
# Ordenar uma lista de nomes
sort nomes.txt

# Ordenar numericamente
sort -n numeros.txt

# Ordenar por tamanho de arquivo (resultado do ls -l)
ls -l | sort -k5n
```

### uniq - Removendo ou Contando Duplicatas

O comando `uniq` trabalha com linhas duplicadas consecutivas:

```
uniq lista.txt  # Remove duplicatas consecutivas
```

**Nota importante:** O `uniq` só funciona com linhas consecutivas, por isso geralmente é usado junto com `sort`:

```
sort lista.txt | uniq  # Ordena e depois remove duplicatas
```

**Opções úteis:**
- `uniq -c`: Conta ocorrências de cada linha
- `uniq -d`: Mostra apenas linhas duplicadas
- `uniq -u`: Mostra apenas linhas únicas (não duplicadas)

**Exemplo prático:**
```
# Contar quantas vezes cada erro ocorre em um log
grep "ERROR" log.txt | sort | uniq -c | sort -nr
```

Este comando encontra todas as linhas com "ERROR", ordena-as, conta as ocorrências únicas e depois ordena numericamente em ordem reversa, mostrando os erros mais frequentes primeiro.

## Ferramentas de Corte e Junção

### cut - Extraindo Colunas de Dados

O comando `cut` permite extrair seções específicas (colunas) de cada linha:

```
cut -d"," -f1,3 arquivo.csv  # Extrai as colunas 1 e 3 de um arquivo CSV
```

**Opções principais:**
- `-d` define o delimitador (o caractere que separa as colunas)
- `-f` especifica quais campos (colunas) extrair
- `-c` extrai caracteres específicos por posição

**Exemplos:**
```
# Extrair nomes de usuários do arquivo /etc/passwd
cut -d: -f1 /etc/passwd

# Extrair os primeiros 10 caracteres de cada linha
cut -c1-10 arquivo.txt
```

### paste - Juntando Arquivos Lado a Lado

O comando `paste` combina linhas de diferentes arquivos lado a lado:

```
paste nomes.txt idades.txt > combinado.txt
```

**Opções úteis:**
- `-d` define o delimitador entre as colunas
- `-s` junta todas as linhas de cada arquivo em uma única linha

## Ferramentas de Fluxo e Redirecionamento

### Redirecionamento com > e >>

O símbolo `>` redireciona a saída de um comando para um arquivo (sobrescrevendo-o):
```
ls > arquivos.txt
```

O símbolo `>>` adiciona a saída ao final de um arquivo existente:
```
echo "Nova linha" >> notas.txt
```

### Pipes (|) - Conectando Comandos

O símbolo de pipe `|` permite conectar a saída de um comando à entrada de outro:

```
comando1 | comando2
```

Isso cria um "pipeline" de processamento, onde os dados fluem de um comando para o próximo.

**Exemplos poderosos de pipelines:**

Encontrar os 5 arquivos mais grandes em um diretório:
```
du -h /diretorio | sort -hr | head -n 5
```

Contar quantas linhas contêm uma palavra específica:
```
cat arquivo.txt | grep "palavra" | wc -l
```

Extrair emails únicos de um documento:
```
grep -o '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}' documento.txt | sort | uniq
```

### wc - Contando Linhas, Palavras e Caracteres

O comando `wc` (word count) conta linhas, palavras e caracteres em um arquivo:

```
wc arquivo.txt
```

A saída mostra três números: número de linhas, palavras e bytes.

**Opções específicas:**
- `wc -l`: Conta apenas linhas
- `wc -w`: Conta apenas palavras
- `wc -c`: Conta apenas bytes
- `wc -m`: Conta caracteres (pode diferir de bytes em codificações multibyte)

## Exemplos Práticos Combinados

### Analisando Logs de Servidor Web

Encontrar os IPs que mais acessam um site:
```
cat access.log | cut -d' ' -f1 | sort | uniq -c | sort -nr | head -n 10
```

### Processando Dados CSV

Extrair e contar valores únicos da terceira coluna:
```
cut -d',' -f3 dados.csv | sort | uniq -c | sort -nr
```

### Monitorando Erros em Tempo Real

Observar erros em um arquivo de log em tempo real:
```
tail -f log.txt | grep --color "ERROR"
```

### Criando um Relatório de Uso de Disco

Listar os 10 diretórios que mais ocupam espaço:
```
du -h /home | sort -hr | head -n 10
```

## Dicas e Boas Práticas

1. **Use aspas para padrões de busca com espaços:**
   ```
   grep "erro fatal" log.txt
   ```

2. **Teste expressões regulares complexas em pequenas amostras primeiro**

3. **Use `grep -v` para filtrar informações indesejadas:**
   ```
   cat arquivo.txt | grep -v "comentário" | grep -v "^$"
   ```
   (Remove linhas com "comentário" e linhas vazias)

4. **Combine `head` e `tail` para extrair linhas do meio:**
   ```
   head -n 20 arquivo.txt | tail -n 5
   ```
   (Mostra as linhas 16-20)

5. **Use `grep -A`, `-B` e `-C` para mostrar contexto:**
   ```
   grep -A 2 -B 2 "erro" log.txt
   ```
   (Mostra linhas com "erro" e 2 linhas antes e depois)

## Resumo

O Linux oferece um conjunto poderoso de ferramentas para buscar e manipular dados em arquivos de texto:

- **grep**: Busca padrões em arquivos
- **cat, head, tail**: Exibem conteúdo de arquivos
- **sort, uniq**: Organizam e removem duplicatas
- **cut, paste**: Manipulam colunas de dados
- **wc**: Conta linhas, palavras e caracteres
- **Redirecionamento (>, >>) e pipes (|)**: Conectam comandos e redirecionam saídas

Dominar essas ferramentas permite que você encontre, filtre e manipule dados de forma eficiente, economizando tempo e esforço em tarefas que seriam tediosas ou impossíveis de fazer manualmente.
# Transformando Comandos em Scripts

## Introdução

Até agora, aprendemos a executar comandos individuais no terminal. Mas e se você precisar executar uma sequência de comandos repetidamente? É aí que entram os scripts de shell - uma forma de automatizar tarefas combinando vários comandos em um único arquivo executável.

### O que é um script de shell?

Um script de shell é simplesmente um arquivo de texto contendo uma série de comandos que o shell pode executar. Em vez de digitar cada comando manualmente, você pode executar o script e todos os comandos serão executados automaticamente, na ordem em que foram escritos.

**Analogia:**
Um script de shell é como uma receita de culinária. Em vez de dar instruções verbais para cada passo ("pegue a farinha", "adicione os ovos", "misture"), você escreve todos os passos em um papel e entrega para o cozinheiro seguir do início ao fim.

## Criando seu Primeiro Script

### Passo 1: Criar um arquivo de texto

Use qualquer editor de texto para criar seu script. Vamos usar o `nano`, que é simples e amigável para iniciantes:

```
nano meu_primeiro_script.sh
```

### Passo 2: Adicionar o shebang

A primeira linha de um script geralmente começa com `#!` (chamado de "shebang" ou "hashbang"), seguido pelo caminho para o interpretador que deve executar o script. Para scripts Bash:

```bash
#!/bin/bash
```

Esta linha diz ao sistema que o script deve ser executado pelo Bash, mesmo que você esteja usando outro shell.

### Passo 3: Adicionar comandos

Agora, adicione os comandos que você quer executar, um por linha:

```bash
#!/bin/bash

# Meu primeiro script
echo "Olá, mundo!"
echo "Hoje é $(date)"
echo "Meu diretório atual é $(pwd)"
```

As linhas que começam com `#` (exceto a primeira linha com shebang) são comentários e são ignoradas pelo shell.

### Passo 4: Salvar e tornar executável

Depois de salvar o arquivo, você precisa torná-lo executável:

```
chmod +x meu_primeiro_script.sh
```

### Passo 5: Executar o script

Agora você pode executar seu script:

```
./meu_primeiro_script.sh
```

O `./` indica que o script está no diretório atual.

## Variáveis em Scripts

As variáveis permitem armazenar e manipular dados em seus scripts.

### Declarando e usando variáveis

```bash
#!/bin/bash

# Declarando variáveis
NOME="Maria"
IDADE=30

# Usando variáveis
echo "Olá, meu nome é $NOME e tenho $IDADE anos."
```

**Observações importantes:**
- Não há espaços antes ou depois do sinal de igual
- Para acessar o valor de uma variável, use o prefixo `$`
- Por convenção, nomes de variáveis são escritos em maiúsculas (embora não seja obrigatório)

### Variáveis especiais em scripts

O Bash tem algumas variáveis especiais:

- `$0` - Nome do script
- `$1`, `$2`, etc. - Argumentos passados para o script
- `$#` - Número de argumentos
- `$@` - Todos os argumentos
- `$?` - Código de retorno do último comando (0 geralmente significa sucesso)
- `$$` - ID do processo do script atual

**Exemplo com argumentos:**

```bash
#!/bin/bash

echo "Nome do script: $0"
echo "Primeiro argumento: $1"
echo "Segundo argumento: $2"
echo "Número de argumentos: $#"
echo "Todos os argumentos: $@"
```

Se você executar:
```
./script.sh maçã laranja
```

A saída será:
```
Nome do script: ./script.sh
Primeiro argumento: maçã
Segundo argumento: laranja
Número de argumentos: 2
Todos os argumentos: maçã laranja
```

## Entrada do Usuário

Você pode tornar seus scripts interativos solicitando entrada do usuário:

```bash
#!/bin/bash

echo "Qual é o seu nome?"
read NOME

echo "Olá, $NOME! Bem-vindo ao mundo dos scripts!"
```

O comando `read` pausa o script e espera que o usuário digite algo.

## Estruturas de Controle

### Condicionais (if/else)

As estruturas condicionais permitem que seu script tome decisões:

```bash
#!/bin/bash

echo "Quantos anos você tem?"
read IDADE

if [ $IDADE -lt 18 ]; then
    echo "Você é menor de idade."
elif [ $IDADE -eq 18 ]; then
    echo "Você acabou de atingir a maioridade!"
else
    echo "Você é maior de idade."
fi
```

**Operadores de comparação numérica:**
- `-eq`: Igual a
- `-ne`: Diferente de
- `-lt`: Menor que
- `-le`: Menor ou igual a
- `-gt`: Maior que
- `-ge`: Maior ou igual a

**Para comparação de strings:**
- `=`: Igual a
- `!=`: Diferente de
- `-z`: String vazia
- `-n`: String não vazia

### Loops (for e while)

Os loops permitem repetir comandos:

**Loop for:**
```bash
#!/bin/bash

echo "Contando de 1 a 5:"
for i in 1 2 3 4 5; do
    echo "Número: $i"
done
```

**Loop while:**
```bash
#!/bin/bash

CONTADOR=1
echo "Contando de 1 a 5:"
while [ $CONTADOR -le 5 ]; do
    echo "Número: $CONTADOR"
    CONTADOR=$((CONTADOR + 1))
done
```

## Funções

As funções permitem organizar e reutilizar código:

```bash
#!/bin/bash

# Definindo uma função
saudacao() {
    echo "Olá, $1! Como vai?"
}

# Chamando a função
saudacao "João"
saudacao "Maria"
```

As funções podem receber argumentos (acessados como `$1`, `$2`, etc.) e retornar valores usando o comando `return`.

## Exemplos Práticos

### Script de Backup

```bash
#!/bin/bash

# Script simples de backup

# Diretório a ser copiado
ORIGEM="/home/usuario/documentos"

# Destino do backup
DESTINO="/home/usuario/backup"

# Nome do arquivo de backup (com data)
DATA=$(date +%Y-%m-%d)
ARQUIVO="backup_$DATA.tar.gz"

# Criar o backup
echo "Criando backup de $ORIGEM..."
tar -czf "$DESTINO/$ARQUIVO" "$ORIGEM"

# Verificar se o backup foi bem-sucedido
if [ $? -eq 0 ]; then
    echo "Backup concluído com sucesso: $DESTINO/$ARQUIVO"
else
    echo "Erro ao criar backup!"
fi
```

### Script de Monitoramento de Espaço em Disco

```bash
#!/bin/bash

# Monitoramento de espaço em disco

# Limite de alerta (em porcentagem)
LIMITE=90

# Verificar uso do disco
USO=$(df -h / | grep / | awk '{print $5}' | sed 's/%//')

if [ $USO -gt $LIMITE ]; then
    echo "ALERTA: O disco está com $USO% de uso, acima do limite de $LIMITE%!"
else
    echo "OK: Uso do disco em $USO%, abaixo do limite de $LIMITE%."
fi
```

## Dicas e Boas Práticas

1. **Sempre comece com shebang**
   ```bash
   #!/bin/bash
   ```

2. **Adicione comentários explicativos**
   ```bash
   # Este é um comentário explicando o que o script faz
   ```

3. **Use nomes descritivos para variáveis**
   ```bash
   # Bom
   IDADE_USUARIO=25
   
   # Evite
   x=25
   ```

4. **Verifique erros e forneça mensagens úteis**
   ```bash
   if [ ! -f "$ARQUIVO" ]; then
       echo "Erro: O arquivo $ARQUIVO não existe!"
       exit 1
   fi
   ```

5. **Indente seu código para melhor legibilidade**
   ```bash
   if [ $IDADE -lt 18 ]; then
       echo "Menor de idade"
   else
       echo "Maior de idade"
   fi
   ```

6. **Use códigos de saída apropriados**
   ```bash
   # 0 para sucesso, valores diferentes de 0 para erro
   exit 0  # Sucesso
   exit 1  # Erro genérico
   ```

7. **Teste seu script com dados de exemplo**

8. **Faça backup antes de executar scripts que modificam arquivos importantes**

## Depurando Scripts

Se seu script não estiver funcionando como esperado, você pode depurá-lo:

1. **Modo verbose**: Adicione `-x` ao shebang para ver cada comando sendo executado
   ```bash
   #!/bin/bash -x
   ```

2. **Depuração parcial**: Use `set -x` e `set +x` para depurar apenas partes específicas
   ```bash
   set -x  # Inicia depuração
   # comandos a serem depurados
   set +x  # Termina depuração
   ```

3. **Verificação de sintaxe**: Use `-n` para verificar a sintaxe sem executar o script
   ```
   bash -n meu_script.sh
   ```

## Resumo

Os scripts de shell são uma ferramenta poderosa para automatizar tarefas repetitivas no Linux. Eles permitem combinar comandos, tomar decisões baseadas em condições, processar entrada do usuário e muito mais.

Pontos-chave para lembrar:
- Um script é um arquivo de texto com comandos
- Comece com `#!/bin/bash` (shebang)
- Torne o script executável com `chmod +x`
- Use variáveis para armazenar dados
- Estruturas como `if/else` e loops permitem lógica mais complexa
- Funções ajudam a organizar e reutilizar código

Com prática, você poderá criar scripts cada vez mais sofisticados para automatizar praticamente qualquer tarefa no Linux.


