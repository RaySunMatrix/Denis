# O que é DNS? | Como o DNS funciona

DNS é o que permite aos usuários se conectarem a sites usando nomes de domínio em vez de endereços de IP. Saiba como o DNS funciona.
Central de Aprendizagem

    O que é DNS?
    O que é 1.1.1.1?
    Registros DNS
    Protegendo o DNS
    Registro de domínios
    Glossário de DNS
    theNET

Objetivos de aprendizado

Após ler este artigo, você será capaz de:

    Definição de DNS
    Entenda como o DNS funciona
    Diferencie entre pesquisas de DNS recursivas e iterativas
    Separe authoritative nameservers dos resolvedores de DNS recursivos
    Explore como o cache do DNS funciona

Conteúdo relacionado

Segurança de DNS

Zona de DNS

Servidor raiz de DNS

DNS primário x secundário

DNS reverso
Quer saber mais?

Assine o theNET, uma recapitulação mensal feita pela Cloudflare dos insights mais populares da internet.
E-mail: *

As informações que você fornece à Cloudflare são regidas pelos termos da nossa Política de Privacidade.

Copiar o link do artigo
O que é DNS?

O Domain Name System (DNS) é a lista telefônica da internet. Os seres humanos acessam informações on-line por meio de nomes de domínio, como nytimes.com ou espn.com. Os navegadores da web interagem por meio de endereços de Protocolo de internet (IP). O DNS converte os nomes de domínio em endereços de IP para que os navegadores possam carregar os recursos da internet.

Cada dispositivo conectado à internet tem um endereço IP único que outras máquinas utilizam para localizar o dispositivo. Os servidores de DNS eliminam a necessidade de que humanos memorizem endereços IP como 192.168.1.1 (no IPv4) ou endereços IP alfanuméricos mais complexos mais recentes, como 2400:cb00:2048:1::c629:d7a2 (no IPv6).
DNS – lupa examina endereços de IP, encontra www.example.com
Como funciona o DNS?

O processo de resolução do DNS envolve a conversão de um hostname (como www.example.com) em um endereço IP fácil de ser entendido por um computador (como 192.168.1.1). Um endereço IP é fornecido para cada dispositivo na internet, e esse endereço é necessário para que o dispositivo de internet apropriado seja encontrado — como um endereço postal é usado para encontrar uma determinada casa. Quando um usuário deseja carregar uma página da internet, precisa haver uma tradução daquilo que o usuário digita no navegador web (example.com) para o endereço de máquina necessário para localizar a página do site example.com.

Para entender o processo por trás da resolução do DNS, é importante aprender sobre os diferentes componentes de hardware pelos quais uma consulta de DNS deve passar. Para o navegador da web, a busca pelo DNS ocorre "nos bastidores" e não exige nenhuma interação do computados do usuário além da solicitação inicial.
Relatório
2023 GigaOm Radar for DNS Security attacks
Acesse o relatório
Fale com um especialista
Saiba como a Cloudflare pode proteger sua empresa
Entre em contato com vendas
Existem 4 servidores de DNS envolvidos no carregamento de uma página da internet:

    Recursor de DNS — o recursor pode ser imaginado como um bibliotecário solicitado a procurar um livro específico em algum lugar de uma biblioteca. O recursor de DNS é um servidor projetado para receber consultas de máquinas clientes por meio de aplicações como navegadores web. De modo geral, o recursor é responsável por fazer solicitações adicionais para atender à consulta de DNS do cliente.
    Servidor raiz — o servidor raiz é a primeira etapa da tradução (resolução) de host names legíveis por humanos em endereços IP. Pode ser imaginado como um índice em uma biblioteca que aponta para diferentes estantes de livros — geralmente serve como referência para outros locais mais específicos.
    Nameserver TLD - Pense no servidor de domínio de nível superior (TLD) como uma estante de livros específica em uma biblioteca. Esse nameserver é o próximo passo na busca de um endereço de IP específico e hospeda a última parte de um hostname (em example.com, o servidor de TLD é "com").
    Servidor de DNS autoritativo — esse servidor de DNS final pode ser imaginado como um dicionário em uma estante de livros, no qual um nome específico pode ser traduzido em sua definição. O nameserver autoritativo é a última parada na consulta de um servidor de DNS. Se tiver acesso ao registro solicitado, o nameserver autoritativo retornará o endereço IP do hostname solicitado de volta ao recursor de DNS (o bibliotecário) que fez a solicitação inicial.

