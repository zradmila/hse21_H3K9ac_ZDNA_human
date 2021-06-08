# hse21_H3K9ac_ZDNA_human

### Cтудент - Заикина Радмила
| Организм      | Структура ДНК | Тип клеток | Гистоновая метка| .bed файл 1| .bed файл 2  |
| ------------- |:-------------:|:----------:|:---------------:|:----------:|:------------:|
| human(hg38)   | ZDNA          | K562       | H3K9ac          | ENCFF148UQI| ENCFF891CHI |

С помощью команды wget были получены файлы с пиками:

`wget https://www.encodeproject.org/files/ENCFF148UQI/@@download/ENCFF148UQI.bed.gz` 

`wget https://www.encodeproject.org/files/ENCFF891CHI/@@download/ENCFF891CHI.bed.gz`

Оставили первые пять столбцов:

`zcat ENCFF148UQI.bed.gz | cut -f1-5 > H3K9ac_K562.ENCFF148UQI.hg38.bed` 

`zcat ENCFF891CHI.bed.gz | cut -f1-5 > H3K9ac_K562.ENCFF891CHI.hg38.bed`
