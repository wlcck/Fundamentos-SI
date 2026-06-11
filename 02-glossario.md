## Conceitos Rápidos ##
Governança (COBIT/ITIL): COBIT define o que controlar (alinhamento e riscos); ITIL define como gerenciar (processos e serviços de TI).
Princípios LGPD: Finalidade (usar dados só para o que foi avisado), Necessidade (coletar o mínimo possível) e Segurança (proteger o software).
Privacy by Design: Embutir privacidade desde o início do código, por padrão (default), e não como um ajuste final.
Dados Sensíveis: Dados de saúde, biometria, religião ou raça. Exigem proteção jurídica e técnica máxima.

## Resolução do Desafio: Caso MedAgenda ##
1. O que deu errado?
Dados Expostos: Nomes e CPFs (dados pessoais) vinculados a Diagnósticos (dados sensíveis de saúde).
Princípios Violados: Falha grave de Segurança (vazamento físico), falta de Prevenção e desvio de Finalidade (usar produção em testes).
2. Como a Tecnologia evitaria isso?
Ambientes Isolados (Docker): Desenvolvedores rodam bancos locais via Docker usando apenas dados falsos (mocks) ou sintéticos. Produção fica isolada.
Anonimização / Mascaramento: Se precisar de dados reais, rodar um script antes para apagar nomes/CPFs e embaralhar os diagnósticos, tornando impossível identificar os pacientes.
3. Como a Governança deve agir na Nuvem (AWS)?
Princípio do Menor Privilégio: Bloquear o acesso de desenvolvedores ao banco de produção (via AWS IAM). Programador não faz dump de produção.

Segurança de Endpoints: Proibir dados em notebooks pessoais e exigir criptografia de disco rígido (se o PC for roubado, os dados continuam ilegíveis).

## 1. Máquina Virtual (Virtual Machine - VM)
## O que é?
Uma Máquina Virtual é como um computador completo correndo dentro do seu próprio computador. Ela simula um hardware real (processador, memória, disco rígido) através de um software chamado Hypervisor. Isso permite que você instale um sistema operacional inteiro (como o Linux) dentro de outro (como o Windows).
## Para que serve?
Testar sistemas operacionais: Experimentar o Linux ou o Windows 11 sem precisar formatar seu computador real.
## Segurança e Isolamento:
Rodar arquivos suspeitos ou navegar em sites perigosos. Se a VM pegar um vírus, seu computador real continua 100% seguro.
## Rodar programas antigos:
Usar um software antigo que só funciona no Windows XP ou Windows 7.
Servidores em Nuvem: Empresas (como Google Cloud ou AWS) usam VMs para dividir um servidor físico gigante em centenas de computidores virtuais menores para os clientes.

## Exemplos:
**VirtualBox (da Oracle):** Gratuito, de código aberto e excelente para usuários comuns e estudantes.
**VMware Workstation / Player:** Uma das ferramentas mais potentes e profissionais do mercado, muito usada em empresas.
**Hyper-V:** O sistema de criação de VMs nativo do próprio Windows (disponível nas versões Pro e Enterprise).

## 2. Ambiente Virtual (Virtual Environment)
## O que é?
Um Ambiente Virtual é um espaço isolado dentro do seu sistema operacional dedicado a um projeto específico (geralmente de programação). Em vez de simular um computador inteiro, ele apenas isola pastas, bibliotecas e versões de linguagens de programação (como Python ou Node.js).
## Para que serve?
Evitar conflitos de versões: Imagine que o Projeto A precisa da versão 1.0 de uma biblioteca e o Projeto B precisa da versão 2.0. O ambiente virtual permite que ambos coexistam no mesmo computador sem que um quebre o outro.
## Organização:
Mantém o seu computador "limpo", instalando as ferramentas de desenvolvimento apenas dentro da pasta daquele projeto específico.
## Facilidade de compartilhamento: 
Permite que outros programadores rodem o seu código exatamente com as mesmas configurações que você usou.

