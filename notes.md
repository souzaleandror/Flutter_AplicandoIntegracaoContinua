##### 22/01/2024

Curso de Flutter: aplicando integração contínua (CI)

@01-Conhecendo o Codemagic e o CI

@@01
Apresentação

Olá, Dev! Bem-vindo a mais um curso de Flutter da Alura. Eu sou William Bezerra.
Audiodescrição: William se identifica como um homem pardo de cabelos e barba escuros. Usa óculos com armação arredondada, camiseta marrom e fones sem fio. Ao fundo, parede lisa com iluminação degradê de branco para azul.
O que vamos aprender?
No curso que você vai começar a estudar hoje, vamos falar sobre integração contínua com Flutter, que é um processo para automatizar uma série de tarefas durante nosso processo de desenvolvimento, elevando a qualidade da escrita do código e garantindo que nosso aplicativo chegue com o mínimo de bugs possível na mão da pessoa usuária.

Agora, vamos demonstrar um pouco sobre o que vamos aprender ao longo deste curso.

A plataforma Codemagic nos auxiliará a configurar todos esses processos para elevar a qualidade e automatizar esse processo, garantindo que todos os códigos escritos - independentemente de quem os tenha feito - passem por um alto grau e nível de qualidade para assegurar que foram escritos da maneira mais correta e adequada, sem quebrar nada na aplicação.

Além disso, vamos aprender a como configurar pipelines, estruturar alguns processos.

Pré-requisitos
Como pré-requisito para você fazer este curso, é muito importante que já tenha um bom conhecimento de testes unitários, testes de widgets e testes de integração.

Esperamos você no próximo vídeo. Valeu!

@@02
Preparando o ambiente

Durante o curso, utilizaremos o projeto Sorteador de amigo secreto. E como o nome já diz, este é um app que auxilia pessoas que querem organizar uma brincadeira de amigo secreto.
Você pode baixá-lo aqui.

Para o projeto, utilizamos a versão 3.10.5 do Flutter e 3.0.5 do Dart, certifique-se que sua máquina está com essas configurações para rodar o projeto.

Bons estudos!

https://github.com/alura-cursos/ci-alura-course

https://docs.flutter.dev/release/archive?

https://dart.dev/get-dart/archive

@@03
Integração contínua no Flutter

Imagine a seguinte situação: você está trabalhando para um grande grupo em uma rede varejista em um aplicativo para o usuário final. E, juntamente com você, há algumas outras pessoas desenvolvedoras. Todo mundo está construindo features (recursos), corrigindo bugs (erros), enfim, garantindo tudo na mais alta qualidade.
Integração contínua no Flutter
Em um certo dia, você estava trabalhando nesse aplicativo, construindo uma feature, você garantiu que tudo estava funcionando. Os testes funcionaram, você iniciou todo o processo, garantiu que estava tudo ok.

E aí, você fez o merge e finalizou a sua entrega. Entretanto, o seu colega estava trabalhando em uma funcionalidade que tinha alguns conflitos com o que você entregou. E quando ele foi abrir o PR (Pull Request), obviamente, esses conflitos aconteceram.

Ao resolver esses conflitos, ele alterou a sua lógica. Como ele já tinha testado a funcionalidade antes, ele acabou esquecendo de rodar novamente os testes para garantir que estava tudo funcional e apenas subiu a entrega, resolvendo os conflitos.

O que ele não imaginava era que essas alterações alterariam bastante a sua entrega. E quando essa entrega chegou ao usuário final, a sua feature parou de funcionar!

Agora você teria que rodar os testes, encontrar o bug, corrigir, enviar para a produção novamente e esperar de um a dois dias até chegar na loja. Que dificuldade! Isso poderia ter sido evitado, não é verdade?

É aí que entra o Continuous Integration (Integração Contínua ou CI) que serve justamente para garantir que o código sempre vai passar por todos os processos e critérios de qualidade que sua empresa definiu - independente de quem fez as alterações.
Desse modo, evitamos sustos quando a funcionalidade chegar ao usuário final.

