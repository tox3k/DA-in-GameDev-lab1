# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
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
 - Научиться использовать Python для заполнения Google Sheets
 - Научиться вытаскивать данные из Google Sheets в Unity для их дальнейшего использования

## Задание 1
### Выберите одну из компьютерных игр, приведите скриншот её геймплея и краткое описание концепта игры. Выберите одну из игровых переменных в игре (ресурсы, внутри игровая валюта, здоровье персонажей и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.
###Ход работы:
В качестве примера я выбрал игру Car For Sale Simulator.
![image](https://github.com/tox3k/DA-in-GameDev-lab1/assets/146218000/7127c0a1-7ff4-4ed7-b877-d1460d96e39d)
![cfs gameplay](https://github.com/tox3k/DA-in-GameDev-lab1/assets/146218000/884bf312-a1a9-4c49-8baa-d5cc7bdd1164)

###Концепт игры:
Игра представляет собой симулятор перекупщика автомобилей, целью которого является заработать много денег и стать главным продажником в городе.

###Игровая переменная
В качестве рассматриваемого ресурса я выбрал деньги. На старте игры мы имеем 10.000р, на которые и приобретаем свой первый автомобиль, который впоследствии продаем дороже чем купили. Деньги мы можем получить лишь двумя способами:
 - Продаем автомобили
 - Берем кредит (если вдруг что-то пошло не так)
Тратим мы деньги на:
 - Покупку автомобилей (выгодность сделки зависит от прокачки навыка "красноречие")
 - Прокачку (тюнинг) автомобилей (клиенты будут сильно сбивать цену или вовсе отказываться от покупки в случае отсутсвия хотя бы минимального тюнинга)
 - Оплату налогов (в начале игры это мизерная сумма, однако по ходу развития в игре они начинают существенно влиять на кошелек игрока)

Также стоит отметить, что по понедельникам, средам и пятницам (речь идет про внутреигровое время) работает аукцион, на котором машины можно купить гораздо дешевле.

Вот краткая экономическая модель:
![экономическая модель](https://github.com/tox3k/DA-in-GameDev-lab1/assets/146218000/a39f1a44-8693-426e-8383-c49d3cfd36f0)

## Задание 2
### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в выбранной игре (в качестве таких переменных может выступать игровая валюта, ресурсы, здоровье и т.д.). Средствами google-sheets визуализируйте данные в google-таблице (постройте график, диаграмму и пр.) для наглядного представления выбранной игровой величины.

Вот Python-скрипт, который заполняет таблицу данными:
```py
import gspread
import numpy as np
gc = gspread.service_account(filename='unitedatascience-c08f927977c4.json')
sh = gc.open("UnityWorkshop2")
car_price = np.random.randint(2000, 8000, 31)

row = 2
money = 10000
money_delta = 0

def update_sheet(action):
    sh.sheet1.update(('A' + str(row)), str(row - 1))
    sh.sheet1.update(('B' + str(row)), action)
    sh.sheet1.update(('C' + str(row)), str(money))
    sh.sheet1.update(('D' + str(row)), str(money_delta).replace('.', ','))

# Используем money //= 1 и money = int(money), чтобы кол-во денег было целым числом
for i in range(0, 31):
    #Покупка машины
    money_delta = -float(car_price[i]) / money * 100
    money -= car_price[i]
    money //= 1
    money = int(money)
    update_sheet('Покупка машины')
    row += 1
    
    #Тюнинг машины (обычно 5% от стоимости авто)
    money_delta = -float(car_price[i]) * 0.05 / money * 100
    money -= float(car_price[i]) * 0.05
    money //= 1
    money = int(money)
    update_sheet('Тюнинг машины машины')
    row+= 1
    
    #Продажа машины (машины продаются в среднем на 20% дороже, чем покупались)
    money_delta = float(car_price[i]) * 1.2 / money * 100
    money += float(car_price[i]) * 1.2
    money //= 1
    money = int(money)
    update_sheet('Продажа машины')
    row+= 1
```

Ссылка на заполненную таблицу с диаграммами: https://docs.google.com/spreadsheets/d/1CFY3Rg7sctCH_TUMQNnqaoIoNQcipHkDgAYE4MDeSNM/edit#gid=0

## Задание 3
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.

Если кол-во денег изменилось больше чем на 100%, то хорошая озвучка, если упала от 0 до 20 %, то средняя и если упала более чем на 20%, то плохая
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string,float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (dataSet.Count == 0)
        {
            return;
        }

        foreach (var pair in dataSet)
        {
            print(pair.Value);
        }
        if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] < 0 & dataSet["Mon_" + i.ToString()] > -20 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] < -20 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1CFY3Rg7sctCH_TUMQNnqaoIoNQcipHkDgAYE4MDeSNM/values/Лист1?key=AIzaSyAAH_TS6-XESBjiQNd5bTzkhWs3_PbCIdQ");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        bool skipFlag = false;
        foreach (var itemRawJson in rawJson["values"])
        {
            if (!skipFlag)
            {
                skipFlag = true;
                continue;
            }
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[3]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```

## Выводы

В ходе данной лабораторной работы я научился подключаться к Google таблицам через API-ключ для получения данных из них в Unity-скриптах, научился заполнять таблицы через Python gspread, а также работать со звуковыми файлами в Unity
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