## Exemplos (focados em programação):
**venv ou virtualenv (Python):** Cria pastas isoladas para que você instale pacotes Python específicos para cada projeto.
**Conda (Python/Data Science):** Muito usado por cientistas de dados para gerenciar pacotes e ambientes complexos.
**Contêineres (Docker):** Embora seja um conceito um pouco mais avançado, o Docker funciona como um "ambiente virtual supremo", empacotando o aplicativo e tudo o que ele precisa para rodar em qualquer lugar.

## Tutorial de como criar um docker 
Criar um "Docker" geralmente significa duas coisas: criar uma **Imagem Docker** (o modelo do seu aplicativo) e rodar um **Contêiner Docker** (a instância viva dessa imagem executando no seu computador).
Para este tutorial, vamos criar um projeto simples: uma página web básica rodando dentro do Docker.

## Pré-requisitos
Antes de começar, você precisa ter o **Docker Desktop** instalado no seu computador. Você pode baixá-lo no site oficial do Docker e seguir o instalador padrão.

## Passo a Passo: Criando seu primeiro Contêiner
**Passo 1: Criar a pasta do projeto**
Crie uma pasta vazia no seu computador com o nome que desejar (ex: meu-projeto-docker).

**Passo 2: Criar o arquivo do seu aplicativo**
Dentro dessa pasta, crie um arquivo simples que queremos que o Docker execute. Vamos criar uma página web básica.

- Crie um arquivo chamado index.html.
- Cole o seguinte código dentro dele:
<img width="645" height="291" alt="{674244CC-826F-4D12-8D2D-ED465AEA0255}" src="https://github.com/user-attachments/assets/54514871-b39b-4226-b7f6-4bc2abc84071" />

## Passo 3: Criar o Dockerfile
O Dockerfile é a "receita do bolo". É um arquivo de texto sem extensão que diz ao Docker como construir a sua imagem.
- Dentro da mesma pasta, crie um arquivo de texto e mude o nome dele para exatamente: Dockerfile (sem .txt no final).
- Abra o arquivo e cole as seguintes instruções:
<img width="670" height="246" alt="{D0FBD545-5D15-4290-87CE-1E959CEA2B0B}" src="https://github.com/user-attachments/assets/40c62f12-170f-4d95-80f9-33925f6d40b6" />

## Passo 4: Construir e Rodar no Terminal
Agora, abra o terminal do seu computador (Prompt de Comando, PowerShell ou Terminal do Linux/Mac) e navegue até a pasta do seu projeto usando o comando cd (ex: cd caminho/da/pasta/meu-projeto-docker).
Siga o fluxo abaixo no terminal:

## 1. Construir a Imagem (Build)
Execute o comando abaixo para compilar a sua receita (Dockerfile) e transformá-la em uma imagem. Não esqueça do ponto . no final!
<img width="559" height="91" alt="{4BF01207-753E-4D46-9463-BA90EED95C89}" src="https://github.com/user-attachments/assets/1debdc27-1641-4d23-a369-080b2225b5f8" />
(O -t meu-primeiro-site dá um nome amigável para a sua imagem).

## 2. Rodar o Contêiner (Run)
Agora que a imagem está pronta, vamos transformá-la em um contêiner ativo:
<img width="638" height="85" alt="{6978BD78-A960-4736-9F06-6373CAF7684A}" src="https://github.com/user-attachments/assets/d0d9c443-eb1a-4b0c-bc88-036234d568a2" />

## O que significam esses parâmetros?
- -d: Roda o contêiner em segundo plano (libera o seu terminal).
- -p 8080:80: Redireciona a porta 8080 do seu computador real para a porta 80 interna do Docker.
- --name: Dá um nome para o seu contêiner.

## Passo 5: Testar o resultado 
Abra o seu navegador de internet e digite o seguinte endereço:
http://localhost:8080
Você verá a sua página HTML rodando direto de dentro do contêiner Docker!

## Comandos Úteis para o Dia a Dia
Se quiser gerenciar o seu novo contêiner pelo terminal, aqui estão os comandos principais:
Ver contêineres ativos: docker ps
Parar o contêiner: docker stop meu-container-vivo
Iniciar novamente: docker start meu-container-vivo
Excluir o contêiner: docker rm -f meu-container-vivo





## O qué CRM ##
CRM é a sigla para **Customer Relationship Management**, que em português significa **Gestão de Relacionamento com o Cliente.**