Quando você implementa o CI no seu app, você tem a certeza de que ele vai passar por todo esse processo de qualidade quando tiverem alterações. Ou seja, vai rodar os testes para verificar se o código está bom e garantir que, de fato, quando chegar no usuário final, o app terá passado por uma regra de qualidade altíssima.

Isso ajuda a minimizar os danos e vai lhe ajudar a economizar, principalmente, tempo. Porque você não vai precisar verificar manualmente toda vez que ocorrerem alterações. Uma vez que você abrir o PR, ele vai passar por um processo de qualidade automaticamente, pois está integrado ao seu projeto, justamente para garantir que tudo estará funcional.

Além do mais, ele não vai apenas rodar os testes, também vai garantir que o seu código não vai ter code smells.

Os code smells são pedaços de código que não necessariamente quebram a aplicação, mas que são desnecessários.
Por exemplo, se há um import no projeto que não estamos utilizando, ele é desnecessário e vai dificultar a manutenção futura. Então, é melhor removê-lo. O CI vai nos alertar quando identificar esses code smells no nosso processo para que possamos resolver.

Por exemplo, uma forma muito simples de identificar isso é rodando o flutter analyze para trazer todos os problemas.

Além de auxiliar com o processo de teste, garantir que o nosso projeto vai passar por todos os testes possíveis, testes de integração, testes de widgets, testes unitários, o CI também vai estar identificando os code smells.

Tudo de maneira integrada e contínua, o que vai garantir qualidade do código, uma menor quantidade de falhas e, principalmente, a saúde da aplicação.

@@04
Configurando o Codemagic

Seguindo com o nosso curso, precisamos definir a configuração inicial da integração contínua para o nosso aplicativo em Flutter.
E aí existem diversas especificidades quando se trata de desenvolvimento mobile, principalmente no que diz respeito a teste de integração e a definição de ambientes para fazer a execução da integração contínua.

Quando vamos para o mercado buscar quais são as ferramentas que fazem isso para o Flutter, existem algumas opções que são bem importantes e que têm uma boa presença no mercado. Mas, qual então escolher?

Neste curso, optamos por utilizar o Codemagic, que é uma ferramenta que, além de ter um preço acessível e ser gratuita no início, oferece 400 minutos gratuitos, tem uma interface amigável para que possamos fazer a configuração de maneira mais simples.

Mas, antes de começar a fazer uma configuração no Codemagic, vamos primeiro conhecer o nosso projeto.

Conhecendo o projeto
Vamos abrir o projeto no Visual Studio Code.

Lembre-se que você pode baixar o projeto na atividade anterior de "Preparando o Ambiente", onde temos o link do repositório do projeto no GitHub.
O projeto é definido em algumas camadas. Temos a configuração inicial do Flutter, onde temos a pasta "lib". Dentro dela, definimos as pastas "layout", "logic", "pages", "widgets" e o arquivo main.dart.

Está estruturado de forma simples, por camadas, pois é um projeto com apenas duas páginas. Porém, trabalhamos bastante a questão da lógica nesse projeto.

E quando é relacionado à lógica, precisamos testar bastante. Por isso, na pasta "test > logic", temos os testes de lógica, onde fizemos testes unitários para validar todo o funcionamento da lógica do aplicativo.

Além disso, também temos os testes de widgets na pasta "test > widgets", onde separamos nosso aplicativo em microcomponentes e validamos todo o processo de formulário e widgets, para garantir que tudo está funcionando de maneira separada.

Por fim, já que testamos a lógica e os componentes, testamos também a integração do nosso projeto em "integration_test > app_test.dart", onde executamos um processo de teste end-to-end, validando todo o funcionamento, do início ao fim. Desse modo, garantimos que está tudo funcionando como esperado.

No emulador, também temos a visualização onde conseguimos validar o funcionamento do nosso projeto.

