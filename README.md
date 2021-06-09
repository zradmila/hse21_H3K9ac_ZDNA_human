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

## Гистограммы длин участков 

![alt text]()

<p float="left">
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.ENCFF148UQI.hg38.png" />
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.ENCFF148UQI.hg19.png" />
</p>

<p float="left">
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.ENCFF891CHI.hg38.png" />
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.ENCFF891CHI.hg19.png" />
</p>


## Распредление длин пиков после фильтраци ( < 5000)

<p float="left">
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.ENCFF148UQI.hg19.png" />
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/filter_peaks.H3K9ac_K562.ENCFF148UQI.hg19.filtered.hist.png" />
</p>

<p float="left">
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.ENCFF891CHI.hg19.png" />
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/filter_peaks.H3K9ac_K562.ENCFF891CHI.hg19.filtered.hist.png" />
</p>

## Расположение пиков гистоновой метки H3R9ac относительно аннотироанных генов
<p float="left">
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/chip_seeker.H3K9ac_K562.ENCFF148UQI.hg19.filtered.plotAnnoPie.png" />
  <img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/chip_seeker.H3K9ac_K562.ENCFF891CHI.hg19.filtered.plotAnnoPie.png" />
</p>




Объединяем файлы с пиками с помощью bedtools

`cat  *.filtered.bed  |   sort -k1,1 -k2,2n   |   bedtools merge   >  H3K9ac_K562.merge.hg19.bed`

Визуализируем в геномном браузере 

`track visibility=dense name="ENCFF148UQI"  description="H3K9ac_K562.ENCFF148UQI.hg19.filtered.bed"
https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/data/H3K9ac_K562.ENCFF148UQI.hg19.filtered.bed`

`track visibility=dense name="ENCFF891CHI"  description="H3K9ac_K562.ENCFF148UQI.hg19.filtered.bed"
https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/data/H3K9ac_K562.ENCFF891CHI.hg19.filtered.bed`

Визуализируем объединения на геномном браузере

`track visibility=dense name="ChIP_merge"  color=50,50,200   description="H3K9ас_K562.merge.hg19.bed"
https://raw.githubusercontent.com/zradmila/hse21_H3K9ac_ZDNA_human/main/data/H3K9ac_K562.merge.hg19.bed`


## Анализ участков вторичной стр-ры ДНК
### Распределение длин участков вторичной структуры ДНК 

<img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.DeepZ.png" />

### Расположение участков вторичной структуры относительно аннотированных генов

<img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/chip_seeker.DeepZ.plotAnnoPie.png" />

## Анализ пересечений гистоновой метки и структуры ДНК

Находим пересечения между гистоновой меткой и ZDNA

`bedtools intersect -a DeepZ.bed -b H3K9ac_K562.merge.hg19.bed > H3K9ac_K562.intersect_with_DeepZ.hg19.bed`

### Распределние длин участков пересечений

<img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/len_hist.H3K9ac_K562.intersect_with_DeepZ.hg19.png" />

### Визуализация в геномном браузере исходных участков структуры ДНК, а также их пересечения с гистоновой меткой

`track visibility=dense name="DeepZ"  color=0,200,0  description="DeepZ"
https://raw.githubusercontent.com/zradmila/hse21_H3K9ac_ZDNA_human/main/data/DeepZ.bed`

`track visibility=dense name="intersect_with_DeepZ"  color=200,0,0  description="H3K9ac_K562.intersect_with_DeepZ.bed"
https://raw.githubusercontent.com/zradmila/hse21_H3K9ac_ZDNA_human/main/data/H3K9ac_K562.intersect_with_DeepZ.hg19.bed`

Координаты: chr12:46,113,780-46,131,507 

<img alt="ex1" src="https://user-images.githubusercontent.com/49398049/121356735-cdeb4980-c939-11eb-96b4-69a35d2c7a9a.png">

Координаты: chr12:69,975,062-69,983,874

<img alt="ex2" src="https://user-images.githubusercontent.com/49398049/121357941-e4de6b80-c93a-11eb-945b-8060e2143dee.png">

### Ассоциируем полученные пересечения с ближайшими генами

<img width="45%" src="https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/images/chip_seeker.H3K9ac_K562.intersect_with_DeepZ.hg19.plotAnnoPie.png" />

Всего [10120](https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/data/H3K9ac_K562.intersect_with_DeepZ.genes.txt) пиков, ассоциированных с генами, из них [6928](https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/data/H3K9ac_k562.intersect_with_DeepZ.genes_uniq.txt) уникальных

## GO-анализ

Был проведен GO-анализ для уникальных генов с использованием сайта http://pantherdb.org/ 

<img width="946" alt="go_analysis" src="https://user-images.githubusercontent.com/49398049/121353676-c6767100-c936-11eb-944e-87e501aa780a.png">

Полный список категорий приведен [здесь](https://github.com/zradmila/hse21_H3K9ac_ZDNA_human/blob/main/data/pantherdb_GO_analysis.txt.txt)
