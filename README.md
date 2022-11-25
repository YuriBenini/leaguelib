# LeagueLib
#### Por [Anshu Chimala](http://www.achimala.com), Tyrus Tenneson e Gavin Saldanha.

LeagueLib é uma biblioteca Java para a API [League of Legends](http://www.leagueoflegends.com) [RTMPS](http://en.wikipedia.org/wiki/Real_Time_Messaging_Protocol), construída sobre [LoLRTMPSClient] (http://code.google.com/p/lolrtmpsclient) por Gabriel Van Eyck.

O LeagueLib foi desenvolvido para alimentar aplicativos da Web simultâneos, escaláveis ​​e eficientes do League of Legends. Melhor servido em uma estrutura como [Play](http://www.playframework.com/).

Este é o material que construímos para substituir o back-end que executa [LoLTeam](http://www.lolteam.net) e [LoLTalk](http://loltalk.achimala.com). Nosso código original fazia seu trabalho, mas não era escalável ou eficiente o suficiente para atender ao nosso tráfego crescente. Em resposta, começamos a construir uma estrutura nova, altamente escalável e massivamente simultânea para esses aplicativos, para atender a dezenas de milhares de jogadores em todo o mundo. E estamos tornando-o de código aberto para que outros desenvolvedores como nós possam criar aplicativos incríveis de League of Legends.

### Características
* Chamadas de API completamente assíncronas para o servidor RTMP de League of Legends.
* Chamadas de API síncronas com a mesma facilidade, para uso em aplicativos simples ou em plataformas distribuídas, escaláveis ​​e simultâneas como [Akka](http://www.akka.io).
* Suporte fácil para várias contas de League of Legends para maior simultaneidade e efeitos colaterais mínimos de limitação de taxa.
* Design eficiente: solicite apenas o máximo de informações necessárias, usando as mesmas chamadas de API e estrutura que o League of Legends usa internamente.
* Padrões MVC limpos: as contas podem ser facilmente empacotadas em arquivos ou registradas em bancos de dados, distribuídas para diferentes filas de contas para diferentes servidores, e um único modelo LeagueSummoner pode conter referências a dados em tempo real em seu aplicativo que são atualizados no local.

### Uso

Pretendemos apresentar uma melhor forma de documentação no futuro, mas até lá, aqui estão algumas notas básicas de implementação.
* LeagueLib não incorpora nenhum tipo de agendamento de thread/trabalho ou arquitetura de computação distribuída. Achamos que existem mais do que suficientes e, em vez disso, optamos por construir algo que pudesse se conectar a qualquer um deles facilmente. Para LoLTeam e LoLTalk, simplesmente escrevemos uma camada em cima de LeagueLib que o conecta ao agendamento de trabalho assíncrono do Play Framework criado em cima de Akka, que é executado em vários processos distribuídos na nuvem via Heroku.
* LeagueLib foi projetado com o objetivo principal de nos dar andaimes para construir LoLTeam e LoLTalk em cima. Como tal, é robusto, mas não necessariamente completo. Nós vamos continuar adicionando a ele.
* O objeto LeagueSummoner é o foco de tudo no LeagueLib como é agora. As chamadas de API do serviço de invocador muito fundamentais retornam contêineres de invocador vazios com nomes e IDs e nada mais. À medida que você solicita diferentes tipos de informações de diferentes serviços, eles são preenchidos em seu único objeto de invocador. Você não deve manter várias cópias de um invocador ou jogá-las fora sem motivo.

### Licença
LeagueLib está licenciado sob a GNU GPL v3. Você pode usar este código para fins comerciais ou não comerciais.

Você pode:
* Use LeagueLib em produtos pessoais ou comerciais, com atribuição.
* Modificar e distribuir LeagueLib, com atribuição.

Talvez você não:
* Venda qualquer parte do LeagueLib.
* Use ou distribua qualquer parte do LeagueLib sem as informações de licenciamento incluídas ou sem atribuição.

### Cuidado
LeagueLib ainda está em desenvolvimento. Aconselhamos não usá-lo em aplicativos de produção até que esteja pronto.

O código retirado do branch master deve sempre funcionar corretamente e passar em todos os testes. Pretendemos colocar um código de amostra em breve, mas até então você deve ser capaz de descobrir como usar LeagueLib visualizando [MainTest.java](https://github.com/achimala/leaguelib/blob/master/src/ com/achimala/leaguelib/tests/MainTest.java) ou lendo os comentários nas classes LeagueConnection, LeagueAccount e *Service.java.
