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

#### 24/01/2024

@02-CI no Codemagic

@@01
Projeto da aula anterior

Antes de continuar é importante que tenha feito a configuração do projeto no Codemagic que foi levantado na aula anterior.

@@02
Para saber mais

É importante que antes de avançarmos para a configuração do CI, você tenha um entendimento básico sobre testes, tanto os unitários, quanto os de integração. Para isso, fica aqui como sugestão 2 artigos aqui da Alura, que podem lhe auxiliar a entender melhor essas etapas.
Testes unitários
Testes de integração

https://www.alura.com.br/artigos/tipos-de-testes-principais-por-que-utiliza-los?_gl=1*73mhky*_ga*MTgwMzIzMjk2Ni4xNjg4ODE5OTcz*_ga_1EPWSW3PCS*MTcwNjEzMzM0My4xNzMuMS4xNzA2MTM3MDkzLjAuMC4w*_fplc*SzU5czdFYTJDcE5vM1BsYlVnWUtESnV0MEl6VFNTYU5VWnlTNW1LR2JlQkZySE1HaTNBdSUyQnFkRHhFOUt6RUZnRjZ1eWtBcEhvOWo3akRVa2sxSHdNNXJNYzR2S1NRY1FscVk4YXJmJTJGUlVQcmtNSVhXU1RSMjVoM2NuNVljQSUzRCUzRA..

https://www.alura.com.br/artigos/dicas-desenvolver-testes-unitarios-integracao-front-end?_gl=1*73mhky*_ga*MTgwMzIzMjk2Ni4xNjg4ODE5OTcz*_ga_1EPWSW3PCS*MTcwNjEzMzM0My4xNzMuMS4xNzA2MTM3MDkzLjAuMC4w*_fplc*SzU5czdFYTJDcE5vM1BsYlVnWUtESnV0MEl6VFNTYU5VWnlTNW1LR2JlQkZySE1HaTNBdSUyQnFkRHhFOUt6RUZnRjZ1eWtBcEhvOWo3akRVa2sxSHdNNXJNYzR2S1NRY1FscVk4YXJmJTJGUlVQcmtNSVhXU1RSMjVoM2NuNVljQSUzRCUzRA..

@@03
Configurando as etapas do CI

Já passamos pelo processo de configuração inicial do Codemagic, criamos nossa conta e definimos algumas coisas. Entendemos também um pouco sobre o processo de CI, em que precisamos executar de maneira integrada e contínua os processos de qualidade de código e os processos de testes que definimos em nosso repositório.
Até aí, está tudo certo. Mas agora precisamos configurar isso para que nosso projeto esteja integrado dentro do Codemagic, de modo que esses processos sejam de fato um CI, porque até agora só temos a configuração inicial. Uma vez que configuramos isso de maneira integrada e contínua, nosso projeto para de ter esses problemas e começamos a elevar significativamente a barra de qualidade do nosso projeto.

Configurando as etapas para o CI
Seguindo o processo, para conseguirmos elevar a barra de qualidade do nosso aplicativo, precisamos definir justamente as etapas. A primeira seria melhorar a qualidade do código.

Poderíamos trazer algumas ferramentas que existem no mercado para fazer essa avaliação e garantir isso, que executam junto dentro do CI, mas o Flutter tem uma ferramenta sensacional, o flutter analyze. É justamente um comando nativo do Flutter que vai passar por todo o código do projeto, verificar arquivo por arquivo e trazer os problemas que existem no código.

Podemos executar isso apenas abrindo o terminal, indo até a pasta do projeto e executando o flutter analyze, uma vez que temos o Flutter instalado. É muito útil e auxilia bastante, então essa seria a primeira etapa.

flutter analyze
COPIAR CÓDIGO
Indo para a segunda etapa, temos o processo de testes. Existem duas maneiras de executar os testes dentro do aplicativo no Flutter. Temos o comando flutter test, que executa tanto os testes unitários quanto os testes de widgets, executando todos ao mesmo tempo. E temos o flutter drive, para executar os testes de integração.

