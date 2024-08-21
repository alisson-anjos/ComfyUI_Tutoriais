### Criar Ambiente Virtual para a instalação das dependencias do ComfyUI

* Para criar o ambiente virtual vamos executar o comando a seguir:

```
python -m venv venv
```
* Ativar o ambiente virtual

```
source venv/bin/activate
```

### Clonar o repositório do ComfyUI

* Abrir o terminal dentro do RunPod e executar o comando abaixo:

```
git clone https://github.com/comfyanonymous/ComfyUI.git
```

### Instalar as dependencias necessárias para o funcionamento do ComfyUI

* Com o ambiente virtual ativo vamos executar os comandos para instalar as dependencias
* Considerando que você esteja no diretório do workspace execute o comando abaixo:

```
pip install -r ComfyUI/requirements.txt
```

### Clonar o repositório do ComfyUI Manager (Custom Node)


```
git clone https://github.com/ltdrdata/ComfyUI-Manager.git ComfyUI/custom_nodes/ComfyUI-Manager
```

### Clonar o repositório do ComfyUI BitsAndBytes NF4

```
git clone https://github.com/comfyanonymous/ComfyUI_bitsandbytes_NF4.git ComfyUI/custom_nodes/ComfyUI_bitsandbytes_NF4
```

### Instalar as dependencias do custom node omfyUI BitsAndBytes NF4

```
pip install -r ComfyUI/custom_nodes/ComfyUI_bitsandbytes_NF4/requirements.txt
```

### Atualizar o PyTorch instalado no RunPod

* Para atualizar a versão do Pytorch instalado no RunPod segue o comando abaixo:

```
pip install torch==2.4.0 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

### Instalar o xformers

```
pip install xformers --index-url https://download.pytorch.org/whl/cu121
```

### Fazer o download do modelo do FLUX NF4

```
wget -c https://huggingface.co/lllyasviel/flux1-dev-bnb-nf4/resolve/main/flux1-dev-bnb-nf4-v2.safetensors -P ComfyUI/models/checkpoints/
```

### [Opcional] Vou deixar aqui como fazer o download do Hugging Face se o repositório for privado e precisar de autenticação
```
wget --header="Authorization: Bearer [COLOCA SEU TOKEN DO HUGGING FACE AQUI]" https://huggingface...........
```

### Criar um script de start para facilitar a execução do ComfyUI

* Criar um arquivo start_comfyui.sh com o conteudo abaixo

```
cat << 'EOF' > start_comfyui.sh
#!/bin/bash
source "$(pwd)/venv/bin/activate"
python ComfyUI/main.py --listen
EOF
````

* Caso queira incluir o novo frontend

```
cat << 'EOF' > start_comfyui.sh
#!/bin/bash
source "$(pwd)/venv/bin/activate"
python ComfyUI/main.py --listen --front-end-version Comfy-Org/ComfyUI_frontend@latest
EOF
````

* Conceder permissão de execução para o arquivo

```
chmod +x start_comfyui.sh
```

### Executar o start_comfyui.sh

```
./start_comfyui.sh
```
