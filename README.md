
# 🎯 Jogo de Adivinhação com Docker Compose

Este projeto consiste na orquestração completa de um jogo de adivinhação (baseado no repositório [fams/guess_game](https://github.com/fams/guess_game)) utilizando contêineres Docker. A aplicação é composta por:

- ✅ Um backend em **Python Flask**
- ✅ Um frontend em **React**, servido via **NGINX**
- ✅ Um banco de dados **PostgreSQL**

---

## 🧱 Estrutura e Opções de Design

### Serviços Utilizados

| Serviço   | Função                                                                 |
|-----------|------------------------------------------------------------------------|
| `backend` | Roda o Flask responsável pela lógica do jogo                           |
| `frontend`| Compila o React, serve com NGINX e faz o proxy reverso para o backend  |
| `db`      | Banco PostgreSQL para armazenar dados do jogo                          |

### Volumes

- Um volume nomeado `postgres_data` foi criado para persistir os dados do Postgres entre os ciclos de vida dos containers.

```yaml
volumes:
  postgres_data:


Comunicação entre serviços
- Os serviços estão conectados implicitamente pela rede padrão do Docker Compose.
- O serviço frontend utiliza NGINX com um proxy reverso configurado para encaminhar requisições da API (/api/) para o container backend.

🚀 Instalação e Execução
1. Pré-requisitos
- Docker instalado (instalar Docker)
- Docker Compose v2+
2. Clone o repositório
git clone https://github.com/andersonhrosa/guess_game.git
cd guess_game


3. Estrutura esperada
Garanta que os diretórios backend/, frontend/, e repository/ estejam corretamente posicionados. O frontend deve conter o arquivo default.conf com a configuração do NGINX embutido.
4. Build e execução dos containers
docker compose up --build


O primeiro build pode demorar alguns minutos.

5. Acesse a aplicação
- Interface do jogo (frontend): http://172.19.0.4:3000

🔄 Atualização dos Componentes
A estrutura foi pensada para permitir atualizações individuais.
🔹 Backend
docker compose build backend
docker compose restart backend


🔹 Frontend
docker compose build frontend
docker compose restart frontend


🔹 Banco de Dados
Para atualizar a versão:
image: postgres:16  # por exemplo


E depois:
docker compose down
docker compose up --build


ℹ️ O volume persistente postgres_data manterá os dados. Sempre faça backup antes de upgrades de versão!


📁 Organização
guess_game/
├── backend/           # Código Flask + Dockerfile
├── frontend/          # Código React + Dockerfile + default.conf (NGINX)
├── docker-compose.yml # Orquestração dos serviços
└── README.md



📌 Considerações Finais
- A estrutura garante resiliência automática com restart: always nos serviços
- O frontend atua como proxy reverso e servidor com NGINX embutido
- O banco de dados é persistente e facilmente atualizável
- O sistema é modular, permitindo atualizações parciais sem interromper tudo

🪪 Licença
Distribuído sob a licença MIT. Consulte o arquivo LICENSE.

