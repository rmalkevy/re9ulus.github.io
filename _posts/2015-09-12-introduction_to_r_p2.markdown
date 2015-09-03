---
layout:     post
title:      "Основы R, типы данных часть 2"
date:       2015-09-12 12:00:00
author:     "Vasiliy Zemlyanov"
header-img: "img/post-bg-03.jpg"
---

Продолжение повествования о типах данных в `R`, первая часть здесь `вставить линк`.

#Factors

`Factors` тип данных позволяющий работать с категорическими переменными, т.е. такими переменными которые принимают ограниченное число значений и относятся к некоторой категории.
`TODO: Посмотреть в википедии понятие categorical variable и перевод на русский язык.`
Создается `factor` из вектора функцией `factor()`.

{% highlight R %}
> age <- c("young", "mature", "old", "young", "young", "mature")
> age_factor <- factor(age)
> age_factor

> str(age_factor)

> age_factor2 <- factor(age,
>                       levels = c("young", "mature", "old"))
> age_factor2

> str(age_factor2)
{% endhighlight %}

##Переименование категорий

#Lists

#Data frames