=====================================
## Requerimentos:

#### 'Pasta emoções'
Ela é necessaria para a análise de sentimento, e deve ser copiada na pasta raiz onde está o script.<br><br>


#### Substituir os 'xpto'
Em 1.2 <br>
"consumer_key = xpto1"<br>
"consumer_secret_key = xpto2"<br>
com as chaves obtidas para comunicação com a API do twitter
<br>
<br>
Em 4.1 <br>
"credentials = ServiceAccountCredentials.from_json_keyfile_name('xpto3', scope)"<br>
com o arquivo Json de credenciais obtido para comunicação com a API do google
<br><br>
Em 5.3 <br>
plt.savefig('xpto4',bbox_inches='tight')<br>
com o link do google drive na maquina local
<br><br>
#### No Cron:
setar o script para rodar com o parâmetro:
00,15,30,45 * * * *

#### No MongoDB

Criar um database chamado 'twitter_db'
Criar no database, as coleções:
'twitter_lst_br' <br>
'twitter_lst_ww' <br>
Sendo repectivamente para armazenar a lista de trending topics nacionais e globais.<br>
Cada coleção possuirá 3 campos após a primeira gravação.<br>
'id', 'trends' e 'Date' <br>
Contendo respectivamente, o id do objeto, uma array de 50 elementos com os trending topics, e um campo datetime.


=====================================
## Seções do Script.

#### 1 - Coleta dos trend topics
Autentica no twitter, recolhe os trend topics, higieniza a lista removendo os campos desnecessários, conecta no MongoDB e faz a gravação.

#### 2 - Geração da Tabelas
Gera as 4 tabelas:
Trendings Nacionais do momento
Trendings Globais do momento
Trendings Nacionais de 1h atrás
Trendings Globais de 1h atrás

#### 3 - Análise de sentimentos
Usando a tabela de Trendings nacionais do momento, faz uma busca e coleta uma porção de frases para cada Trending, emcima dessa coleção, faz a análise de sentimentos usando o algoritmo Naive Bayes. Na ultima rodada da busca, usa o termo 'carrefour'.

#### 4 - Análise estatística 'Carrefour'
Como o elemento 'carrefour' foi o ultimo à ser buscado, a tabela ainda contém as citações na memória. A tabela é aproveitada e enviada ao google para ser exibida no Dashboard.

#### 5 - Wordlist Carrefour
Gera uma Wordlist usando as citações que estão na memória e salva no Google Drive.