# disp_moveis
Repositório com a finalidade de anexar as atividades 4 e 5 aplicadas em sala de aula, dia 5 de março de 2026

# Em qual camada foi implementado o mecanismo de cache? Explique por que essa decisão é adequada dentro da arquitetura proposta.
Na camada de Data. Faz sentido porquê a camada Domain não sabe de onde vêm os dados, repositório é o lugar certo pra orquestrar fontes de dados, a presentation não fica presa a lógica de erro e cada datasource tem responsabilidade única.

# Por que o ViewModel não deve realizar chamadas HTTP diretamente?

# O que poderia acontecer se a interface acessasse diretamente o DataSource?

# Como essa arquitetura facilitaria a substituição da API por um banco de dados local?
