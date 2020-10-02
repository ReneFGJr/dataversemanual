Handle.net

Configurando a Database, as opções da Database são configuradas através de requisições http através da linha de comando. Para esse fim utiliza-se o CURL

Para listar as configurações atuais, execute:
# curl localhost:8080/api/admin/settings

Para editar alguma configuração, execute:

# curl -X PUT -d (novo valor) localhost:8080/api/admin/settings/:(configuração)

Primeiro é necessário informar o Dataverse que será utilizado handle em vez do DOI que vem por padrão. Para isso, edita-se o valor de : “Protocol” para hdl

curl -X PUT -d 'hdl' localhost:8080/api/admin/settings/:Protocol
Em seguida, é necessário informar o Dataverse o prefixo handle através da configuração :Authority
# curl -X PUT -d '20.500.11959' localhost:8080/api/admin/settings/:Authority

Configurar o estilo de geração do identificador, uma vez que o HANDLE funciona com números e o dataverse vem configurado de modo a gerar uma string de caracteres aleatórios para o doi, deve-se mudar a opção :IdentifierGenerationStyle com o comando:
# curl -X PUT -d 'sequentialNumber' localhost:8080/api/admin/settings/:IdentifierGenerationStyle
Após, baixe o arquivo createsequence.sql no link http://guides.dataverse.org/en/latest/_downloads/createsequence.sql e através do usuario postgres execute-o na tabela dvndb, para gerar o contador da sequência na base de dados.
sudo -u postgres -i
wget http://guides.dataverse.org/en/latest/_downloads/createsequence.sql
psql dvndb 
\i createsequence.sql


curl -X PUT -d 'cedap' localhost:8080/api/admin/settings/:Shoulder

Configurando a JVM
Há dois modos de configurar as opções da JVM: via linha de comando através ou editando o arquivo domain.xml. A maior diferença entre um e outro é que editar o arquivo requer que o servidor seja reiniciado para que as alterações façam efeito. Por tanto, é preferível configurar via linha de comando. Caso seja necessário, o arquivo domain.xml fica no seguinte caminho:
/usr/local/glassfish4/glassfish/domains/domain1/config/domain.xml

Para acessar o aplicativo e configurar via linha de comando, é necessário estar no diretório /bin do servidor.
cd /usr/local/glassfish4/glassfish/bin
Dentro do diretório, é só executar o app asadmin passando os comandos como parâmetros.
Para listas as configurações atuais execute:
./asadmin list-jvm-options
Caso o sistema peça por senha, ela se encontra no arquivo local-password dentro da pasta glassfish/domains/domain1/config

Para alterar configurações já definidas, se faz necessário deletar a versão atual e depois cria-la novamente através dos comandos delete-jvm-options e create-jvm-options.
Como o dataverse vem configurado para doi, inicialmente não há a necessidade de substituir(deletar e criar novamente) sendo possível, somente criar as configurações do HANDLE
./asadmin create-jvm-options '-Ddataverse.handlenet.admcredfile=/hs/svr_1/admpriv.bin'
./asadmin create-jvm-options '-Ddataverse.handlenet.admprivphrase=SENHA DO ADMPRIV AQUI'
./asadmin create-jvm-options '-Ddataverse.handlenet.index=300'