Não se preocupe com o flutter drive agora; iremos abordá-lo apenas na próxima aula.
flutter test
COPIAR CÓDIGO
flutter drive
COPIAR CÓDIGO
Agora que já sabemos como executar o flutter analyze para garantir o código, e como executar o flutter test para garantir que os testes funcionam, precisamos trazer isso para nossa integração. É isso que vamos abordar agora durante o processo.

Abrindo o Codemagic, temos alguns setups, algumas configurações como mencionamos na última aula, iniciando pela seção "Build for platforms" ("Construir para plataformas"). Encontramos várias opções. Como estamos fazendo o setup de CI, não vamos marcar nenhuma das plataformas. Vamos desmarcar "Android" e "iOS" e vamos marcar apenas o "Run tests only" ("Executar apenas testes").

Em seguida, entramos na etapa dos testes. Temos o "Build triggers", "Environment variables", algumas configurações, mas o que é interessante para nós agora são os testes ("Tests"). Ao expandir essa categoria, conseguimos configurar algumas coisas. A primeira delas é "Stop build if tests or analysis fail" ("Interrompa a compilação se os testes ou análises falharem").

Com essa opção, ele vai parar a compilação se, ao analisar o código ou rodar o teste, acontecer algum erro. Vamos marcar que sim. Seguindo esse processo, vai fazer muito mais sentido quando formos trabalhar com o Codemagic. Mas não se preocupe; vamos apenas deixar marcado para evitar qualquer problema.

Na seção "Static code analysis", queremos que seja executado o flutter analyze, então vamos simplesmente marcar a caixa de seleção para ativar. O Codemagic pergunta quais são os argumentos para executar. No nosso caso, é só o flutter analyze, como comentamos. Como ele já define isso por padrão, apenas deixamos o comando analyze no campo "Flutter analyze arguments", que já está definido e funcional.

Agora, na seção "Integration and unit tests", entramos justamente no que seriam os testes de integração e os testes unitários. Os de integração serão abordados na próxima aula, mas os unitários vamos conhecer agora.

Basicamente, temos que habilitar a opção "Enable Flutter test". Serão solicitados os argumentos. Se você quiser rodar só o flutter test, sem problemas; se quiser rodar apenas em uma pasta específica, você pode adicionar. Vamos colocar como argumento test. As seções "Run Flutter Driver tests on" e "Flutter drive arguments" ficarão apenas para a próxima aula, que é justamente para rodar a pasta do teste de integração.

Para rodar o flutter test, basicamente temos que habilitar "Enable Flutter test" e trazer o "Flutter test arguments". Uma vez que salvamos, já temos todo o nosso processo de teste integrado dentro do nosso projeto e podemos rodar.

Como já tínhamos lincado, podemos escolher qual branch queremos rodar, qual é o workflow, e isso vamos abordar um pouco melhor nas aulas seguintes para entender como funciona. Definidas as configurações, conseguimos fazer o "Start new build" para rodar o CI. Faremos isso manualmente, mas não se preocupe que logo aprenderemos a rodar de forma integrada.

Após começar a rodar, ele vai passar por todas as etapas, o que pode demorar um tempo, então vamos pular para o momento em que o teste foi executado. Temos o final, após ter rodado todo o processo, passando por algumas etapas.

Ele vai preparar a máquina; pegar os dados do app, fazendo um git clone; instalar os SDKs, garantindo que o Flutter está bem instalado e que está tudo funcional; instalar as dependências, executando um flutter packages pub get; e depois disso, ele começa o processo de teste, passando por toda a questão dos testes em que tínhamos quatro arquivos, e a partir disso trazendo um resultado. Foi garantido que ele passou por 14 testes, então deu tudo certo e ele finalizou.

Conclusão
Já temos todo o processo configurado, porém, ainda não temos um CI, porque só garantimos que os testes e o flutter analyze estão rodando.

Precisamos garantir, a partir de agora, que ele vai estar integrado com nosso repositório, para que quando houver alterações, por exemplo, quando alguém quiser subir uma branch ou fazer um pull request, isso seja rodado de maneira automática, para garantir que nenhum teste vai estar quebrado e que vamos estar com alto nível de qualidade.

