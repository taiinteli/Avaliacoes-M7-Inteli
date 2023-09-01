# Avaliacoes-M7-Inteli
Avaliações do Módulo 7

Para executar o backend:

```bash
python main.py
```

Para executar o frontend:

```bash
node server.js
```

| ***IMPORTANTE:*** Utilizar dentro do contexto do container.

## Requisitos de Desenvolvimento

1. **Framework Web**: FastAPI
2. **Ferramenta de Containerização**: Docker

## Desenvolvimento da Aplicação

### 1. Criando a Aplicação

-  Instale o FastAPI usando o seguinte comando:

<p align="center"> pip install fastapi </p>

### 2. Crie um arquivo Python chamado `app.py` contendo o código da aplicação. Um exemplo básico pode ser:

```python
from fastapi import FastAPI, Request
from fastapi.templating import Jinja2Templates
from fastapi.responses import HTMLResponse

app = FastAPI()
templates = Jinja2Templates(directory="templates")

@app.get("/", response_class=HTMLResponse)
def curriculum(request: Request):
    return templates.TemplateResponse("curriculum.html", {"request": request})
```

-  Crie um diretório chamado templates e crie o arquivo html dentro dele. 
 
### 3. Containerização da Aplicação

- Crie um arquivo chamado Dockerfile na raiz do seu projeto com o seguinte conteúdo: 

# Use a imagem base oficial do Python (escolha da versão desejada)
FROM python:3.9

# Instale o FastAPI
RUN pip install fastapi
# Copie o código fonte da aplicação para o container
COPY . /app
WORKDIR /app

# Exponha a porta 80
EXPOSE 80

# Comando para iniciar a aplicação
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "80"]

### 4. Construindo e Executando o Container Docker

- Abra o terminal e navegue até o diretório do seu projeto.

- Execute o seguinte comando para construir a imagem do Docker (substitua <nome-da-imagem> pelo nome que você deseja dar à imagem):

<p align="center"> docker build -t <nome-da-imagem> </p>

- Após a construção da imagem, execute o seguinte comando para iniciar o container (substitua <nome-do-container> pelo nome que você deseja dar ao container):
<p align="center"> docker run -d -p 80:80 --name <nome-do-container> <nome-da-imagem> </p>

- A aplicação estará disponível em http://localhost:80.

## Publicação no Docker Hub

Para publicar a imagem no Docker Hub, siga os seguintes passos:

  - Faça o login no Docker Hub usando o comando:
<p align="center"> docker login </p>

- Renomeie a imagem que você criou para seguir o padrão de nome do Docker Hub (usuário/nome-da-imagem):

  <p align="center"> docker tag nome-da-imagem> usuário-no-docker-hub>/nome-da-imagem> </p>

- Faça o push da imagem para o Docker Hub:

<p align="center">docker push <usuário-no-docker-hub>/<nome-da-imagem>
 </p>
