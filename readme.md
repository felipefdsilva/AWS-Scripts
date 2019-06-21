Felipe Ferreira : Mudança de Reservas por Código - Guia do Usuário  

1.  [Felipe Ferreira](index.html)

Felipe Ferreira : Mudança de Reservas por Código - Guia do Usuário
==================================================================

Created by Felipe Ferreira, last modified on Jun 17, 2019

Este artigo tem o intuito de orientar o uso do programa que realiza a troca de reservas.

/\*<!\[CDATA\[\*/ div.rbtoc1561152126897 {padding: 0px;} div.rbtoc1561152126897 ul {list-style: upper\\2D roman;margin-left: 0px;} div.rbtoc1561152126897 li {margin-left: 0px;padding-left: 0px;} /\*\]\]>\*/

*   [Introdução](#MudançadeReservasporCódigo-GuiadoUsuário-Introdução)
*   [Instruções](#MudançadeReservasporCódigo-GuiadoUsuário-Instruções)
*   [Related articles](#MudançadeReservasporCódigo-GuiadoUsuário-Relatedarticles)

Introdução
----------

O programa é constituído de três arquivos. São eles:

*   **modify.py** - função auxiliar que implementa a divisão da reserva atual em N reservas menores
*   **exchange.py** - função auxiliar que implementa a troca de uma reserva por outra de plataforma diferente (Linux, Windows, etc) ou tipo de instância EC2 diferente
*   **process-reservation.py** - função principal que orquestra a operação da funções descritas acima

Além disso, o programa conta com um um arquivo que possui os parâmetros de entrada em sintaxe json. Este arquivo é nomeado **input.json**. 

Instruções
----------

  

1.  Abra o arquivo input.json em qualquer editor de texto e edite conforme necessário para uma execução pro programa. Os parâmetro de entrada são os seguintes:
    *   AWSProfile: o perfil configurado via AWS CLI com as credenciais adequadas para as funções serem executadas com sucesso
    *   Region: a região onde encontram-se as reservas
    *   ReservationId: o ID da reserva que possui desperdício
    *   WastedInstanceCount: a quantidade de instâncias que estão sendo desperdiçadas na reserva
    *   T3NanoExpectedInstanceCount: o número de instâncias t3.nano que espera-se com a primeira troca
    *   MaxHourlyPriceDifference: a máxima diferença de custo por hora, entre a reserva original e as novas
    *   T3NanoSplitInstanceCountList: lista onde cada item é a contagem de instâncias de uma nova reserva gerada pela divisão da reserva t3.nano
    *   TargetPlatformList: lista com as plataformas (Linux, Windows, etc) de cada uma das novas reservas desejadas ao fim da execução do programa
    *   TargetInstanceTypeList: lista com os tipos de instância da novas reservas geradas ao fim da execução do programa
        
        **Exemplo: input.json**
        
        {
        	"AWSProfile" : "painel",
        	"Region" : "us-east-1",
        	"ReservationId": "b12a3677-8d1c-47a1-87c9-240b8de3d8ac",
        	"WastedInstanceCount": 8,
        	"T3NanoExpectedInstanceCount": 8,
        	"MaxHourlyPriceDifference": 0.005,
        	"T3NanoSplitInstanceCountList":\[
        		4, 
        		4
        	\],
        	"TargetPlatformList":\[
        		"Linux/UNIX",
        		"Linux/UNIX"
        	\],
        	"TargetInstanceCountList":\[
        		1,
        		1
        	\],
        	"TargetInstanceTypeList":\[
        		"t2.small",
        		"t2.small"
        	\]
        }
        
2.  Salve as alterações no arquivo input.json
3.  Abra um terminal, e digite o seguinte comando:
    
    **Bash/Terminal**
    
    python process-reservation.py input.json
    
4.  Aguarde o programa terminar a execução. Alguns dados serão impressos na tela, indicação o decorrer da operação.

Related articles
----------------

*   Page:
    
    [Mudança de Reservas por Código - Guia do Usuário](/wiki/spaces/~327718203/pages/574816257)
    

  

  

Document generated by Confluence on Jun 21, 2019 18:22

[Atlassian](http://www.atlassian.com/)
