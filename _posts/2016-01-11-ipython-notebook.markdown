---
layout:     post
title:      "Зачем нужен IPython Notebook и как его использовать"
date:       2016-01-10 00:00:00
author:     "Vasiliy Zemlyanov"
header-img: "img/post-bg-05.jpg"
---

IPython Notebook - это интерактивная среда для программирования на python, которая позволяет объеденить код, текст (включая Markdown), графики, математические формулы (MathJax) и скомбинировать все в одном отчете.

#Установка

Для запуска notebook нужно в терминале выбрать директорию и воспользоваться командой `ipython notebook`.
Команда запускает сервер на 8888 порту и открывает в браузере страницу с блокнотом.

Файлы имеют расширение...

#Использование

Эти элементы называются cell-s.

`Скриншот New notebook`

Описание cell-ов.

- Code cells.
- Markdown cells.
- Raw cells.
- Heading cells.

Описание рабочего процесса
The normal workflow in a notebook is, then, quite similar to a standard IPython session, with the difference that you can edit cells in-place multiple times until you obtain the desired results, rather than having to rerun separate scripts with the %run magic command.

Возможность разбить задачу на части и организовать их в качестве cell-ов.
Typically, you will work on a computational problem in pieces, organizing related ideas into cells and moving forward once previous parts work correctly. This is much more convenient for interactive exploration than breaking up a computation into scripts that must be executed together, as was previously necessary, especially if parts of them take a long time to run.

Прервать вычисления
At certain moments, it may be necessary to interrupt a calculation which is taking too long to complete. This may be done with the Kernel | Interrupt menu option, or the Ctrl-m i keyboard shortcut. Similarly, it may be necessary or desirable to restart the whole computational process, with the Kernel | Restart menu option or Ctrl-m . shortcut.

A notebook may be downloaded in either a .ipynb or .py file from the menu option File | Download as. Choosing the .py option downloads a Python .py script, in which all rich output has been removed and the content of markdown cells have been inserted as comments.

`Скриншот ввод кода и результат`

Код cell-a выполняется комбинацией `Shift+Enter` либо кнопкой play.

`Скриншот с ошибкой`

`Скриншот с графиком`

`Скриншот с markdown`

`Скриншот с формулами`

`Sharing`

Комбинации клавиш:
Shift-Enter: run cell
Ctrl-Enter: run cell in-place
Alt-Enter: run cell, insert below
Esc and Enter: Command mode and edit mode

Пользователи `R` могут в качестве похожего инструмента использовать `R-markdown.`.
