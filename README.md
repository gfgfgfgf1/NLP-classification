# Pet-проект "NLP-classification".
Основная идея данного проекта заключалась в изучении классификации текстов.


**Используемые языки:**
* Python


**Используемые данные:**

Этот набор данных является частью коллекции новостей AG. Он содержит 4 класса новостей: мировые, спортивные, деловые и научно-технические.
Имеется 120 тысяч тренировочных выборок.

Описание столбцов:

- Class Index  - содержит идентификатор класса, к которому относится выборка
- Title - название новости
- Description - текст новости


**Признание**

Благодарю AG за предоставленные данные и людей, чей вклад сделал этот корпус доступным для образования, творчества и научных исследований.
http://www.di.unipi.it/~gulli/AG_corpus_of_news_articles.html


## Project structure:
    .
    ├── data                        # папка под данные, необходимые для/полученные при работе
    │   ├── cleared                 # папка с сохраненными вариантами очистки текста
    │   │   └── ...
    │   ├── normalized              # папка с сохраненными вариантами нормализации текста
    |   |   └── ...
    │   ├── vectorized              # папка с сохраненными варинтами векторизации текста
    |   |   └── ...
    │   ├── test.csv                # тестовый датасет
    │   └── train.csv               # тренировочный датасет      
    ├── losses                      # папка под loss модели
    │   └── ...
    ├── models                      # общая папка под модели
    |   └── ...
    ├── preds                       # папка под сохраненные предсказания модели
    │   └── ... 
    ├── submissions                 # папка под сохраненные предсказания модели в формате csv
    |   └── ...
    ├── vectorizers                 # папка под сохраненные векторные представления данных (но они занимают слишком много места, поэтому на git их всех не выложить)
    |   └── ...
    ├── README.md                   # файл, содержащий основную информацию о проекте
    └── NLP-classification.ipynb    # файл программы

В папке data/ должен лежать файл glove.6B.100d.txt с GloVe векторами для слов, его можно скачать по ссылке (http://nlp.stanford.edu/data/glove.6B.zip)


## Задачи

1. Рассмотреть методы очистки текста из приведенного ниже списка. Изучить влияние данных методов на качество модели.

    1. удаление стоп-слов

    2. удаление знаков препинания

    3. удаление мусора (лишних пробелов / специальных символов (например, @#~<> и т.д.))

    4. удаление цифр

2. Рассмотреть стемминг (stemming) и лемматизацию (lemmatization). Изучить их влияние на качество модели.

3. Рассмотреть типы векторизации и сравните модели, обученные с их помощью:

    1. Count vectorizer

    2. TF-IDF

    3. Word2Vec

    4. GloVe or Fast Text

4. Провести обучение модели

5. Провести анализ ошибки модели, чтобы найти наилучший метод оптимизации NN.

6. Написать свою собственную модель и обучить ее.


# Полученные результаты и выводы

1. Очистку данных стоит проводить хоть какую-нибудь (лучше всего — полную), так как при её отсутствии были получены худшие метрики. 

2. Для нормализации токенов лучше всего использовать lemmatization. С ним, в среднем, модели имели больший score.

3. В качестве векторизации можно использовать Count Vectorizer, TF-IDF и GloVe (чем больше словарь/размерность вектора — тем качественнее получаются модели, но и обучение их начинает занимать больше времени). Кроме того, в Count Vectorizer и TF-IDF координаты вектора соответствуют реальным токенам, а в Word2Vec и Glove можно считать расстояние(схожесть) между токенами. Для использования Word2Vec, возможно, нужно было его больше обучать на корпусе данных.

4. Лучшей субъективной комбинацией оказалась: полная очистка текста + лемматизация + glove. (По таблице: очистка только чисел + отсутствие нормализации + glove, однако разница между ними не большая, только начиная с третьего знака после запятой). 