Emulador da tela inicial do projeto. No topo, fundo azul com ilustração de um dado acima do título "Sorteador de amigo secreto". Logo abaixo, ilustração de uma pessoa interagindo com um objeto em suas mãos. No centro, fundo bege com letreiro "vamos começar!", caixa de texto com placeholder "Insira os nomes dos participantes" e botão cinza "Adicionar". Logo abaixo, ilustração de sacolas de compra em tons de azul.

No sorteador, podemos inserir o nome de pessoas. Por exemplo, vamos inserir o nome da "Erica" e "Will".

Após inserir essas duas pessoas, aparece o botão "Iniciar a brincadeira". O botão antes não estava ativado, devido à regra de lógica já existente. E caso clicamos em cima do nome adicionado, ele é removido.

Também não podemos adicionar um nome que já esteja na lista.

Ops! Este nome já foi adicionado!
Existe uma série de lógicas dentro da tela inicial, assim como nas demais.

Agora que adicionamos os dois nomes, vamos iniciar a brincadeira.

Podemos selecionar quem está tirando o papel no dropdown da página seguinte. Após selecionar, clicamos no botão "Sortear" para sortear a pessoa.

Nesse caso, obviamente a Erica tira o Will. E da mesma forma, quando selecionamos o Will, ele vai tirar a Erica.

Tem uma série de lógicas nessa parte também. Por exemplo, se o Will quiser sortear de novo, ele não vai conseguir, porque já sorteou um nome anteriormente.

Ops! Esta pessoa já sorteou um nome anteriormente.
É assim que funciona o aplicativo e todo o nosso projeto. Tem muita lógica envolvida. Sugerimos que você baixe, brinque, verifique, teste e tente implementar algo interessante também.

Nos acompanhe a partir de agora, iniciando a integração contínua do nosso projeto.

Configurando Codemagic
Agora, vamos abrir o Codemagic no navegador, cujo link também está na sessão anterior, onde falamos dos primeiros passos para iniciar as aulas.

Em Codemagic.io, você pode se cadastrar clicando no botão "Sign up" no canto superior direito. É possível entrar com GitHub, Bitbucket, GitLab. Sugerimos que entre com a conta com a qual você está construindo o projeto - no nosso caso é o GitHub, mas você pode utilizar uma dessas outras ferramentas.

Uma vez que você faz o cadastro com uma dessas contas, automaticamente ele dá acesso aos repositórios que você quer integrar. Se fizer login com o e-mail, você terá que fazer depois a vinculação com todas as suas contas - o que pode ser um pouco complexo.

Como já temos uma conta, vamos fazer o login. Feito isso, vamos ser redirecionados para a tela inicial, uma vez que já criou uma conta no Codemagic.

Você ainda não vai ter nenhum aplicativo, por isso, pode clicar no botão "add your first app" (adicionar seu primeiro aplicativo). Em seguida, vai selecionar qual é a plataforma que está utilizando, como já conectamos com o GitHub, vamos escolher essa opção.

Ao clicar em "Next" (próximo), vamos selecionar o repositório. Como ele está integrado automaticamente, ele vai trazer uma lista de todos os nossos repositórios em um dropdown. No nosso caso, vamos utilizar o repositório secret_friend_draw.

Após selecionar qual é o repositório, vamos selecionar qual é o tipo do projeto. Nesse caso, vamos utilizar o "Flutter App". Por fim, clicamos em "Finish" para adicionar a aplicação ao Codemagic.

Com isso, conseguimos fazer todas as configurações e utilizar todas as ferramentas do Codemagic. Podemos fazer builds, fazer integração contínua, trazer alguns detalhes de teste, distribuição e notificação.

São conteúdos que vamos trabalhar ao longo de toda essa formação, mas no curso de agora vamos trabalhar apenas com a parte de integração contínua.

Se você ficou ansioso(a) para saber como vamos configurar isso no Codemagic, esperamos você na próxima aula. Até lá!

