<h1 align="center">
  <img src="https://user-images.githubusercontent.com/36782514/118198660-bb0f5300-b427-11eb-80a2-091c733366e1.png" alt="logo Java" width="240">
</h1>
<br>

<p align="center"><b>Guia de instalação Oracle-JDK-11</b></p>

<p  align="center">
  <a href="#-Baixando-JDK">Baixar</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-Preparação">Preparação</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Instalacao">Instalação</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-Teste">Teste</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-Desinstalação">Desinstalação</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Conclusão">Conclusão</a>
</p>

<br>
<br>

## ⚠️ Observações

Este guia foi criado com base na versão **11.0.11** do JDK e no Ubuntu **20.04-lts** e alguns passos podem **não funcionar** em outras distribuições ou mesmo em outras versões do Ubuntu.

Sigua este guia com cuidado se atentando aos detalhes como a versão dos pacotes (**11.0.11 / 11.X.XX**), que podem variar dependendo de quando está vendo este guia.

## ☁️ Baixando JDK
Para esta instalação vamos usar o pacote compactado ``.tar.gz`` disponível no site da Oracle que é o formato mais usado para esta instalação.

[Clique para ir a pagina de download](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)

Nesta página você precisara aceitar os termos de uso, e caso não tenha uma conta Oracla o cadastro será requisitado antes do download.

![list-jdk](https://user-images.githubusercontent.com/36782514/118189336-03bf1000-b418-11eb-9f71-b575c604e9e6.JPG)

Fique atento para baixar o arquivo correto para a arquitetura do seu processador, onde o padrão da maioria é o **X64**.

## 🛠️ Preparação

Antes de prosseguir com a instalação vamos precisar instalar algumas dependências antes.

A primeira é o ``software-properties-common`` para habilitar a instalação de software de terceiros. Uma vez que o JDK disponibiliazado pela Oracle não pode ser obtido atravez do repositório oficial do Ubuntu.

**INPUT:**
```
sudo apt install software-properties-common
```

Em seguida baixamos a chave de assinatura, para o software que vamos instalar logo em seguida. Essa chave é usada para verificar se o software é válido.

**INPUT:**
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EA8CACC073C3DB2A
```

Agora vamos adicionar um PPA, que é basicamente um repositório extra que irá nos fornecer pacotes/softwares que não estão disponíves por padrão, quando tentamos fazer uma instalação via apt por exemplo.

**OBS:** copie apenas um comando por vez.

**INPUT:**
```
sudo add-apt-repository ppa:linuxuprising/java

sudo apt update
```

<div id="Instalacao" />
## ⚙️ Instalação
Agora que já baixamos o pacote do JDK ele deve se encontrar disponível na sua pasta de **Downloads**. Copie o arquivo para sua pasta pessoal.

Uma vez tendo copiado o arquivo para a sua pasta pessoal abra o terminal ``ctrl + alt + t``, e vamos criar um novo diretório para onde copiaremos novamente o arquivo do JDK.

**INPUT:**
```
sudo mkdir -p /var/cache/oracle-jdk11-installer-local/
```

É importante que a pasta criada tenha exatamente o mesmo nome especificado no comando acima ``oracle-jdk11-installer-local`` e esteja criada no mesmo diretório ``/var/cache/`` pois o intalador que executaremos em passos seguintes neste guia, usa esta pasta como referência para buscar o pacote contendo o JDK que baixamos.

Agora vamos copiar o packote que está na pasta pessoal para o diretório que acabamos de criar. Lembre de verificar o comando abaixo, pois nele escrevemos exatamente o nome do arquivo da pasta pessoal, onde dependendo de quando estiver executando esse guia o JDK pode estar em uma versão acima da expecificada neste guia que é a **11.0.11** e caso a sua seja diferente, terá que alterar o comando abaixo.

**INPUT:**
```
sudo cp jdk-11.0.11_linux-x64_bin.tar.gz /var/cache/oracle-jdk11-installer-local/
```

Lembra que disse que o PPA disponibiliza novos pacotes para baixarmos? é neste passo que ele será necessário para instalação do ```oracle-java11-installer-local``` que é um script disponibilizado pela Oracle para instalação/configuração do **Oracle-JDK**.

Durante o processo de instalação aparecerá uma caixa de diálogo com os termos de uso da Oracle para aceitar, para selecionar o **Ok** use as teclas direcionais do teclado e a barra de espaço para confirmar. 

Apos essa primeira tela de seleção aparecerá uma nova tela contendo duas opções de escolha **Yes / No** selecione **Yes** e confirme.

**OBS**: as caixas de diálogo só aparecerão caso seja a primeira vez que está executando está instalação. mas não se preocupe se não aparecer.

**INPUT:**
```
sudo apt install oracle-java11-installer-local
```

Com isso o JDK11 já deve estar instalado e configurado no seu sistema.

## 🧪 Teste
Caso tenha mais de uma versão do **JDK** instalado pode usar o ``update-alternatives --config`` para alternar entre eles. Este passo pode servir de garantia para saber se o processo de instalação correu bem.

**INPUT:**
```
sudo update-alternatives --config java
```

Caso tenha apenas uma versão do **JDK** instalada no sistema, aparecerá uma mensagem informando que só existe uma alternativa.

**OUTPUT:**
```
Existe apenas uma alternativa no grupo de ligação java (que disponibiliza /usr/bin/java: /usr/lib/jvm/java-11-openjdk-amd64/bin/java
Nada para configurar.
```

Mas caso tenha outros instalados aparecerá uma listagem com todos os packotes Java conhecidos pelo sistema, e pedirá que escolha qual usar.

**OUTPUT:**
```
Existem 2 escolhas para a alternativa java (disponibiliza /usr/bin/java).

  Selecção   Caminho                                      Prioridade Estado
------------------------------------------------------------
  0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java   1111      modo automático
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java   1111      modo manual
* 2            /usr/lib/jvm/java-11-oracle/bin/java          1091      modo manual

Pressione <enter> para manter a escolha actual[*], ou digite o número da selecção:
```

Apos todo esse processo poderá executar o comando ``java -version`` no terminal e se tudo correu bem aparecera algo como:

**OUTPUT:**
```
java version "11.0.11" 2021-04-20 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.11+9-LTS-194)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.11+9-LTS-194, mixed mode)
```

## ❌ Desinstalação
Se decidir remover o Oracle-JDK-11 instalado por este guia basta desinstalar o pacote ``oracle-java11-installer-local``.

**INPUT:**
```
sudo apt remove oracle-java11-installer-local
```

## Conclusão
Espero ter ajudado alguém com esse guia e se encontrou algum problema ou tem algo a acrescentar sinta-se avontade.

<hr />

### 🔗 Links
[Tutorial refêrencia para criação deste repositório](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04)

