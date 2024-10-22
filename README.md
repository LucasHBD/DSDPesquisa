# DSDPesquisa

Link para o artigo completo: https://repositorio.uft.edu.br/bitstream/11612/3145/1/Cicero%20Matheus%20da%20Silva%20Lacerda%20-%20Disserta%C3%A7%C3%A3o.pdf

#Artigo:

Projeto de uma Rede de Sensores Sem Fio para
Monitoramento Ambiental em Cidades Inteligentes

Por Cícero Matheus da Silva Lacerda, 2021

# Resumo:

  O presente trabalho apresenta o projeto de uma rede de sensores sem fio para monitoramento
  ambiental em cidades inteligentes. Para tal, inicialmente, são conceituadas tanto as premissas
  que definem uma cidade inteligente quanto as ferramentas tecnológicas que possibilitam a
  comunicação remota entre máquinas. Adiante, são apresentados o microcontrolador usado para
  realizar o monitoramento, que é o ESP32, e a infraestrutura de TI necessária para manter o
  sistema funcionando. Essa infraestutura, por sua vez, conta com ferramentas como StrongSwan
  para VPN, Bacula para backup, IPTables como firewall, Docker para publicação e GitLab
  como gerenciador de repositórios e executor das pipelines CI/CD. Logo em seguida, através da
  conceituação da arquitetura limpa, é explicado como é possível construir um sistema flexível,
  mesmo em nível de hardware. Como resultados, o trabalho mostra as aplicações e APIs feitas
  em .NET 5 para acessar os dados de monitoramento armazenados em um SQL Server 2019.
  Posteriormente são detalhados os testes, os quais atenderam às expectativas, e, além disso, são
  discutidos tópicos sobre eficiência, escalabilidade, confiabilidade, resiliência e segurança do
  protótipo apresentado. Para finalizar, há ainda uma seção dedicada à sugestão de trabalhos
  futuros.

# Objetivos do Projeto:

  # 1.1 Objetivo Geral:
  
  Implementar uma rede de sensores sem fio para fazer o monitoramento ambiental da
  cidade de Porto Nacional, Tocantins, incluindo servidores, aplicações, hardware, firewalls, VPNs
  e demais equipamentos de rede que viabilizam a comunicação via internet e disponibilizando
  interfaces de interação com o usuário para que todos possam usufruir do sistema.
  
  # 1.2 Objetivos Específicos:
  
  • Implementar um sistema embarcado para realizar o monitoramento ambiental e enviar as
  informações pela internet;
  • Configurar a infraestrutura de TI necessária para viabilizar o transporte de informações
  sobre o monitoramento;
  • Implementar as APIs que possibilitam a comunicação do circuito de monitoramento com
  os servidores;
  • Desenvolver uma aplicação web de administração para que os servidores públicos da
  prefeitura possam gerenciar a rede de sensores sem fio;
  • Publicar uma aplicação web para que os cidadãos (também chamados de usuários comuns)
  possam visualizar as medidas coletadas nos monitoramentos;
  • Disponibilizar uma API pública de leitura para que os cidadãos possam usar os dados para
  seus próprios objetivos.

