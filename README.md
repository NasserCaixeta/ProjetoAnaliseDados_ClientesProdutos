## Projeto de Análise de Dados
Este projeto tem como objetivo realizar uma análise de dados relacionada a funcionários, serviços prestados, clientes e áreas de atuação da empresa. O código em Python utiliza a biblioteca Pandas para manipulação e análise de dados. A seguir, uma descrição das principais funcionalidades:

## Importação de Módulos e Arquivos
O código começa importando os módulos necessários e carregando dados a partir de arquivos CSV e Excel. Os conjuntos de dados incluem informações sobre funcionários, serviços prestados e clientes.

```
import pandas as pd
funcionarios_df = pd.read_csv('CadastroFuncionarios.csv', sep=';', decimal=',')
servicos_prestados = pd.read_excel('BaseServiçosPrestados.xlsx')
clientes_df = pd.read_csv('CadastroClientes.csv', sep=';', decimal=',')
```
## Entendendo a Folha Salarial
O script calcula o total da folha salarial mensal considerando salário base, impostos, benefícios, vale-transporte (VT) e vale-refeição (VR). O resultado é exibido na saída padrão.

```
funcionarios_df['Salario Total'] = funcionarios_df['Salario Base'] + funcionarios_df['Impostos'] + funcionarios_df['Beneficios'] + funcionarios_df['VT'] + funcionarios_df['VR']
print("Total da Folha Salarial Mensal é: {:,}".format(funcionarios_df['Salario Total'].sum()))
```
## Entendendo o Faturamento da Empresa
O código relaciona informações sobre serviços prestados e clientes para calcular o faturamento total da empresa. O resultado é exibido na saída padrão.

```
faturamentos_df = servicos_prestados[['ID Cliente', 'Tempo Total de Contrato (Meses)']].merge(clientes_df[['ID Cliente', 'Valor Contrato Mensal']], on='ID Cliente')
faturamentos_df['Faturamento Total'] = faturamentos_df['Tempo Total de Contrato (Meses)'] * faturamentos_df['Valor Contrato Mensal']
print("Faturamento Total: {:,}".format(faturamentos_df['Faturamento Total'].sum()))
```
## Análise de Funcionários e Contratos
O código realiza análises estatísticas sobre o número de funcionários, a porcentagem de funcionários que fecharam contratos e a quantidade de contratos por área de atuação.

```
qtd_funcionario_total = len(funcionarios_df['ID Funcionário'])
qtd_funcionario_fecharamcontrato = len(servicos_prestados['ID Funcionário'].unique())
print("O Percentual de Funcionários que Fecharam contrato é de: {:.2%}".format(qtd_funcionario_fecharamcontrato / qtd_funcionario_total))

contratos_area_df = servicos_prestados.merge(funcionarios_df[['ID Funcionário', 'Area']], on='ID Funcionário')
contratos_area_qtd = contratos_area_df['Area'].value_counts()
print(contratos_area_qtd)
```
## Análise de Funcionários por Área
O código gera um gráfico de barras representando a quantidade de funcionários por área de atuação.

```
funcionarios_area = funcionarios_df['Area'].value_counts()
print(funcionarios_area)
funcionarios_area.plot(kind='bar')
```
## Ticket Médio Mensal
Por fim, o código calcula e exibe o ticket médio mensal dos contratos dos clientes.

```
ticket_medio = clientes_df['Valor Contrato Mensal'].mean()
print('Ticket Médio Mensal: R${:,}'.format(ticket_medio))
```
Observação: Certifique-se de que os arquivos CadastroFuncionarios.csv, BaseServiçosPrestados.xlsx e CadastroClientes.csv estão presentes no mesmo diretório que este script para garantir o funcionamento adequado.

## Contribuições
Contribuições são bem-vindas. Sinta-se à vontade para abrir issues ou pull requests para melhorar este projeto.
