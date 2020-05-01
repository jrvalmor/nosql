Agora, de dentro da imagem faça os sefuintes procedimentos:
	1. Crie a tabela com 2 famílias de colunas:
	a. personal-data
	b. professional-data

hbase(main):004:0> create 'italians', 'personal-data', 'professional-data'
Created table italians
Took 0.7927 seconds
=> Hbase::Table - italians
hbase(main):005:0> 


	2. Importe o arquivo via linha de comando

root@6da1bf094c16:/tmp# hbase shell /tmp/italians.hbase
2020-05-01 20:28:16,843 WARN  [main] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Took 0.4528 seconds
Took 0.0047 seconds
Took 0.0042 seconds
Took 0.0048 seconds
Took 0.0043 seconds
Took 0.0055 seconds
Took 0.0042 seconds
Took 0.0041 seconds
Took 0.0026 seconds
Took 0.0028 seconds
Took 0.0023 seconds
Took 0.0026 seconds
Took 0.0037 seconds
Took 0.0031 seconds
Took 0.0031 seconds
Took 0.0055 seconds
Took 0.0039 seconds
Took 0.0040 seconds
Took 0.0039 seconds
Took 0.0061 seconds
Took 0.0034 seconds
Took 0.0033 seconds
Took 0.0026 seconds
Took 0.0033 seconds
Took 0.0045 seconds
Took 0.0030 seconds
Took 0.0035 seconds
Took 0.0029 seconds
Took 0.0037 seconds
Took 0.0133 seconds
Took 0.0035 seconds
Took 0.0072 seconds
Took 0.0024 seconds
Took 0.0032 seconds
Took 0.0029 seconds
Took 0.0033 seconds
Took 0.0031 seconds
Took 0.0030 seconds
Took 0.0045 seconds
Took 0.0031 seconds
HBase Shell
Use "help" to get list of supported commands.
Use "exit" to quit this interactive shell.
For Reference, please visit: http://hbase.apache.org/2.0/book.html#shell
Version 2.1.2, r1dfc418f77801fbfb59a125756891b9100c1fc6d, Sun Dec 30 21:45:09 PST 2018
Took 0.0017 seconds
hbase(main):001:0>



	Agora execute as seguintes operações:
	1. Adicione mais 2 italianos mantendo adicionando informações como data de nascimento nas informações pessoais e um atributo de anos de experiência nas informações profissionais;

hbase(main):008:0> put 'italians', '21', 'personal-data:name',  'Giovanni Milano'
Took 0.0429 seconds
hbase(main):009:0> put 'italians', '21', 'personal-data:city',  'Verona'
Took 0.0027 seconds
hbase(main):010:0> put 'italians', '21', 'personal-data:borndate',  '20001201'
Took 0.0051 seconds
hbase(main):011:0> put 'italians', '21', 'professional-data:role',  'Gestao Comercial'
Took 0.0045 seconds
hbase(main):012:0> put 'italians', '21', 'professional-data:salary',  '2394'
Took 0.0076 seconds
hbase(main):013:0> put 'italians', '21', 'professional-data:experience',  '4'
Took 0.0031 seconds
hbase(main):014:0> put 'italians', '22', 'personal-data:name',  'Domingos Athena'
Took 0.0027 seconds
hbase(main):015:0> put 'italians', '22', 'personal-data:city',  'Padua'
Took 0.0029 seconds
hbase(main):016:0> put 'italians', '21', 'personal-data:borndate',  '20051212'
Took 0.0027 seconds
hbase(main):017:0> put 'italians', '22', 'professional-data:role',  'Psicopedagogia'
Took 0.0034 seconds
hbase(main):018:0> put 'italians', '22', 'professional-data:salary',  '11890'
Took 0.0055 seconds
hbase(main):019:0> put 'italians', '21', 'professional-data:experience',  '1'
Took 0.0059 seconds
hbase(main):020:0>



	2. Adicione o controle de 5 versões na tabela de dados pessoais.