Embora muita gente pense que é apenas um software, o CRM é, na verdade, uma combinação de **estratégia, processo e tecnologia** focada em entender e antecipar as necessidades dos clientes atuais e potenciais de uma empresa.

## Os Três Pilares do CRM
Para entender como ele funciona na prática, podemos dividi-lo em três frentes:

**Estratégia:** É a mentalidade de colocar o cliente no centro do negócio (customer centric). Em vez de focar apenas no produto, a empresa foca em criar uma jornada de compra personalizada e positiva.
**Processo:** Define como as equipes de vendas, marketing e atendimento devem interagir com o cliente em cada etapa da jornada.
**Tecnologia (O Software):** É a ferramenta que centraliza todos os dados. Imagine uma agenda super inteligente que guarda desde o e-mail do cliente até o histórico de compras, reclamações e a última vez que ele visitou seu site.

### O que um software de CRM faz por você?
<img width="725" height="407" alt="{A919581A-164C-4C12-8731-B44A28486E04}" src="https://github.com/user-attachments/assets/29ee1e5b-a0a5-4fdd-8c59-e4750d688dcd" />

### Por que ele é importante?
Sem um CRM, é muito fácil "deixar dinheiro na mesa". Se um vendedor esquece de retornar uma ligação ou se o marketing envia uma promoção de algo que o cliente acabou de comprar, a experiência é prejudicada.
## Em resumo: ## 
O CRM serve para que a empresa pareça uma pessoa só conversando com o cliente, independentemente de quem está atendendo ou de qual canal está sendo usado.


## Técnica vs. Metodologia ##
**Metodologia (O "Caminho"):** É a estratégia macro, o estudo dos métodos. É o plano de ação que define como você vai abordar um problema de forma científica ou profissional.
Exemplo: Em um projeto de software, a Metodologia Ágil (Scrum) é a escolha estratégica de como a equipe se organiza e se comunica.

**Técnica (A "Ferramenta"):** É a aplicação prática, o procedimento específico e operacional para realizar uma tarefa dentro da metodologia.
Exemplo: Dentro do Scrum, usar a Técnica de Estimativa Planning Poker ou o Daily Stand-up são os procedimentos técnicos para executar a metodologia.

## Integração Trello + GitHub: Passo a Passo ##
**Para conectar suas tarefas do Trello com o código no GitHub, siga estes passos:**
**Ativar o Power-Up:**
* No seu quadro do Trello, clique em Power-Ups (no menu superior ou lateral).
* Busque por GitHub e clique em Adicionar.

**Autorizar a Conta:**
* Abra um cartão qualquer no Trello.
* No menu lateral do cartão, clique no botão GitHub que apareceu.
* Clique em Autorizar conta do GitHub e faça login para dar permissão ao Trello.

**Vincular Repositórios:**
* No mesmo botão GitHub do cartão, escolha Vincular Repositório.
* Selecione o repositório do projeto que você quer monitorar.

**Uso Prático:**
* Agora, dentro de cada cartão, você pode clicar em GitHub para anexar um Commit, uma Issue ou um Pull Request específico.
* O cartão mostrará automaticamente se o código foi aprovado ou se há conflitos, sem você precisar sair do Trello.


## IoT e Modelo TCP/IP (16/04/2026) ##

## 🌐 O Modelo TCP/IP na IoT ##
**Camada de Aplicação:** É onde a "mágica" acontece para o usuário. Dispositivos usam protocolos leves como **MQTT** (focado em baixo consumo de bateria) ou **CoAP** para enviar mensagens como "luz acesa" ou "temperatura: 22°C".

**Camada de Transporte:** Define como o dado viaja.

* **TCP:** Garante que o dado chegue inteiro (ex: atualização de software).

* **UDP:** Foca na velocidade (ex: sensores que enviam dados constantes onde perder um pacote não é crítico).

**Camada de Internet:** Responsável pelo endereçamento. Cada dispositivo IoT precisa de um **IP** para ser encontrado na rede global ou local.

**Camada de Acesso à Rede:** É a parte física e o sinal. Envolve o hardware e tecnologias como **Wi-Fi, Bluetooth, Zigbee ou Ethernet.**

