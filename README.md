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

 
 ![image](https://github.com/user-attachments/assets/1ee66eea-97f2-4888-8992-44c073242b46)


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

```rb
   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   using UnityEngine.Networking;
   using SimpleJSON;
   using Unity.Loading;
   
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
       StartCoroutine(WaitForDataLoad());
   }
   
   IEnumerator WaitForDataLoad()
   {
       yield return StartCoroutine(GoogleSheets());
       Debug.Log("Data Loaded: " + dataSet.Count);
   }
       void Update()
       {
   
           if (dataSet.Count == 0) return;
           
           if ( i <= dataSet.Count & statusStart == false)
           {
               if (dataSet["Mon_" + i.ToString()] >= 30){
                   StartCoroutine(PlaySelectAudioGood());
                   Debug.Log(dataSet["Mon_" + i.ToString()]);
                   Debug.Log("Проигрывается звук 'Horosho'");
               }
               if (dataSet["Mon_" + i.ToString()] < 30 & dataSet["Mon_" + i.ToString()] > 10){
                   StartCoroutine(PlaySelectAudioNormal());
                   Debug.Log(dataSet["Mon_" + i.ToString()]);
                   Debug.Log("Проигрывается звук 'Sredne'");
               }
               if (dataSet["Mon_" + i.ToString()] <= 10 ){
                   StartCoroutine(PlaySelectAudioBad());
                   Debug.Log(dataSet["Mon_" + i.ToString()]);
                   Debug.Log("Проигрывается звук 'Ploho'");
               }
           }
       }
   
       IEnumerator GoogleSheets()
       {
           UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1Tfu2cJdkJ5ElY76Vt6D2tfWT4o0mDWsLmklOmf_sOMM/values/Лист1?key=AIzaSyAK9_9JK7Lfg2aoR1yjk81On-3xTOzgKb8");
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


После запуска все 3 записи прооигрались без ошибок.

 ![image](https://github.com/user-attachments/assets/990d5b37-65de-4268-9cb0-5ba75a4c12ff)

 ## Задание 5
### Задание 5.1. Выберите одну из игровых переменных в игре СПАСТИ РТФ: Выживание (HP, SP, игровая валюта, здоровье и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.

Ход работы:  
- В качестве переменной была выбрана **"здоровье" (hp)**, которая отражает состояние героя, за которого играет игрок. Ее значение определяет уровень "жизни" персонажа и влияет на условия завершения игры (при hp = 0 игра заканчивается).  
  Изменение переменной:  
  - При получении урона здоровье уменьшается.  
  - Если во время прокачки игрок выбирает соответствующие навыки, они восстанавливают здоровье.  

Допустимый диапазон значений:  
 - Значение переменной варьируется от **0** до установленного в игре максимального лимита.
 - Схема экономической модели ресурса:

 ![image](https://github.com/user-attachments/assets/5f09ca66-309a-4595-8087-b851016351a3)

 
 ### Задание 5.2 С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в игре “СПАСТИ РТФ:Выживание”. Средствами google-sheets визуализируйте данные в google-таблице (постройте график / диаграмму и пр.) для наглядного представления выбранной игровой величины. Опишите характер изменения этой величины, опишите недостатки в реализации этой величины (например, в игре может произойти условие наступления эксплойта) и предложите до 3-х вариантов модификации условий работы с переменной, чтобы сделать игровой опыт лучше.
 
 Ход работы:
 - Сначала необходимо определить, как изменяется выбранная игровая переменная:
   В данном случае — здоровье игрока. Оно изменяется в зависимости от получаемого урона, что делает его зависимым от действий игрока и его навыков. Поскольку существует множество сценариев изменения этого параметра, для упрощения я рассмотрел ситуацию, в которой игрок получает урон с определенным временным интервалом.
 
 Ссылка на таблицу: https://docs.google.com/spreadsheets/d/1Tfu2cJdkJ5ElY76Vt6D2tfWT4o0mDWsLmklOmf_sOMM/edit?gid=0#gid=0

![image](https://github.com/user-attachments/assets/1ee66eea-97f2-4888-8992-44c073242b46)
 
 - Из графика видно, что значение здоровья колеблется от 30 (максимальный лимит) до 10. Уменьшение происходит при получении урона (в данном примере — на 10 единиц), а увеличение — когда игрок либо использует способность "вампиризм", либо завершает волну.

Так как в игре СПАСТИ РТФ механик, влияющих на здоровье, не так много, можно расширить функционал следующими идеями:
- Добавить предмет, восстанавливающий здоровье либо мгновенно, либо постепенно.
- Ввести возможность обмена здоровья на другой ресурс (например, патроны). При этом, возможно, потребуется добавить новые предметы, чтобы сохранить баланс.
- Разрешить временное увеличение предела здоровья (не через прокачку), например, для подготовки к битве с боссом.
 
 
 ### Задание 5.3 Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.

 Ход работы:
 - Для реализации данного задания я выделил правильно по которым описывается динамика изменения здоровья:
     - Если хп около лимита (в моем случае hp >= 30), то воспроизводится звук "хороший"
     - Если хп около среднего значения (в моем случае 30 > hp > 10), то воспроизводится звук "средний"
     - Если хп около минимума (в моем случае hp <= 10), то воспроизводится звук "плохой"
 - Для отображения этой динамики в Unity я создал компонент с таким скриптом (Это скрипт из методички, с небольшими изменениями):
 
 ![image](https://github.com/user-attachments/assets/990d5b37-65de-4268-9cb0-5ba75a4c12ff)
 
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
