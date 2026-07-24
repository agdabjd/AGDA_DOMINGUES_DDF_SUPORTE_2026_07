# Step 1 – Troubleshooting

Esse passo se trata da resolução de um chamado criado pois o usuário reportou um erro na importação dos dados da Dadosfera.

## Resposta ao chamado

Bom dia, prezado.

Analisei a planilha utilizada na pipeline e identifiquei duas inconsistências na aba performanceRating. Na coluna EmployeeNumber, há uma célula com o erro #NAME?. Também existe o texto NULL na coluna PerformanceRating do funcionário 274, que deve ser substituído por uma célula vazia caso a avaliação não esteja disponível.

Recomendo corrigir esses dois valores e validar se EmployeeNumber contém apenas números e se PerformanceRating possui somente valores numéricos ou células vazias. A mistura de erros de fórmula, textos e números na mesma coluna pode impedir a identificação correta do tipo de dado durante a importação.

Para consultar os detalhes da execução, acesse a pipeline na Dadosfera, abra o área de status, selecione a execução com falha, clique na opção de "actions" e utilize a opção de download dos logs.

Ao carregar dados do Google Sheets, também é importante manter uma única linha de cabeçalho, evitar células mescladas e linhas vazias no meio da tabela, utilizar nomes de colunas únicos e sem aspas duplas, manter um único tipo de dado por coluna e corrigir erros como #NAME?, #REF! e #VALUE!.

Após realizar as correções, salve a planilha e execute novamente a sincronização da pipeline. Caso o erro continue, encaminhe os logs da nova execução para que possamos prosseguir com a investigação.

At.te., Agda Beatriz Jedliczka Domingues
Suporte Técnico