@@05
Importância da integração contínua

Você está liderando um projeto para construção de um app para uma grande empresa e tem o compromisso de entregá-lo dentro do prazo, com qualidade e sem bugs. Como implementar o CI poderia lhe ajudar?

Ao implementar o processo de CI, você passa a ter mais velocidade no processo de desenvolvimento, uma vez que ele te ajuda a gerar códigos e construir/identificar possíveis melhorias no projeto.
 
Alternativa correta
Ao implementar o processo de CI, você passa a ter a execução de forma automática de testes e análises de códigos, que garantem a qualidade do que está sendo construído antes que chegue ao usuário.
 
Correta, o processo de CI garante que todo o código está bem escrito e que todos os testes passaram, auxiliando a identificar problemas de qualidade de forma eficaz, e ajudando a economizar tempo.
Alternativa correta
Ao implementar o processo de CI, você consegue melhorar a comunicação com o cliente, garantindo que ele receba uma nova versão do aplicativo de forma automática, sempre que finalizarmos uma nova versão.

@@06
Faça como eu fiz: estruturando o Codemagic para nosso projeto

Vimos como criar e fazer a configuração do Codemagic para iniciarmos no processo de CI para nosso projeto. Chegou a hora de você replicar e criar sua conta para já deixar tudo preparado para próxima aula, onde iremos fazer a configuração do nosso primeiro processo de CI.

Minha sugestão:
Crie uma conta no codemagic, clicando aqui.
Vincule sua conta do git com o codemagic.
Adicione o projeto que vamos utilizar ao codemagic e verifique se não apresentou nenhum erro.
O resultado deve ficar assim:

 Print apresentando visualização inicial, de um projeto novo no codemagic. Apresenta o nome do projeto, um botão azul e grande com “Start your first build” e o workflow editor, que seria a aba de configuração do projeto.

Vamos lá?

Faça a configuração e deixe tudo pronto para iniciarmos a configuração na próxima aula.

https://codemagic.io/

@@06
Faça como eu fiz: estruturando o Codemagic para nosso projeto

Vimos como criar e fazer a configuração do Codemagic para iniciarmos no processo de CI para nosso projeto. Chegou a hora de você replicar e criar sua conta para já deixar tudo preparado para próxima aula, onde iremos fazer a configuração do nosso primeiro processo de CI.
VER OPINIÃO DO INSTRUTOR
Opinião do instrutor

Minha sugestão:
Crie uma conta no codemagic, clicando aqui.
Vincule sua conta do git com o codemagic.
Adicione o projeto que vamos utilizar ao codemagic e verifique se não apresentou nenhum erro.
O resultado deve ficar assim:

 Print apresentando visualização inicial, de um projeto novo no codemagic. Apresenta o nome do projeto, um botão azul e grande com “Start your first build” e o workflow editor, que seria a aba de configuração do projeto.

Vamos lá?

Faça a configuração e deixe tudo pronto para iniciarmos a configuração na próxima aula.

@@07
O que aprendemos?

Aprendemos a importância do processo de integração contínua para nossos aplicativos. Vamos revisar?
Nesta aula, você aprendeu a:

Importância do CI: Aprendemos que o CI garante que todas as alterações no código, independentemente de quem as fez, antes que o aplicativo chegue ao usuário, passe por todos os testes de forma automática e por outras réguas de qualidade, para garantir que temos um aplicativo, funcional, bem escrito e de fácil manutenção.
Quais etapas o CI executa: Aprendemos também que o CI executa os processos de testes, tanto unitários quantos de integração e também executa os processos para garantir qualidade de código, como o flutter analyse.
Configuração inicial do codemagic: Fizemos a configuração inicial do codemagic, já fazendo o vínculo com Github e criando um projeto apontando para nosso repositório.
Na próxima aula, vamos fazer nossa primeira configuração de um processo estruturado de CI, para aplicarmos na prática, os conceitos que aprendemos até agora. Te vejo lá!