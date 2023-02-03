# UiPath StudioX

![](imgs/rpa2.png)

## Interface

![](imgs/uipath_imgs/interface_i.png)
![](imgs/uipath_imgs/interface_ii.png)
![](imgs/uipath_imgs/interface_iii.png)
***

## Anatomia de uma Atividade

Atividades são os blocos de construção da automação. É um grupo de instruções que o robô segue para performar a tarefa. O Studio e StudioX usam atividades para montar a automação

No StudioX existem 2 tipos de atividades, cada uma com seus próprios propósitos 

**Recursos ↓** 

São as atividades que dizem ao robô que aplicativo usar. Essas são aplicativos dedicados, como Office apps, ou genéricos

Quando são dedicados, é necessário especificar o documento ou conta de email para que possam ser usados na automação

![](imgs/uipath_imgs/recursos.gif)

O genérico Application/Browser serve para indicar outros aplicativos e navegadores. Para indicar um aplicativo, ela já deve estar aberta (rodando)


**Ações ↓**

São atividades que dão ao robô instruções do que fazer com os recursos. São agrupados de acordo com o propósito do aplicativo

![](imgs/uipath_imgs/acoes.gif)

Algumas ações dependem do recurso. Como exemplo, não se pode usar ações do Word em um arquivo Excel. As exceções são as ações comuns que podem ser usadas em qualquer aplicativo e as ações de arquivo que não precisam de um recurso

As ações são nomeadas baseado nas ações comuns que performam em certas aplicações

![](imgs/uipath_imgs/recursos_x_acoes.gif)

### Diferença entre Step, Task and Process

**Steps (passos) →** é uma ação necessária para completar um propósito específico e bem definido

ex: baixar uma planilha 

**Tasks (tarefas) →** sequência de steps realizados por operador (humano/manual, robô/automatizado)

ex: juntar dados de 2 arquivos diferentes e salva em um novo arquivo numa pasta local

**Processes (processos) →** múltiplas, inter-relacionadas tarefas constroem um processo que almeja alcançar um objetivo maior. Pode ser um grupo de ambas tarefas automatizadas e manuais

ex: requisição de compra que precisa de múltiplos sistemas e requer validação humana para enviar 

***

## HumanPath para RobotPath

Framework que ajuda a organizar a tarefa de uma maneira visual. Também ajuda há traduzir a tarefa para o que é conhecido como "robot language" (linguagem do robô)

**HumanPath →** visualização high-level de tarefa em uma maneira sequencial

**RobotPath →** visualização detalhada, esta moldando o design dos steps que o robô leva para automatizar a tarefa

**Vantagens:**

- Quebra o processo em pequenos passos lógicos
- Ajuda a moldar o escopo do que se quer construir
- Outlines pontos de decisões-chave e cenários de tarefas de automação
- Serve para guiar na construção do robô 

### Como usar?

**HumanPath**

![](imgs/uipath_imgs/humanpath.gif)

- A tarefa deve sempre começar com um **Start**
- Tudo deve estar conectado com flechas, não deixe nada independente
- Cada passo deve ter uma etiqueta de aplicativo, indicando onde cada ação acontece
- Todo começo tem um final, termine o flow com um **END**


**RobotPath**

![](imgs/uipath_imgs/robotpath.gif)

- Deve começar de mesma forma que o HumanPath, com um **Start**
- Tudo deve estar conectado com flechas, não deixe nada independente
- Ás vezes o robô tem que tomar decisões entre 2 ou mais opções, dependente de uma condição de verificação, ou repetir ações para certo item
- Cada passo deve ter uma etiqueta de aplicativo, indicando onde cada ação acontece
- Quebre cada passo a nível de clique. Todo passo deve ser precisamente definido e só pode ter um significado
- Os passos devem seguir uma ordem específica. Uma falha na ordem significa um resultado provavelmente incorreto
- Todo começo tem um final, termine o flow com um **END**

[Template para construir ambos os caminhos](HumanPath%20-%20RobotPath%20Templates%20-StudioX.pptx)

***

## User Interface

É uma série de telas, páginas e elementos visuais - como botões e campos de input - que permitem a interação com o aplicativo. StudioX, por meio de seu pacote de atividades, imita a forma como o usuário interage com as aplicações e reconhece os elementos da interface independente de posição, resolução ou tamanho de fonte 

