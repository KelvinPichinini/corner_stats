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

- generate_report()
    Acessa o site https://www.totalcorner.com/match/today, pega as informações de todas as partidas de hoje que ainda não aconteceram e faz uma análise baseada em jogos passados para obter a chance (e também a odd considerada justa) de acontecer um número de escanteios acima ou abaixo de alguns limites comumente utilizado em casas de apostas esportivas. Ao final salva essas odds justas em uma planilha do excel.
    
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

