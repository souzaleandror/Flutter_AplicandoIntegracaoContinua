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

#### 29/01/2024

@03-Testes de integração no Codemagic

@@01
Projeto da aula anterior

Antes de continuar é importante que tenha feito a configuração do projeto no Codemagic que foi levantado nas últimas duas aulas, agora vamos seguir o processo, configurando mais uma etapa para nosso processo de CI.

@@02
Testes de integração

Daremos continuidade à nossa integração contínua. Na aula passada, já fizemos todo o processo de configuração da integração contínua em um fluxo bem básico, onde sempre que temos uma alteração no PR, rodamos um fluxo para validar apenas o flutter analyze e o flutter test.
No entanto, precisamos avançar um pouco mais. E aí, entra a questão dos testes de integração.

Por quê? Já estamos executando o flutter test, que roda os testes de widgets e os testes unitários. Mas, dentro das configurações dos projetos, também fazemos configurações dos testes de integração para garantir que o aplicativo está funcionando integralmente após todas as alterações.

Como fazemos isso no CI? É justamente isso que vamos aprender agora.

Antes de passar para o Codemagic, queremos apresentar como funciona o teste de integração.

É muito importante ressaltar que na Alura já temos um curso de testes de integração com Flutter. Se você está nunca fez, indicamos conferir esse conteúdo.
Entendendo os testes de integração
Antes de começar a configuração desse processo no fluxo de integração contínua, vamos abrir o VS Code com o projeto que estamos trabalhando e reiniciar o emulador.

Dentro do projeto, temos a seguinte estrutura: o diretório "test_driver" com o arquivo integration_test.dart que é um setup básico para os testes de integração. Esse arquivo para fazer o setup corretamente é um padrão para todos os testes de integração que você for fazer.

integration_test.dart:
import 'package:integration_test/integration_test_driver_extended.dart';

Future<void> main() async {
  integrationDriver();
}
COPIAR CÓDIGO
Também temos a pasta "integration_tests". Lembra que a pasta de testes unitários de widgets fica dentro de "tests", enquanto os testes de integração ficam dentro de "integration_tests".