## Situações Fictícias: O Problema vs. A Solução ##
Abaixo, três cenários práticos baseados nas camadas do modelo TCP/IP:

**Cenário 1: O Termostato Espião (Camada de Aplicação/Internet)**
* A Situação: Uma empresa instala termostatos inteligentes que usam o protocolo **HTTP** comum e possuem endereços **IP públicos** diretos. Um hacker descobre o IP, intercepta o tráfego (sem criptografia) e descobre a rotina dos funcionários pela temperatura das salas.
* A Mitigação: A empresa atualiza o sistema para usar **HTTPS/MQTTS (Criptografia)** e coloca os dispositivos atrás de uma **VPN**. Agora, o tráfego é ilegível para externos e o IP do dispositivo não é mais visível na internet aberta.

**Cenário 2: A Câmera "Zumbi" (Ataque DDoS)**
* A Situação: Uma creche compra câmeras baratas com a senha padrão "123456". Um software malicioso (tipo a botnet Mirai) faz uma varredura na rede, "sequestra" 50 câmeras da creche e as usa para atacar o site de um banco, tirando-o do ar.
* A Mitigação: O administrador da creche força a alteração de senhas para **combinações complexas** e instala um Firewall de borda que bloqueia o envio massivo de pacotes de dados anômalos partindo das câmeras.

**Cenário 3: O Sensor de Umidade "Mentiroso" (Camada de Transporte)**
* A Situação: Uma fazenda usa sensores que enviam dados via **UDP** (rápido, mas sem confirmação). Devido a uma interferência na rede Wi-Fi, os pacotes chegam corrompidos ou não chegam. O sistema entende que o solo está seco e gasta milhares de litros de água sem necessidade.
* A Mitigação: O produtor altera a configuração para **TCP** em alertas críticos. O TCP garante que, se o pacote de dado "Solo Úmido" não chegar, ele seja reenviado até que o sistema de irrigação confirme o recebimento (Confiabilidade).


## Como Mitigar o Máximo de Riscos (Resumo Estratégico) ##
1**Criptografia de Ponta a Ponta:**
Nunca envie dados em "texto puro". Use TLS/SSL (como o HTTPS ou MQTTS). Se o dado for interceptado, ele será ilegível.

**Higiene de Credenciais:**
Banir senhas padrão (admin/admin). Implementar a troca obrigatória no primeiro acesso e usar autenticação de dois fatores (2FA) ou certificados digitais para os dispositivos.

**Segmentação de Rede (VLANs):**
Colocar os dispositivos IoT em uma rede separada da rede principal (onde estão computadores com dados bancários, por exemplo). Se a lâmpada for hackeada, o hacker não chega ao seu PC.

**Atualização de Firmware (Patching):**
Escolher dispositivos de fabricantes que ofereçam atualizações automáticas. Um dispositivo sem atualização é uma bomba-relógio.

**Minimização de Portas:**
Fechar todas as portas de comunicação que o dispositivo não utiliza. Se ele só envia dados, não precisa "ouvir" conexões externas (bloqueio por Firewall).

<img width="724" height="355" alt="{B856A97C-4228-489F-B50A-A2153F442E08}" src="https://github.com/user-attachments/assets/e8d8a427-2e53-4aa4-8389-5ce0a879e3f4" />




## Computação em nuvem e IoT (09/04/2026) ##

**🌐 Computação em Nuvem e IoT**

A Internet das Coisas (IoT) refere-se à conexão de objetos físicos à internet, permitindo que eles coletem, processem e troquem dados automaticamente. Esses dispositivos incluem:

Sensores (temperatura, movimento, pressão)
Câmeras e sistemas de segurança
Veículos conectados
Eletrodomésticos inteligentes (geladeiras, lâmpadas, etc.)

Já a computação em nuvem é um modelo que permite acessar recursos computacionais (armazenamento, servidores, banco de dados e software) pela internet, sob demanda, sem necessidade de infraestrutura local.

Grandes provedores incluem:

* Amazon Web Services (AWS)
* Microsoft Azure
* Google Cloud Platform




**🔗 Relação entre IoT e Nuvem**

A IoT depende fortemente da nuvem para funcionar de forma eficiente. Essa integração permite:

**📊 Processamento de grandes volumes de dados**

Dispositivos IoT geram **dados em tempo real**, e a nuvem fornece capacidade para armazenar e processar tudo isso.

⚡ Escalabilidade

É possível aumentar ou reduzir recursos rapidamente conforme a quantidade de dispositivos conectados cresce.

**🤖 Inteligência Artificial e Machine Learning**

A nuvem permite aplicar algoritmos avançados para:

* Prever falhas
* Automatizar decisões
* Identificar padrões
🔒 Segurança e gerenciamento

Plataformas em nuvem oferecem:

* Criptografia de dados
* Monitoramento contínuo
* Atualizações automáticas

**👉 Insight importante:**
Sem a nuvem, a IoT seria limitada, pois dispositivos físicos geralmente não possuem poder computacional suficiente para análises complexas.



## 🧠 Sistemas Pervasivos vs. Sistemas Ubíquos ##

Ambos fazem parte do conceito de computação integrada ao ambiente, mas têm diferenças importantes.

**📡 Sistemas Pervasivos**
* São **visíveis e focados em tarefas específicas**
* Estão presentes em ambientes definidos (casa, empresa)
* Funcionam muitas vezes em segundo plano
**Características:**
* Automação
* Integração entre dispositivos
* Eficiência operacional
**Exemplos:**
* 🏠 Automação residencial (luzes, portas, segurança)
* 🏥 Monitoramento de saúde com sensores
* 🏭 Monitoramento industrial (temperatura, vibração)

**🌍 Sistemas Ubíquos**
* São **invisíveis ou quase imperceptíveis**
* Altamente integrados ao cotidiano
* Adaptam-se ao usuário em tempo real
**Características:**
* Personalização extrema
* Interação natural (voz, contexto)
* Integração com o ambiente físico
**Exemplos:**
* 🎙️ Assistentes de voz (como Alexa, Google Assistente)
* 🪞 Espelhos inteligentes
* 💺 Cadeiras inteligentes com sensores

**👉 Insight importante:**
Enquanto sistemas pervasivos **automatizam tarefas**, sistemas ubíquos **transformam a experiência do usuário**, tornando a tecnologia “invisível”.

**⚙️ Como Construir Sistemas Ubíquos**

Para desenvolver sistemas realmente eficientes, é necessário considerar:

**🔧 1. Integração de Tecnologias**
**Combinar:**
* Sensores
* Redes
* Software
* Inteligência artificial

Tudo deve funcionar de forma harmoniosa.

**👤 2. Design Centrado no Usuário**
* Interface intuitiva
* Experiência fluida
* Adaptação ao comportamento do usuário

👉 A tecnologia deve se adaptar à pessoa, não o contrário.

**📈 3. Escalabilidade**
* Suportar milhares ou milhões de dispositivos
* Crescimento sem perda de desempenho

**🔐 4. Segurança**
* Proteção de dados pessoais
* Prevenção contra ataques
* Controle de acesso

**👉 Ponto crítico:** Sistemas IoT são alvos frequentes de ataques.

**🌐 5. Conectividade**
* Comunicação eficiente entre dispositivos
* Uso de protocolos como Wi-Fi, Bluetooth, 5G

**🗃️ 6. Gerenciamento de Dados** 
* Coleta eficiente
* Armazenamento escalável
* Processamento inteligente

**🚀 Aplicações Reais e Impacto**
A combinação de IoT + Nuvem + Sistemas Ubíquos já está transformando diversos setores:

* **🏙️ Cidades inteligentes (Smart Cities)**
* 🚗 Veículos autônomos
* 🏥 Saúde digital e telemedicina
* 🌾 Agricultura de precisão
* 🏭 Indústria 4.0

**💡 Conclusão**
A integração entre **IoT, computação em nuvem e sistemas ubíquos** está moldando o futuro da tecnologia:

* **A IoT conecta o mundo físico**
* **A nuvem fornece inteligência e escala**
* **Os sistemas ubíquos tornam tudo invisível e natural**

👉 O resultado é um mundo cada vez mais automatizado, inteligente e conectado.



## Trabalho fundamentos SI **(19/03)**

