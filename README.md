# Case Técnico – Support Intern | Dadosfera

Este repositório contém a resolução do case técnico para a oportunidade de Support Intern na Dadosfera.

O projeto simula atividades relacionadas à rotina de suporte técnico da plataforma, incluindo troubleshooting de importação de dados, preparação de infraestrutura Linux, administração de banco de dados, configuração de VPN, criação de pipelines, catalogação de ativos, consultas SQL, visualizações e diagnóstico de problemas de conectividade.

Cada etapa foi documentada em um diretório próprio, contendo o arquivo Markdown correspondente e, quando aplicável, as evidências geradas durante a execução.

---

## Contexto do desenvolvimento

Quando recebi o case técnico, as credenciais necessárias para acessar a plataforma Dadosfera ainda não haviam sido disponibilizadas. Por esse motivo, iniciei a execução das atividades que podiam ser realizadas de forma independente, como a análise dos dados, a preparação do servidor, a criação do banco MySQL e a configuração inicial do OpenVPN.

O acesso à plataforma foi solicitado em 17/07/2026. Após o recebimento das credenciais em 20/07/2026, foi possível concluir as etapas que dependiam dos módulos de Coleta, Catálogo e Visualização da Dadosfera.

A primeira implementação da infraestrutura foi realizada localmente em uma máquina virtual criada com o Oracle VirtualBox. O MySQL e o OpenVPN foram instalados e configurados, porém, durante os testes de conectividade, foi identificado que a infraestrutura da rede residencial não permitia o recebimento adequado das conexões externas necessárias pela porta UDP 1194.

Diante dessa limitação, o ambiente foi migrado para uma instância na AWS EC2. Essa mudança permitiu utilizar um servidor Ubuntu em uma rede pública, controlar diretamente as regras de entrada e concluir a integração com a Dadosfera sem expor publicamente a porta 3306 do MySQL.

---

## Arquitetura da solução

A arquitetura final foi composta pelos seguintes elementos:

- Workstation Windows utilizada para acessar a AWS, a Dadosfera e o GitHub;
- Instância AWS EC2 executando Ubuntu Server 26.04;
- MySQL Server utilizado para armazenamento dos dados;
- OpenVPN responsável pela comunicação privada entre a Dadosfera e a EC2;
- Security Group configurado para controlar o acesso à instância;
- Pipeline Full Load responsável pela coleta dos dados;
- Catálogo da Dadosfera utilizado para documentação dos datasets;
- Módulo de Visualização utilizado para consultas SQL e análises descritivas.

A porta TCP 22, utilizada pelo SSH, foi restrita ao endereço IP autorizado. A porta UDP 1194 foi disponibilizada para o OpenVPN, enquanto a porta TCP 3306 permaneceu sem exposição pública.

A Dadosfera acessa o banco por meio do túnel VPN, utilizando o endereço privado da instância e um usuário MySQL dedicado com permissão somente de leitura.

---

## Tecnologias e ferramentas utilizadas

- Amazon Web Services;
- Amazon EC2;
- AWS Security Groups;
- Oracle VirtualBox;
- OpenVPN;
- OpenSSH;
- SSH e SCP;
- PowerShell;
- Bash;
- MySQL Server;
- SQL;
- Microsoft Excel;
- Google Sheets;
- Arquivos CSV;
- Dadosfera;
- Pipelines de coleta;
- Catálogo de Dados;
- Módulo de Visualização;
- Git;
- GitHub.

---

## Estrutura do repositório

```text
AGDA_DOMINGUES_DDF_SUPORTE_2026_07/
│
├── Step 1 - Troubleshooting/
│   └── STEP1.md
│
├── Step 2 - Criacao bd/
│   ├── Evidencias/
│   └── STEP2.md
│
├── Step 3 - Configuracao VPN/
│   ├── Evidencias/
│   └── STEP3.md
│
├── Step 4 - Conexao com Dadosfera/
│   ├── Evidencias/
│   └── STEP4.md
│
├── Step 5 - Catalogo de dados/
│   ├── Evidencias/
│   └── STEP5.md
│
├── Step 6 - Consultas SQL/
│   ├── Evidencias/
│   └── STEP6.md
│
├── Step 7 - Suporte hibrido ou presencial/
│   └── STEP7.md
│
├── Tentativa de realizar os steps 2 3 4 5 6 e 7 em servidor local/
│   └── Documentação e evidências da implementação inicial no VirtualBox
│
└── README.md
```

As pastas nomeadas com "Step" possuem todas um arquivo markdown com o passo a passo do que foi realizado e os prints de comprovação.

O diretório `Tentativa de realizar os steps 2 3 4 5 6 e 7 em servidor local` preserva a documentação da primeira implementação. Esses arquivos registram a configuração realizada no VirtualBox e as evidências que levaram à decisão de migrar o ambiente para a AWS.

