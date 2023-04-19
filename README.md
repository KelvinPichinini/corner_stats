# corner_stats
Projeto de web scrapping e análise de dados sobre escanteios em partidas de futebol.

As informações são retiradas do site https://www.totalcorner.com/.

FUNÇÕES:

- get_corner_stats(team_id:str,is_home:bool)
    Recebe como paramentros o id do time no site totalcorner, e um booleano informando se você quer as informações do time jogando como visitante ou em casa.

- generate_report()
    Acessa o site https://www.totalcorner.com/match/today, pega as informações de todas as partidas de hoje que ainda não aconteceram e faz uma análise baseada em jogos passados para obter a chance (e também a odd considerada justa) de acontecer um número de escanteios acima ou abaixo de alguns limites comumente utilizado em casas de apostas esportivas. Ao final salva essas odds justas em uma planilha do excel.

![Alt text](/Screenshot1.png "Planilha")

1H: Primeiro tempo
FT: Full-time, Jogo completo