Os Sistemas de Informação (SI) são conjuntos organizados de pessoas, processos e tecnologias que coletam, processam e distribuem informações para apoiar decisões e atividades dentro de uma organização ou no dia a dia das pessoas. Existem diferentes tipos de sistemas de informação, cada um com uma finalidade específica.

Um dos principais tipos é o **Sistema de Processamento de Transações (SPT)**. Ele é responsável por registrar operações rotineiras, como vendas, pagamentos e cadastros. Um exemplo simples é o sistema de um supermercado, que registra cada compra realizada no caixa.

Outro tipo é o **Sistema de Informação Gerencial (SIG)**. Esse sistema organiza dados e gera relatórios para ajudar gestores a tomar decisões. Por exemplo, uma empresa pode usar um SIG para analisar suas vendas mensais e identificar quais produtos têm maior saída.

Também existe o **Sistema de Apoio à Decisão (SAD)**, que auxilia na resolução de problemas mais complexos. Ele utiliza dados e modelos para simular cenários. Um exemplo seria um sistema que ajuda uma empresa a decidir se deve investir em um novo produto.

O **Sistema de Informação Executiva (SIE)** é voltado para altos gestores. Ele apresenta informações estratégicas de forma resumida e clara, facilitando decisões importantes. Um exemplo é um painel com indicadores de desempenho da empresa.

Outro tipo importante é o **Sistema de Automação de Escritório (SAE)**, que ajuda nas tarefas do dia a dia, como edição de documentos, envio de e-mails e organização de agendas. Um exemplo é o uso de aplicativos de edição de texto e planilhas.

Além desses, existem os **Sistemas de Informação Integrados (ERP)**, que conectam diferentes setores de uma empresa em um único sistema, permitindo que todos compartilhem informações em tempo real. Um exemplo é um sistema que integra estoque, financeiro e vendas.

Agora, analisando alguns sistemas conhecidos:

* **gov.br**: é um sistema voltado ao cidadão que integra diversos serviços públicos. Pode ser considerado um **Sistema de Informação Gerencial e de Serviços**, pois organiza informações e oferece serviços digitais do governo.

* **Netflix**: é um sistema que fornece conteúdo sob demanda e utiliza dados dos usuários para recomendar filmes e séries. Pode ser classificado como **Sistema de Apoio à Decisão e Sistema de Informação para o Consumidor**.

* **Minha agenda UFN**: é um sistema utilizado por estudantes para organização de horários e compromissos. Ele se encaixa como **Sistema de Automação de Escritório**.

* **Sistema de Imposto de Renda do Governo Brasileiro**: é um sistema que coleta, processa e armazena dados financeiros dos cidadãos. Pode ser classificado como **Sistema de Processamento de Transações**.

* **Spotify**: é um sistema de streaming de música que também utiliza dados para recomendar conteúdos. Pode ser considerado um **Sistema de Apoio à Decisão e Sistema de Informação para o Consumidor**.

Em resumo, os Sistemas de Informação estão presentes em praticamente todas as áreas da sociedade e são essenciais para organizar dados, melhorar processos e apoiar decisões.



## Assunto: Trabalho fundamentos SI (Complemento final)

Além do CRM, existem outros tipos de Sistemas de Informação que também são muito utilizados e podem complementar o trabalho.

Um deles é o **ERP (Enterprise Resource Planning)**, ou Sistema de Gestão Empresarial. Ele integra diferentes áreas de uma empresa, como financeiro, estoque, vendas e recursos humanos, permitindo que todas compartilhem informações em um único sistema. Um exemplo é quando uma venda registrada já atualiza automaticamente o estoque e o caixa da empresa.

Outro tipo é o **SCM (Supply Chain Management)**, que gerencia a cadeia de suprimentos. Ele controla desde a compra de matéria-prima até a entrega do produto final ao cliente. Um exemplo é uma indústria que acompanha todo o processo de produção e distribuição por meio desse sistema.

Também podemos citar o **KMS (Knowledge Management System)**, ou Sistema de Gestão do Conhecimento. Ele serve para armazenar e compartilhar conhecimento dentro de uma organização, como manuais, treinamentos e boas práticas. Um exemplo é uma empresa que mantém uma base de dados com soluções para problemas comuns enfrentados pelos funcionários.

