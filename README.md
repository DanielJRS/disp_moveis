# disp_moveis
Repositório com a finalidade de anexar as atividades 4 e 5 aplicadas em sala de aula, dia 5 de março de 2026

# Em qual camada foi implementado o mecanismo de cache? Explique por que essa decisão é adequada dentro da arquitetura proposta.
Na camada de Data. Cache é um detalhe de implementação — é uma fonte de dados assim como a API. O ProductRepositoryImpl orquestra: tenta o remote, salva no cache, e se falhar busca do cache. A camada Domain nem sabe que cache existe, ela só chama getProducts() e recebe a lista. Isso é o certo porque se amanhã você trocar o cache em memória por SharedPreferences ou Hive, nada acima muda.

# Por que o ViewModel não deve realizar chamadas HTTP diretamente?
Porque a responsabilidade do ViewModel é uma só: gerenciar estado da UI. Ele recebe dados, atualiza o state, e a tela reage. Se ele fizer HTTP direto, ele passa a acumular duas responsabilidades — controlar UI e saber como buscar dados. Além disso, você perde a capacidade de trocar a fonte de dados sem mexer na apresentação, e testar o ViewModel fica mais difícil porque você precisa mockar HTTP em vez de só mockar o repository.

# O que poderia acontecer se a interface acessasse diretamente o DataSource?
Quebraria a separação de camadas. A tela ficaria acoplada à implementação — se o endpoint muda, você mexe na tela. Se você quer adicionar cache, mexe na tela de novo. Testar fica difícil porque não dá pra substituir o datasource real por um fake facilmente. E o pior: a lógica de "tenta remote, faz fallback pro cache" que hoje vive no repository teria que ser reescrita dentro de cada tela que usa produto.

# Como essa arquitetura facilitaria a substituição da API por um banco de dados local?
Você cria um novo datasource, tipo ProductLocalDatasource usando SQLite ou Floor, e injeta ele no ProductRepositoryImpl no lugar do remote. O repository recebe os datasources pelo construtor, então é só trocar na hora de montar a dependência. O contrato ProductRepository continua o mesmo, o ViewModel continua chamando getProducts(), e a tela não muda uma linha.
