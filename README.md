

<i>Material recomendado pela <a href="https://github.com/appium/appium/tree/master/sample-code/python#tutorial">documentação oficial do Appium</a>.</i>
</div>

 
Este é um guia para o setup do ambiente de configuração e uso do Appium para automação de testes funcionais em dispositivos móveis: <i>&#128513;</i>

<ul>
    <li>Entender como funciona o framework Appium e como fazer o setup desta aplicação nas plataformas: Windows, Linux e Mac;</li>
    <li>Como instanciar um dispositivo Android emulado através do Android Studio;</li>
    <li>Como fazer mapeamento de elementos de uma aplicação em seu dispositivo;</li>
    <li>Como instalar um aplicativo da PlayStore em seu dispositivo emulado;</li>
    <li>Como iniciar testes de UI em sua aplicação através do Appium com a linguagem de programação Python;</li>
    <li>Conhecer sos e funcionalidades específicas do Appium.</li>
</ul>

___

🗂 **Seções:**
<ul>
    <li>Introdução</li>
    <li>Setup do ambiente</li>
    <ul>
        <li>Download de tudo que precisa</li>
        <li>Configuração Windows</li>
        <li>Configuração Linux</li>
        <li>Configuração Mac</li>
        <li>Setup simplificado para todos os SOs</li>
        <li>Instalação do Appium</li>
    </ul>
    <li>Appium Doctor: como validar se tá tudo configurado?</li>
    <li>Checklist</li>
    <li>Iniciando o Appium</li>
    <li>Comandos ADB</li>
    <li>Emulando um dispositivo Android através do Android Studio</li>
    <li>Recursos específicos do Appium</li>
</ul>

___

## Conhecendo métodos do Appium

Recursos e funcionalidades específicas do Appium. Os exemplos listados aqui serão em Python, mas quase todos os recursos usados aqui também existem em qualquer outra linguagem de programação que o Appium tenha suporte.

- Comandos sobre o dispositivo
- Interações
- Controle de recursos de rede
- Controle do sistema
___

Este tutorial foi criado pois para aprender essa ferramenta tive que recorrer a diferentes fontes. Espero que este documento seja muito útil pra você e te incentive a também compartilhar seu aprendizado <i>&#129304;</i>

___

# Um pouco sobre Appium

_Appium_ é uma ferramenta open-source e multi-plataforma (isso quer dizer que funciona em Windows, Linux e Mac) e cujo foco é de interações via UI em dispositivos móveis, possibilitando a automação de aplicações: nativas, híbridas e sites mobile para as plataformas Android e iOS.

Considero _Appium_ uma excelente ferramenta para quem quer começar a aprender automação em dispositivos móveis ou para quem já é da área de mobile e gostaria de se aprofundar mais sobre o assunto.


**Links importantes para esta seção:** <i>&#129304;</i>

