# storage_account_az900
All notes about storage acount class 
# AZ-900 — Resumo: Storage Account, Migração e Containers

# AZ-900 — Resumo: Storage Account, Migração e Containers

## 1. Conta de Armazenamento (Storage Account)

- O nome da conta de armazenamento deve ser **exclusivo** (único globalmente no Azure)
- **Modelo Standard**: usado para modo geral, em qualquer cenário
- **Modelo Premium**: usado para cenários de baixa latência e melhor performance; cobra desde o início pela alocação total, mesmo sem usar

---

## 2. Azure Blob Storage

- Blobs (Binary Large Objects) são o serviço de armazenamento de objetos do Azure
- Usado para guardar grandes quantidades de **dados não estruturados** (que não seguem formato de tabela como um banco relacional)
- Exemplos: imagens, vídeos, áudios, documentos (PDFs, backups, logs), arquivos de configuração, dados de IoT

**Estrutura básica:**
- **Storage Account** → a conta onde tudo fica
- **Container** → como uma pasta dentro da conta, organiza os blobs
- **Blob** → o arquivo em si, dentro do container

**Tipos de blob:**
- **Block Blob** – o mais comum, usado para arquivos de texto e binários (imagens, vídeos, docs)
- **Append Blob** – otimizado para operações de adicionar dados no final (ex: logs)
- **Page Blob** – usado para arquivos de acesso aleatório, como discos virtuais (VHDs) de VMs

**Camadas de acesso (tiers)** — importante para a prova, reduzem custo conforme a frequência de acesso:
- **Hot** – acesso frequente, custo de armazenamento maior, custo de acesso menor
- **Cool** – acesso pouco frequente (mínimo 30 dias)
- **Cold** – acesso raro (mínimo 90 dias)
- **Archive** – acesso raríssimo, armazenamento offline, custo baixíssimo mas leva horas para recuperar

---

## 3. Migração para o Azure

- Mover recursos (aplicações, dados, infraestrutura) que estão on-premises ou em outra nuvem, para dentro do Azure
- **Motivos comuns**: reduzir custo com hardware próprio, ganhar escalabilidade, mais segurança/disponibilidade, não precisar manter servidores fisicamente

**Estratégias dos 5 Rs (ou 6 Rs)** — bem cobrado na prova:
- **Rehost** ("lift and shift") – move a aplicação como está, sem alterar código (ex: VM local → VM no Azure)
- **Refactor** ("repackage") – pequenos ajustes, sem mudar arquitetura principal (ex: migrar para containers)
- **Rearchitect** ("revise") – modifica a arquitetura para aproveitar recursos nativos da nuvem (ex: monolito → microsserviços)
- **Rebuild** – reconstrói a aplicação do zero com tecnologias cloud-native
- **Replace** ("repurchase") – abandona o sistema antigo por uma solução SaaS pronta (ex: e-mail próprio → Microsoft 365)
- **Retire** (6º R, às vezes citado) – desliga sistemas que não são mais necessários

**Azure Migrate** — ferramenta principal/central para planejar e executar migrações:
- Faz descoberta e avaliação dos servidores/VMs existentes (compatibilidade, estimativa de custo)
- Ajuda a migrar servidores, bancos de dados e VMs (ex: de VMware, Hyper-V, AWS)
- Tem dashboard central para acompanhar o progresso

**Outras ferramentas relacionadas:**
- **Azure Database Migration Service** – migra bancos de dados (SQL Server, MySQL, PostgreSQL etc.)
- **Azure Data Box** – dispositivo físico enviado pela Microsoft para transferir grandes volumes de dados offline
  - **Data Box Disk** – até 5 discos por pedido
  - **Data Box** – uso de 10 dias sem custo extra; suporta conta de blobs
  - **Data Box Heavy** – uso de 20 dias sem custo extra
- **TCO Calculator** – estima quanto você economizaria migrando para o Azure comparado a manter on-premises
- **AzCopy** – funciona também para outros sistemas operacionais (não é exclusivo do Windows)

---

## 4. Containers

- Empacotam uma aplicação junto com tudo que ela precisa para rodar (código, bibliotecas, dependências, configurações) em uma unidade isolada e portátil
- É diferente de uma máquina virtual (VM)

**Container vs Máquina Virtual (VM)** — comparação muito cobrada na prova:
- **O que virtualiza**: VM virtualiza o hardware inteiro (SO completo próprio); Container virtualiza só a aplicação (compartilha o SO do host)
- **Tamanho**: VM é pesada (GBs); Container é leve (MBs)
- **Tempo de inicialização**: VM leva minutos; Container leva segundos
- **Isolamento**: VM tem isolamento total (SO próprio); Container tem isolamento parcial (compartilha o kernel do host)
