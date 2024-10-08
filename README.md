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

# MARCADORES STRs

Para esse curso, utilizaremos um computador virtual, devido à incompatibilidades com a nova versão do compilador C++. Portanto, teremos que baixar o computador virtual com os arquivos necessários para o curso, e virtual box que permitirá executar o computador virtual.

PRIMER PASO - DESCARGAS

1. Baixar o computador virtual Ubuntu (baixar e descomprimir o arquivo zip). 

Link para baixar o computador virtual: https://drive.google.com/file/d/1Pnw3KGixyB6ur2h9zDA3zSAeHj8OzvyX/view?usp=drive_link

1. Baixar virtual box e o pacote de instalação. 

Link para baixar virtual box que mostrará o computador virtual Linux: https://www.virtualbox.org/wiki/Downloads

Baixar DUAS coisas deste link virtual box: 

1. **VirtualBox Platform Packages**
2. **VirtualBox Extension Pack**

Escolher o sistema operativo do computador (windows, mac ou linux) e baixar. 

<img width="1284" alt="VB" src="https://github.com/user-attachments/assets/a5fc02f6-8fd7-4ff6-a178-5047f1052f2d">

Logo de instalar, escolher o computador virtual Ubuntu que baixamos no primer link. 

Senha do computador virtual instalado: bioinformatica

Link tutorial de ajuda: https://drive.google.com/file/d/1bPgrcmzdD3b_ELsGPKUMBllZ7G0SJR18/view?usp=drive_link

## HIPSTR

**H**aplotype **i**nference and **p**hasing for **S**hort **T**andem **R**epeats ou HipSTR é um programa que foi desenvolvido por Thomas Willems para capturar marcadores STRs a partir de dados de sequenciamento de nova geração. 

Link do Github: 

https://github.com/tfwillems/HipSTR

INTSLAÇÃO

Infelizmente a última versão do compilador C++ apresenta uma incompatibilidade com HipSTR. Portanto, iremos utilizar um computador virtual que já contem o programa instalado. 

O computador virtual tem uma pasta chamada “curso” no desktop, onde se encontra:

- O genoma de referência (arquivo.fa)
- O índice do genoma de referência (arquivo.fai)
- Amostras em formato bam (HG00118.bam, etc)
- O arquivo bed com as regiões que serão analizadas

Com isso, iremos correr o comando do HipSTR para genotipar essas amostras

CÓMO CRIAR OS ÍNDICES DAS AMOSTRAS? 

- Utilizaremos samtools index

```jsx
cd rota_da_pasta
samtools index nome_da_amostra.bam
```

Fazer esse comando para todas as amostras. 

Link tutorial de ajuda: https://drive.google.com/file/d/17vv41Hf0ezyEHzAHne1e4iPbzCemDgXN/view?usp=drive_link

COMANDOS 

Arquivos necessários

![image](https://github.com/user-attachments/assets/e5f57a64-0194-48f6-b09f-e768901405c9)


IMPORTANTE

- Antes de correr o comando do HipSTR, verifiquem que todas as amostras que serão incluidas no comando, já tenham o seu índice (Arquivo fai, gerado com samtools index)
- Preparar o comando previamente em algum arquivo de texto, substituindo nome_da_amostra1 pelo nome real da amostra.
- Podem rodar varias amostras no mesmo comando, separando elas por virgulas SEM espaço, como no exemplo embaixo.

```jsx
cd rota_da_pasta
--bams nome_da_amostra1.bam,nome_da_amostra2.bam --fasta GRCh38_full_analysis_set_plus_decoy_hla.fa --regions regionsx.bed --str-vcf nome_de_saida.vcf.gz --min-reads 8 --def-stutter-model --max-flank-indel 0.50 --max-str-len 127 --viz-out aln.viz.gz
```

Link de ajuda: https://drive.google.com/file/d/1Vzw8K7-Jh-ud7ul_0bNhKpJ4gw0zxqvo/view?usp=drive_link

INTERPRETAÇÃO DO ARQUIVO DE SAÍDA

HipSTR gera como arquivo de saída um arquivo vcf.gz. Logo de descomprimir o arquivo teremos um vcf. 

O vcf podemos abrir com Excel e realizar a interpretação dos dados para genotipar as amostras. 

Durante a aula aprenderemos a realizar essa interpretação.
