# АНАЛИЗ ДАННЫХ В РАЗРАБОТКЕ ИГР
 Отчет по лабораторной работе №2 выполнил:
 - Подповетный Данил Артемович
 - Нмт-232203
 
 Отметка о выполнении заданий (заполняется студентом):
 
 | Задание | Выполнение | Баллы |
 | ------ | ------ | ------ |
 | Задание 1 | * | ? |
 | Задание 2 | * | ? |
 | Задание 3 | * | ? |
 
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
 - Задание 4.
 - Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
 - Задание 5.
 - Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
 - Выводы.
 
 ## Цель работы
 Научиться передавать в Unity данные из Google Sheets с помощью Python.
 
 ## Задание 1
 ### Настроить доступ к google-таблице по api
 Ход работы:
 - Перейти в https://console.cloud.google.com
 - Создать новый проект, выбрав Select a project - New project
 - Дать имя проекту и нажмите кнопку Create
 - Перейти в Dashboard созданного проекта
 - Перейти в google drive api, используя строку поиска
 - Нажать кнопку Enable API
 - Завершить создание, нажав кнопку Done
 - Сохранить файл с ключом в формате json на свой компьютер
 - Скопировать адрес сервисного аккаунта
 - Создать google-таблицу и открыть к ней доступ для редактирования с созданного сервисного аккаунта

 Все указанные действия были выполнены.