[Página oficial do Appium](http://appium.io)

[Página oficial do repo do Appium no GitHub](https://github.com/appium/)

A finalidade do Appium é testar aplicações em dispositivos móveis, e aplicações podem ser classificadas em três diferentes naturezas : nativas, híbridas e móveis.

  - **Nativas:** aquelas aplicações que foram desenvolvidas especificamente para Android ou iOS, ou seja, a partir de seus específicos SDKs.
  - **Híbridas:** aquelas que são desenvolvidas em HTML, CSS, JavaScript e que são compatíveis com qualquer plataforma (Android, iOS, Windows).
  - **Móveis:** aquelas que podemos acessar através de um link, via página web.

___

Vamos lá ver os passos para realizarmos o setup do ambiente para Windows, Linux e Mac. 

✨ **Dica muito importante:**

Você também pode optar por uma configuração mais simples e que vai te poupar de muito tempo, Caso deseje pode pular direto para o tópico "Forma simplificada para Windows/Linux/Mac". O mesmo procedimento é utilizado para qualquer sistema operacional.

# 📥 Download do necessário

Vamos utilizar algumas ferramentas essenciais para a prática de automação. Baixe e instale as seguintes ferramentas, que são comuns para Windows, MAC ou Linux:
  - **Appium Desktop:** é a interface da ferramenta Appium que será o foco do nosso tutorial. O download está [disponível aqui:](https://github.com/appium/appium-desktop/releases/) (aqui tem um acervo para vários Sistemas Operacionais. Baixe apenas aquele que for direcionado para o seu SO.)
  
  - **JDK (JAVA Development Kit):** https://www.java.com/pt_BR/download/ 

  - **Android Studio:** é um pacote do Android Studio que possibilita que possamos instanciar dispositivos móveis de várias configurações e modelos de forma emulada e em vários níveis de API. Para isso, é preciso baixar o Android Studio e, durante o setup, marcar a opção de instalar também o AVD: https://developer.android.com/studio/index.html?hl=pt-br

  
  Depois de fazer o download de todo o conteúdo, agora podemos avançar com o setup do ambiente. Podemos configurar as variáveis de ambiente à nível de sistema (abaixo eu deixo detalhado como fazer para cada SO) e também podemos fazer de maneira bem mais simplificada, onde explico melhor após o detalhe de setup para cada SO.
  
# Variáveis de ambiente - Mac:

Feito as devidas instalações é hora de configurarmos as variáveis de ambiente para que seu sistema operacional identifique os processos  e as aplicações de forma mais rápida e prática.
Para isso, abra o seu terminal, identifique a localização de instalação dos pacotes e os exporte para a variável PATH.
Após identificar a localização de onde foi instalado o seu Android, copie o caminho da pasta.
Por exemplo, para macOS a localização normalmente fica em:

```bash
/Users/user_name/Library/Android/sdk
```

Então será a partir desta pasta que vamos identificar os outros caminhos necessários, como:
```bash
/Users/user_name/Library/Android/sdk/platform-tools
/Users/user_name/Library/Android/sdk/tools
/Users/user_name/Library/Android/sdk/build-tools
```

Quando você identificar estes caminhos em sua máquina, é hora de exportar esses valores para a variável PATH.
Para isso, confira se no diretório "/Users/user_name" existe o arquivo ".bash_profile".
Caso não exista, crie:
```bash
touch .bash_profile
```

O próximo passo é abrir o editor de texto do arquivo:
```bash
open -e ~/.bash_profile
```

Digite os comandos como sugere o exemplo a seguir e salve o arquivo:
```bash
export ANDROID_HOME=/your/path/to/Android/sdk 
export PATH=$ANDROID_HOME/platform-tools:$PATH 
export PATH=$ANDROID_HOME/tools:$PATH 
export PATH=$ANDROID_HOME/build-tools:$PATH 
export JAVA_HOME=/your/path/to/jdk1.8.0_112.jdk/Contents/Home 
export PATH=$JAVA_HOME/bin:$PATH
```

# Variáveis de ambiente - Windows:
Após o download "link acima" e instalação do JDK do seu ambiente Windows, é hora de configurar as variáveis de ambiente. Para isso, siga as opções de menu:
1- Propriedades do Sistema >> Configurações avançadas do sistema >> Variáveis de ambiente >> Variáveis de usuário >> Novo.
2- Insira o nome da variável como "JAVA_HOME" e insira como valor a localização exata do seu arquivo jre, por exemplo, "C:\Arquivos de Programa\Java\jdk1.2.2_2\jre".
3- Na seção de variáveis de sistema, dê um clique duplo em "Path" e adicione a expressão "%JAVA_HOME%\bin". Isto significa que você está adicionando o mesmo valor criado para JAVA_HOME, só que também para a pasta \bin.
4- É só clicar OK e aplicar as mudanças de configuração.

Agora baixe "link acima" e instale o Android SDK, siga os passos:
1. Siga o mesmo passo #1- descrito acima até alcançar o campo de variáveis de ambiente.
2. Agora, insira o nome da variável como "ANDROID_HOME" e insira como valor a localização exata onde seu Android SDK foi instalado, por exemplo, "C:\android-sdk".
3. Agora, mais uma vez precisamos adicionar o valor da sua nova variável à sua variável global do sistema, que é o Path: "%ANDROID_HOME%\platform-tools" e também "%ANDROID_HOME\tools%".
4. É só clicar OK e aplicar as alterações.

# Variáveis de ambiente - Linux:
A configuração de variáveis de ambiente para Linux é muito semelhante a do Mac. Basta que vc identifique o caminho exato de instalação do JDK e do Android e aplicar (através de export) os caminhos no seu arquivo de configuração global, que neste caso é o ~/.bashrc

Por exemplo, para Linux a localização normalmente fica em:

```bash
/Users/user_name/Library/Android/sdk
```

Então será a partir desta pasta que vamos identificar os outros caminhos necessários, como:
```bash
/Users/user_name/Library/Android/sdk/platform-tools
/Users/user_name/Library/Android/sdk/tools
/Users/user_name/Library/Android/sdk/build-tools
```

Quando você identificar estes caminhos em sua máquina, é hora de exportar esses valores para a variável PATH, como sugere o exemplo a seguir:

```bash
export ANDROID_HOME=/your/path/to/Android/sdk 
export PATH=$ANDROID_HOME/platform-tools:$PATH 
export PATH=$ANDROID_HOME/tools:$PATH 
export PATH=$ANDROID_HOME/build-tools:$PATH 
export JAVA_HOME=/your/path/to/jdk1.8.0_112.jdk/Contents/Home 
export PATH=$JAVA_HOME/bin:$PATH
```

✨ **Dica muito importante - Windows/Linux/Mac:**
Para identificar onde está a sua pasta para JAVA_HOME, é só usar o seguinte comando no terminal:
```bash
which java
```
Deverá ser retornado o caminho até seu pacote JAVA.

✨ **Dica muito importante - Linux/Mac:**
Para evitar que suas variáveis de ambiente percam os valores, salve o conteúdo da variável no seu arquivo bashrc (Linux) ou bash_profile (macOS). Após salvar os valores, não esqueça de "compilar" o arquivo para as mudanças serem refletidas:
Para macOS:
```bash
source ~/.bash_profile
```

Para Linux:
```bash
source ~/.bashrc
```

# Forma simplificada para Windows-Linux-Mac
Caso deseje simplificar a sua configuração de ambiente, é só utilizar o atalho de configuração do Appium e inserir manualmente os caminhos para as suas variáveis ANDROID_HOME e JAVA_HOME. Esta etapa é bem mais simples. Basta seguir os passos adiante:

Abra sua ferramenta Appium Desktop e clique no botão "Edit Configurations".
<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/1.png">
</p>

Ao clicar em "Edit Configurations", uma nova janela vai abrir com 2 campos: ANDROID_HOME e JAVA_HOME. É só você identificar estes caminhos na sua máquina conforme deixei acima comandos e dicas para obter estes valores, copiar e colar nestes campos e em seguida clicar em "Save and Restart". configuração do Appium realizada com sucesso!!

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/2.png">
</p>

___

# Instalando o Appium

A instalação do Appium é bastante simples e não requer configuração adicional, além da do Android e do JDK é necessário baixar o Appium Desktop na página oficial do Appium "conforme link acima" ou via linha de comando através do terminal:

```bash
npm install -g appium
```
**ATENÇÃO:** Não instale o Appium com sudo.

✨ **Dica muito importante - npm????**

Npm é o gerenciador de downloads para pacotes node.js. 

___

# Vamos validar se tudo está ok?

Uma funcionalidade que o Appium oferece é o pacote <em>"Appium-doctor"</em>, que confere o checklist necessário para que seu ambiente funcione. Caso algo esteja faltando, o Appium-doctor te lista exatamente o que falta. Ele também confirma o que tá configurado como esperado. Para instalá-lo, é só instalar o pacote npm no seu terminal:

```bash
npm install -g appium-doctor --android
```

✨ **Dica muito importante:**
Estamos usando a flag **--android** para indicar a plataforma que vamos usar o Appium. Caso fôssemos usar o iOS, usaríamos a flag **--ios--**.

Depois de instalado o <em>Appium-doctor</em>, é só fazer a chamada via terminal:

```bash
appium-doctor
```

Abaixo segue um exemplo de como é o retorno do <em>Appium-doctor</em> via terminal:
```bash
➜  bin appium-doctor
info AppiumDoctor Appium Doctor v.1.10.0
info AppiumDoctor ### Diagnostic for necessary dependencies starting ###
info AppiumDoctor  ✔ The Node.js binary was found at: /usr/local/bin/node
info AppiumDoctor  ✔ Node version is 8.11.4
WARN AppiumDoctor  ✖ Xcode is NOT installed!
info AppiumDoctor  ✔ Xcode Command Line Tools are installed in: /Library/Developer/CommandLineTools
info AppiumDoctor  ✔ DevToolsSecurity is enabled.
info AppiumDoctor  ✔ The Authorization DB is set up properly.
info AppiumDoctor  ✔ Carthage was found at: /usr/local/bin/carthage
info AppiumDoctor  ✔ HOME is set to: /Users/BEZERRA
WARN AppiumDoctor  ✖ ANDROID_HOME is NOT set!
WARN AppiumDoctor  ✖ JAVA_HOME is NOT set!
WARN AppiumDoctor  ✖ adb could not be found because ANDROID_HOME is NOT set!
WARN AppiumDoctor  ✖ android could not be found because ANDROID_HOME is NOT set!
WARN AppiumDoctor  ✖ emulator could not be found because ANDROID_HOME is NOT set!
WARN AppiumDoctor  ✖ Bin directory for $JAVA_HOME is not set
info AppiumDoctor ### Diagnostic for necessary dependencies completed, 7 fixes needed. ###
```

Tudo que estiver acompanhado do símbolo **✔** está instalado corretamente.
Tudo que estiver acompanhado do símbolo **✖** NÃO está instalado ou identificado. deve ser ajustado.

✨ **Dica muito importante:**
O pacote do **Xcode** é específico para iOS, então, para Android, não devemos nos preocupar.

___
# Checklist do que já fizemos até agora

Até aqui, significa que provavelmente o seu setup está pronto e você já pode usar todos os recursos do Appium!
- Appium Desktop **✔**
- Android Studio (pacote AVD) **✔**
- JAVA **✔**
- IDE **✔**
- Configuração de variáveis de ambiente **✔**

___

# Iniciando o Appium

Agora é hora de iniciarmos o Appium Desktop.

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/1.png">
</p>

Assim que aberto o appium traz preenchidos os campos:<br>
**HOST:** 0.0.0.0<br>
**Port:** 4723

Estes são valores padrões do Appium e indicam que sempre que você começar a realizar requisições (lembra que o Appium é baseado em servidor HTTP?), o Appium irá utilizar o Host 0.0.0.0 e o serviço irá funcionar na porta 4723. Caso você queira mudar estes valores (quando algum outro serviço já está alocado para esta porta, por exemplo), é só você realizar a customização dessa configuração manualmente clicando no botão **Advanced**, que fica ao lado do já selecionado **Simple**. Você também pode salvar suas configurações personalizadas e exportá-las através do button **Presets**. Eu, particularmente, nunca precisei utilizar nenhuma das configurações além das que já vem por padrão. Também não vi nenhum material pela internet em que fosse necessário customizar a configuração. siga com essa configuração padrão que tudo vai funcionar bem.

Agora podemos clicar em **Start Server** e observar a segunda tela do Appium: uma escuta da chamada HTTP. Observe que ele indica aí exatamente o endereço onde o serviço está sendo executado (que são inseridos nos campos de <i>Host</i> e <i>Port</i> da tela anterior, onde deixamos os valores padrões).

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/3.png">
</p>

Agora podemos ir para a tela seguinte do Appium, onde vamos começar iniciar uma sessão (essa é a expressão utilizada quando vamos iniciar o uso do Appium), e pra isso vamos clicar no ícone da lupa, onde diz: **Start Inspector Session** (como a imagem abaixo).

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/4.png">
</p>

Agora podemos ver uma tela com vários campos para o Appium, mas aqui podemos seguir na aba <i>Custom Server</i>, que já vem escolhida por padrão. Observamos também os seguintes campos já preenchidos:<br>
**Remote Host:**  127.0.0.1<br>
**Remote Path:** /wd/hub<br>
**Remote Port:** 4327<br>

O **Remote Port** já falamos anteriormente. **Remote Host** tá com o valor de <i>localhost</i> para o serviço, mais uma vez você pode alterar caso já tenha algum serviço rodando local. Caso contrário, pode deixar esse valor mesmo. **Remote Path** também é um valor padrão do Appium e nunca precisei alterar, sempre deixo esse mesmo valor.

**Agora chegou o momento de aprendermos um dos pontos mais importantes quando começamos a usar o Appium: entender o funcionamento dos Desired Capabilities** (abaixo eu deixo o link oficial listando todos os valores que podemos usar nos desired capabilitites). <i>Desired Capabilities</i> pode ser grosseiramente traduzido por "Configurações desejadas". É onde você vai informar ao Appium o que é pra ele fazer exatamente.

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/5.png">
</p>

Como citado mais acima, o Appium funciona através de requisições HTTP e, como padrão deste tipo de comunicação, utilizamos arquivos em JSON para indicar qualquer mensagem. O appium nos traz uma interface gráfica com campos de entrada de texto mas, após preenchermos os campos de texto, ao lado ele já converte o que digitamos em um arquivo JSON. Você pode editar diretamente no JSON ou usar o campo de texto, como quiser. As duas formas funcionam bem.

Para iniciarmos uma sessão vamos precisar de pelo menos 2 campos, que são:

```bash
{
    'platformName': 'Android',
    'deviceName': '<InserirOnomeDoSeuDispositivoAqui>'
}
```

**Atenção:** para entender como obter o valor do nome do seu dispositivo, você vai precisar ler a seção mais adiante sobre comandos ADB.

Os nomes são bem intuitivos, devemos criar um dicionário com a chave <i>'platformName'</i> para indicar a plataforma que irei utilizar, que pode ser: Android, Windows, iOS. 
O identificador do dispositivo móvel que iremos inserir em <i>'deviceName'</i>, podemos obter esse valor através do comando adb <i>'adb devices'</i> que já explicamos anteriormente. Assim fica um exemplo de preenchimento destes campos básicos e ao lado já o retorno do conteúdo em JSON:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/6.png">
</p>

✨ **Dica muito importante:**
**Página oficial do Appium listando todos os Desired Capabilities:** <br>http://appium.io/docs/en/writing-running-appium/caps/

___
# Emulando um dispositivo Android através do Android Studio
Podemos usar o Appium em dispositivos reais, dispositivos emulados ou até mesmo em farms de dispositivos da Amazon, que funcionam com o mesmo conceito de computação em nuvem, onde você aloca recursos sob demanda e paga apenas o que for consumido.
Podemos utilizar dispositivos emulados para a realização dos nossos testes. Isso nos dá grande versatilidade pela possibilidade de escolher o tipo de dispositivo e a versão de Android que iremos utilizar. É possível validar o mesmo apk em cenários diversos apenas alterando configurações, onde atingimos uma característica muito forte no Android que é a granularidade de versões: https://developer.android.com/about/dashboards?hl=pt-br

✨ **Dica muito importante:**
**Antes de tudo... o que é um dispositivo emulado?**<br>
É a (criação) de um dispositivo que simula um celular real, só que ele é emulado a partir dos recursos da sua máquina. É como se fosse uma máquina virtual, só que o Sistema Operacional utilizado será alguma versão oficial do Android e o formato da máquina será uma réplica do celular de verdade, inclusive sob aspectos de tamanho das telas.

Vamos utilizar um recurso do próprio <i>Android Studio</i> para instanciarmos nosso dispositivo emulado: o <i>Android Virtual Device Manager</i>. Para acessá-lo, basta abrir o seu <i>Android Studio</i> e seguir até o seguinte ícone:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/7.png">
</p>

Ao clicar no ícone do <i>AVD Manager</i>, o seguinte popup vai abrir e você vai clicar em <i>+ Create Virtual Device...</i> para criar o seu novo dispositivo emulado:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/8.png">
</p>

Nesta nova tela, devemos escolher qual o tipo de dispositivo que queremos: TV, Phone, Wear OS, Tablet; tamanho e resoluções de tela e também a densidade. Vamos focar em **phone** o produto <i>Pixel 2</i>, já que é um produto da Google e que tem um ótimo tamanho de tela. Escolhido isso, é só clicar em <i>Next</i>.

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/9.png">
</p>

Agora é hora de escolher a versão do Android que você irá emular em seu produto na lista abaixo. O **Android P**, que é minha versão favorita atualmente. Vou prosseguir nos testes com o Android P, mas fique à vontade para baixar a versão que você quiser. Caso a imagem ainda não esteja disponível para você, clique em download. Caso já tenha baixado, é só selecionar a imagem e clicar em <i>Next</i>

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/10.png">
</p>

Dispositivo criado, tente realizar algumas ações nele como abrir aplicativos, utilizar botões de acesso como Home, Back, Recent Apps.

**Lembra quando falamos dos Desired Capabilities?** Agora podemos adicionar a configuração para abrir o emulador em conjunto com a requisição de servidor do Appium. 
Faremos isso a partir do nome que demos ao Virtual Device que cadastramos anteriormente. Assim:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/11.png">
</p>

___

# Comandos ADB
ADB grosseiramente traduzindo, é uma ferramenta que faz uma "ponte" de comunicação entre o seu computador e o seu dispositivo móvel Android através de linhas de comando. Através do ADB, é possível que possamos manipular o dispositivo através de comandos, de forma muito prática, como:
- Instalar/desinstalar aplicativos;
- Mudar configurações internas, como: tempo de desligar tela, bloqueio/desbloqueio de tela, etc.
- Habilitar/desabilitar funções de conexões, como: wifi, dados, modo avião.
- Transferência/manipulação de arquivos;
- Reiniciar e desligar o dispositivo - não funciona para ligá-lo (mas isso pode ser resolvido através de frameworks).

É também possível automatizar algumas atividades de rotina combinando comandos ADB e Python Script.

**Links importantes desta seção:**<br>
**Um pouco mais sobre comandos ADB:** https://developer.android.com/studio/command-line/adb?hl=pt-br<br>
**Um pouco Python Script:** https://realpython.com/run-python-scripts/<br>

___

# Tutorial 1: instalando uma aplicação no meu dispositivo Android emulado

**Para realizar este tutorial é preciso que você tenha:**
<ul>
    <li>Dispositivo emulado ativo - passo a passo na seção anterior</li>
    <li>ADB configurado e funcionando em seu terminal</li>
    <li>Conta na Play Store</li>
</ul>

O primeiro de tudo é escolher algum aplicativo disponível na <i>Play Store</i> para a realização dos estudos ou utilizar um APK.

Agora, é só copiar a URL da página principal do aplicativo:

https://urldapagina

Agora vamos acessar um site chamado Evozi, que tem como objetivo baixar qualquer aplicativo da Play Store tendo como base apenas o endereço URL da aplicação da Play Store, como mostro a seguir:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/12.png">
</p>

Clique em **Generate Download Link** e faça o download da sua aplicação. Ela será baixada no formato <i>.apk</i>. Agora é só salvar no seu computador e vamos instalar essa aplicação em seu dispositivo emulado, e isso podemos fazer de duas maneiras: segurando e arrastando o aplicativo; utilizando comando ADB. Vou ensinar as duas formas.

**Segurando e arrastando:**<br>
Essa forma é super simples, basta que você esteja com seu dispositivo emulado ativo e em paralelo abra a pasta que sua aplicação está. Agora, segure o seu aplicativo e arraste até o seu dispositivo móvel e, quando chegar no dispositivo, pode soltar. Você verá que vai aparecer uma imagem de <i>instalando...</i> e em poucos segundos sua aplicação estará disponível em seu dispositivo. É só acessar via menu e utilizar para ver que funciona direitinho.

**Através de comandos ADB:**<br>
Esta forma é mais elegante. É só você abrir o terminal, ir até a pasta que está sua aplicação (via terminal mesmo) e utilizar o seguinte comando:<br>
```bash
adb install nome-do-apk
```

**Links utilizados neste tutorial:**<br>
**Evozi - APK Downloader:** https://apps.evozi.com/apk-downloader/<br>
**Google Play Store:** https://play.google.com/store/apps?hl=pt_BR<br>

___
# Tutorial 2: Desired Capabilities: como iniciar uma sessão com o Appium

**Para realizar este tutorial é preciso que você tenha:**<br>
<ul>
    <li>Dispositivo emulado ativo - passo a passo na seção anterior</li>
    <li>ADB configurado e funcionando em seu terminal</li>
    <li>Aplicação da Play Store já instalada no dispositivo</li>
    <li>Appium Desktop configurado e funcionando</li>
</ul>

Caso você ainda não tenha lido a seção **Iniciando com o Appium**, recomendo que você dê um pulo lá para ler alguns conceitos que vai ajudar bastante neste segundo tutorial, especialmente porque fala da importância que são os <i>Desired Capabilites</i> para o Appium. Reforçando o que foi dito por lá, os <i>Desired Capabilites</i> são uma parte muito especial e importante quando estamos trabalhando com Appium. É a partir deles que vamos dizer o que queremos fazer exatamente utilizando o Appium.

Como mostra a [documentação oficial do Appium sobre os Desired Capabilites](http://appium.io/docs/en/writing-running-appium/caps/), temos uma extensa lista de opções de uso e podemos partir de um uso mais genérico até um uso mais específico. Aqui vamos realizar a ação destas nesses dois formatos.

**Desired Capabilities - forma genérica**

Para isso, vamos precisar identificar apenas qual o <i>platformName</i> e o <i>deviceName</i>, que querem dizer o a plataforma (Android, iOS, Windows) e o nome do produto (serial number), respectivamente. O primeiro valor é bastante simples de saber, basta indicar a plataforma que você está usando no seu estudo - durante este tutorial irei usar Android. Para saber o <i>Serial Number</i> do seu celular, é só utilizar o seguinte comando ADB em seu terminal:

```bash
    adb devices
```

O comando irá retornar algo mais ou menos assim:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/13.png">
</p>

Assim que dou o comando <i>adb devices</i> o serviço ADB é iniciado e em seguida o valor de identificação do meu celular é retornado, que no caso foi: **emulator-5554**. É este o valor que vamos usar no campo <i>deviceName</i>. 

Segue então valores que irei utiliar para o <i>Desired Capabilities</i>:

```bash
{
    'platformName': 'Android',
    'deviceName': 'emulator-5554',
    'avd': 'AppiumP'
}
```

Agora com os valores identificados, podemos abrir o Appium até chegarmos na tela que temos a aba de <i>Desired Capabilites</i> e preencher os campos como mostra a imagem a seguir:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/14.png">
</p>

Eu insiro o valor apenas na aba <i>Desired Capabilities</i> e automaticamente o Appium converte tudo em JSON na tela ao lado, onde aponto com uma seta. Uma dica que acrescento é a de salvar essa sua configuração, pois ela será a base de alguns outros tutoriais que vamos fazer. Para isso, é só clicar em **Save As**. Para acessar qualquer capability já salva, é só acessar a aba <i>Save Capability Sets</i>, que fica ao lado da aba <i>Desired Capabilities</i>.

Agora, é só clicar no botão **Start Session** que o Appium irá iniciar uma sessão com base nas informações que indicamos. Com os campos corretos e identificados (ou seja, celular detectado e compatível com o que você informou), agora podemos ver a seguinte tela:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/15.png">
</p>

Esta é a tela de início de atividades com o Appium, que veremos nos próximos tutoriais. Aqui já é possível ver que o Appium tirou um <i>screenshot</i> da tela em que estava o nosso celular no momento em que demos início à sessão. Essa é uma das características do Appium: ele espelha a tela exatamente de onde você iniciou a sessão - em casos de uso genérico do <i>Desired Capabilities</i>. Além disso, também já vemos novos botões e novas seções. Agora vamos ver como podemos iniciar uma sessão sendo mais específicos com as informações que queremos que o Appium trate.

**Desired Capabilities - forma específica**

Vimos anteriormente como criamos uma sessão genérica com o <i>Appium</i> e conhecemos também algumas telas e algumas características à medida que fomos avançando as ações.
A finalidade de você iniciar uma sessão de forma mais específica é que vc indica ao <i>Appium</i> **exatamente** a tela que ele deve iniciar a sessão.

**Exemplo:**<br>
Vamos querer automatizar nossa calculadora nativa do Android. Como já sabemos que nosso foco será essa aplicação específica, podemos ir direto para ela, pulando o fluxo em que chamamos a aplicação através de interface gráfica. Para isso, vamos incrementar os valores de <i>Desired Capabilities</i> que já tínhamos preparado no passo anterior, só que agora precisamos dos valores para as chaves: <i>appPackage</i> e <i>appActivity</i>. Segue explicação para cada um dos campos:

**appPackage:**
<br>
É o nome do pacote da sua aplicação. Isso é definido à nível de desenvolvimento da aplicação.

**appActivity:**
<br>
Uma tela em desenvolvimento Android é chamada de activity. Este valor é basicamente para indicar em qual tela da aplicação você quer estar quando a sessão for iniciada.

**E como obter estes valores?**
<br>
Através de comando ADB! <3 Para isso, vamos para nosso celular em teste (emulado ou real) e vamos abrir a aplicação que queremos testar e vamos deixar exatamente na tela que queremos fazer nossos teses. Depois disso, vamos usar o seguinte comando no terminal:

```bash
    adb shell dumpsys window windows | grep -E 'mCurrentFocus'
```

Visualmente fica assim:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/16.png">
</p>

Note que deixo em destaque o seguinte trecho do que foi retornado na estrutura:

```bash
com.android.calculator2/com.android.calculator2.Calculator
```

Este é trecho em que temos tanto o valor de <i>appPackage</i> quanto o de <i>appActivity</i>. A divisão entre os dois campos se dá pela / (barra) que existe bem no meio do trecho. Sempre o que tiver antes da barra será o valor do package. O que tiver depois será o do activity da sua aplicação. Agora é só copiar e preencher nos campos com mostro a seguir:

```bash
{
    'platformName': 'Android',
    'deviceName': 'emulator-5554',
    'avd': 'AppiumP',
    'appPackage': 'com.android.calculator2',
    'appActivity': 'com.android.calculator2.Calculator'
}
```

Visualmente fica assim (em destaque no JSON o que eu acrescentei):

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/17.png">
</p>

Agora, com todos os valores preenchidos, você pode salvar novamente esta configuração clicando em <i>Save As...</i> e em seguida podemos iniciar nossa sessão clicando em <i>Start Session</i>. Quando a sessão for iniciada, você verá que agora o print da tela será direto da aplicação Calculadora, que foi a que indiquei nos campos de <i>appPackage</i> e de <i>appActivity</i>. Veja que no seu dispositivo (emulado ou real) também vai estar na mesma tela que você indicou:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/18.png">
</p>

**Links Importantes para este tutorial:**<br>
Página oficial do Appium com os Desired Capabilities listados: http://appium.io/docs/en/writing-running-appium/caps/

___
# Tutorial 3: Identificando os elementos da nossa aplicação

**Para realizar este tutorial é preciso que você tenha:**<br>
<ul>
    <li>Realizado o Tutorial 2</li>
</ul>

Realizar a identificação de elementos é muito fácil quando estamos trabalhando com ferramentas/frameworks que tem o <i>webDriver</i> como base. Inclusive, a simples ação de **mapear elementos** de aplicações móveis também pode ser realizada através do UIAutomator, que é uma funcionalidade nativa também do <i>Android Studio</i>. Se você já trabalhou com Selenium, sabe que para mapearmos elementos de uma página web, basta clicar com o botão direito do mouse e selecionarmos a opção "inspecionar elementos" ou "inspecionar".

Com falei mais acima, identificar elementos é **relativamente simples**, **porém, o grande desafio** do mapeamento de elementos está em mapear de maneira inteligente e eficiente, de maneira que seu código não vá quebrar e, além disso, de maneira que a manutenabilidade do seu código não seja comprometida.
<br>

**Qual a melhor prática?** <br>
No mundo perfeito, todos os elementos de uma aplicação/página web estão identificados seguindo boas práticas de desenvolvimento, com IDs intuitivos e únicos. Outro excelente caminho é se você tem acesso aos desenvolvedores da aplicação e consegue solicitar esse tipo de ajuste a eles. Porém, sabemos que essa é uma realidade muito específica e que não estará presente na maioria das aplicações que formos interagir - especialmente agora na nossa fase de estudos.

Uma ótima prática é utilizar partes estáticas quando temos IDs dinâmicos. No caso de usar IDs dinâmicos, os seus valores serão atualizados a cada acesso, ação normalmente realizada pelo framework utilizado em nível de desenvolvimento. Uma boa dica para isso? CSS Selector.

Em algums casos você vai ter que trabalhar com hierarquia dos seus elementos. Nestas condições, opte sempre pela hierarquia mais próxima ao elemento em foco e, melhor ainda, se o elemento pai/filho possuir IDs únicos.

Outra dica, já acompanhada de um exemplo para tornar o entendimento mais claro, é poder dividir os valores (muitas vezes gigantes) que você pode encontrar por XPATH, tornando-os mais curtos:

```bash
<button type=“submit” class=“signup-button button--black button--active”>Signup Here!</button>
```

Diante deste exemplo simples de XPATH, onde vemos um valor grande, podemos tratá-lo da seguinte maneira:

```bash
WebElement signupXPath = browser.findElement(By.xpath(“//button[contains(@id, ‘signup-button’)]”));
```

Também, de forma muito similar, podemos realizar a identificação do elemento a partir de CSS Selector:

```bash
WebElement signupCSS = browser.findElement(By.cssSelector(“button[class*=‘signup-button’]”));
```

Destas formas seu elemento será sendo identificado da mesma maneira, só que agora de forma mais legível e com menor vulnerabilidade de quebra futura :)

**Qual a prática devemos evitar?** <br>
A prática ruim mais comum que vejo acontecer é o uso de XPATH longos, sem tratamentos, e uso de identificadores dinâmicos, que deixam de fazer sentido numa segunda execução - visto que ele muda a cada load da página.

**Agora identificando elementos no Appium**<br>
Para realizar a identificação de elementos, basta dar um clique no elemento que você deseja mapear e, na barra lateral direita, irá aparecer uma lista de opções de valores que você pode utilizar no seu mapeamento:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/19.png">
</p>
<br>

No meu print, utilizei o elemento "9" e me foi retornado 2 opções: id, xpath. Como o número 9 tem ID e vejo que ele é único (clicando nos demais elementos pude perceber isso), então decidi que o valor de ID é a melhor abordagem para eu seguir na identificação dos elementos da minha calculadora.


___
# Tutorial 4: Realizando um fluxo simples de teste funcional

Agora é hora realizarmos um fluxo bem simples de teste funcional em uma aplicação. Como estamos iniciando, vou realizar este tutorial através da aplicação Calculadora nativa do Android emulado. Como estamos falando de um teste funcional, irei estruturar o teste aqui:

<b>Cenário de teste:</b><br>
Realizar operações aritméticas
<br>
<table style="width:100%">
  <caption>Caso de Teste 1 - Realizar operação de soma com 2 valores de entrada</caption>
  <tr>
    <th>Setup</th>
    <th>Passo a passo</th>
    <th>Resultado esperado</th>
  </tr>
  <tr>
    <td>1. Dispositivo conectado (real ou emulado)<br>
        2. Sessão de Appium iniciada<br>
        3. Aplicação Calculadora iniciada<br>
    </td>
    <td>1. Insira 1 entrada numérica válida<br>
        2. Aplique a operação de soma<br>
        3. Insira outra entrada numérica válida<br>
        4. Checar resultado
    </td>
    <td>
        1. Número é inserido corretamente<br>
        2. Operação inserida corretamente<br>
        3. Número inserido corretamente<br>
        4. O resultado condiz com os elementos inseridos.
    </td>
  </tr>
</table>

O caso de teste é bastante simples, vou realizar a soma dos números 2 e 3:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/30.gif">
</p>

É só clicar nos elementos seguindo o fluxo definido e verificar que no final ele retorna o resultado de forma correta. Depois vamos fazer um tutorial para validar isso através de linguagem de programação :)

___
# Tutorial 5: Gravando nossas ações e transformando isso em código

**Para realizar este tutorial é preciso que você tenha:**<br>
<ul>
    <li>Tenha um dispositivo (real ou emulado) ativo</li>
    <li>Uma sessão iniciada no Appium</li>
    <li>Calculadora inicializada</li>
</ul>

Agora é hora de conhecermos uma outra funcionalidade muito boa que o Appium traz, que é o de converter em **código de programação** qualquer ação que você realizar em seu dispositivo, seja esta ação apenas para inicializar uma aplicação, ou até para ações mais elaboradas e interessantes como os que vimos mais acima: <i>swipe</i> e <i>tap coordinates</i>.

Considero essa função uma das que torna o Appium uma excelente aplicação para automação, especialmente se você está iniciando neste mundo ou ainda não tem muito contato com alguma linguagem de programação - de forma geral ou em alguma linguagem específica. O Appium consegue converter código para as seguintes linguagens: Python, JAVA, Ruby, RobotFramework e JS.

A funcionalidade de gravar as ações fica disponível com o seguinte ícone na aplicação:

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/31.png">
</p>

Basta clicar neste ícone e deixar também ativa a função "Select elements", que fica ao lado esquerdo do botão <i>swipe</i>. Vou deixar em destaque na próxima imagem. Ao clicar em cada um dos ícones do teste, teremos que clicar também no botão <i>Tap</i>, que irá realizar a ação de clique no elemento. Este botão também deixo em destaque na imagem que segue: 

<p align="center">
<img src="https://github.com/fabiosouthsystem/appium/blob/main/32.png">
</p>

Agora é só realizar alguma ação e irei repetir o fluxo que fizemos no tutorial anterior, só que agora vamos gravar cada uma das ações que realizarmos:

Observe que à medida que nós vamos inserindo os dígitos na nossa calculadora, o código vai sendo gerado no campo **Recorder** que fica ao lado direito veja que o código já faz atribuições às variáveis que ele mesmo cria para receber elementos e assim facilitar acções como o <i>.click</i>. O código gerado será assim para Python:

```bash
el1 = driver.find_element_by_id("com.android.calculator2:id/digit_2")
el1.click()
el2 = driver.find_element_by_accessibility_id("plus")
el2.click()
el3 = driver.find_element_by_id("com.android.calculator2:id/digit_3")
el3.click()
el4 = driver.find_element_by_accessibility_id("equals")
el4.click()

```

___
# Tutorial 6: Replicando tudo o que fiz utilizando apenas Python

**Para realizar este tutorial é preciso que você tenha:**<br>
<ul>
    <li>Tenha um dispositivo (real ou emulado) ativo</li>
    <li>Uma sessão iniciada no Appium</li>
    <li>Calculadora inicializada</li>
</ul>

Brincamos bastante com o Appium ao longo dos tutoriais e conhecemos as principais funcionalidades gráficas que conseguimos acessar com muita facilidade, basicamente clicando nos elementos e coletando os códigos gerados.

Agora, podemos ir direto pra IDE de sua escolha (eu estou utilizando o PyCharm durante este documento) para replicarmos tudo que já fizemos, só que agora sem interagir diretamente com o Appium. Vamos utilizá-lo agora apenas para mapear elementos que ainda não mapeamos :)

Como estou utilizando o PyCharm, então criei um novo projeto, então um novo arquivo Python e instalei os seguintes pacotes no terminal do projeto:

1. Selenium:

```bash
pip install selenium
```

2. Appium:

```bash
npm install -g appium
```

O princípio se dá importando a biblioteca necessária para que a gente possa utilizar os recursos do Appium em qualquer linguagem de programação. Lembram que já citamos acima que o Appium e o Selenium tem muita coisa em comum? Aqui a gente vê de forma mais explícita que tanto o Appium quanto o Selenium utilizam recursos da biblioteca <i>webdriver</i>, e ele que iremos importar pra dar início ao nosso projeto:

```bash
from appium import webdriver
```

Como já vimos por aqui na seção Iniciando com o Appium, o **Desired Capabilities** é uma parte super importante no Appium pois é através dele que faremos a conexão HTTP entre o Appium e o nosso dispositivo, além de indicarmos se queremos apenas iniciar o dispositivo ou se queremos iniciar numa aplicação em especial, através do uso das chaves: <i>appPackage</i> e <i>appActivity</i>. Nos exemplos anteriores já tivemos uma ideia de como isso acontece, que é através de um dicionário contendo as chaves e valores que precisamos:

```bash
caps = {}
caps["platformName"] = "Android"
caps["deviceName"] = "AppiumP"
caps["avd"] = "AppiumP"
caps["appPackage"] = "com.android.calculator2"
caps["appActivity"] = "com.android.calculator2.Calculator"
```

Outro ponto importante é como a conexão é estabelecida. O Appium nos retorna essa solução:

```bash
driver = webdriver.Remote("http://127.0.0.1:4723/wd/hub", caps)
```

É aí que começamos a utilizar os recursos da biblioteca <i>WebDriver</i>. Criamos uma variável chamada **driver** e dentro dela armazenamos a instância de uma nova conexão, que se dá através da chamada do recurso <i>Remote</i>. Passamos 2 parâmetros para essa chamada:
1. Localização do nosso serviço: <i>"http://127.0.0.1:4723/wd/hub"</i>, que é composto pelos valores que já conhecemos via interface do Appium. Aí está uma junção dos campos que são preenchidos de forma padrão: Remote Host + Remote Port + Remote Path.
2. <i>Desired capabilities:</i> Como já explicamos anteriormente, nós criamos um dicionário para armazenarmos as chaves e valores do que queremos que o Appium trate. Aqui é só passar o nome deste dicionário.

```bash
from appium import webdriver

desired_cap = {
    "platformName": "Android",
    "deviceName": "AppiumP",
    "avd": "AppiumP",
    "appPackage": "com.android.calculator2",
    "appActivity": "com.android.calculator2.Calculator"
}

driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_cap)
```


___
# Parte 2 - Recursos e Funcionalidades do Appium

Uma das vantagens de se utilizar um framework para resolver um problema, é o uso dos recursos que esse framework é capaz de prover ao seu ambiente de automação. O Appium traz muitos recursos poderosos que dão contexto mobile pros seus testes, e que podem ser utilizados de acordo com sua estratégia de testes.

## Network - rede
Considerar cenários e interações de rede é um dos itens obrigatórios quando estamos falando de testes para mobile. Aqui estão alguns dos comandos que podemos utilizar neste sentido:

### ☎️ **Chamadas:**

Esse recurso é chamado de GSM Call. Sua estrutura espera 2 parâmetro: "phone_number" e "action", ambos são strings em Python, onde "phone_number" é o número a ter interações e "action" é a ação a ser feita, e pode ser: call (realizar a chamada), accept (aceitar a chamada), cancel (recusar a chamda) e hold (colocar a chamada em aguardo). 

Receber uma chamada:
Para aparecer a notificação de chegada de ligação. Por si só este comando não irá aceitar a chamada, apenas irá notificar a chegada de uma nova ligação.

```python
driver.make_gsm_call("123123", "call")
```

### **Aceitar uma chamada:**
Com o uso do comando acima, a chamada irá aparecer na sua tela. Para aceitá-la, é preciso utilizar o seguinte comando:

```python
driver.make_gsm_call("123123", "accept")
```

## **Recusar uma chamada, ou finalizar uma chama estabelecida:**

Porém, se você quiser recursar a chamada, basta utilizar o seguinte comando:

```python
driver.make_gsm_call("123123", "cancel")
```

Este comando também é utilizado para finalizar uma chamada em curso.

## **Colocar uma chamada em espera (on hold):**

Uma vez que a chamada é estabelecida, você pode colocá-la em aguardo através do seguinte comando:

```python
driver.make_gsm_call("123123", "hold")
```

[Referência oficial do Appium](https://appium.readthedocs.io/en/stable/en/commands/device/network/gsm-call/)

### 📜 **Receber um SMS:**

```python
driver.send_sms('1010101', 'hello wold')
```

## **Interações com o dispositivo:**

### **Sistema e notificações:**

- Mudar orientação da tela:

A depender da disposição de tela do seu dispositivo, isso pode habilitar ou desabilitar nossas funcionalidades no sistema ou no aplicativo em teste. Um exemplo disso, é a Calculadora do Android que na posição "portrait" tem a Calculadora padrão, porém, quando na posição "landscape", a Calculadora se transforma em Calculadora Científica.

Em alguns momentos do teste pode ser necessário você verificar a orientação corrente que está seu dispositivo, e com base nisso realizar alguma ação. Para identificar a orientação atual do dispositivo, utilize o seguinte recurso:

```python
driver.orientation()
```

## **Deixar em modo "portrait":**

Este é o modo na vertical, o que usamos como padrão.

```python
driver.orientation = "PORTRAIT"
```

## **Deixar em modo "landscape":**

Este é o modo de visão na horizontal.

```python
driver.orientation = "LANDSCAPE"
```

## **Controle de carga e percentual de bateria:**

- 🔋 Alterar o % de bateria do dispositivo:

Este é um recurso super poderoso pois a depender do % de bateria do seu dispositivo podemos ver a presença de alguma notificação do sistema indicando nível crítico de bateria, ou até mesmo sugerindo que você entre no modo econômico de bateria. Tudo isso pode influenciar no estado do seu dispositivo e, consequentemente, influenciar na condução dos seus testes ou até mesmo sugerir uma suíte de testes voltada para esse tipo de validação.

O recurso para isto é o set_power_capacity e apenas 1 parâmetro é passado, que é o valor de 0 a 100 para o valor do nível de bateria.

```python
driver.set_power_capacity(10)
```

- 🔌 Simular estar ligado no carregador:

O recurso para isto é o set_power_ac, e aguarda apenas 1 parâmetro que é a string "on" para indicar que está em carga ou "off" para indicar que não está em carga.

```python
driver.set_power_ac("on")
```

- Verificar se um aplicativo está instalado no sistema:

Testes de instalação também é algo muito presente no universo mobile. É muito frequente que a instalação/desinstalação de aplicativos seja uma realidade na rotina de quem utiliza um dispositivo móvel. E, se sua aplicação será lançada na Play Store, testar se o aplicativo foi instalado com sucesso será um dos primeiros testes que você deve considerar.

O recurso para isto é o "is_app_installed" que retorna um booleano (True/False) para o valor do pacote que você deverá passar como parâmetro na chamada da função.

```python
driver.is_app_installed('com.example.appiumcurso')
```

### **Identificar contexto:**

Saber o contexto da sua aplicação é algo muito importante. Se for uma aplicação nativa, pode ser que você tenha que utilizar uma abordagem diferente dos casos de uma aplicação web, por exemplo. Apenas olhando um aplicativo muitas vezes não é possível dizer qual o tipo daquele aplicativo, mas o Appium fornece um recurso para nos ajudar com isso.

```python
driver.contexts
```

Este comando retorna uma string indicando se o aplicativo que estiver aberto na tela do dispositivo naquele momento é um aplicativo nativo, híbrido ou web.

### Lista de métodos:

```python
driver.AC_OFF
```

```python
driver.AC_ON
```

```python
driver.activate_app()
```

```python
driver.activate_ime_engine()
```

```python
driver.active_ime_engine
```

```python
driver.add_cookie()
```

```python
driver.add_credential()
```

```python
driver.add_virtual_authenticator()
```

```python
driver.all_sessions
```

```python
driver.app_strings()
```

```python
driver.application_cache
```

```python
driver.available_ime_engines
```

```python
driver.back()
```

```python
driver.background_app()
```

#### Checar informação sobre bateria:
```python
driver.battery_info
```

```python
driver.bidi_connection()
```

```python
driver.capabilities
```

```python
driver.caps
```

```python
driver.close()
```

#### Fechar aplicativo específico:
```python
driver.close_app()
```
É necessário indicar o nome do aplicativo, como nesse exemplo:
```python
driver.close_app('com.example.cursoappium')
```
```python
driver.command_executor

```python
driver.context
```

```python
driver.contexts
```

```python
driver.create_web_element()
```


#### Retorna o nome da activity em primeiro plano da aplicação:
```python
driver.current_activity
```

#### Retorna o contexto da aplicação em primeiro plano:
```python
driver.current_context
```
Pode ser uma aplicação "nativa" ou "web".

#### Retorna o nome do pacote da aplicação em primeiro plano:
```python
driver.current_package
```

driver.current_url
driver.current_window_handle
driver.deactivate_ime_engine()
driver.delete_all_cookies()
driver.delete_cookie()
driver.delete_extensions()
driver.desired_capabilities
driver.device_time
driver.drag_and_drop()
driver.end_test_coverage()
driver.error_handler
driver.events
driver.execute()
driver.execute_async_script()
driver.execute_driver()
driver.execute_script()
driver.file_detector
driver.file_detector_context()
driver.find_element()
driver.find_elements()
driver.find_image_occurrence()
driver.finger_print()
driver.flick()
driver.forward()
driver.fullscreen_window()
driver.get()
driver.get_clipboard()
driver.get_clipboard_text()
driver.get_cookie()
driver.get_cookies()
driver.get_credentials()
driver.get_device_time()
driver.get_display_density()
driver.get_events()
driver.get_images_similarity()
driver.get_log()
driver.get_performance_data()
driver.get_performance_data_types()
driver.get_pinned_scripts()
driver.get_screenshot_as_base64()
driver.get_screenshot_as_file()
driver.get_screenshot_as_png()
driver.get_settings()
driver.get_system_bars()
driver.get_window_position()
driver.get_window_rect()
driver.get_window_size()
driver.hide_keyboard()
driver.implicitly_wait()

#### Instala uma apk no dispositivo:
```python
driver.install_app()
```

#### Verifica se uma aplicação está instalada no dispositivo em teste:
```python
driver.is_app_installed()
```

É necessário informar o nome do aplicativo nesse formato:
```python
driver.is_app_installed('com.example.cursoappium')
```

```python
driver.is_ime_active()
```

```python
driver.is_keyboard_shown()
```

#### Retorna se o dispositivo está com tela bloqueada ou não:
```python
driver.is_locked()
```

#### Enviar algum keyevent para o dispositivo:
```python
driver.keyevent()
```
A lista completa de todos os keyevents e seus respectivos valores pode ser encontrada na página oficial do [Android aqui](https://developer.android.com/reference/android/view/KeyEvent).


#### Inicia uma aplicação já instalada no dispositivo:
```python
driver.launch_app()
```

driver.location
driver.lock()
driver.log_event()
driver.log_types
driver.long_press_keycode()
driver.make_gsm_call()
driver.match_images_features()
driver.maximize_window()
driver.minimize_window()
driver.mobile
driver.name
driver.network_connection
driver.open_notifications()
driver.orientation
driver.page_source
driver.pin_script()
driver.pinned_scripts
driver.press_button()
driver.press_keycode()
driver.print_page()
driver.pull_file()
driver.pull_folder()
driver.push_file()
driver.query_app_state()
driver.quit()
driver.refresh()
driver.remove_all_credentials()
driver.remove_app()
driver.remove_credential()
driver.remove_virtual_authenticator()
driver.reset()
driver.save_screenshot()
driver.scroll()
driver.send_sms()
driver.session
driver.session_id
driver.set_clipboard()
driver.set_clipboard_text()
driver.set_gsm_signal()
driver.set_gsm_voice()
driver.set_location()
driver.set_network_connection()
driver.set_network_speed()
driver.set_page_load_timeout()
driver.set_power_ac()
driver.set_power_capacity()
driver.set_script_timeout()
driver.set_user_verified()
driver.set_value()
driver.set_window_position()
driver.set_window_rect()
driver.set_window_size()
driver.shake()
driver.start_activity()
driver.start_client()
driver.start_recording_screen()
driver.start_session()
driver.stop_client()
driver.stop_recording_screen()
driver.swipe()
driver.switch_to
driver.tap()
driver.terminate_app()
driver.timeouts
driver.title
driver.toggle_location_services()
driver.toggle_touch_id_enrollment()
driver.toggle_wifi()
driver.touch_id()
driver.unlock()
driver.unpin()
driver.update_settings()
driver.virtual_authenticator_id
driver.wait_activity()
driver.window_handles