DNS rápido e seguro
DNS gratuito incluído em qualquer plano da Cloudflare
Comece agora gratuitamente
Qual é a diferença entre um servidor DNS autoritativo e um resolvedor recursivo de DNS?

Ambos os conceitos se referem a servidores (grupos de servidores) que são parte integrante da infraestrutura do DNS, mas cada um desempenha uma função diferente e fica em locais diferentes dentro do pipeline de uma consulta de DNS. Uma forma de se pensar sobre a diferença é que o resolvedor recursivo está no início da consulta de DNS e o nameserver autoritativo está no final.
Resolvedor recursivo de DNS

O resolvedor recursivo é o computador que responde a uma solicitação recursiva de um cliente e dedica algum tempo a rastrear o registro de DNS. Isso é feito por meio de uma série de solicitações até chegar ao nameserver autoritativo de DNS do registro solicitado (ou atingir o limite de tempo ou retornar um erro se nenhum registro for encontrado). Felizmente, nem sempre os resolvedores recursivos de DNS precisam fazer diversas solicitações para rastrear os registros necessários para responder a um cliente; o armazenamento em cache é um processo de persistência de dados que ajuda a encurtar o caminho das solicitações necessárias fornecendo o registro do recurso solicitado mais no início da pesquisa de DNS.
Sequência de solicitação de registro de DNS – O resolvedor de DNS recursivo obtém a solicitação do cliente
Servidor de DNS autoritativo

Em termos simples, um servidor DNS autoritativo é o servidor que realmente mantém e é responsável pelos registros de recursos de DNS. Trata-se do servidor na parte inferior da cadeia de pesquisa de DNS, que responderá com o registro do recurso consultado, em última instância permitindo que o navegador de internet faça a solicitação para alcançar o endereço IP necessário para acessar um site ou outros recursos da internet. Um nameserver autoritativo pode atender a consultas com seus próprios dados, sem precisar consultar outra fonte, já que se trata da fonte final da verdade para determinados registros de DNS.
Sequência de solicitação de registro de DNS – A consulta de DNS chega a um nameserver autoritativo para cloudflare.com

Vale mencionar que, nos casos em que a consulta é para um subdomínio, como foo.example.com ou blog.cloudflare.com, um nameserver adicional será adicionado à sequência após o nameserver autoritativo, que é responsável por armazenar o registro CNAME do subdomínio.
Sequência de solicitação de registro de DNS – Consulta de DNS para registro CNAME para o subdomínio blog.cloudflare.com

Há uma diferença fundamental entre os diversos serviços de DNS e o fornecido pela Cloudflare. Diferentes resolvedores recursivos de DNS, como o Google DNS, o OpenDNS e provedores como a Comcast, mantêm instalações de data center com resolvedores recursivos de DNS. Esses resolvedores permitem consultas rápidas e fáceis por meio de grupos otimizados de sistemas de computador otimizados para DNS, mas são fundamentalmente diferentes dos nameservers hospedados pela Cloudflare.

A Cloudflare mantém nameservers em nível de infraestrutura que são essenciais para o funcionamento da internet. Um exemplo importante é a rede de servidores raiz F, por cuja hospedagem a Cloudflare é parcialmente responsável. O raiz F é um dos componentes da infraestrutura de nameservers de DNS no nível raiz, responsável por bilhões de solicitações de internet por dia. Nossa rede Anycast nos coloca em uma posição única para lidar com grandes volumes de tráfego de DNS sem interrupção do serviço.
Quais são as etapas de uma pesquisa de DNS?

