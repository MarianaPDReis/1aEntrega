## Faculdade de Design, Tecnologia e Comunicação
**Universidade Europeia**

**Elementos do grupo:** Mariana Pinheiro dos Reis | Número | Email

**Nome do projeto:** CultivaInteligente??

**Unidades Curriculares incluidas:** Engenharia de software

**Palavras-chave:** Agricultura, ...

**Link para reportorio do GitHub:** (https://github.com/MarianaPDReis/Documenta-o-1aEntrega)

## Introdução 
O presente documento tem como objetivo apresentar a especificação dos requisitos funcionais e não funcionais de um sistema de monitorização e controlo de estufas agrícolas inteligentes. 

Na agricultura, em ambientes de estufa, é necessário controlar com rigor a temperatura, a humidade do ar e a humidade do solo, para garantir a qualidade e produtividade das plantas. A ausência de informação detalhada e em tempo real desse controlo dificulta a prevenção de perdas nas colheitas e a otimização dos recursos hídricos. 

Atualmente, principalmente produtores agrícolas de pequena e média dimensão fazem esse controlo de forma manual. Embora já existam no mercado algumas soluções industriais de automação agrícola, estas tendem a ser demasiado complexas e dispendiosas para este tipo de produtores. Este método tradicional apresenta limitações significativas: 

* Deteção tardia de anomalias: Picos de calor ou falta de humidade no solo podem danificar irreversivelmente as colheitas antes de serem identificados. 

* Desperdício de recursos: A rega efetuada sem base em dados precisos conduz frequentemente ao uso excessivo de água e energia. 

* Ausência de histórico: A falta de registos estruturados impede a análise de padrões climáticos internos e a otimização da produção ao longo do tempo. 

Para resolver isto, propõe-se criar um sistema baseado em IoT que faça a monitorização e controlo remoto de estufas agrícolas, disponibilizando informação organizada, ferramentas de análise e alertas, que permite aos produtores acompanhar as condições dos seus cultivos em tempo real. 

Neste documento, são descritos o funcionamento geral da aplicação, os guiões de utilização e a respetiva especificação de requisitos funcionais e não funcionais. 

 ## Descrição da aplicação 

O CultivaInteligente é uma solução tecnológica que combina dispositivos físicos instalados na estufa com uma plataforma web de gestão acessível a partir de qualquer lugar. 

O funcionamento da aplicação baseia-se numa comunicação contínua entre os componentes físicos instalados na estufa e a plataforma digital de gestão. Todo o processo começa nos sensores de temperatura, humidade do ar e humidade do solo, que funcionam como os "olhos" do sistema, medindo constantemente o estado do ambiente e da terra. 

Estes sensores estão ligados a um microcontrolador ESP32, uma pequena placa eletrónica com Wi-Fi integrado que atua como o cérebro local na estufa. O ESP32 lê os valores recolhidos pelos sensores e envia-os pela internet, através do protocolo REST, até um servidor na nuvem. Nesse servidor, os dados são recebidos e organizados numa base de dados relacional, como MySQL, garantindo que toda a informação fica guardada de forma segura e estruturada para consulta de históricos. 

Por fim, o produtor acede a uma interface web, via computador ou telemóvel, onde consegue visualizar todos estes dados em tempo real através de gráficos e indicadores simples. Sempre que algum valor sai dos limites definidos, o sistema emite alertas automáticos e permite atuar diretamente sobre a estufa, seja de forma remota, através de botões na aplicação, ou automatizada, acionando equipamentos como eletroválvulas de rega ou ventoinhas para repor as condições ideais das plantas. 

**Público-Alvo e Utilizadores** 

Agricultor / Produtor Agrícola (Utilizador Principal): Responsável pela gestão diária da estufa. Utiliza a aplicação para consultar os parâmetros ambientais em tempo real, configurar limites ideais para cada tipo de cultura, receber alertas críticos e controlar os sistemas de rega ou ventilação à distância. 

Administrador de Sistema: Responsável pela gestão de contas de utilizadores, associação inicial dos dispositivos IoT e manutenção técnica da plataforma.
