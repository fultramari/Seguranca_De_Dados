# Lista de exercícios

## 1) Considere os requisitos de confidencialidade, integridade, disponibilidade, autenticidade, e responsabilização. Quais desses requisitos estão mais em risco em um ataque dos tipos a seguir? Justifique.
  ### a) Intromissão usando um sniffer?
  R: A confidencialidade é o requisito que mais sofre nessa ocasião, uma vez que os pacotes foram acessados por um interceptador que não deveria ter acesso á informação.
  ### b) Negação de serviço de um servidor web?
  R: Nesse caso, o requisito que mais sofre é a disponibilidade, visto que a negação de serviço torna o servidor indisponível e inacessível para os usuários.
  ### c) Phishing se passando por uma página de banco falsa?
  R: Nesse caso, a confidencialidade das informações dos clientes serão perdidas. Além disso, a autenticidade da página também é afetada.
  ### d) Vírus de computador que altera executáveis do sistema operacional?
  R: Nesse caso, a integridade dos executáveis sofre riscos.



  ## 2) Leia a seção 1.2.1. – Cibersegurança (páginas 5 a 11) do minicurso “Ciência de Dados Aplicada à Cibersegurança: Teoria e Prática” (disponível para download noMoodle ou no link abaixo) https://doi.org/10.5753/sbc.15101.8.1
  ## Responda às perguntas abaixo baseado nesse texto:
  ### a) Tradicionalmente, a cibersegurança era definida com base na tríade
  Confidencialidade, Integridade e Disponibilidade (CIA). Por que essa
  abordagem, centrada apenas na tríade CIA, é considerada limitada nos dias
  de hoje?
    R: O fato do ciberespaço hoje apresentar caráter político, social e econômico exigiu uma definição mais completa, que levasse em conta esses aspectos para uma definição mais precisas. A tríade CIA leva em conta apenas o aspecto tecnológgico e técnico da cibersegurança, sendo necessária uma visão mais ampla.

  ### b) Defina os seguintes conceitos: Confidencialidade, Integridade,
  Disponibilidade, Autenticidade, e Não repúdio (ou Responsabilização).
  Confidencialidade: Apenas o remetente e o destinatário sabem da informação.
  Integridade: A informação não pode, em hipótese alguma, sofrer alterações/distorções.
  Disponibilidade: A informação deve estar disponível sempre que um usuário deseja acessar.
  Autenticidade: Deve ser possível identificar corretamente os elementos da comunicação, não sendo possível falseá-los.
  Não Repúdio : Logs com informação de todas as ações, de modo que seja possível a responsabilização.

  ### c) Explique os conceitos de vulnerabilidade, exploit, e ameaça.
  Vulnerabilidade: Algum comportamento ou atributo da rede que pode ser visto como um ponto de exploração para eventuais danos à cibersegurança.
  Exploit: Trata-se de um software ou processo capaz de explorar determinadas vulnerabilidades da rede.
  Ameaça: Um agente que tem motivação e capacidade de causar danos à segurança de uma rede é visto como uma ameaça. 

  ### d) O que é um ataque de negação de serviço distribuído (DDoS)? Quais propriedades listadas no item (b) podem ser comprometidas nesse tipo de ataque?
  Um ataque de negação de serviço é uma forma de atacar a propriedade de disponibilidade de uma rede ou servidor. Através do excesso de requisições, feito por meio de diversos bots comandados por um atacante, o servidor fica indisponível por não conseguir lidar com o alto número de requisições.