Na maioria das situações, o DNS se preocupa com a tradução de um nome de domínio para o endereço IP apropriado. Para aprender como esse processo funciona, é útil seguir o caminho de uma pesquisa de DNS à medida que ela viaja, partindo de um navegador web, ao longo do processo de pesquisa de DNS e de volta à origem. Vamos examinar essas etapas.

Observação: muitas vezes, as informações da pesquisa de DNS são armazenadas em cache localmente dentro do computador de consulta ou remotamente na infraestrutura de DNS. De modo geral, uma pesquisa de DNS tem 8 etapas. Quando as informações de DNS são armazenadas em cache, algumas etapas do processo de pesquisa de DNS são ignoradas, o que o torna mais rápido. O exemplo abaixo descreve todas as 8 etapas, quando não há nada armazenado em cache.
As 8 etapas de uma pesquisa de DNS:

    Um usuário digita "example.com" em um navegador web; a consulta viaja para a internet e é recebida por um resolvedor recursivo de DNS.
    O resolvedor então consulta um nameserver raiz de DNS(.).
    O servidor raiz responde ao resolvedor com o endereço de um servidor DNS de Domínio de Nível Superior (TLD) (como .com ou .net) que armazena as informações de seus domínios. Quando buscamos example.com, nossa solicitação é direcionada para o TLD .com.
    A seguir, o resolvedor faz uma solicitação ao TLD .com.
    A seguir, o servidor de TLD responde com o endereço IP do nameserver do domínio, example.com.
    Para finalizar, o resolvedor recursivo envia uma consulta ao nameserver do domínio.
    O endereço IP de example.com é a seguir retornado ao resolvedor partindo do nameserver.
    Em seguida, o resolvedor de DNS responde ao navegador web com o endereço IP do domínio solicitado inicialmente.

    Assim que as 8 etapas da pesquisa de DNS tiverem retornado o endereço IP para example.com, o navegador consegue fazer a solicitação da página da internet:
    O navegador faz uma solicitação de HTTP para o endereço IP.
    O servidor nesse IP retorna a página da internet que deverá ser renderizada no navegador (etapa 10).

Pesquisa de DNS completa e Consulta da página web – 10 etapas
O que é um resolvedor de DNS?

O resolvedor de DNS é a primeira parada da pesquisa de DNS e é responsável por lidar com o cliente que fez a solicitação inicial. O resolvedor inicia a sequência de consultas que, em última instância, leva à tradução de uma URL para o endereço IP necessário.

Observação: uma pesquisa típica de DNS não armazenada em cache envolverá consultas recursivas e iterativas.

É importante estabelecer a diferença entre uma consulta recursiva de DNS e um resolvedor recursivo de DNS. A consulta refere-se à solicitação feita a um resolvedor de DNS requerendo a resolução da consulta. Um resolvedor recursivo de DNS é o computador que aceita uma consulta recursiva e processa a resposta fazendo as solicitações necessárias.
A consulta recursiva de DNS vai do cliente de DNS para o resolvedor de DNS recursivo
Quais são os tipos de consultas de DNS?

Em uma pesquisa típica de DNS, ocorrem três tipos de consultas. Por meio do uso de uma combinação dessas consultas, um processo otimizado para a resolução do DNS pode resultar em uma redução da distância percorrida. Em uma situação ideal, os dados do registro armazenado em cache estarão disponíveis, permitindo que um nameserver de DNS retorne uma consulta não recursiva.
Três tipos de consultas de DNS:

    Consulta recursiva — em uma consulta recursiva, um cliente de DNS solicita que um servidor de DNS (geralmente um resolvedor recursivo de DNS) responda ao cliente com o registro do recurso solicitado ou uma mensagem de erro se o resolvedor não conseguir encontrar o registro.
    Consulta iterativa — nessa situação, o cliente de DNS permitirá que um servidor de DNS retorne a melhor resposta possível. Se não encontrar uma correspondência para o nome na consulta, o servidor de DNS consultado retornará uma recomendação para um servidor de DNS autoritativo para um nível inferior do namespace do domínio. O cliente de DNS, então, fará uma consulta ao endereço recomendado. Esse processo continua com servidores de DNS adicionais na cadeia de consulta até que ocorra um erro ou o limite de tempo seja atingido.
    Consulta não recursiva — de modo geral, isso ocorre quando um resolvedor de DNS cliente consulta um servidor de DNS em busca de um registro ao qual ele tenha acesso porque é autoritativo para o registro ou o registro existe dentro de seu cache. De modo geral, o servidor de DNS irá armazenar os registros de DNS em cache para evitar um consumo adicional de largura de banda e carregar nos servidores mais acima na cadeia de consulta.

