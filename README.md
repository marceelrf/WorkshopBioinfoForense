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

### Instale o HipSTR

~Infelizmente~ O HipSTR não está disponível para instalação via conda. Então faremos manualmente. Para isso primeiro vamos clonar o repositório do github com os códigos.
Para garantir reprodutibilidade vamos fazer isso na pasta home. O comando abaixo entra na pasta home.

`cd ~`

Em seguida vamos clonar o repositório:

`git clone https://github.com/HipSTR-Tool/HipSTR`

Entramos na pasta HipSTR e fazemos a instalação com `make`.

`cd HipSTR`

`make`

Para rodar o HipSTR:

`./HipSTR --help`