É isso que vamos abordar no próximo vídeo. Vamos lá!

@@04
Automatizando o processo de CI

De volta à configuração na tela do Codemagic, vamos seguir o processo. Já configuramos todas as etapas, os testes, a questão de rodar o Analyze, mas eles ainda não estão integrados continuamente no nosso projeto. Eles estão presentes, mas se não apertarmos o botão, não vão rodar. Então, precisamos fazer essa configuração para realizar a integração contínua, porque até agora não temos isso, apenas preparamos o ambiente para ela.
Integrando as etapas ao CI
Realizar a integração contínua com o Codemagic é bem simples. A primeira coisa que precisamos fazer é definir qual será o gatilho (trigger). Trata-se da primeira etapa "Build triggers", que é a maneira como o Codemagic vai ouvir o projeto no GitHub e garantir que tudo funcione corretamente.

Por exemplo, se houver um pull request, um merge ou qualquer outra ação, o Codemagic ouvirá e, conforme definirmos, ele vai rodar. Se não configurarmos isso, teremos problemas e precisaremos rodar manualmente.

Nesse caso, vamos definir o trigger como "Trigger on pull request update", que vai ouvir todas as alterações em pull requests. Então, se abrirmos um pull request para a main ou fizermos um novo commit, ele estará ouvindo a partir do momento que tivermos um pull request.

Uma vez definido o gatilho, precisamos definir quais branches vamos ouvir. Podemos ouvir todas as branches deixando um asterisco (*) como padrão, ou podemos especificar, como apenas ouvir para a branch main, por exemplo. Depende de como está configurado no projeto. No nosso caso, vamos ouvir todas as branches, mas mais adiante, conseguiremos definir situações específicas e você observará na prática, ouvindo diferentes branches e criando diferentes workflows.

Após salvar essa alteração, o Codemagic vai fazer uma configuração no GitHub para poder ouvir essas mudanças. É importante saber disso, porque se o Codemagic não tiver permissão para configurar isso automaticamente, você precisará fazer manualmente, configurando o webhook do Codemagic.

Na tela inicial do GitHub, iríamos em "Settings", na seção de "Webhooks". Se o Codemagic estiver integrado diretamente com o GitHub e tiver as permissões, ele configurará o webhook automaticamente. Caso contrário, teremos que adicionar o webhook, colar o link copiado das configurações do Codemagic e definir os eventos que ele poderá ouvir, como "Branch or tag creation", "Pull requests" e "Pushes".

Agora que o trigger está definido, toda vez que houver um pull request update, o Codemagic executará. Teoricamente, nosso primeiro CI está configurado, mas precisamos verificar se isso funcionará na prática.

Vamos abrir o VS Code para fazer alterações no código, criando uma branch chamada fix/remote-unit-test. Vamos quebrar os testes para abrir um pull request e observar o Codemagic rodando integrado continuamente.

Abrindo a pasta "test > widgets", vamos acessar o arquivo draw_form_test.dart, e no teste que verifica se o nome correto foi selecionado, mudaremos para clicar no nome "Alice2" (find.text('Alice2')), que não existe no projeto, causando um erro.

draw_form_test.dart:
// Enter a selected option in the Dropdown
await tester.tap(find.byType(DropdownInputWidget));
await tester.pumpAndSettle();
await tester.tap(find.text('Alice2'));
await tester.pumpAndSettle();
COPIAR CÓDIGO
Após salvar e rodar o testWidgets(), ele quebra, e temos a certeza de que isso causará um erro. Faremos um commit com a mensagem "fix: break widget test", publicaremos a branch e voltaremos para o GitHub.

No canto superior direito, teremos a opção "Compare and pull request". Ao abrir, podemos verificar as alterações e, nesse cenário, quando for criado o pull request, o Codemagic deverá executar automaticamente. Ele vai aparecer no GitHub e nem habilitará a opção de fazer o merge, porque primeiro executa.

