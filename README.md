# CORNER_STATS
Projeto de web scrapping e análise de dados sobre escanteios em partidas de futebol.

Bibliotecas utilizadas:
Pandas,
Selenium,
BeautifulSoup,
cloudscrapper,

As informações são retiradas do site https://www.totalcorner.com/.



FUNÇÕES:

- get_corner_stats(team_id:str,is_home:bool)

    Recebe como paramâtros o id do time no site totalcorner, e um booleano informando se você quer as informações do time jogando como visitante ou em casa. O parametro is_home é opcional, caso não seja passado nenhum valor o dataframe resultante irá conter as informaçoes de todos os jogos (tanto em casa quanto fora).
    Essa função retorna uma tupla com o nome do time e um dataframe com as estatisticas de escanteio.

- get_league_stats(league_href:str, minimum_games:int)

    Recebe como parametro a referencia da URL da pagina da liga no site total corner, por exemplo a pagina da Serie A do Brasil tem a seguinte url de referencia: '/league/view/129'. O parametro minimum_games é o número mínimo de jogos a serem coletados. retorna um DataFrame com as colunas: 
    'date',
    'home_team' ,
    'home_goals' ,
    'away_goals' ,
    'away_team' ,
    'ft_home_corners' ,
    'ft_away_corners' ,
    'ht_home_corners' ,
    'ht_away_corners' ,
    'home_atacks' ,
    'away_attacks' ,
    'home_shots' ,
    'away_shots' ,

- get_expected_corners(league_df, df_home, df_away):

    Deve receber como parametro o dataframe retornado na função 'get_league_stats' (league_df) e dois dataframes retornados da função 'get_corner_stats'(df_home,df_away). Essa função calcula a força relativa entre os times e a média da liga para retornar um valor de escanteios esperados no confronto entre as duas equipes. Retorna um dicionário com as chaves:
    'home_ft' - Escanteios a favor do time mandante durante a partida completa
        'home_ht' - Escanteios a favor do time mandante durante o primeiro tempo
        'away_ft' - Escanteios a favor do time visitante durante a partida completa
        'away_ht' - Escanteios a favor do time visitante durante o primeiro tempo
        
- get_fairlines(expected_corners,corners_range,ht_corners_range):

    Recebe como parametro o dicionario retorno da função 'get_expected_corners' e os ranges desejados para as odds de over e under escanteios no full-time e half-time. Utiliza distribuição de poisson para encontrar as probabilidades e retorna um dicionário com todas as fairlines calculadas. 

- generate_report()

    Acessa o site https://www.totalcorner.com/, pega as informações de todas as partidas do dia que ainda não aconteceram e faz uma análise baseada em jogos passados para obter a chance (e também a odd considerada justa) de acontecer um número de escanteios acima ou abaixo de alguns limites comumente utilizado em casas de apostas esportivas. Ao final salva essas odds justas em uma planilha do excel.
    
- get_odds()

    Acessa o site da Betano e busca todas as odds nos mercados de escanteios HT e FT. recebe como parametro uma string com o jogo a ser procurado no site.
    retorna um objeto onde as chaves são os nomes dos mercados encontrados e os valores são as odds.
    
    Exemplo de retorno:
    {
    "Name":"Corinthians X Palmeiras",
    "FT_over_9.5": 1.5,
    "1H_under_4.5": 1.2
    }
    
    FT_over_9.5 significa mais de 9.5 escanteios no fulltime(jogo completo)
    
    1H_under_4.5 significa menos de 4.5 escanteios no primeiro tempo
    
    

![Alt text](/Screenshot1.png "Planilha")

Os valores da tabela são as odds consideradas justas pelo modelo. A odd justa é o inverso da probabilidade de um evento acontecer. (um evento com 50% de acontecer irá ter odd justa = 1/0.5 = 2.0

1H: Primeiro tempo

FT: Full-time, Jogo completo

### ATENÇÃO! O MODELO PARA CÁLCULO DA CHANCE DE OCORRER MAIS OU MENOS QUE UM DETERMINADO NÚMERO DE ESCANTEIOS NÃO FOI TESTADO AINDA. PROJETO APENAS PARA FINS ACADÊMICOS, NÃO É UMA RECOMENDAÇÃO DE APOSTA