ANTES:

hbase(main):024:0> describe 'italians'
Table italians is ENABLED
italians
COLUMN FAMILIES DESCRIPTION
{NAME => 'personal-data', VERSIONS => '1', EVICT_BLOCKS_ON_CLOSE => 'false', NEW_VERSION_BEHAVIOR => 'false', KEEP_DELETED_CELLS => 'FALSE
', CACHE_DATA_ON_WRITE => 'false', DATA_BLOCK_ENCODING => 'NONE', TTL => 'FOREVER', MIN_VERSIONS => '0', REPLICATION_SCOPE => '0', BLOOMFI
LTER => 'ROW', CACHE_INDEX_ON_WRITE => 'false', IN_MEMORY => 'false', CACHE_BLOOMS_ON_WRITE => 'false', PREFETCH_BLOCKS_ON_OPEN => 'false'
, COMPRESSION => 'NONE', BLOCKCACHE => 'true', BLOCKSIZE => '65536'}
{NAME => 'professional-data', VERSIONS => '1', EVICT_BLOCKS_ON_CLOSE => 'false', NEW_VERSION_BEHAVIOR => 'false', KEEP_DELETED_CELLS => 'F
ALSE', CACHE_DATA_ON_WRITE => 'false', DATA_BLOCK_ENCODING => 'NONE', TTL => 'FOREVER', MIN_VERSIONS => '0', REPLICATION_SCOPE => '0', BLO
OMFILTER => 'ROW', CACHE_INDEX_ON_WRITE => 'false', IN_MEMORY => 'false', CACHE_BLOOMS_ON_WRITE => 'false', PREFETCH_BLOCKS_ON_OPEN => 'fa
lse', COMPRESSION => 'NONE', BLOCKCACHE => 'true', BLOCKSIZE => '65536'}
2 row(s)
Took 0.0405 seconds

EXECUÇÃO:

hbase(main):025:0> alter 'italians', NAME => 'personal-data', VERSIONS => 5
Updating all regions with the new schema...
1/1 regions updated.
Done.
Took 2.0400 seconds


DESPOIS:

hbase(main):026:0> describe 'italians'
Table italians is ENABLED
italians
COLUMN FAMILIES DESCRIPTION
{NAME => 'personal-data', VERSIONS => '5', EVICT_BLOCKS_ON_CLOSE => 'false', NEW_VERSION_BEHAVIOR => 'false', KEEP_DELETED_CELLS => 'FALSE
', CACHE_DATA_ON_WRITE => 'false', DATA_BLOCK_ENCODING => 'NONE', TTL => 'FOREVER', MIN_VERSIONS => '0', REPLICATION_SCOPE => '0', BLOOMFI
LTER => 'ROW', CACHE_INDEX_ON_WRITE => 'false', IN_MEMORY => 'false', CACHE_BLOOMS_ON_WRITE => 'false', PREFETCH_BLOCKS_ON_OPEN => 'false'
, COMPRESSION => 'NONE', BLOCKCACHE => 'true', BLOCKSIZE => '65536'}
{NAME => 'professional-data', VERSIONS => '1', EVICT_BLOCKS_ON_CLOSE => 'false', NEW_VERSION_BEHAVIOR => 'false', KEEP_DELETED_CELLS => 'F
ALSE', CACHE_DATA_ON_WRITE => 'false', DATA_BLOCK_ENCODING => 'NONE', TTL => 'FOREVER', MIN_VERSIONS => '0', REPLICATION_SCOPE => '0', BLO
OMFILTER => 'ROW', CACHE_INDEX_ON_WRITE => 'false', IN_MEMORY => 'false', CACHE_BLOOMS_ON_WRITE => 'false', PREFETCH_BLOCKS_ON_OPEN => 'fa
lse', COMPRESSION => 'NONE', BLOCKCACHE => 'true', BLOCKSIZE => '65536'}
2 row(s)
Took 0.0309 seconds
hbase(main):027:0>



	3. Faça 5 alterações em um dos italianos;

hbase(main):027:0> put 'italians', '21', 'personal-data:city',  'Sicilia'
Took 0.0120 seconds
hbase(main):028:0> put 'italians', '21', 'personal-data:city',  'Roma'
Took 0.0038 seconds
hbase(main):029:0> put 'italians', '21', 'personal-data:city',  'Turin'
Took 0.0050 seconds
hbase(main):030:0> put 'italians', '21', 'personal-data:city',  'Veneza'
Took 0.0038 seconds
hbase(main):031:0> put 'italians', '21', 'personal-data:city',  'Saldagna'
Took 0.0047 seconds
hbase(main):032:0>



	4. Com o operador get, verifique como o HBase armazenou o histórico.

hbase(main):033:0> get 'italians', '21', {COLUMN => 'personal-data:city', VERSIONS => 5}
COLUMN                              CELL
 personal-data:city                 timestamp=1588366350806, value=Saldagna
 personal-data:city                 timestamp=1588366344828, value=Veneza
 personal-data:city                 timestamp=1588366340308, value=Turin
 personal-data:city                 timestamp=1588366333721, value=Roma
 personal-data:city                 timestamp=1588366326866, value=Sicilia
1 row(s)
Took 0.0283 seconds
hbase(main):034:0>


	5. Utilize o scan para mostrar apenas o nome e profissão dos italianos.

hbase(main):035:0> scan 'italians', {COLUMNS => ['personal-data:name', 'professional-data:role']}
ROW                                 COLUMN+CELL
 1                                  column=personal-data:name, timestamp=1588364897747, value=Paolo Sorrentino
 1                                  column=professional-data:role, timestamp=1588364897787, value=Gestao Comercial
 10                                 column=personal-data:name, timestamp=1588364897980, value=Giovanna Caputo
 10                                 column=professional-data:role, timestamp=1588364897999, value=Comunicacao Institucional
 2                                  column=personal-data:name, timestamp=1588364897798, value=Domenico Barbieri
 2                                  column=professional-data:role, timestamp=1588364897810, value=Psicopedagogia
 21                                 column=personal-data:name, timestamp=1588365754442, value=Giovanni Milano
 21                                 column=professional-data:role, timestamp=1588365776287, value=Gestao Comercial
 22                                 column=personal-data:name, timestamp=1588365784168, value=Domingos Athena
 22                                 column=professional-data:role, timestamp=1588365784258, value=Psicopedagogia
 3                                  column=personal-data:name, timestamp=1588364897820, value=Maria Parisi
 3                                  column=professional-data:role, timestamp=1588364897827, value=Optometria
 4                                  column=personal-data:name, timestamp=1588364897834, value=Silvia Gallo
 4                                  column=professional-data:role, timestamp=1588364897842, value=Engenharia Industrial Madeireira
 5                                  column=personal-data:name, timestamp=1588364897856, value=Rosa Donati
 5                                  column=professional-data:role, timestamp=1588364897872, value=Mecatronica Industrial
 6                                  column=personal-data:name, timestamp=1588364897885, value=Simone Lombardo
 6                                  column=professional-data:role, timestamp=1588364897904, value=Biotecnologia e Bioquimica
 7                                  column=personal-data:name, timestamp=1588364897913, value=Barbara Ferretti
 7                                  column=professional-data:role, timestamp=1588364897923, value=Libras
 8                                  column=personal-data:name, timestamp=1588364897932, value=Simone Ferrara
 8                                  column=professional-data:role, timestamp=1588364897952, value=Engenharia de Minas
 9                                  column=personal-data:name, timestamp=1588364897964, value=Vincenzo Giordano
 9                                  column=professional-data:role, timestamp=1588364897972, value=Marketing
12 row(s)
Took 0.0710 seconds
hbase(main):036:0>



	6. Apague os italianos com row id ímpar



	7. Crie um contador de idade 55 para o italiano de row id 5



	8. Incremente a idade do italiano em 1