Uma vez que falhar, o CI identificará um problema no código e não permitirá o merge. No Codemagic, podemos acompanhar isso em tempo real na opção "Builds" do menu lateral esquerdo. Ele vai preparar a máquina, pegar os app sources, instalar o SDK, instalar todas as dependências e rodar. Esse processo demora um pouco, e ao final ele falha. No GitHub, teremos a informação de que todos os cheques falharam e não é possível fazer o merge.

Se voltarmos ao VS Code e corrigirmos o erro de "Alice2" para "Alice", que é o formato correto, e subirmos essa correção, o CI rodará todo o processo para verificar se está tudo correto. Como ele monitora todas as atualizações do pull request, ele executará novamente o Default Workflow.

Agora, como a correção foi feita corretamente, ele habilitará o merge na branch. No Codemagic, também estará executando e mostrará que o primeiro deu erro e o segundo teve sucesso. Todos os testes passaram e tudo funcionou bem. No GitHub, também passou tudo e temos a opção de fazer o merge.

Conclusão
Com isso, já verificamos a confiabilidade do processo de CI. Por mais que ainda seja simples e esteja rodando tudo automaticamente, é um processo que garante uma boa qualidade para nosso projeto. A cada alteração, ele garante que não temos nenhum problema no código, que os testes estão passando e que não vamos subir nada que quebre o projeto.

Ainda falta configurarmos os testes de integração, que são um pouco mais complexos e exigem o uso de um emulador. É isso que vamos abordar na próxima aula!

@@05
Comandos no CI

Você está configurando um fluxo de CI para um projeto Flutter no Codemagic. Um dos requisitos é definir os comandos para executar testes unitários e testes de widgets no seu projeto.
Qual das seguintes alternativas representa corretamente os comandos a serem definidos para executar esses testes no Codemagic?

flutter test para rodar ambos, tanto testes unitários, quanto testes de widgets.
 
O comando flutter test, executa ambos os tipos de testes, tanto unitário, quanto de widget.
Alternativa correta
flutter test -all para rodar ambos, tanto testes unitários, quanto testes de widgets.
 
Incorreto, o comando –all, não é aplicativo nos testes para definir que deve-se executar todos juntos.
Alternativa correta
flutter test para testes unitários e flutter test widget para testes de widgets.

@@06
Faça como eu fiz

Até agora, você aprendeu como fazer a configuração de um processo básico e estruturado para um fluxo de CI estruturado e sincronizado com o seu repositório Git.
Agora é com você, faça a configuração do seu projeto e garanta que será acionado sempre que houver atualização/abertura em um pull request para uma branch do projeto.

Após o cadastro do projeto, inicie o processo de configuração, passando pelas seguintes etapas:
Em ‘Build for platforms’ selecione a opção ‘run tests only’.
Depois em ‘build triggers’ em ‘Automatic build triggering’ selecione a opção ‘Trigger on pull request update’ e em ‘Watched branch patterns’ deixe o ‘source’ como *, que irá ouvir todas as ações.
Por fim, na aba de testes, ative o ‘Static code analysis’ e ative o ‘Flutter test’, passando corretamente os argumentos.
Prontinho, agora é só executar em ‘Start New Build’ para vermos a CI executando o que configuramos. Você pode também, validar ao abrir um PR, que deve rodar o processo automaticamente.

@@07
O que aprendemos?

Você aprendeu como fazer uma configuração inicial de um processo de CI para seu aplicativo. Vamos revisar?
Configurando as etapas: Precisamos garantir que os testes e a análise serão executados, então entramos no projeto, dentro do codemagic e ativamos o static code analysis e também a execução do flutter test, importante ressaltar que devemos revisar os comandos gerados pelo codemagic e alterar caso não esteja adequado ao seu projeto.
Automatizando o processo: Agora, vamos integrar as etapas antes definidas, para garantir que será adequado ao fluxo de trabalho. Para tal, devemos abrir a aba build triggers do codemagic e ajustar os gatilhos que se adequem ao seu contexto, na aula, optamos por utilizar o trigger on pull request update para todas as branchs, para assim executar o fluxo sempre que houver alguma alteração dentro de um pull request.
E já já, vamos elevar ainda mais a régua de CI, te vejo lá!