Além disso, existem os **Sistemas de Informação para Comércio Eletrônico**, que permitem compras e vendas pela internet. Esses sistemas cuidam de pedidos, pagamentos e entregas. Um exemplo são lojas online que processam pedidos automaticamente.

Outro ponto interessante é que muitos sistemas atuais utilizam **Inteligência Artificial (IA)** para melhorar seu desempenho. Isso permite, por exemplo, recomendar produtos, prever comportamentos e automatizar atendimentos, como acontece em aplicativos de música e filmes.

Por fim, é importante destacar que os Sistemas de Informação estão cada vez mais presentes no cotidiano, tanto em empresas quanto na vida pessoal, facilitando tarefas, organizando dados e ajudando na tomada de decisões de forma mais rápida e eficiente.



## Tarefa 1 - Aula 3
  ## Realizar uma pesquisa (em IA generativa ou livros da área) sobre os conceitos ligados aos modelos de arquitetura de software:
    
## DaaS(Data as a Service)
- Descrição:
DaaS significa Dados como Serviço. Nesse modelo, os dados são armazenados e disponibilizados na nuvem para que usuários ou aplicações possam acessá-los pela internet, geralmente através de APIs ou plataformas online.
- Para que serve:
Permite que empresas acessem e compartilhem dados sem precisar armazená-los localmente ou gerenciar toda a infraestrutura de dados.
- Exemplo de mercado:
Snowflake — plataforma que permite compartilhar e acessar grandes volumes de dados na nuvem.


  
## DBaaS (Database as a Service)
- Descrição:
DBaaS significa Banco de Dados como Serviço. O provedor de nuvem oferece um banco de dados gerenciado, cuidando de instalação, manutenção, backups e atualizações.
- Para que serve:
Permite que desenvolvedores utilizem bancos de dados sem precisar configurar ou administrar servidores.
- Exemplo de mercado:
Amazon RDS — serviço da Amazon Web Services que oferece bancos de dados gerenciados na nuvem.


    
## FaaS (Function as a Service)
- Descrição:
FaaS significa Função como Serviço. Nesse modelo, o desenvolvedor cria pequenas funções de código que são executadas somente quando ocorre um evento específico.
- Para que serve:
Permite executar código sem gerenciar servidores, pagando apenas pelo tempo de execução.
- Exemplo de mercado:
AWS Lambda — serviço da Amazon Web Services que executa funções automaticamente na nuvem.


    
## IaaS (Infrastructure as a Service)
- Descrição:
IaaS significa Infraestrutura como Serviço. O provedor fornece recursos básicos como máquinas virtuais, armazenamento e redes.
- Para que serve:
Permite que empresas criem servidores e infraestrutura de TI na nuvem sem precisar comprar hardware físico.
- Exemplo de mercado:
Amazon EC2 da Amazon Web Services — permite criar e gerenciar servidores virtuais.


    
## PaaS (Platform as a Service)
- Descrição:
PaaS significa Plataforma como Serviço. O provedor oferece um ambiente completo para desenvolver, testar e publicar aplicações.
- Para que serve:
Facilita o desenvolvimento de software, pois os desenvolvedores não precisam gerenciar a infraestrutura.
- Exemplo de mercado:
Google App Engine da Google — plataforma para desenvolver e hospedar aplicações na nuvem.



## SaaS (Software as a Service)
- Descrição:
SaaS significa Software como Serviço. O software é acessado diretamente pela internet, sem necessidade de instalação no computador do usuário.
- Para que serve:
Permite usar aplicativos online com atualizações automáticas e acesso de qualquer lugar.
- Exemplo de mercado:
Google Docs da Google — editor de documentos acessado pelo navegador.


   
## SECaaS (Security as a Service)
- Descrição:
SECaaS significa Segurança como Serviço. Nesse modelo, ferramentas de segurança digital são oferecidas pela nuvem.
- Para que serve:
Protege sistemas, redes e dados sem a necessidade de instalar e gerenciar soluções de segurança localmente.
- Exemplo de mercado:
Cloudflare — oferece serviços de proteção contra ataques, firewall e segurança para sites.
