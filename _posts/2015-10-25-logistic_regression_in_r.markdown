---
layout:     post
title:      "Логистическая регрессия"
date:       2015-09-12 12:00:00
author:     "Vasiliy Zemlyanov"
header-img: "img/post-bg-03.jpg"
---

`Логистическая регрессия` - статистическая модель, которая применяется для предсказания вероятности возникновения некоторого события по значениям множества признаков.

#Модель
Обозначим предсказываемую, зависимую переменную как $$y$$. $$y$$ может принимать два значения:

$$1$$ событие произошло
$$0$$ событие не произошло

Вероятность того, что событие произойдет: $$P(y=1)$$ 

Тогда: $$P(y=0)=1 - P(y=1)$$ вероятносто того что событие не произойдет.

Используя для предсказания независимые переменные $$x_1, x_2...,x_k$$ получим функцию предсказания:

$$P(y=1)=\frac{1}{1+e^{-(B_0+B_1*x_1+B_2*x_2+...+B_k*x_k)}}$$

Функция возвращает вероятность того, что $$y=1$$, т.е. событие произошло и имеет вид:

![Logistic regression image](/assets/logistic_regression/Logistic-curve.png)

##Логистическая регрессия в R

{% highlight R %}
#  Загружаем данные в dataframe
quality = read.csv("quality.csv")
#  Анализируем структуру данных
str(quality)

#  Устанавливаем пакет, который используем для разделения наших данных на тренировочный и тестовый
install.packages("caTools")
library(caTools)

#  Случайным образом разделим наши данные на тренировочные и тестовые
#  75% - тренировочные, 25% - тестовые
split = sample.split(quality$PoorCare, SplitRatio = 0.75)
#  Тренировочные данные
qualityTrain = subset(quality, split == TRUE)
#  Тестовые данные
qualityTest  = subset(quality, split == FALSE)

#  Создаем модель функцией glm
#  Модель имеет вид:
#  НезависимаяПеременная ~ ЗависимаяПеременнеая1 + ЗависимаяПеременная2 + ... ЗависимаяПеременнаяN
#  family = binomial именно этот параметр указывает что мы хотим использовать логистическую регруссию

QualityLog = glm(PoorCare ~ OfficeVisits + Narcotics, data=qualityTrain,
                 family = binomial)

#  Рассмотрим нашу модель
summary(QualityLog)

## Вставить описание того, как читать summary модели, про важность переменных и т.д.

# Используем модель для предсказаний
predictTrain = predict(QualityLog, type="response")
summary(predictTrain)

{% endhighlight %}


# ROC (Receiver Operator Characteristics) кривая

##Threshold Value
Результатом логистической регрессии является вероятность, но чтобы сделать бинарное предсказание нам необходимо определить пороговое (`threshold`) значение, такое что:

`If P(PoorCare = 1) >= t`, predict poor qiality
`If P(PoorCare = 1) < t`, predict good quality

Если мы установим высокое пороговое значение, мы будем редко предсказывать позитивный исход (при высокой вероятности `P(y=1)`).

Если пороговое значение слишком маленькое мы будем предсказывать позитивный исход редко.

Для численного представления качества оценки можно использовать `confusion matrix`.

Если предпочтений нет можно оставить `t = 0.5`.

###Табличка
|               | Predicted = 0 | Predicted = 1|
| ------------- |:-------------:| -----:|
| Actual = 0    | True Negatives (TN) | False Positives (FP) |
| Actual = 1    | False Negatives (FN) |   True Positives (TP) |

В таблице мы видем случаи, когда наша модель делает правильные предсказания:

* TN - предсказано False, в действительности False
* TP - предсказано True, в действительности True

И когда модель ошибается

* FP - предсказано True, в действительности False
* FN - предсказано False, в действительности True.

Отсюда можно получить два значения, которые помогут нам определить какие ошибки делает модель:
Чувствительность
`Sensitivity = TP / (TP + FN)` True positive rate. И показывает процент True позитивных случаев, которые модель классифицирует верно.

Специфичность
`Specificity = TN / (TN + FP)` True negative rate. И изменяет процент негативных случаев, которые модель классифицирует верно.

Модель с более высоким пороговым значением будет иметь более высокую `sensitivity` и более низкую `Specificity`.

Классификационная таблица в `R` для разныз пороговых значений:

{% highlight R %}
# 0.5 в данном случае является пороговым значением
> table(qualityTrain$PoorCare, predictTrain > 0.5)
> sensitivity = 
> specificity = 
{% endhighlight %}

## ROC в R

Подобрать необходимое пороговое значение можно с помощью ROC-кривой.

### Картинка ROC кривой

True negative rate указывается на оси абсцисс.
True positive rate указывается на оси ординат.
Кривая показывает, как эти значения соотносятся при разных значения пороговой величины.

Построить ROC-кривую в R можно следующим набором команд:

{% highlight R %}

# Устанавливаем необходимый пакет
install.package("ROCR")
package(ROCR)

ROCRpred = prediction(predictTrain, qualityTrain$PoorCare)
ROCRperf = performance(ROCRpred, "tpr", "fpr")
plot(ROCRperf, colorize=TRUE, print.cutoffs.at=seq(0,1,0.1), text.adj=c(-0.2,1.7))

{% endhighlight %}

{% highlight R %}


{% endhighlight %}