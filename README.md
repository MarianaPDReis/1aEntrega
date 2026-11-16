## Faculdade de Design, Tecnologia e Comunicação
**Universidade Europeia**

**Elementos do grupo:** Mariana Pinheiro dos Reis | Número | Email

**Nome do projeto:** Recolha e Tratamento de dados de sensores IoT | **CultivaInteligente** 

**Unidades Curriculares incluídas:** Engenharia de software

**Palavras-chave:** Estufa Inteligente, Monitorização Agrícola, Automação de Cultivos

**Link para reportório do GitHub:** (https://github.com/MarianaPDReis/Documenta-o-1aEntrega)

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

## Guiões de Utilização (User Scenarios / Guiões de Teste) 

Para ilustrar o comportamento esperado do sistema e o fluxo de interação dos utilizadores, apresentam-se dois guiões principais de utilização: 

**Guião 1: Monitorização e Resposta a Alerta de Solo Seco** 

1. O agricultor acede à aplicação web **CultivaInteligente** através do seu smartphone e inicia sessão com as suas credenciais (**RF01**).
2. No painel principal (*dashboard*), verifica que a "Estufa 1 (Tomates)" apresenta uma temperatura de 26 ºC e humidade do solo de 45% (**RF05**).
3. Durante a tarde, o sensor de humidade do solo envia uma leitura de 24% para o servidor (**RF03**), valor inferior ao limite mínimo configurado de 30% (**RF07**).
4. O sistema deteta a anomalia, regista o evento na base de dados e envia imediatamente uma notificação na aplicação e um alerta por e-mail ao agricultor (**RF08**).
5. O agricultor abre o alerta, consulta o gráfico das últimas 24 horas para confirmar a descida acentuada da humidade (**RF06**) e seleciona a opção "Ativar Rega" na interface web (**RF09**).
6. O sistema envia o comando ao microcontrolador da estufa, que liga a eletroválvula de rega e atualiza o estado no painel para "Rega Ativa".

**Guião 2: Configuração de Automação e Exportação de Dados** 

1. O agricultor acede às definições da "Estufa 2 (Morangos)" na plataforma web.
2. Ajusta o limiar de temperatura máxima para 28 ºC e ativa a funcionalidade "Modo Automático de Rega" (**RF07**, **RF10**).
3. No final do mês, o agricultor acede à secção de "Relatórios", seleciona o intervalo correspondente aos últimos 30 dias e clica em "Exportar CSV" (**RF11**).
4. O sistema gera e descarrega um ficheiro estruturado com as médias diárias de temperatura e humidade para arquivo e análise da produção.

## 4. Requisitos Funcionais

Os Requisitos Funcionais descrevem as funcionalidades, comportamentos e regras de negócio que o sistema deve disponibilizar aos utilizadores e componentes externos.

| ID | Nome do Requisito | Descrição Detalhada | Prioridade |
| :--- | :--- | :--- | :--- |
| **RF01** | **Autenticação de Utilizadores** | O sistema deve permitir que os utilizadores registados iniciem sessão na plataforma web através de endereço de e-mail e palavra-passe. | Alta |
| **RF02** | **Registo de Dispositivos IoT** | O utilizador deve poder associar um novo nó sensor/atuador (ESP32) à sua conta e atribuir-lhe a identificação de uma estufa específica. | Alta |
| **RF03** | **Recolha Periódica de Dados** | O sistema (via API REST) deve receber e processar as leituras de temperatura, humidade do ar e humidade do solo enviadas pelos sensores a cada 5 minutos. | Alta |
| **RF04** | **Persistência de Dados** | O sistema deve armazenar todas as leituras recebidas na base de dados relacional, associando cada registo à data, hora e identificador do sensor. | Alta |
| **RF05** | **Dashboard em Tempo Real** | O utilizador deve visualizar um painel principal com os valores mais recentes de temperatura, humidade do ar e humidade do solo de cada estufa, bem como o estado atual dos atuadores (ligado/desligado). | Alta |
| **RF06** | **Consulta de Histórico** | O utilizador deve poder consultar o histórico de medições através de gráficos temporais, filtrando os dados por dia, semana ou mês. | Média |
| **RF07** | **Configuração de Limiares** | O utilizador deve poder definir valores mínimos e máximos aceitáveis (ex: humidade mínima do solo de 30%, temperatura máxima de $32\,^\circ\text{C}$) para cada estufa. | Alta |
| **RF08** | **Sistema de Alertas Automáticos** | Sempre que uma leitura ultrapassar os limiares definidos no RF07, o sistema deve gerar uma notificação na plataforma web e enviar um alerta por e-mail ao utilizador. | Alta |
| **RF09** | **Atuação Manual Remota** | O utilizador deve poder ligar ou desligar manualmente o sistema de rega e o sistema de ventilação através de controlos na interface web. | Média |
| **RF10** | **Automação de Rega** | Quando ativado o modo automático pelo utilizador, o sistema deve acionar a rega automaticamente caso a humidade do solo desça abaixo do limite mínimo, desligando-a assim que o valor ideal seja restabelecido. | Média |
| **RF11** | **Exportação de Relatórios** | O utilizador deve poder exportar os dados históricos de um determinado período em formato CSV ou PDF para análise externa. | Baixa |

## 5. Requisitos Não Funcionais

Os Requisitos Não Funcionais definem os critérios de qualidade, desempenho, segurança e restrições técnicas que o software deve cumprir.

| ID | Categoria | Descrição Detalhada | Critério de Aceitação / Métrica |
| :--- | :--- | :--- | :--- |
| **RNF01** | **Desempenho** | O carregamento do painel principal e a atualização dos gráficos históricos devem ser rápidos para garantir uma boa experiência de utilização. | Tempo de resposta inferior a $2\text{ segundos}$ para $95\%$ dos pedidos. |
| **RNF02** | **Segurança (Comunicação)** | Toda a comunicação entre os dispositivos IoT, o servidor backend e o navegador do utilizador deve ser cifrada. | Utilização obrigatória do protocolo HTTPS (TLS 1.2 ou superior). |
| **RNF03** | **Segurança (Dados)** | As palavras-passe dos utilizadores não podem ser armazenadas em texto limpo na base de dados. | Utilização de algoritmos de *hashing* seguros (ex: bcrypt ou Argon2). |
| **RNF04** | **Segurança (API)** | Apenas dispositivos autorizados podem submeter dados de sensores para a API REST. | Autenticação via *API Key* ou *Token JWT* em cada pedido `POST`. |
| **RNF05** | **Disponibilidade** | O servidor de recolha de dados e a base de dados devem operar de forma contínua para evitar a perda de leituras ambientais. | Disponibilidade mínima de $99{,}5\%$ ao longo do mês. |
| **RNF06** | **Usabilidade e Responsividade** | A interface web deve adaptar-se a diferentes tamanhos de ecrã, permitindo a gestão tanto em computador como em smartphone no terreno. | Compatibilidade total com resoluções desde $360\text{px}$ (mobile) até $1920\text{px}$ (desktop). |
| **RNF07** | **Tolerância a Falhas** | Caso a ligação Wi-Fi da estufa falhe temporariamente, o sistema não deve perder a consistência dos dados quando a ligação for reposta. | O servidor deve aceitar pacotes com *timestamp* retroativo enviados em lote após reconexão. |
| **RNF08** | **Manutenibilidade** | O código-fonte do backend e frontend deve seguir boas práticas de arquitetura modular e estar devidamente documentado. | Documentação da API via Swagger/OpenAPI e repositório versionado em Git. |
