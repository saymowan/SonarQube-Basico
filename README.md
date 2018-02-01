# SonarQube-Basico-C#



Projeto voltado para desenvolvedores, analistas de testes automatizados e DevOps que queiram criar o ambiente de qualidade contínua de código utilizando a ferramenta SonarQube para a linguagem C#. Pretendo em outro projeto incluir uma explicação de um novo step no pipeline de integração contínua com a ferramenta SonarQube. 


# Features deste projeto
  - Pré-requisitos e instalações
  - Criar um servidor SonarQube (Windows)
  - Configurar um projeto no SonarQube (chave e token)
  - Rodando o SonarQube-Scanner em seu projeto localmente
  - Acessando os dados gerados pela ferramenta
  


> O intuito deste projeto é colaborar com pessoas aprendizes deste assunto
> assim como eu, as quais queiram implantar esse tipo de analise no seu projeto.
> Tive algumas dificuldades, porém a documentação da ferramenta é bem explicativa.
> Qualquer dúvida é só contactar: saymowan@gmail.com

### Pré-requisitos e instalações

Vamos trabalhar com a plataforma Windows, ok? Você irá precisar instalar no seu servidor ou na sua máquina local, as seguintes ferramentas:

* [MsBuild](https://www.microsoft.com/en-us/download/details.aspx?id=48159) - Ferramenta para realizar build do projeto C#
* [NuGet](https://www.nuget.org/downloads) - Ferramenta para recuperar pacotes de projetos C#
* [SonarQube (6.7.1 Lite)](https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-6.7.1.zip) - Ferramenta que criará um servidor localmente com o report das analises do código verificadas
* [SonarQube Scanner for MsBuild 4.0.2.892](https://github.com/SonarSource/sonar-scanner-msbuild/releases/download/4.0.2.892/sonar-scanner-msbuild-4.0.2.892.zip) - Ferramenta que realiza a varredura no código do projeto 

Após instalar, seguiremos para o próximo passo. 

### Criar um servidor SonarQube (Windows)

Para a ferramenta SonarQube, extraia o conteudo da mesma no diretório: "C:\sonarqube". Verifique se o servidor estará funcionando conforme o esperado com a seguinte linha de comando via prompt:
```
C:\sonarqube\bin\windows-x86-64\StartSonar.bat
```
Deverá apresentar esta informação:
![](https://i.imgur.com/dztHO2y.png)]


Após verificar a saúde do servidor conforme imagem acima, acesse o seguinte link no navegador: http://localhost:9000. Alguns segundos para configurar e após, já estará disponível a ferramenta para seu uso. Clique em Log in e utilize as credenciais "admin/admin" para se autenticar.

### Configurar um projeto no SonarQube (chave e token)

Verifique que você está na página inicial do SonarQube autenticado, e que para o seu primeiro acesso, a ferramenta disponibiliza um recurso de configurar seu primeiro projeto. Será necessário associar seu projeto local através de uma chave e um token que serão gerados na ferramenta.

ANOTE SEU TOKEN E CHAVE(KEY) PARA SEREM UTILIZADOS!

Inicialmente você configura seu nome do token e após, o mesmo é gerado:
.

![](https://i.imgur.com/8bfIVr6.png)

Após, o token gerado será exibido:
.

![](https://i.imgur.com/TJNC4jW.png)

No passo 2, escolha a opção de projeto "C# or VB.NET", coloque um nome para sua chave (key) e clique em "Done".
.
 
![](https://i.imgur.com/GNYfYN7.png)


Pronto! Seu projeto já está configurado e podemos iniciar a execução do SonarQubeScanner que analisará o código referente à este projeto.

Obs: este tutorial nativo do SonarQube está disponível na sessão "Help" a qualquer momento ou faça o seguinte passo a passo:
- Criar um novo token: Acesse o "menu com o ícone do seu usuário/Administrator" clique em "Security" e crie um novo token.
- Criar um novo projeto: acesse o menu "Administration/Projects/Management" e o menu "Create Project". Coloque o nome do projeto e o token criado no passo anterior.
- Ambas as informações serão necessárias.


Após este passo, vamos realizar a varredura no código.

### Rodando o SonarQube-Scanner em seu projeto localmente

Pré-requisito:
- Passos anteriores estarem funcionando.
- Token e chave(key) do projeto que será analisado.

Após realizado os passos anteriores, chegou a hora de varrer o código e extrair as informações. Para isso iremos utilizar os seguintes passos:
1. Executar a ferramenta SonarQube.Scanner
2. Realizar um Rebuild no projeto 
3. Executar a varredura com a ferramenta SonarQube.Scanner

##### 1. Executar a ferramenta SonarQube.Scanner

Abra um prompt de comando, entre no diretório do projeto e execute o seguinte comando (troque as variaveis KEY_DO_PROJETO e TOKEN_DO_PROJETO pelas suas informações):
```
"C:/Sonar S/SonarQube.Scanner.MSBuild.exe" begin /k:"KEY_DO_PROJETO" /d:sonar.host.url="http://localhost:9000" /d:sonar.login="TOKEN_DO_PROJETO"
```
Segue abaixo uma imagem da execução:
![](https://i.imgur.com/VFioPrF.png)

#### 2. Realizar um Rebuild no projeto 

Um Rebuild (reconstruir) será necessário para o projeto que será verificado, assim execute a seguinte linha de código, lembre-se que neste tutorial está exemplificado com o Msbuild 14.0. Utilize o mesmo prompt de comando do Passo 1.
```
"C:\Program Files (x86)\MSBuild\14.0\Bin\MsBuild.exe" /t:Rebuild
```
#### 3. Executar a varredura com a ferramenta SonarQube.Scanner

Agora o passo final será executar a varredura do código e analisar os resultados. Para isso utilize o trecho de código abaixo no mesmo prompt de comando dos demais passos (use o mesmo token na variável TOKEN_DO_PROJETO):
```
"C:/Sonar S/SonarQube.Scanner.MSBuild.exe" end /d:sonar.login="TOKEN_DO_PROJETO"
```

Algo semelhante será apresentado ao iniciar:

![](https://i.imgur.com/rlDbnKS.png)

E ao final, será exibido o trecho abaixo representado a finalização da varredura do projeto:

![](https://i.imgur.com/31SxRQc.png)

Pronto! Seu código já foi analisado e você tem os resultados pronto para analise.



### Acessando os dados gerados pela ferramenta

Agora temos a fase de analise do que foi coletado com a ferramenta SonarQube e SonarQube-Scanner. Assim, utilize o link http://localhost:9000 e acesse seu sevidor para verificar o projeto, o mesmo será exibido na home:
![](https://i.imgur.com/mRPn96k.png)

Tudo pronto e agora é somente analisar o que tens de problemas interpretados pela analise do projeto pelo SonarQube.
Lembre-se que este recurso é uma ferramenta de apoio para evitar dívidas técnicas e futuros problemas de código que não são interpretados pelos compiladores. 

### Próxima versão do projeto

Para a próxima versão deste projeto, pretendo entrar mais a fundo no mundo DevOps junto com esta boa prática de codificação. Assim, pretendo em outro projeto incluir uma breve explicação de como criar/incluir um novo step/passo no pipeline de integração contínua com a ferramenta SonarQube, assim pegaremos códigos versionados e evitaremos os problemas de maneira ágil e bem dinânima.

Até mais!!!!

