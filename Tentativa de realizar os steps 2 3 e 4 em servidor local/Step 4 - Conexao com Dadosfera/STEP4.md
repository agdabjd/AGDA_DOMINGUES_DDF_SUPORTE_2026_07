# Step 4 – Conexão com a Plataforma Dadosfera

O objetivo desta etapa é integrar o banco de dados MySQL configurado localmente à plataforma Dadosfera para que seus dados possam ser coletados por meio de uma Pipeline.

Como o banco de dados está hospedado em uma rede privada, a comunicação com a plataforma depende da VPN configurada no Step 3. Dessa forma, a VPN fornece um canal seguro para que a Dadosfera consiga alcançar a máquina virtual sem expor o banco de dados diretamente à internet, conforme arquitetura recomendada pela documentação oficial da plataforma.

## Atividades previstas pelo case
De acordo com o enunciado, esta etapa consistiria em:
- Cadastrar a VPN utilizando o arquivo `dadosfera.ovpn` gerado no Step 3;
- Criar uma conexão (Fonte de Dados) do tipo MySQL;
- Associar essa conexão à VPN cadastrada;
- Validar a conectividade entre a plataforma e o banco de dados;
- Criar uma Pipeline consumindo a tabela `TB_agda_domingues_support_intern`.

## Limitação encontrada
A execução desta etapa depende obrigatoriamente de acesso autenticado à plataforma Dadosfera.

As credenciais de acesso foram solicitadas ao responsável pelo processo seletivo em 17/07/2026, porém não foram disponibilizadas até o prazo de entrega deste case. Em razão dessa limitação, não foi possível acessar a interface da plataforma para cadastrar a VPN, configurar a conexão com o banco de dados, validar a conectividade ou criar a Pipeline solicitada.

Por esse motivo, esta etapa não pôde ser executada na prática.

## Entendimento da arquitetura
Com base na documentação oficial da Dadosfera, o fluxo esperado seria o seguinte:
1. Cadastrar a OpenVPN na seção Coletar → Gestão de Conexões → Redes, utilizando o arquivo `dadosfera.ovpn` gerado anteriormente.
2. Criar uma Fonte de Dados do tipo MySQL, informando:
   - Endereço IP do servidor;
   - Porta do MySQL;
   - Usuário e senha;
   - Banco de dados;
   - VPN previamente cadastrada.
3. Validar a conexão diretamente pela interface da plataforma, verificando se a instância MySQL está acessível através da VPN.
4. Criar uma Pipeline, selecionando a fonte MySQL cadastrada e configurando os parâmetros de coleta, como tabela, colunas, modo de sincronização e frequência de execução.

## Conceitos envolvidos
Na arquitetura da Dadosfera, a VPN é responsável apenas por disponibilizar um acesso seguro à rede privada onde a fonte de dados está hospedada. A conexão com o banco de dados é realizada pela Fonte de Dados, que centraliza todas as credenciais e parâmetros necessários para acessar o MySQL.

A Pipeline representa o processo automatizado de coleta de dados (EL(T)), sendo responsável por extrair os dados da fonte configurada e disponibilizá-los para as etapas posteriores da plataforma, como processamento, exploração, análise e construção de aplicações baseadas em dados.

## Situação do ambiente
Apesar da impossibilidade de acesso à plataforma, toda a infraestrutura local necessária para esta integração foi preparada com sucesso:
- Máquina virtual Ubuntu configurada;
- Servidor MySQL instalado e operacional;
- Banco de dados criado e populado;
- Servidor OpenVPN configurado e em execução;
- Arquivo `dadosfera.ovpn` gerado para cadastro na plataforma.

Dessa forma, a única pendência para conclusão desta etapa foi a indisponibilidade das credenciais de acesso à plataforma Dadosfera.