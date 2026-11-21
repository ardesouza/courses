# RELATÓRIO DE IMPLEMENTAÇÃO DE SERVIÇOS AWS

**Data:** 21/11/2026  
**Empresa:** Abstergo Industries  
**Responsável:** Aleksandro Rodrigues de Souza

## 1. Introdução

Este relatório apresenta uma proposta de implementação de serviços da Amazon Web Services (AWS) na empresa Abstergo Industries, com o objetivo de reduzir custos operacionais relacionados à infraestrutura de tecnologia da informação.

A proposta contempla três serviços AWS que permitem identificar oportunidades de economia, otimizar a utilização dos recursos computacionais e reduzir despesas com armazenamento de dados.

O projeto busca proporcionar uma infraestrutura mais eficiente, escalável e alinhada às necessidades do negócio, evitando investimentos desnecessários em recursos tecnológicos.

A implementação será realizada de forma gradual, permitindo avaliar os resultados financeiros e operacionais antes de ampliar a utilização dos serviços.

## 2. Descrição do Projeto

O projeto de implementação de ferramentas AWS foi dividido em três etapas, cada uma com objetivos específicos voltados à redução de custos e à melhoria da eficiência operacional.

### Etapa 1: AWS Cost Explorer

- **Nome da ferramenta:** AWS Cost Explorer.
- **Foco da ferramenta:** Análise e otimização dos custos da infraestrutura AWS.
- **Descrição do caso de uso:**

O AWS Cost Explorer permite visualizar, analisar e acompanhar os gastos relacionados aos serviços AWS, possibilitando identificar quais recursos apresentam maior impacto financeiro.

A ferramenta será utilizada para analisar o histórico de consumo da infraestrutura, identificar recursos subutilizados e avaliar oportunidades de redução de despesas.

Com base nas informações obtidas, será possível estabelecer prioridades de otimização e acompanhar os resultados financeiros das ações implementadas.

**Benefícios esperados:**
- Maior controle sobre os gastos com tecnologia.
- Identificação de recursos com potencial de economia.
- Apoio à tomada de decisão do departamento financeiro.
- Acompanhamento dos resultados das iniciativas de redução de custos.

### Etapa 2: Amazon EC2 Auto Scaling

- **Nome da ferramenta:** Amazon EC2 Auto Scaling.
- **Foco da ferramenta:** Otimização dos recursos computacionais e redução de custos com servidores.
- **Descrição do caso de uso:**

O Amazon EC2 Auto Scaling permite ajustar automaticamente a quantidade de instâncias computacionais de acordo com a demanda da aplicação.

Na Abstergo Industries, o serviço poderá ser utilizado em sistemas que apresentam variações de utilização ao longo do dia, evitando a manutenção de servidores em quantidade superior à necessária.

Durante períodos de baixa demanda, a quantidade de instâncias poderá ser reduzida. Em períodos de maior utilização, novos recursos poderão ser disponibilizados automaticamente, mantendo a capacidade necessária para atender aos usuários.

**Benefícios esperados:**
- Redução de gastos com servidores ociosos.
- Melhor aproveitamento dos recursos computacionais.
- Ajuste automático da infraestrutura conforme a demanda.
- Maior disponibilidade e capacidade de resposta dos sistemas.

A economia dependerá do perfil de utilização das aplicações e da configuração dos recursos. Sistemas que exigem capacidade constante poderão apresentar menor potencial de redução de custos.

### Etapa 3: Amazon S3 com regras de ciclo de vida

- **Nome da ferramenta:** Amazon Simple Storage Service (Amazon S3).
- **Foco da ferramenta:** Redução dos custos de armazenamento e gerenciamento eficiente de dados.
- **Descrição do caso de uso:**

O Amazon S3 oferece armazenamento de objetos com diferentes classes de armazenamento, permitindo selecionar a opção mais adequada de acordo com a frequência de acesso aos dados.

A proposta consiste em armazenar documentos, arquivos de sistemas, relatórios e cópias de segurança no Amazon S3, utilizando regras de ciclo de vida para transferir automaticamente dados menos acessados para classes de armazenamento de menor custo.

Por exemplo, arquivos que precisam permanecer disponíveis para consulta, mas são raramente acessados, poderão ser transferidos para classes como S3 Standard-IA ou S3 Glacier, conforme os requisitos de recuperação e disponibilidade.

Essa estratégia permite manter os dados armazenados pelo período necessário, reduzindo despesas sem comprometer a continuidade das operações.

**Benefícios esperados:**
- Redução dos custos com armazenamento de dados.
- Gerenciamento automatizado do ciclo de vida dos arquivos.
- Melhor aproveitamento dos recursos de armazenamento.
- Possibilidade de expansão da capacidade sem aquisição de novos equipamentos físicos.

A escolha das classes de armazenamento deverá considerar os custos de recuperação, as tarifas de acesso e os períodos mínimos de armazenamento aplicáveis.

## 3. Conclusão

A implementação dos serviços AWS propostos para a Abstergo Industries tem como objetivo principal reduzir os custos operacionais de tecnologia da informação, aumentar a eficiência da infraestrutura e melhorar o controle financeiro dos recursos computacionais.

O AWS Cost Explorer permitirá identificar oportunidades de economia e acompanhar os gastos. O Amazon EC2 Auto Scaling contribuirá para adequar a capacidade computacional à demanda real dos sistemas. Já o Amazon S3, por meio de suas regras de ciclo de vida, possibilitará reduzir despesas com o armazenamento de dados.

A combinação dessas ferramentas poderá proporcionar maior previsibilidade financeira, melhor utilização dos recursos tecnológicos e redução de investimentos desnecessários em infraestrutura.

Recomenda-se a aprovação de um projeto-piloto para implementação dos serviços, acompanhado de uma análise dos custos atuais e posteriores à implantação. Dessa forma, será possível comprovar os benefícios financeiros obtidos e avaliar a viabilidade de expansão da solução.

A continuidade do projeto deverá considerar os resultados do piloto, os custos efetivos dos serviços AWS e as necessidades operacionais da empresa.

## 4. Anexos

- Anexo I: Levantamento dos custos atuais de infraestrutura.
- Anexo II: Proposta de arquitetura dos serviços AWS.
- Anexo III: Estimativa de custos e oportunidades de economia.
- Anexo IV: Plano de implementação e acompanhamento dos resultados.

## 5. Aprovação

**Assinatura do responsável pelo projeto:**

Aleksandro Rodrigues de Souza

**Aprovação do gerente financeiro:**

[Nome do gerente financeiro]

**Data da aprovação:** ____/____/________

**Observações:**

________________________________________________________________

________________________________________________________________

