---
layout: post
title:  "Нейронные сети - это просто! Или классифицируем текст с помошью fasttext"
date:   2018-04-12
image: posts/2018_06_04_00.png
category: Tutorial
---
<p class="intro"><span class="dropcap">В</span>сем добрый день! на дворе лето, а значит пришло время заняться чем то необычным. Сейчас многие говорят про исскуственный интелект, восстание роботов и прочее. Вот и я решил приобщиться в созданию матрицы))0) Да ладно, шучу. На самом деле я как то набрел на одну очень занятную библиотеку от Facebook и решил поведать вам о ней.</p>

<blockquote>Сегодня мы поробуем классифицировать текст с помощью <b>fastText</b>.</blockquote>

### About fastText
**fastText** – это библиотека для обучения представлениям слов и классификации предложений. Инструмент поддерживает несколько языков, включая английский, немецкий, испанский, французский, чешский и *русский (!)*.

Для эффективной обработки массивов данных с большим количеством различных категорий fastText использует *иерархический классификатор*, который организовывает различные категории в древовидную структуру вместо плоской.

Проект полностью открытый и исходный код доступен на [GthHub](https://github.com/facebookresearch/fastText), что не может не радовать.

fastText может как распозновать текст, выделяя классы, так и понимать похожие слова.
Для классификации текста используется [Bag of Tricks for Efficient Text Classification](https://arxiv.org/abs/1607.01759), а для слов [Enriching Word Vectors with Subword Information](https://arxiv.org/abs/1607.04606). Это пожалуй все, то нужно знать. *А теперь поехали учить компьютеры захватывать миры! Ой что это я)*

### Практика
Специально для этого переписал часть питоновского кода на `C++` и собрал проект с *Visual Studio 2017*. По этому для `Windows` ничего собирать не нужно. `Linux` - пользователи я думаю без труда соберут все необходимое себе сами, через терминал.

И так качаем [этот архив](https://1drv.ms/u/s!AqJZnSntVbn1iK9eYIhmFgLnLxJglg) и распаковываем его. В архиве валяется сам **EXE**-файл и **DLL** к нему. Если вы хотите использовать функции *fastText* в другой win32 программе - вы всегда можете сделать `DLL-Import` и вызывать необходимые вункции откуда угодно. В рамках этой статьи мы отсановимся на консольной версии приложения.

К стати о функциях, чтобы их посмотреть достаточно просто вбить имя программы в *CMD*. Вся документация перенесена и прописана:

{% highlight PowerShell %}
$ fasttext
fasttext
usage: fasttext <command> <args>

The commands supported by fasttext are:

  supervised              train a supervised classifier
  quantize                quantize a model to reduce the memory usage
  test                    evaluate a supervised classifier
  predict                 predict most likely labels
  predict-prob            predict most likely labels with probabilities
  skipgram                train a skipgram model
  cbow                    train a cbow model
  print-word-vectors      print word vectors given a trained model
  print-sentence-vectors  print sentence vectors given a trained model
  print-ngrams            print ngrams given a trained model and word
  nn                      query for nearest neighbors
  analogies               query for analogies
  dump                    dump arguments,dictionary,input/output vectors
{% endhighlight %}

Нас интересует функция `supervised`:

{% highlight PowerShell %}
$ fasttext supervised
Empty input or output path.

The following arguments are mandatory:
  -input              training file path
  -output             output file path

The following arguments are optional:
  -verbose            verbosity level [2]

The following arguments for the dictionary are optional:
  -minCount           minimal number of word occurences [1]
  -minCountLabel      minimal number of label occurences [0]
  -wordNgrams         max length of word ngram [1]
  -bucket             number of buckets [2000000]
  -minn               min length of char ngram [0]
  -maxn               max length of char ngram [0]
  -t                  sampling threshold [0.0001]
  -label              labels prefix [__label__]

The following arguments for training are optional:
  -lr                 learning rate [0.1]
  -lrUpdateRate       change the rate of updates for the learning rate [100]
  -dim                size of word vectors [100]
  -ws                 size of the context window [5]
  -epoch              number of epochs [5]
  -neg                number of negatives sampled [5]
  -loss               loss function {ns, hs, softmax} [softmax]
  -thread             number of threads [12]
  -pretrainedVectors  pretrained word vectors for supervised learning []
  -saveOutput         whether output params should be saved [false]

The following arguments for quantization are optional:
  -cutoff             number of words and ngrams to retain [0]
  -retrain            whether embeddings are finetuned if a cutoff is applied [false]
  -qnorm              whether the norm is quantized separately [false]
  -qout               whether the classifier is quantized [false]
  -dsub               size of each sub-vector [2]
{% endhighlight %}

#### Начинаем обучать.


Для начала подготовим **датасет**. Данные хранятся в обычном текстовом файле, где каждая строка выгядят следующим образом:

Класс | Предложение  
--- | --- 
__label__greet | *Привет* 

Все классы помечаются особым префиксом вида: `__<prefix>__<subprefix>`. Префиксы могут быть любые, но по умолчанию используется `__label__`. Префиксы вы можете задать вручную, при вызове функции отребутом `-label`.

Пусть для начала нейросеть отличает 2 класса: `приветствие` и `прощание`.

Создаем наш файл `train.txt` в дериктории с EXE - файлом:

{% highlight PowerShell %}
__label__greet Привет
__label__greet Здравствуй
__label__greet Добрый день
__label__greet Добрый вечер
__label__greet Здравствуйте
__label__greet Приветствую
__label__greet Здорова
__label__greet Доброе утро
__label__byby Пока
__label__byby До встречи
__label__byby До свидания
__label__byby Прощай
__label__byby Еще увидимся
__label__byby скоро увидимся
__label__byby до новых встречь
__label__byby Дотвиданья

{% endhighlight %}

*P.s. Enter в после последней строки - обязателен.*

**Обучим модель:**

{% highlight PowerShell %}
$ fasttext supervised -input train.txt -output model

Read 0M words
Number of words:  23
Number of labels: 2
Progress: 100.0% words/sec/thread:  153500 lr:  0.000000 loss:  0.682726 ETA:   0h 0m
{% endhighlight %}

Ура! Она обучилась! Программа создаст 2 файла: `model.bin` и `model.vec`. В *VEC* - файле - хранятся векторы наших предложений, а в *BIN* файле - сама модель. **Ну что затестим?**

Создадим текстовый файл `test.txt`:

{% highlight PowerShell %}
Дотвиданья
Пока
Прива
Приветики
Пока-пока
до вствечи
скоро увидимся
приветик
здрасьте
{% endhighlight %}

Запустим тест!!!

{% highlight PowerShell %}
$ fasttext predict model.bin test.txt
__label__byby
__label__byby
__label__greet
__label__greet
__label__greet
__label__greet
__label__greet
__label__greet
__label__greet
{% endhighlight %}

Хм... Как то сраанно оно работает? Почему так? Дело в том что изначалино программа берет очень небольное колличество итераций обучения (эпох). Как вы уже заметили на выходе она пишет: `loss:  0.682726`. Это означает, что вероянтность ошибки равна **0.6**. Увеличим эпохи. Пусть поучится подольше!

{% highlight PowerShell %}
$ fasttext supervised -input train.txt -output model -epoch 100
Read 0M words
Number of words:  23
Number of labels: 2
Progress: 100.0% words/sec/thread:   55134 lr:  0.000000 loss:  0.456773 ETA:   0h 0m
{% endhighlight %}

Уже лучше! Пробуем еще! Как завещал **Ленин**: *"Учиться, учиться..."*!

{% highlight PowerShell %}
$ fasttext supervised -input train.txt -output model -epoch 100
Read 0M words
Number of words:  23
Number of labels: 2
Progress: 100.0% words/sec/thread: 5535271 lr:  0.000000 loss:  0.008991 ETA:   0h 0m
{% endhighlight %}

Превосходно! Тестим!

{% highlight PowerShell %}
$ fasttext predict model.bin test.txt
__label__byby
__label__byby
__label__greet
__label__greet
__label__greet
__label__byby
__label__byby
__label__greet
__label__greet
{% endhighlight %}

PROFIT!

### P.s.
Я надеюсь, что благодаря этой статье вы сможете поиграться с нейронками и классификацией текста. Безусловно, для чего то более серьезного - требуются более серьезные наборы данных, подготовленных специальным образом. В общем эксперементируйте и дерзайте!