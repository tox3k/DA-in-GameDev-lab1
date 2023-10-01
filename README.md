# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил:
- Колчин Андрей Алексеевич
- РИ220950
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Установить программное обеспечение, необходимое для работы с курсом и познакомиться с первыми этапами его использования.

## Задание 1
### Написать программу Hello World на Python с запуском в Jupiter Notebook.
Ход работы:
- Устанавливаем Anaconda и открывает Jupiter Notebook
- Создаем папку и в ней создаем файл .ipynb
- Открываем файл
- Используем функцию print()

```py
print('Hello World!')
```
![image](https://github.com/tox3k/DA-in-GameDev-lab1/assets/146218000/01258a16-93c6-48b3-89dd-3a8a307d34ab)


## Задание 2
###  Написать программу Hello World на C# с запуском на Unity. 
Ход работы:
- Устанавливаем Unity и создаем проект
- Создаем скрипт и вешаем его на любой объект сцены
- В методе Start используем print() и выводим строку в консоль

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HelloWorldScript : MonoBehaviour
{
    void Start()
    {
        print("Hello World!");
    }
}

```
![image](https://github.com/tox3k/DA-in-GameDev-lab1/assets/146218000/e8e927ea-2662-4149-8067-2fc2c3444af2)

![image](https://github.com/tox3k/DA-in-GameDev-lab1/assets/146218000/44b32ae2-b65c-4537-b9b4-1e0717bce923)


## Задание 3
### Оформить отчет в виде документации на github (markdown-разметка).
Ход работы:
- Создаем аккаунт на GitHub
- Клонируем репозиторий шаблона
- Пишем отчет

## Выводы

В результате проделанной работы я познакомился с таким ПО как Anaconda и впервые использовал его для написания кода на языке Python. Использование Unity не было для меня новинкой, поэтому я просто вспомнил и закрепил для себя такие базовые вещи как вывод информации в консоль при помощи скрипта. GitHub также не был для меня чем-то новым, но как гласит русская поговорка "Повторенье - мать ученья!"

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