O que é o armazenamento de DNS em cache? Onde o armazenamento de DNS em cache ocorre?

O objetivo do armazenamento em cache é armazenar dados temporariamente em um local que resulte em um aumento de desempenho e de confiabilidade para as solicitações de dados. O armazenamento de DNS em cache envolve o armazenamento de dados mais perto do cliente que os solicita, para que a consulta de DNS possa ser resolvida mais cedo e consultas adicionais mais à frente na cadeia de pesquisa de DNS possam ser evitadas, reduzindo os tempos de carregamento e o consumo de largura de banda/CPU. Os dados de DNS podem ser armazenados em cache em diversos locais, cada um dos quais irá armazenar registros de DNS por um período de tempo definido, determinado por uma vida útil (TTL).
Armazenamento em cache do DNS do navegador

Os navegadores web modernos são projetados por padrão para armazenar os registros de DNS em cache por um período de tempo definido. O objetivo aqui é óbvio: quanto mais próximo do navegador web o armazenamento do DNS em cache ocorrer, menos etapas de processamento precisarão ser realizadas para verificar o cache e fazer as solicitações corretas para um endereço de IP. Quando uma solicitação de um registro de DNS é feita, o cache do navegador é o primeiro local verificado na busca do registro solicitado.

No Chrome, você pode ver o status do seu cache de DNS acessando chrome://net-internals/#dns.
Armazenamento de DNS no cache ao nível do sistema operacional (OS)

O resolvedor de DNS no nível do sistema operacional é a segunda e última parada local antes que uma consulta DNS saia da sua máquina. O processo dentro do seu sistema operacional projetado para lidar com essa consulta geralmente é chamado de "resolvedor de stub" ou cliente de DNS. Quando recebe uma solicitação de uma aplicação, um resolvedor de stub primeiro verifica seu próprio cache para ver se tem o registro. Caso contrário, envia uma consulta de DNS (com um sinalizador recursivo definido) para fora da rede local, para um resolvedor recursivo de DNS dentro do provedor de serviços de internet (ISP).

Como ocorre em todas as etapas anteriores, quando recebe uma consulta de DNS o resolvedor recursivo dentro do ISP também verifica se a tradução do host em endereço IP solicitada já está armazenada dentro de sua camada de persistência local.

O resolvedor recursivo também apresenta uma funcionalidade adicional, dependendo dos tipos de registros que estão em seu cache:

    Se não tiver os registros A, mas tiver os registros de NS dos nameservers autoritativos, o resolvedor consultará esses nameservers diretamente, ignorando as várias etapas de uma consulta de DNS. Esse atalho evita as pesquisas dos servidores raiz e dos nameservers .com (em nossa pesquisa do example.com) e ajuda a resolução da consulta de DNS a ocorrer mais rapidamente.
    Se não tiver os registros NS, o resolvedor enviará uma consulta aos servidores de TLD (.com, no nosso caso), ignorando o servidor raiz.
    Na improvável hipótese de não encontrar nenhum registro apontando para os servidores de TLD, o resolvedor irá consultar os servidores raiz. Esse evento geralmente ocorre após uma limpeza de um cache de DNS.

Saiba mais sobre o que diferencia o DNS da Cloudflare de outros provedores de DNS.
