# РАЗРАБОТКА ИГРОВЫХ СЕРВИСОВ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Рыков Дмитрий Алексеевич
- РИ000024
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

## Цель работы
Подготовить разрабатываемое приложение к сборке и публикации. 
## Задание 1
### По теме видео практических работ 1-4 повторить реализацию игры на Unity. Привести описание выполненных действий.
## Ход работы:
– 1 Практическая работа «Создание анимации объектов на сцене»

– 2 Практическая работа «Создание стартовой сцены и переключение
между ними»

– 3 Практическая работа «Доработка меню и функционала с остановкой
игры»

– 4 Практическая работа «Добавление звукового сопровождения в игре»

## Результат выполнения хода работы
### 1) Создание анимации объектов на сцене
1. Создадим копию сцены OScene и переименуем ее в 1Scene, а получившуюся копию в 0Scene. 
![image](https://user-images.githubusercontent.com/91608946/198101019-9b9ecf83-511f-440c-beed-015dcb95d5a1.png)

2. Затем удалим все ненужные скрипты с получившейся сцены, изменим анимацию главного героя, добавим какой-нибудь объект для дальнейшей анимации (в моем случае ToxicFrog), а также поработаем с общим видом сцены. Вот итог: 
![SDUfzsLl71](https://user-images.githubusercontent.com/91608946/198102057-0c3768ee-b4ba-4353-8ecd-19f9f595cde4.gif)

3. Теперь анимируем добавленный ранее объект (ToxicFrog), чтобы сцена выглядела интереснее. Для этого зайдем в аниматор и создадим новую анимацию FrogAnimation. В моей анимации объект меняет свое положение по Y. В итоге перечисленных действий получаем следующее: 
![VcNAdQJaeR](https://user-images.githubusercontent.com/91608946/198102701-e77919f9-f4bf-4dbe-87e9-7347432e8c5a.gif)

### 2) Создание стартовой сцены и переключение между ними
1. Создадм тайтл. Для этого создадим объект Text. Затем скачаем ассет со шрифтами. Я выбрал ассет "Free Pixel Font - Thaleah".
 ![image](https://user-images.githubusercontent.com/91608946/198117660-0f16b895-1a25-4883-bbf5-50efc87730ea.png)
 Настроим расположение тайтла на экране и получим следующее:
 
 ![image](https://user-images.githubusercontent.com/91608946/198117834-31b32ee0-e8cd-4d28-ae95-cd9d6e5ea4d0.png)
 
2. Затем создадим пустой объект и назовем его MainMenu. В нем будут храниться все кнопки главного меню, а именно: Play, Option и Exit. После этого создадим скрипт, в котором пропишем функционал наших кнопок. Код выглядит следующим образом:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenu : MonoBehaviour
{
public void PlayGame(){
    SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex + 1);
}

public void QuitGame(){
    Application.Quit();
}
}
```
3. Затем расположим кнопки на экране так, чтобы игроку было удобно с ними взаимодействовать, после этого найдем ассет, который будет вписывать в наш дизайн. Я выбрал ассет 2D UI Buttons Free Package for unity developer by Javedkhanme
![image](https://user-images.githubusercontent.com/91608946/198118526-b8ed4f4d-c9ac-48c7-bbfd-b5832cff3321.png)

4. Затем подключим ранее написанный скрипт к кнопкам главного меню через компонент Button и получаем следующий результат:
![CEbwYqNQnS](https://user-images.githubusercontent.com/91608946/198119294-82517f18-8f01-499d-9e91-f64b2e45d526.gif)

### 3) Доработка меню и функционала с остановкой игры
1. Для начала сделаем новое меню, меню Settings. Для этого копируем объект MainMenu и удалим оттуда все элементы, кроме кнопки Exit. Ее мы переименуем в кнопку Back. Затем сделаем новый объект неактивным. После этого добавим методу OnClick кнопке Options два события. Первое будет делать объект MainMenu неактивным, а второе наоборот делать активным объект Settings, все это будет происходить при нажатии на кнопку Options в главном меню. Затем добавим 2 события методу OnClick для кнопки Back объекта Settings. Выполняемые события будут зеркальными для событий кнопки Options. В итоге получаем следующий результат: 

![J1M6kLFPcw](https://user-images.githubusercontent.com/91608946/198145086-bae8b79c-5520-459b-bbb9-1ce104e952d2.gif)

2. Теперь добавим нашей игре дополнительный функционал - возможность поставить игру на паузу и выхода в главное меню. Для этого создадим скрипт Pause и создадим объект Text, который в дальнейшем подключим к написанному нами скрипут. Скрипт выглядит следующим образом:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
public class Pause : MonoBehaviour
{

    private bool paused = false;
    
    public GameObject panel;
    void Update()
    {
         if (Input.GetKeyDown(KeyCode.Space)){
            if(!paused){
                Time.timeScale = 0;
                paused = true;
                panel.SetActive(true);
            }
            else{
                Time.timeScale = 1;
                paused = false;
                panel.SetActive(false);
            }
    
         }

         if (Input.GetKeyDown(KeyCode.Escape)){
            SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex - 1);
            Time.timeScale = 1;
            paused = false;
            panel.SetActive(false);
         }
        
    }
}

```
После этого подключим написанный нами скрипт к объекту MainCamer. В результате выполнения скрипта получаем следующий функционал:

![VknBr4oxVH](https://user-images.githubusercontent.com/91608946/198146178-1fce8cbc-e88f-47bb-b8c3-493e3bc464a1.gif)

### 4) Добавление звукового сопровождения в игре

1. Для начала добавим музыкальное сопровождение как в главное меню, так в и в сам игровой процесс. Для этого подключим к камере в сцене 0 и 1 компонент AudioSourse и добавим в него музыку на наш в кус в формате wav. Также зациклим ее, активировав параметр Loop.
2. Затем добавим все тот же компонент к префабу Taddy и Case, убрав параметр PlayOnAwake, добавим звуки на свой вкус. Затем отредактируем скрипты Case и Taddy, добавив туда следующие строки:
```c#
public AudioSource audioSource;
audioSource = GetComponent<AudioSource>();
audioSource.Play();
```
В итоге получаем следущее:

https://user-images.githubusercontent.com/91608946/198162730-5323402b-9278-41dc-9bad-a5bbcb719f6b.mp4




## Задание 2
### Привести описание того, как происходит сборка проекта проекта под другие платформы. Какие могут быть особенности?

 Чтобы посмотреть на то, как проект будет выглядеть вне редактора или для публикации проекта испольуется функция Build. Unity позволяет делать билды проектов как для ПК, например для Windows или IOS, так и для мобильный устройств или консолей. В результате билда в итоге могут получаться разные файлы. Например, при билдне под Windows мы получаем папку Data, содержащую все ресурсы и приложения, и исполняемый файл .exe, а при билде под IOS получим “app bundle”, содержащий все необходимые файлы для запуска приложения и его ресурсы.
 
 
## Задание 3
### Добавить в меню Option возможность изменения громкости (от 0 до 100%) фоновой музыки в игре.
1) Для редактирования музыки создадим слайдер и поместим его в меню настроек
2) Затем создадим крипт MusciLvl для редактирования уровня громкости:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MusicLvl : MonoBehaviour
{
    private AudioSource audioSource;
    private float musicVolume = 1f;

    void Start()
    {
        audioSource = GetComponent<AudioSource>();
    }

    // Update is called once per frame
    void Update()
    {
        audioSource.volume = musicVolume;
    }

    public void SetVolume (float vol){
        musicVolume = vol;
    }
}

```
Этот скрипт создает связь между значенем парамерта Volume компонента AudioSource и параметром Value объекта Slider. Затем подключим скрип к камере и перенастроим слайдер. В итоге получаем следующий результат:


https://user-images.githubusercontent.com/91608946/198661556-cdf4dc8c-9686-4f42-821b-85e49384e1fa.mp4








## Выводы
В результате выполнения лабораторной работы №2 мы подготовили разрабатываемое приложение к сборке и публикации. 