Os arquivos sensíveis, como a chave SSH `.pem`, o perfil `.ovpn`, senhas e credenciais, foram mantidos fora do diretório versionado. Endereços IP, identificadores da conta AWS e outras informações sensíveis também foram ocultados nas evidências publicadas.

---

## Resumo das etapas

### Step 1 – Troubleshooting

Foi elaborada uma resposta de atendimento para um chamado relacionado à falha na importação de dados do Google Sheets.

Durante a análise da planilha, foram identificadas inconsistências na aba performanceRating, incluindo um erro `#NAME?` na coluna EmployeeNumber e o uso do texto `NULL` em uma coluna numérica. A resposta orienta a correção dos dados, o download dos logs da pipeline e os principais cuidados durante a preparação de planilhas para coleta.

### Step 2 – Criação de Banco de Dados

Foi criada uma instância AWS EC2 com Ubuntu Server para hospedar o MySQL e o OpenVPN.

O banco `agda_domingues_support_intern` foi estruturado com quatro tabelas relacionais:

TB_agda_domingues_support_intern
TB_performance_rating
TB_environment_management
TB_income

As quatro abas da planilha foram tratadas, convertidas para CSV e importadas. Cada tabela foi validada com 1470 registros e os relacionamentos foram definidos pela coluna `EmployeeNumber`.

### Step 3 – Configuração e Conexão de VPN

O MySQL foi preparado para aceitar conexões pelas interfaces da instância, mantendo a porta 3306 sem exposição pública.

Foi criado o usuário `dadosfera`, com permissão somente de leitura. Em seguida, o OpenVPN foi instalado e configurado, o serviço e a interface `tun0` foram validados e o arquivo de cliente `.ovpn` foi transferido para a workstation e cadastrado na plataforma.

### Step 4 – Conexão com a Dadosfera

A fonte MySQL foi cadastrada utilizando o endereço privado da EC2 e a rede OpenVPN criada anteriormente.

Após o teste de conexão, foi configurada uma pipeline em modo `Full load`. Além da tabela principal exigida no enunciado, as três tabelas complementares também foram coletadas para preservar o conjunto completo e permitir consultas relacionais posteriores.

A pipeline foi executada com sucesso e as quatro tabelas foram carregadas na plataforma.

### Step 5 – Catálogo de Dados

Os quatro datasets gerados pela pipeline foram localizados no Catálogo da Dadosfera.

Cada ativo recebeu um nome amigável e uma descrição em inglês, registrando seu conteúdo e a possibilidade de relacionamento com as demais tabelas por meio da coluna `EmployeeNumber`.

### Step 6 – Consultas SQL e Visualizações

Foi criada a coleção `Agda Domingues - 07 2026` dentro da pasta destinada aos testes técnicos no módulo de Visualização.

Foram desenvolvidas três análises:

- Executive Workforce Overview;
- Attrition Rate by Department;
- Average Monthly Income by Job Role and Gender.

As consultas utilizaram os identificadores técnicos dos datasets e combinaram as tabelas por meio de `JOINs`, produzindo análises sobre força de trabalho, desligamentos, satisfação, desempenho e remuneração.

### Step 7 – Suporte Híbrido/Presencial

Foi produzido um vídeo demonstrando como validar uma estação de trabalho e a infraestrutura utilizada no case.

A apresentação inclui verificações do sistema operacional, acesso SSH, serviços MySQL e OpenVPN, portas, interface VPN, rotas, DNS, MTU, autenticação no banco e validação na Dadosfera.

Também foi apresentada uma estratégia de investigação de lentidão e falhas intermitentes baseada em hipóteses, testes objetivos, evidências e conclusões.

---

## Principais resultados

Ao final do projeto, foram concluídos os seguintes resultados:

- Infraestrutura Linux criada na AWS EC2;
- Banco MySQL configurado e protegido contra exposição pública;
- Quatro tabelas relacionais criadas e populadas;
- 1470 registros validados em cada tabela;
- Usuário de integração com permissão somente de leitura;
- OpenVPN instalado e conectado à Dadosfera;
- Fonte MySQL cadastrada e validada;
- Pipeline Full Load executada com sucesso;
- Quatro datasets disponibilizados e documentados no Catálogo;
- Consultas SQL e visualizações criadas no módulo de Visualização;
- Troubleshooting de importação documentado;
- Vídeo de validação operacional e diagnóstico produzido.

---

## Considerações finais

O desenvolvimento deste case envolveu atividades de suporte técnico, administração Linux, infraestrutura em nuvem, redes, segurança, banco de dados, integração de sistemas, análise de dados e documentação.

Além da execução técnica, o projeto exigiu adaptação diante de duas limitações: a ausência inicial de acesso à plataforma e a impossibilidade de estabelecer adequadamente a VPN no ambiente residencial. A manutenção das etapas já realizadas e a posterior migração para a AWS permitiram concluir a solução de forma segura, rastreável e alinhada aos requisitos do case.

Cada etapa foi documentada separadamente para registrar os comandos executados, as decisões técnicas, os problemas encontrados e as evidências de funcionamento do ambiente.