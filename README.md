# Guia de Instalação do Oracle JDK11

## Observações

Este guia foi criado com base na versão **11.0.11** do JDK e no Ubuntu **20.04-lts** e alguns passos podem **não funcionar** em outras distribuições ou mesmo em outras versões do Ubuntu.

Sigua este guia com cuidado se atentando aos detalhes como a sub versão dos pacotes (**11.0.11 / 11.X.XX**), que podem variar dependendo de quando está vendo este guia.

## Baixando o pacote JDK
Para esta instalação vamos usar o pacote compactado ``.tar.gz`` disponível no site da Oracle que é o formato mais usado para esta instalação.

[Clique para ir a pagina de download](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)

Nesta página você precisara aceitar os termos de uso, e caso não tenha uma conta Oracla o cadastro será requisitado antes do download.

Fique atento para baixar o arquivo correto para a arquitetura do seu processador, onde o badrão da maioria é o **X64**.

## Preparação

Antes de proceguir com a instalação vamos precisar instalar algumas dependências antes.

A primeira é o ``software-properties-common`` para habilitar a instalação de software de terceiros. Uma vez que o JDK disponibiliazado pela Oracle não pode ser obtido atravez do repositório oficial do Ubuntu.

```
sudo apt install software-properties-common
```

Em seguida baixamos a chave de assinatura, para o software que vamos instalar logo em seguida. Essa chave é usada para verificar se o software é válido.

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EA8CACC073C3DB2A
```

Agora vamos adicionar um PPA, que é basicamente um repositório extra que irá nos fornecer pacotes/softwares que não estão disponíves por padrão, quando tentamos fazer uma instalação via apt por exemplo.

**OBS:** copie apenas um comando por vez.

```
sudo add-apt-repository ppa:linuxuprising/java

sudo apt update
```

## Instalação
Agora que já baixamos o pacote do JDK ele deve se encontrar disponível na sua pasta de **Downloads**. Copie o arquivo para sua pasta pessoal.

Uma vez tendo copiado o arquivo para a sua pasta pessoal abra o terminal ``ctrl + alt + t``, e vamos criar um novo diretório onde colocaremos o arquivo do JDK que acabamos de copiar.

```
sudo mkdir -p /var/cache/oracle-jdk11-installer-local/
```

É importante que a pasta criada tenha exatamente o mesmo nome expecificado no comando acima ``oracle-jdk11-installer-local`` e esteja criada no mesmo diretório expecificado ``/var/cache/`` pois o intalador que execultaremos em passos seguintes neste guia usa esta pasta como referência para buscar o pacote contendo o JDK que baixamos.

Agora vamos copiar o packote do JDK que está na nossa pasta pessoal para o diretório que acabamos de criar. Lembre de verificar o comando abaixo pois nele escrevemos exatamente o nome do arquivo do JDK que está na pasta pessoal e dependendo de quando estiver executando esse guia o JDK pode estar em uma versão acima da expecificada neste guia que é a **11.0.11** e caso a sua seja diferente, terá que alterar o comando abaixo.

```
sudo cp jdk-11.0.11_linux-x64_bin.tar.gz /var/cache/oracle-jdk11-installer-local/
```

Lembra que disse que o PPA disponibiliza novos pacotes para baixarmos? é neste passo que ele será necessário para instalação do ```oracle-java11-installer-local``` que é um script disponibilizado pela Oracle para instalação/configuração do **Oracle-JDK**.

Durante o processo de instalação aparecera uma caixa de dialogo com os termos de uso da Oracle para aceitar, para selecionar o **Ok** use as teclas direcionais do teclado e a barra de espaço para confirmar. Apos essa primeira tela de seleção aparecerá uma nova tela contendo duas opções de escolha **Sim/Não** selecione **Sim** e confirme.

**OBS**: as caixas de dialogo só aparecerão caso seja a primeira vez que está tentando execultar o comando abaixo. mas não se preocupe se não aparecer.

```
sudo apt install oracle-java11-installer-local
```

Com isso o JDK11 já deve estar instalado e configurado no seu sistema.

## Utilitário / Teste
Caso tenha mais de uma versão do **JDK** instalado pode usar o ``update-alternatives --config`` para alternar entre eles. Este passo pode servir de garantia para saber se o processo de instalação correu corretamente.

```
sudo update-alternatives --config java
```

Caso só tenha uma versão do **JDK** instalada no sistema aparecera uma mensagem falando qual é o JDK em uso seguido por um texto falando que não tem nada para configurar.

Mas caso tenha outros instalados aparecerá uma listagem com todos os packotes Java conhecidos pelo sistema, e pedirá para que selecione qual você quer usar.

Apos todo esse processo poderá executar o comando ``java -version`` no terminal e se tudo correu bem aparecera algo como:

```
java version "11.0.11" 2021-04-20 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.11+9-LTS-194)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.11+9-LTS-194, mixed mode)
```

## Conclusão
Espero ter ajudado ter ajudado alguem com esse guia e se alguem encontrou algum problema ou tem algo a acrescentar sinta-se avontade.

<hr />

### Links
[Tutorial refêrencia para criação deste repositório](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04)