Todas as interações com o UI podem ser divididas em input (enviar ou adicionar algo o aplicativo) e output (obter algo do aplicativo). Clicar um botão e escrever em uma caixa de texto são exemplos de input, já obter o texto de uma página no navegador é um exemplo de output

No StudioX há 2 maneiras de se automatizar um processo:

- Adicionando atividades passo-a-passo
- Utilizando o recurso "Web/App Recorder" para gravar as ações do usuário

![](imgs/uipath_imgs/recorder.gif)

O gravador só irá funcionar em automações da Interface do Usuário. Não irá funcionar em tarefas que envolvem Excel, Email, Word ou automação de arquivos e pastas.

Atividades input veem com uma propriedade chamada **Input Mode**

### Input Mode

Algumas automações tomam controle do mouse, então impedindo que o usuário possa usar o computador. Para que os projetos possam ser executados em background, sem que afete o uso do computador, é necessário mudar o modo de input no painel de propriedades. Há 2 tipos:

- **Hardware Events →** simulam a ação usando o driver de hardware. É o método mais lento, não pode ser executado em segundo plano, mas é compatível com todos os desktop apps e é o modo padrão
- **Simulate →** simula o modo input da maneira mais rápida e funciona em segundo plano, mas é limitado para certas situações. Por exemplo, só funciona com clique simples (mouse esquerdo) ou se o texto para digitar não inclui caracteres especiais

![](imgs/uipath_imgs/input_mode.gif)

- **Same as App/Browser →** implica que a ação irá usar o mesmo modo de input do recurso Use Application/Browser em que está inserido

***

## Unified Target

É um framework para UI Automation. Atividades como clicar, digitar e, mais importante, localizar os elementos corretamente na tela, estão aprimorados pelo método de unificação de segmentos dos elementos UI para automação

Usando um framework unificado todos os métodos apoiam uns aos outros para maior confiabilidade, assim pode-se garantir que o robô irá superar qualquer roadblock causado por pontos fracos na seleção de elementos UI 

**UI Frameworks**

Por padrão, um proprietary framework é usado para acessar os segmentos da janela do aplicativo, no entanto, se a segmentação não é detectada, StudioX tem 2 alternativas:

- **Active Accessibility →** para aplicativos mais antigos
- **UIA (Microsoft UI Automation →** para aplicativos mais novos

![](imgs/uipath_imgs/ui_frameworks.gif)

Depois de selecionar um segmento, a opção para mudar de framework não estará mais disponível

### Debugging & Troubleshooting

![](imgs/uipath_imgs/target_confg.png)

**Check App State**

É útil para situações onde se quer checar se o aplicativo que irá automatizar existe

![](imgs/uipath_imgs/target_troubleshooting.png)

Pense em abas diferentes em um aplicativo ou navegador. Quando se está adicionando atividades para o workflow, é necessário ter certeza de que se está selecionando os elementos ou abas corretas. Além disso, caso um elemento não seja encontrado é possível adicionar outro conjunto de atividades para serem executadas

![](imgs/uipath_imgs/check_app_state.png)

O tempo para achar o elemento antas da execução da próxima atividade pode ser alterado na opção **Wait For It**


**Show All Matches**

É usado para encontrar todas os matches para o elemento selecionado no aplicativo

![](imgs/uipath_imgs/show_all_matches_i.png)
![](imgs/uipath_imgs/show_all_matches_ii.png)

**Image Selection Mode**

É útil para selecionar um segmento ou âncora que não está disponível em um único clique

![](imgs/uipath_imgs/image_selection.png)
![](imgs/uipath_imgs/image_selection_confg.png)

***

## Word (office) Automation

Alguns capacidades de automação com o Word são:

- Substituir fotos e textos
- Adicionar fotos, anexar textos no final do documento, inserir tabelas em posições especificas relativas ao texto ou um marcador e definir marcadores de conteúdo
- Exportar como PDF ou usar para preencher emails

Para substituir fotos é necessário indica-las pelo seu texto alt. Ao contrário do Excel não se pode indicar os elementos do Word diretamente pelo Ui Path, é preciso escrever a referência do que se vai mudar