# Aplicações e Testes:

  #2.1 Aplicação para Administração:
  
  A aplicação para administração só pode ser acessada através da VPN, portanto somente
  os administradores da RSSF possuem acesso a essa parte. Ao inserir com sucesso as credenciais,
  a primeira tela a ser exibida é essa:
  ![telaADM](https://github.com/user-attachments/assets/ad35bfea-2ecc-40a7-b437-b504b5250ed9)
  A primeira opção é para gerenciar as células, podendo adicionar, alterar, criar ou mesmo
  deletá-las. A segunda, por sua vez, permite ver os monitoramentos agendados ou criar um
  agendamento para o instante atual. Vale recordar que o próprio sistema já agenda monitoramentos
  periodicamente, portanto, a opção de adicionar pelo painel deve ser usada somente em casos
  excepcionais.

  # 2.2 Gerenciar Células:
  
  A tabela exibida na figura em questão possui quatro colunas, uma com o nome atribuído à célula, outra com seu endereço, uma indicado
  o status da célula e a última com três possíveis ações. Por fim, na parte inferior, há um botão
  para adicionar uma nova célula.
    
  A Primeira opção detalha o cadastro da célula. Na Figura são exibidas duas informação além do nome e do endereço já presentes na tabela de listagem: a
  latitude e a longitude. Esses dois campos identificam a localização da célula de forma precisa,
  enquanto o endereço informa onde a célula está de forma amigável aos humanos.
  
  A próxima opção na Figura é a de deletar uma célula. Aqui, é importante salientar
  que deletar significa apenas conferir o status de inativo a célula, de modo que ela não possa mais
  enviar medições. Isso acontece porque, se fosse realmente deletar a célula da base de dados,
  precisaria apagar todos os monitoramentos feitos por ela, algo que não é desejável para esse contexto.
  ![telacelulas](https://github.com/user-attachments/assets/76dcdb55-b31a-4a3d-96c0-16b6168595da)

  # 2.3 Visão Geral:

  A seção de Visão Geral possui duas divisões mostradas na mesma tela: Valores Médios e
  Últimos Alertas. A seção de valores médios, conforme o nome sugere, mostra a média de todas
  as medições de todas as células. Os Últimos Alertas, por sua vez, mostram os cinco alertas mais
  recentes emitidos por qualquer uma das células.
    
  As Figuras mostram as informações que são exibidas na tela. Conforme é possível
  ver, há seis gráficos representando cada uma das seis grandezas: Temperatura (graus
  Celsius), Umidade (porcentagem), Radiação UV (UVi), concentração de fumaça e gases tóxicos
  (ppm) e incêndio (porcentagem de ocorrências em relação ao número de medições). Por fim,
  cada gráfico possui três barras, uma para a média dos valores diurnos, outra para os noturnos e a
  terceira engloba os dois turnos.
  ![valoresmedios](https://github.com/user-attachments/assets/5c8f41fe-7dab-44dc-a647-f181fc879415)

  Por fim, apresenta-se uma tabela com os cinco alertas mais recentes. Na primeira
  coluna, a célula é identificada pelo seu endereço, pois assim fica mais fácil saber onde foi emitido
  o alerta. A segunda coluna, portanto, informa uma descrição amigável sobre o alerta emitido.
  ![image](https://github.com/user-attachments/assets/00bbcfad-f547-4ba9-8810-d42a964e4b06)

  # 2.4 Protótipo de Teste:

  Os primeiros testes com o protótipo foram feitos em locais fechados e controlados, os
  quais contavam com a presença de outros sensores de referência. Os dois locais escolhidos foram
  a Prefeitura Municipal de Porto Nacional e a Universidade Federal do Tocantins (UFT).
  ![prototipoteste1](https://github.com/user-attachments/assets/94c57e7c-5504-47d3-87be-5bdd272d7493)

  Após essa etapa, a célula foi levada para testes em local aberto dentro da UFT. Por último,
  a performance do equipamento foi monitorada no pátio da prefeitura. Vale salientar ainda que
  foi testado a reação da célula ao desligar a conexão com a rede momentaneamente.
  ![prototipoteste2](https://github.com/user-attachments/assets/18394402-3c44-42bd-83b3-ee663b0359d8)
  ![debugg](https://github.com/user-attachments/assets/7e9c8900-4513-493e-aacf-c1478ec19baa)

# 3 Resultados:
  
  Conforme foi possível observar anteriormente, com a aplicação para administração os
  servidores públicos responsáveis pelo sistema poderão gerenciar as células e agendar monitoramentos avulsos. A aplicação para visitantes, por sua vez, permite que os cidadãos acompanhem
  as medidas conforme sua necessidade. Por fim, a API pública concede os dados brutos para
  casos de usos mais específicos.
  Em relação aos testes, a célula se comportou dentro do esperado nas situações, conseguindo enviar as leituras corretamente para o servidor e, no caso da conexão desligada intencionalmente, ela conseguiu se reconectar.

  # 3.1 Eficiência:
    
  Em termos de consumo de dados, o padrão REST possibilita que haja eficiência através
  de suas restrições. Uma vez que cada recurso recebe apenas dados em conformidade com as
  regras programadas, evita-se o desperdício com informações desnecessárias.
  O consumo de energia elétrica é algo a ser comentado também, pois o fato de haver um
  sensor operando em 5 V acarreta no uso de componentes adicionais que aumentam a energia
  necessária. Portanto, a partir desta premissa, é interessante buscar alternativas para que o sistema
  trabalhe em níveis regulares de tensão.
  Outro ponto a ser abordado aqui é o fato de o ESP 32 DevKit V1 ser um kit de desenvolvimento e, portanto, carrega consigo componentes que não são necessários em ambiente de
  produção. Apenas como exemplo, o conversor de interface serial para USB é desnecessário uma
  vez que o microcontrolador esteja programado. O ideal, nesse cenário, é embarcar apenas o
  módulo responsável pela comunicação sem fio e ter um circuito de programação separado.
  
  # 3.2 Escalabilidade:
  
  A capacidade de um sistema crescer é uma métrica importante. Do ponto de vista de
  software, uma arquitetura RESTful permite a separação de funções em serviços, facilitando
  a confecção de sistemas distribuídos. Em outras palavras, o modelo de contêineres facilita o
  crescimento de uma rede de sensores sem fio.
  Do ponto de vista do hardware, o tópico dos componentes desnecessários dificulta
  a escalabilidade em virtude do preço. Nesse caso, reitera-se o que foi dito anteriormente: é
  importante enxugar o sistema quando o mesmo for para um ambiente de produção.

  # 3.3 Resiliência:

  A resiliência de um sistema informa o quanto ele é tolerante a falhas. Do ponto de vista
  de software, a falha de um sensor não compromete o restante da rede por causa da comunicação
  single hop. Nesse sentido, como o servidor é um nó central, é necessário uma política de backup
  e continuidade de serviço para ele.
  No tocante ao hardware, faz-se necessário elaborar um invólucro protetor para mitigar
  os efeitos das intempéries climáticas. Outro ponto importante é assegurar a proteção elétrica das
  células oferecidas equipando as fontes de alimentação com circuitos protetores.

  # 3.4 Confiabilidade:

  A parte de software não faz análise de dados procurando por valores fora do padrão,
  logo, a confiabilidade dos dados lidos fica a mercê da própria célula. Dito isto, a célula realiza
  várias medições e envia para o servidor uma média dos valores. Essa medida consegue suavizar
  eventuais discrepâncias em virtude de ruídos ou perturbações. Contudo, o sistema ainda não é
  capaz de verificar se um sensor está com defeito.

  # 3.5 Segurança:

  O hardware está isento da responsabilidade com segurança, ficando essa responsabilidade
  a cargo do software. Como medidas iniciais, a API conta com um sistema de login, onde as
  credenciais estão gravadas no microcontrolador da célula. Além disso, o servidor conta com
  um firewall para filtrar as conexões e evitar ataques externos. Por fim, vale dizer que esse
  protótipo conta com um certificado de segurança válido, possibilitando, portanto, o envio de
  dados criptografados.

  # 3.6 Interação com o Usuário:
  
  Naturalmente, não é esperado que o usuário interaja com o hardware do sistema, logo,
  esse tópico também é de responsabilidade integral do software. Nesse sentido, o padrão REST
  também é vantajoso, pois oferece a possibilidade de sistemas distribuídos. Dito de outra forma,
  os serviços para enviar avisos ou interfaces de acesso ficam separados da API, consumindo-a
  da mesma forma que a célula faz. Essa separação permite construir aplicativos (para qualquer
  dispositivo ou online) sem precisar alterar a API.
