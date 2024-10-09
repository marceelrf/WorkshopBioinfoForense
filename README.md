# WorkshopBioinfoForense

## Instalação

Usar o CONDA para criar um ambiente garante que todos os participantes estejam utilizando exatamente os mesmos programas e versões, evitando problemas que podem surgir por diferenças entre os computadores. Assim, você terá todas as ferramentas necessárias instaladas de forma organizada e padronizada, facilitando o acompanhamento durante o workshop, mesmo se você não tiver muita experiência com a instalação de programas. Isso ajuda a garantir que todos possam focar no conteúdo sem se preocupar com configurações complicadas.

### Instalando o CONDA via Miniconda

`mkdir -p ~/miniconda3`

`wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh`

`bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3`

`rm -rf ~/miniconda3/miniconda.sh`

`~/miniconda3/bin/conda init bash`

`~/miniconda3/bin/conda init zsh`

Reinicie o sistema.

### Crie e ative o ambiente

`conda env create -f workshopbioinfo.yml`

`conda activate workshopbioinfo`


# HipSTR

**H**aplotype **i**nference and **p**hasing for **S**hort **T**andem **R**epeats ou HipSTR é um programa que foi desenvolvido por Thomas Willems para capturar marcadores STRs a partir de dados de sequenciamento de nova geração. 

Link do Github para o repositório original:

https://github.com/tfwillems/HipSTR

Atualmente, HipSTR apresenta uma incompatibilidade com a nova versão do compilador do C++. Portanto, iremos utilizar um repositório transitório que já contém uma mudança no código fonte, até o Dr. Thomas Willems modificar diretamente no repositório original.   

Link do Github para o repositório alternativo:

https://github.com/Tfronta/HipSTR2

### REQUERIMENTOS

Para compilar HipSTR, são necessários os seguintes pacotes:

- make
- g++
- zlib
- libhts
- libbz2
- liblzma

Se vocês estiverem executando o Ubuntu 16+, os pacotes podem ser facilmente instalados executando:

```jsx
sudo apt install make g++ zlib1g-dev libhts-dev libbz2-dev liblzma-dev git samtools
```

### INSTALAÇÃO DO HIPSTR

HipSTR requer um compilador c++ padrão. Para obter HipSTR, use:

```jsx
git clone https://github.com/Tfronta/HipSTR2 HipSTR
```

Para construir, usem Make:

```jsx
cd HipSTR
make
```

Para que HipSTR esteja disponível no computador, sem necessidade de copiar a rota donde ele está instalado, por exemplo "downloads”, criaremos un symlink. Um **symlink** (ou link simbólico) é um "atalho" que aponta para outro arquivo ou diretório no sistema. Isso permite acessar um arquivo de diferentes locais como se estivesse em várias pastas, mas ele só existe em uma.

```jsx
sudo ln -s $(pwd)/HipSTR /usr/local/bin/HipSTR
```

 

Para saber se o HipSTR foi instalado corretamente ou solicitar ajuda use:

```jsx
HipSTR --help
```

[Tutorial de ajuda](https://drive.google.com/file/d/1H9LA6Yp8Pho_XBQOpNENhL3Egtj1B24R/view?usp=drive_link)

### GENOTIPAGEM

ARQUIVOS NECESSÁRIOS 

- O genoma de referência HG38 (arquivo.fa)
- O índice do genoma de referência HG38 (arquivo.fai)
- Amostras em formato bam (HG00118.bam, etc)
- O índice das amostras em formato bai (HG00118.bai, etc)
- O arquivo bed com as regiões que serão analizadas em este curso

Estes arquivos se encontram dentro de uma pasta de google drive. O genoma de referência já possui o índice, por questões de tempo. Entretanto, vamos a criar os índices para as amostras 

[Acesso aos arquivos](https://drive.google.com/drive/folders/14ZXVyXaDAP_QvTrtizeAtrZTL8E_25GP?usp=drive_link) 

IMPORTANTE

- Deverão baixar todos estes arquivos e coloca-los dentro DA MESMA PASTA
- Se todos estes arquivos não se encontrarem dentro da MESMA pasta, o comando não funcionará.

RECOMENDAÇOES

- Não usar espaços ou maiúsculas no nome da pasta criada. Exemplos sugeridos: curso, curso_bioinfo, cursobioinfo, etc.

CÓMO CRIAR OS ÍNDICES DAS AMOSTRAS? 

- Utilizaremos samtools index

```jsx
cd rota_da_pasta_criada
samtools index nome_da_amostra.bam
```

Fazer esse comando para todas as amostras. 

[Tutorial de ajuda](https://drive.google.com/file/d/1_kTWQTcX4k_adN28sEJb47drwAZAzrm0/view?usp=drive_link)

### COMANDO DO HIPSTR

- Antes de correr o comando do HipSTR, verifiquem que todas as amostras que serão incluidas no comando, já tenham o índice (Arquivo fai, gerado com samtools index)
- Preparar o comando previamente em algum arquivo de texto, substituindo nome_da_amostra1 pelo nome real da amostra.
- Podem rodar varias amostras no mesmo comando, separando elas por virgulas SEM espaço, como no exemplo embaixo.

```jsx
cd rota_da_pasta
HipSTR --bams nome_da_amostra1.bam,nome_da_amostra2.bam --fasta GRCh38_full_analysis_set_plus_decoy_hla.fa --regions regionsx.bed --str-vcf nome_de_saida.vcf.gz --min-reads 8 --def-stutter-model --max-flank-indel 0.50 --max-str-len 127 --viz-out aln.viz.gz
```

[Tutoria de ajuda](https://drive.google.com/file/d/1jBNQ8lxWDYQ-L4U34WVhbenagOPWRerR/view?usp=drive_link)

INTERPRETAÇÃO DO ARQUIVO DE SAÍDA

- HipSTR gera como arquivo de saída um arquivo vcf.gz. Logo de descomprimir o arquivo teremos um vcf.
- Podem abrir com Excel e realizar a interpretação dos dados para genotipar as amostras. Durante a aula aprenderemos a realizar essa interpretação.

ATIVIDADES DO DÍA 6
- Extrair os valores GB e DP de todas as amostras
- Genotipar todas as amostras, incluir valores de cobertura

Perguntas google forms
- Quais são os genótipos do marcador CSF1PO na amostra HG00239?
- Quais são os genótipos do marcador TPOX na amostra NA18602?
- Qual é o comando utilizado para criar os índices das amostras?
- O valor DP indica a diferença de número de bases com o alelo de referênça?
- Alguma das amostras não foi possível genotipar?
