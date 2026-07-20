# Case Técnico – Support Intern | Dadosfera

Este repositório contém a documentação do desenvolvimento do Case Técnico para a vaga de Support Intern da Dadosfera.

O objetivo do desafio foi simular atividades comuns da rotina de suporte técnico da plataforma, envolvendo configuração de ambiente Linux, administração de banco de dados, conectividade por VPN, consultas SQL, troubleshooting e documentação técnica.

Durante o desenvolvimento do case, busquei executar cada atividade solicitada e também documentar todas as decisões tomadas, dificuldades encontradas e respectivas soluções. Dessa forma, este repositório registra todo o processo de implementação, permitindo reproduzir o ambiente e compreender o raciocínio utilizado em cada etapa.

---

## Tecnologias utilizadas
- Ubuntu Server 26.04 LTS
- Oracle VirtualBox
- MySQL Server
- OpenVPN
- OpenSSH
- WinSCP
- Git e GitHub
- Microsoft Excel
- Google Sheets

---

## Estrutura do repositório
O projeto foi organizado em diretórios independentes para cada etapa do case.

```
.
├── Step1_Troubleshooting
├── Step2_Criacao_Banco_De_Dados
├── Step3_Configuracao_OpenVPN
├── Step4_Conexao_Dadosfera
├── Step5_Catalogo_De_Dados
├── Step6_Consultas_SQL
└── Step7_Suporte_Hibrido_Presencial
```

Cada pasta contém um arquivo markdown descrevendo detalhadamente a execução da etapa correspondente, além das evidências utilizadas (prints de tela, comandos executados, consultas SQL e demais arquivos produzidos).

---

## Organização das etapas

### Step 1 — Troubleshooting
Simulação de atendimento de suporte para investigação de falha na importação de um dataset do Google Sheets para a plataforma Dadosfera.

### Step 2 — Criação de Banco de Dados
- Configuração de uma máquina virtual Linux;
- Instalação e configuração do MySQL Server;
- Criação do banco de dados e da tabela solicitados;
- Importação dos dados do dataset fornecido.

### Step 3 — Configuração e Conexão de VPN
Instalação e configuração do OpenVPN seguindo a documentação oficial da Dadosfera, incluindo a geração do arquivo `.ovpn`.

### Step 4 — Conexão com a Dadosfera
Documentação do procedimento para cadastro da fonte de dados, criação da conexão e validação da pipeline.

Esta etapa não pôde ser executada integralmente devido à indisponibilidade de credenciais de acesso à plataforma durante o período de realização do case.

### Step 5 — Catálogo de Dados
Descrição de como a tabela seria disponibilizada e documentada no Catálogo da Dadosfera após a execução da pipeline.

### Step 6 — Consultas SQL
Elaboração de consultas SQL para análise dos dados importados.

Como não foi possível utilizar o módulo de Visualização da plataforma, as consultas foram executadas diretamente no MySQL e os gráficos foram produzidos no Microsoft Excel e Google Sheets para representar as análises solicitadas.

### Step 7 — Suporte Híbrido/Presencial
Produção do vídeo solicitado no case demonstrando:
- Preparação da estação de trabalho;
- Validação do ambiente;
- Testes de conectividade;
- Diagnóstico de problemas de rede;
- Comandos utilizados;
- Abordagem de troubleshooting.

O link para o vídeo encontra-se no arquivo markdown desta etapa.

---

## Limitações encontradas
No dia **17/07/2026**, foi solicitado acesso à plataforma Dadosfera para execução das etapas que dependiam obrigatoriamente de autenticação (Steps 4, 5 e parte do Step 6).

Como o acesso não foi disponibilizado até o prazo de entrega do case, essas etapas foram documentadas teoricamente com base na documentação oficial da plataforma e, sempre que possível, adaptadas para execução em ambiente local.

Todas as demais atividades foram executadas integralmente.

---

## Considerações finais
Além de cumprir os requisitos propostos, este projeto buscou documentar de forma clara todo o processo de configuração do ambiente, investigação de problemas e tomada de decisões técnicas.

Mesmo diante da indisponibilidade de acesso à plataforma Dadosfera, foram implementadas alternativas para demonstrar os conhecimentos exigidos pelo desafio, mantendo a aderência às tecnologias, ferramentas e conceitos envolvidos na rotina de suporte.