app_test.dart:
void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();
  WidgetsFlutterBinding.ensureInitialized();

  testWidgets('E2E - All app flow', (WidgetTester tester) async {
    // Scenario 1: Check initial state in HomeFormWidget
    await tester.pumpWidget(const MyApp());
    expect(find.byType(HomeFormWidget), findsOneWidget);

// restante do código omitido…
}
COPIAR CÓDIGO
Confira o arquivo app_test.dart completo localizado na pasta "integration_test".
No nosso caso, vamos testar todas as funcionalidades ponta a ponta, ou seja, realizar o teste end-to-end. Assim, podemos pegar desde a hora de iniciar o app até o último comportamento.

Podemos fazer isso como um teste end-to-end, mas também podemos configurar cenários específicos. Por exemplo, ele vai entrar e funcionar com determinada seção, depois vai fazer outro teste. Você pode ir separando em arquivos ou testes diferentes. Fique à vontade.

Como nosso projeto é bem simples, decidimos fazer um teste end-to-end porque são só duas telas e vai passar tela a tela. Vamos entender o funcionamento desse teste.

No primeiro cenário, vamos abrir o MyApp(), verificar se carregou corretamente o HomeFormWidget, verificar se os textos estão aparecendo, trazer algumas configurações de botões, inserir texto e implementar ações. Tudo isso tem que funcionar.

Dica: Se você foi fazer teste de integração, é necessário se atentar aos dispositivos a serem utilizados. Isso é válido não apenas para testes de integração, mas sempre que estiver programando em Flutter.
Afinal, cada dispositivo tem um tamanho diferente. Por exemplo, o iPhone SE é muito diferente do iPhone 15. Eles têm necessidades de pixels e tamanhos diferentes. Portanto, é importante debugar, fazer testes e correções para garantir que seu aplicativo funcione tanto no menor quanto no maior dispositivo.

Por exemplo, um dispositivo utilizado dentro do Codemagic é um iPhone SE, que é um dispositivo pequeno. Por isso, preste muita atenção, porque às vezes o que funciona em um dispositivo não funcionará em outro.

Agora que iniciamos o emulador do Galaxy Nexus, vamos rodar os testes para verificar se estão funcionando. Depois vamos levar para o CI.

No terminal integrado, existem duas formas de rodar os testes de integração.

A primeira, que é a forma mais antiga, é usando o flutter drive. Você vai definir o comando flutter drive seguido de --driver indicando o caminho do driver desse teste. Na sequência, você coloca --target para indicar o target onde está o teste. Nesse caso, está dentro da pasta "integration_test", em app_test.dart.

flutter drive --driver=test_driver/integration_test.dart --target=integration_test/app_test.dart
COPIAR CÓDIGO
Esse era o modo antigo. Ainda é utilizado e funciona para rodar os testes de integração no Chrome. Mas para o iOS e para o Android, temos um novo comando simplificado pelo Flutter.

Agora vamos executar os testes de integração para visualizá-los no emulador. Para isso, vamos digitar o seguinte comando:

flutter test integration_test
COPIAR CÓDIGO
Após colocar para executar, vamos abrir o emulador. Vai demorar alguns segundos para fazer a build, pois tem que compilar o APK, configurar os cenários, fazer uma configuração bem específica no nativo para rodar todas as atividades.

Esse tempo de demora para rodar na sua máquina também acontece quando for rodado dentro do Codemagic. Inclusive, o Codemagic demora até um pouco mais. É preciso levar isso em consideração, porque impacta diretamente no custo da aplicação.
Após compilar, os testes vão começar a rodar. Ele vai abrir o app, clicar na caixa de texto, inserir alguns nomes, depois adicionar e remover um nome e, por fim, fazer o sorteio. Ou seja, vai testar tudo, um por um, para verificar se está funcionando.

01:01 +1: All tests passed!
Ele informou que todos os testes passaram e não tivemos problemas.

Basicamente é assim que funcionam os testes de integração localmente. Agora vamos passar isso para o Codemagic para poder rodar esse fluxo também durante as nossas alterações. É isso que faremos a seguir.

@@03
Aplicando os testes de integração no CI

Já estamos logamos no Codemagic e vamos iniciar o setup.
Testes de integração no CI
Eu sei que você já deve imaginar onde vamos configurar o integration test. Vamos abrir a aba de "tests", onde já temos a opção de setup de "Integration and unit tests".

Ao abrir o "Integration and unit tests", tínhamos configurado apenas o "Flutter test" na última aula. Portanto, ele estava rodando apenas o flutter test. Mas a partir de agora, vamos ativar também o flutter driver tests.

Para isso, você tem que marcar essa checkbox "Enable flutter drive test". Daí, você deve trazer o flutter drive arguments. Como explicamos anteriormente, existem duas maneiras de fazer isso.

Podemos utilizar o drive --driver igual ao driver e também --target igual ao o endereço do app_widget.test.

drive --drive=integration --target=app_widget.test
COPIAR CÓDIGO
Mas, nesse caso, indicamos utilizar esse comando apenas se você for rodar os testes de integração no Chrome.

Caso não seja no Chrome, caso você queira rodar mesmo no dispositivo emulado, você pode rodar o outro comando, que é o flutter test integration_test.

test integration_test
COPIAR CÓDIGO
Além disso, você vai selecionar a opção "iOS simulator" para poder rodar esses testes. Lembrando que o iOS simulator usualmente utiliza o iPhone SE, que é um iPhone de proporções pequenas. E isso pode impactar diretamente nos seus testes.

Não adianta você construir no iPhone 15, fazer todos os seus testes de integração no iPhone 15 e querer rodar o teste no iPhone SE sem tê-lo testado antes.

Isso serve tanto para a sua aplicação, para garantir que está tudo funcionando dentro da sua aplicação no CI, quanto para quando você for entregar para o cliente. Porque não tem como saber qual o tamanho de celular que as pessoas vão utilizar.

É muito importante que você se adeque e garanta que o layout do seu aplicativo vai estar responsivo para quase todos os tamanhos.

Finalmente, clicamos em "Save changes". Desse modo, já está configurando os testes de integração para os nossos fluxos de CI.

Antes, para visualizar o funcionamento como fizemos no vídeo anterior, devemos abrir o VS Code e quebrar o nosso teste de integração.

Em app_test.dart, na primeira verificação dos elementos de interface do usuário, ele espera encontrar o texto "vamos começar", usando o expect().

Vamos mudar o texto e pedir para ele procurar o "vamos começar", trocando a letra "Ç" por "C".

E aí ele vai ter que procurar esse texto. Como ele não vai encontrar, ele tem que dar um erro que deve ser avisado no processo de CI.

app_test.dart:
// Check the presence of UI elements
expect(find.text('Vamos comecar!'), findsOneWidget);
COPIAR CÓDIGO
Vamos salvar e criar uma nova branch no VS Code. Em "Source Control" (ou atalho "Ctrl + Shift + G"), vamos em "Create new branch" para criar uma branch fix/breaking_integration_test.

Após criar a branch, vamos clicar no ícone de "+" para fazer o commit com a mensagem fix: breaking integration tests. Vamos clicar em "Commit" e, em seguida, "Publish branch".

Depois de publicar a branch, vamos voltar no navegador, abrir o GitHub e criar um pull request dessa nossa branch para a main, clicando no botão "Compare & pull request".

A única correção é a alteração do texto. Vamos clicar em "Create pull request", e automaticamente, a partir de agora, o Codemagic vai ter que executar o fluxo de CI que acabamos de definir.

Além de rodar o flutter analyze e o flutter test, ele vai ter que rodar os testes de integração. No Codemagic, vamos acessar a aba de "builds" dentro do projeto para acompanhar a execução.

Agora que o processo de CI foi executado, como tínhamos quebrado o nosso teste, ele deu erro. Aparece uma mensagem em vermelho no Codemagic:

Test run failed: Flutter Drive run failed.
Enquanto no PR do GitHub, também vai dar falha e não vai habilitar o botão para fazer o merge automático.

All checks have failed
Verificando logs
No Codemagic, você pode abrir o teste para visualizar os logs e entender o que aconteceu. Desse modo, sabemos que ele passou por todos os testes do flutter test, porém, ele deu erro no flutter drive.

Se você clicar em app_test.dart, será indicado que o erro ocorreu justamente no nosso fluxo E2E (end-to-end).

Na aba "log", você consegue identificar sobre o que foi o erro. Você clicar em "Show the last 50 lines" para carregar o log completo. Nas últimas 15 linhas, vamos verificar onde que ele quebrou.

> flutter -d 4703F852-5C8D-4025-8DFF-153596687231 test --machine integration test
("protocolVersion":"0.1.1", "runnerversion":"1.24.3", "pid":1909, "type":"start","time":0}
("suite":{"id":0,"platform":"vm","path":"/Users/builder/clone/integration_test/app_test.dart"),"type":"suite", "time":0)
("test":{"id":1,"name":"loading /Users/builder/clone/integration_tent/app_test.dart", "suiteID":0,"groupIDs":{},"metadata":
("skip": false, "skipReason":null), "line":null,"column"mill, "url":null},"type":"testStart", "time":0)
{"count":1,"time":3,"type":"allSuites")
Updating project for XCode compatibility.
Upgrading project.pbxproj
Upgrading Runner.xcscheme
Running pod Install... 901 ms
Running Xcode build...
Xcode build done. 29.6s

[{"event":"test.startedProcess", "params":{"vmServiceUri":"http://127.0.0.1:49366/d71FlCs2_4Y=/", "observatoryUri":"http://127.0.0.1:49366/d71FlCs2_4Y=/")}}
("testID":1,"result":"success","skipped":false,"hidden":true,"type":"testDone","time":38911)
{"group":{"id":2,"suiteID":0,"parentID":null,"name", "", "metadata": {"skip": false, "skipReason":null), "testCount":1,"line":null, "column":null,"url":null),"type":"group","time":38913)
("test":{"id":3,"name":"E2E - All app flow","suiteID":0,"groupIDs":[2],"metadata":
("skip": false, "skipReason":null),"line":148,"column":5,"url":"packager:flutter_test/src/widget_tester.dart"), "type": "teststart","time":38919)
("testId":3,"messageType":"print", "message":"*******EXCEPTION CAUGHT BY FLUTTER TEST FRAMEWORKS************","type":"print","time":35552)
("testId":3,"messageType":"print", "message":"The following TestFailure was thrown running a test:","type":"print", "time":39552)
{"testId":3,"messageType":"print", "message":"Expected: exactly one matching node in the widget tree","type":"print", "time":39552)
("testID":3,"messageType":"print", "message":" Actual: _TextFinder:<zero widgets with text \"Vamos comecar!\" (ignoring offstage widgets)>","type":"print","time":39553]
COPIAR CÓDIGO
Vamos passar por todo o processo. Ele começa a rodar o comando na linha 49. Foi executando, buildou, começou a executar e na linha 65 deu um erro no framework. Por que deu um erro no framework? Ele esperava um texto "Vamos começar". Mas, ele não encontrou nenhum widget desse jeito.

Então, aconteceu exatamente o que esperávamos. Se alguém tivesse alterado o texto, que não deveria ser alterado, quebraria o nosso código.

Vamos voltar no VS Code e dar um "Ctrl+Z" para ajustar o teste. Agora vai estar funcional. Ao subir a alteração, dar o commit e sincronizar as mudanças, ele vai começar a executar novamente todo o processo de CI e agora ele vai passar.

Agora que já executamos o processo com o teste correto, ele passou tanto pelo Flutter Drive quanto pelo Flutter Test.

No issues found (ran in 6.4s)
No GitHub, vamos ter a confirmação que tudo passou e estamos aptos para fazer o merge da nossa branch.

All checks have passed
This branch has no conflicts with the base branch

Se você acompanhar o processo de teste, vai perceber que ele demorou pouco mais de 1 minuto e 32 segundos. Toda a duração de execução desse fluxo de CI demorou cerca de 3 minutos.

Pense nisso para todo o PR que estiver sendo feito. Isso acaba aumentando bastante o tempo que usamos do CI. Lembrando que o Codemagic tem uma limitação de 400 minutos por mês. Ou seja, conseguiríamos executar esse processo 100 vezes por mês. Essa quantidade é boa, mas vai depender do tamanho do time.

Por isso, existem estratégias que podemos utilizar para garantir e otimizar esse processo de CI. Assim, vamos garantir que vai passar por tudo antes de chegar na mão da pessoa usuária, além de otimizar esse processo. É isso que vamos aprender na próxima aula.

@@04
Para saber mais

Agora que compreendemos como configurar os testes de integração, é importante considerar alguns pontos essenciais para otimizar a eficiência desses testes. Dois aspectos cruciais que merecem nossa atenção são o tempo de execução dos testes e a escolha do dispositivo para sua execução.
Tempo para execução

Se os testes de integração não forem configurados de forma eficiente, eles podem se tornar excessivamente lentos, resultando em estouro do limite de tempo, atrasos no feedback ou até mesmo timeouts durante a execução do processo de CI.

Portanto, é fundamental manter os testes de integração rápidos e eficazes, para permitir sua execução regular no processo de CI, sem comprometer excessivamente o tempo.

Evitar a utilização excessiva de comandos como pumpAndSettle com Duration alto é uma das melhores práticas.

Escolha do dispositivo

Quando se trata de executar os testes de integração, temos a flexibilidade de escolher o dispositivo onde eles serão executados. Na aula, utilizamos um iPhone SE, mas poderíamos ter optado pelo Chrome ou configurado outro dispositivo que se adequasse ao contexto do nosso app.

Entretanto, ao selecionar os dispositivos para os testes, é recomendável considerar os mais comuns entre seus usuários, para garantir uma cobertura mais abrangente e ajudar a identificar bugs antecipadamente. Não adianta você testar no Iphone 15 e seus usuários utilizarem apenas Android, com certeza vai passar algo para o Android que não consegue identificar no Iphone.

Além disso, você pode escolher executar os testes em uma quantidade maior de dispositivos. Existem ferramentas que podem ser integradas ao Codemagic para facilitar essa abordagem, como o Firebase Test Lab.

Um artigo que pode ser útil nesse contexto é "Flutter integration test with Firebase Test Lab & Codemagic CI/CD", que explica como configurar essa ferramenta, leia o artigo aqui.

https://firebase.google.com/docs/test-lab?hl=pt-br

https://blog.codemagic.io/codemagic-flutter-integration-tests-firebase-test-lab/

@@05
Comandos para rodar os testes de integração

Você está implementando as etapas de CI para seu projeto e agora, falta apenas a última etapa, que seria adicionar o comando para executar os testes de integração.
Seguindo o que foi explicado na aula, qual é o comando correto para executar esses testes?

flutter test integrationtest
 
Correto, com as últimas correções nos testes de integração, o Flutter agora possibilita a execução utilizando o próprio comando nativo (test) para executá-los, apenas passando o texto integration test no final do comando.
Alternativa correta
flutter drive –driver=’driver'.dart’ –target=’target.dart’ –all
 
Incorreto, por mais que o comando flutter drive com os mesmos argumentos seja utilizado para também executar os testes de integração, o sufixo ‘–all’ não é necessário, o que torna a alternativa incorreta.
Alternativa correta
flutter test drive integrationtest
 
Incorreto, o comando flutter test drive não é utilizado para executar os testes de integração.

@@06
Faça como eu fiz

Finalizamos as configurações das etapas para estruturação do CI para nosso projeto, conseguimos finalmente configurar os testes de integração no Codemagic.
E agora, é com você, dando continuidade com o seu projeto, faça a implementação dos testes de integração e execute por meio de um PR, para verificar se funcionou.

Primeiramente, assegure-se de que seu projeto já possui os testes de integração. Caso ainda não tenha desenvolvido esses testes, aproveite a oportunidade para criá-los e elevar ainda mais a qualidade de seu aplicativo.
Após essa etapa, abra o codemagic, navegue até a aba de testes. Selecione a opção de “Integration and unit tests”, agora ative o “Flutter Driver Test” e defina os argumentos para execução. Se você seguiu o padrão definido pelo Flutter, pode utilizar apenas o test integration_test, que funcionará adequadamente.

Depois, salve e ative um dos gatilhos para executar o CI, você pode rodar tanto pelo “Start New build” do Codemagic quanto pelo gatilho que configuramos na aula anterior para execução automática.

https://codemagic.io/

https://docs.flutter.dev/testing/integration-tests?gclid=Cj0KCQiAo7KqBhDhARIsAKhZ4ujJPLNKy41Nm19my3eKZoRFlhpiVtGClgvZ-Z-rBLzPxgBfoLhYGhMaAqgYEALw_wcB&gclsrc=aw.ds

@@07
O que aprendemos?

Na aula, você aprendeu como configurar os testes de integração como uma etapa do processo de CI, vamos recapitular?
Testes de integração: Utilizamos esse tipo de teste para garantir que nossos aplicativos estejam funcionando de maneira integrada, mesmo com as alterações e para executá-los o Flutter possibilita, dois comando diferentes:
flutter test integration_test
flutter driver –driver=”caminho do driver” –target=”caminho do target”
Ambos funcionam, mas o Flutter tem mudado para centralizar apenas na primeira opção.

Implementação do CI: Compreendendo os comandos, fazer a configuração no CI fica bem fácil, apenas abrir a aba de testes e ativar a execução dos testes de integração, passando o argumento correto, prontinho, finalizamos a implementação.
Com isso, conseguimos finalizar toda essa parte de configuração de etapas do nosso processo de CI, porém, existem formas mais eficientes e performáticas de se trabalhar com ele e é isso que veremos na próxima aula, te vejo lá!