![image](https://github.com/user-attachments/assets/43f59523-1103-46a1-891b-0329a75a9646)


 ## Задание 2
 ### Генерация данных с помощью Python и их передача в google таблицу
 Ход работы:
 - Запустить Jupyter Notebook, создать новый .ipynb-файл. Сделать так, чтобы созданный файл и скачанный ранее .json-файл с ключами оказались в одной директории
 - В .ipynb файле на языке Python реализовать передачу данных в созданную ранее google-таблицу. Реализация на Python рассчитывает темп инфляции для экономической модели
 - Запустить .ipynb-файл. Убедиться, что запись данных в google-таблицу происходит корректно


 ```rb
 import gspread
 import numpy as np
 
 gc = gspread.service_account(filename='unity-data-science-11b6b2e69d3c.json')
 sh = gc.open('Unity Лаба 2')
 current_hp = 30
 i = 1
 while i < 4:
     sh.sheet1.update_acell('A' + str(i), str(i))
     sh.sheet1.update_acell('B' + str(i), str(current_hp))
     current_hp = current_hp - 10
     i += 1
 ```

 Был запущен указанный код, после чего таблица заполнилась нужными значениями.

 
 ![image](https://github.com/user-attachments/assets/489c8733-80ff-412d-8d3a-ff3433d6d8a1)



 ## Задание 3
 ### Создание ключа API для передачи данных из google-таблицы в Unity
 Ход работы:
 - Создать API key для получения данных из таблицы и обработки их в Unity
 - В поле “Restrict Key” выберать “Google Sheets API”
 - Открыть к созданной ранее google-таблице доступ по ссылке для редактирования
 - Скопировать API key

 Все указанные действия были выполнены и в дальнейшем я буду использовать этот api ключ в работе.
 
 Api ключ: AIzaSyAK9_9JK7Lfg2aoR1yjk81On-3xTOzgKb8

 ![image](https://github.com/user-attachments/assets/2cb67910-0c3e-4468-a920-655aebe35bb9)

 ## Задание 4
 ### Новый проект на Unity
 Ход работы:
 - Создатть новый 3D проект на Unity
 - Добавить в проект файлы jsonPackage и soundPackage
 - Создать на сцене Unity пустой GameObject и подключить к нему .cs скрипт, в котором описывается подключение к google-таблице по API и воспроизведение звуков в игре в соответствии со считываемыми значениями
 - Настроить инспектор свойства объекта GameObject
 - Запустить сцену. Убедиться, что происходит воспроизведение звуковых файлов в соответствии с данными из таблицы.

Все указанные действия были выполнены, 
 
 ## Задание 5
 ### Выберите одну из игровых переменных в игре СПАСТИ РТФ: Выживание (HP, SP, игровая валюта, здоровье и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.
 Ход работы:
 - Я выбрал переменную здоровье(hp), ее роль в игре отображать насколько "жив" герой за которого играет игрок, а так же ее величиная влияет на ксловие конца игры.
   Изменение переменной:
   - если игрок получил урон, то величина уменьшается
   - если игрок во время прокачки выбрал соотвествующие навыки, то они восполняют здоровье
   Диапазон допустимых значений переменной прост, от 0 и до лимита указанного в игре
 - Схема экономической модели ресурса:
 ![image](https://github.com/user-attachments/assets/06cc9fd8-b2e1-4c71-a48d-92e51eca96e1)
 
 ## Задание 2
 ### ### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в игре “СПАСТИ РТФ:Выживание”. Средствами google-sheets визуализируйте данные в google-таблице (постройте график / диаграмму и пр.) для наглядного представления выбранной игровой величины. Опишите характер изменения этой величины, опишите недостатки в реализации этой величины (например, в игре может произойти условие наступления эксплойта) и предложите до 3-х вариантов модификации условий работы с переменной, чтобы сделать игровой опыт лучше.
 Ход работы:
 - Для начала нужно определить как меняется выбранная мной игровая переменная:
 Здоровье игрока меняется в зависимсоти от получения им урона, это значит, что изменение этой переменной зависит от игрока и его навыка. Поскольку есть множество вариантов изменения этого параметра, я, для простоты, взял ситуацию когда игрок просто получает урон с некоторым промежутком времени.
 - Из-за простоты выбранной ситуации график изменения переменной выглядит как обычная прямая (В более сложных ситуациях график может иметь более сложное поведене):
 ![image](https://github.com/user-attachments/assets/f582d53d-1021-435d-ae6b-f2c698462f8d)
 Ссылка на таблицу: https://docs.google.com/spreadsheets/d/1-TBYwyDcrPz_f4pHD6Jv8I1gbH_UNFmD-HplJS98Nkk/edit?gid=0#gid=0
 - Из графика видно что величина меняться от 30 (лимит здоровья) до 0 (конец игры), уменьшение величины происходит когда игрок получает урон (в данном примере -10),   а увеличение когда игрок либо "вампириться", либо заканчивает волну. Недостатков в реализации величины нету, посколько она изменяется довольно логично и просто
 - Заполнение таблицы было выполненно с помощью кода на Python:
 ```Python
 import gspread
 import numpy as np
 gc = gspread.service_account(filename = 'unitydatascience-438210-b0e595b74019.json')#Создание клиентской сессии 
 sh = gc.open("UnityWorkshop2")#Подключение к таблице
 current_hp = 30
 i = 0
 while current_hp >= 0:
     i += 1
     if i == 0:
         continue
     else:
         sh.sheet1.update_acell(('A' + str(i)), str(i))
         sh.sheet1.update_acell(('B' + str(i)), str(current_hp))
         print(current_hp)
         current_hp -= 10
 ```
 - Поскольку, в игре СПАСТИ РТФ довольно мало взаимодействия с хп и мало условий его изменения, то можно дополнить функционал игры следющими идеями:
     - Добавить предмет который увеличивает текущее здоровье двуями способами, либо моментально, либо переодически
     - Возможность расходовать текущее здоровье в замен на какой ресурс (например патроны), возможно придется добавлять новые предметы чтобы не ломать логику              старого предмета с этим нововведением
     - Возможность прибавлять предел здоровья (вне прокачки) на определенный промежуток времени, например, для битвы с боссом
 
 
 ## Задание 3
 ### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.
 Ход работы:
 - Для реализации данного задания я выделил правильно по которым описывается динамика изменения здоровья:
     - Если хп около лимита (в моем случае hp >= 30), то воспроизводится звук "хороший"
     - Если хп около среднего значения (в моем случае 30 > hp >= 20), то воспроизводится звук "средний"
     - Если хп около минимума (в моем случае hp <= 0), то воспроизводится звук "плохой"
 - Для отображения этой динамики в Unity я создал компонент с таким скриптом (Это скрипт из методички, с небольшими изменениями):
 ```C#
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
     private Dictionary<string, float> dataSet = new Dictionary<string, float>();
     private bool statusStart = false;
     private int i = 1;
     void Start()
     {
         StartCoroutine(GoogleSheets());
     }
     void Update()
     {
         if (dataSet["Mon_" + i.ToString()] >= 30 & statusStart == false & i != dataSet.Count)
         {
             StartCoroutine(PlaySelectAudioGood());
             Debug.Log(dataSet["Mon_" + i.ToString()]);
             Debug.Log("Проигрывается звук 'Horosho'");
         }
         if (dataSet["Mon_" + i.ToString()] < 30 & dataSet["Mon_" + i.ToString()] >= 20 & statusStart == false & i != dataSet.Count)
         {
             StartCoroutine(PlaySelectAudioNormal());
             Debug.Log(dataSet["Mon_" + i.ToString()]);
             Debug.Log("Проигрывается звук 'Sredne'");
         }
         if (dataSet["Mon_" + i.ToString()] < 20 & statusStart == false & i != dataSet.Count)
         {
             StartCoroutine(PlaySelectAudioBad());
             Debug.Log(dataSet["Mon_" + i.ToString()]);
             Debug.Log("Проигрывается звук 'Ploho'");
         }
     }
 
     IEnumerator GoogleSheets()
     {
         UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1-TBYwyDcrPz_f4pHD6Jv8I1gbH_UNFmD-HplJS98Nkk/values/Лист1?key=AIzaSyBFrX6sxQ8GY5gv57Az0AXnpU1rQKbjwJU");
         yield return curentResp.SendWebRequest();
         string rawResp = curentResp.downloadHandler.text;
         var rawJson = JSON.Parse(rawResp);
         foreach (var itemRawJson in rawJson["values"])
         {
             var parseJson = JSON.Parse(itemRawJson.ToString());
             var selectRow = parseJson[0].AsStringList;
             dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[1]));
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
 - Как видно на изображении ниже, скрипт работает без проблем и в Unity наглядно изображена динамика изменения здоровья
 ![image](https://github.com/user-attachments/assets/c48c3e2a-255a-40ad-ba96-99abd890057c)
 
 ## Выводы
 
 В ходе работы я научился ананлизировать ресурсы определенной игры, визуализировать изменения и поведения этого ресурса, с помощью соотвествующих схем и ПО
 
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
