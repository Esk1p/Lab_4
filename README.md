# РАЗРАБОТКА ИГРОВЫХ СЕРВИСОВ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Рыков Дмитрий Алексеевич
- РИ000024
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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
Cоздание интерактивного приложения и изучение принципов интеграции в него игровых сервисов.
## Задание 1
### По теме видео практических работ 1-5 повторить реализацию игры на Unity. Привести описание выполненных действий.
## Ход работы:
1) Выбор игровых моделей и настройка анимаций;
2) Написание скрипта для движения персонажа;
3) Написания скрипта для выпадения подарков и оформление сцены;
4) Написания скриптов для анимации "взрыва" подарка и генерации жизней персонажа;

## Результат выполнения хода работы
### 1) Выбор игровых моделей и настройка анимаций
Я решил не использовать модели, которые были показаны преподавателем, а потому нашел свои. В качестве героя вместо дракона я взял аниме девочку из ассета "Unity-Chan! Model", в котором также были все необходимые анимации.
![image](https://user-images.githubusercontent.com/91608946/194338117-0856c957-4204-4a44-b758-f01c4787f40e.png)

Вместо энергетического щита я решил использовать корзину из ассета "Crate and Barrels".
![image](https://user-images.githubusercontent.com/91608946/194338827-0d49eb75-81bd-486e-a108-9f59b22c7ed4.png)

Вместо драконьих яиц взял мишку из ассета "FREE Christmas Presents / Low Poly".
![image](https://user-images.githubusercontent.com/91608946/194339413-80a560ed-ad7b-44fb-8df0-a0d5373c2756.png)

Затем, после выбора моделей, я приступил к настройке анимаций. Мною был создан контроллер анимаций, в котором содержалась анимация бега персонажа, затем контроллер был подключен к префабу модели. Вот, что вышло в результате: 
![nFUk6KYiCO](https://user-images.githubusercontent.com/91608946/194358546-ff8e6747-64fc-496f-9005-cdcd9c4ddeed.gif)


### 1) Написание скрипта для движения персонажа

Скрипт для движения персонажа выглядит следующим образом:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TyanMove : MonoBehaviour
{
    // Создание переменных
    public GameObject taddyPrefab;

    public float speed = 1;

    public float timeBetweenTaddyDrops = 1f;

    public float leftRightDistance = 10f;

    public float chanceDirection = 0.1f;

    void Start()
    {
    }

    void Update()
    {
      
        //Часть кода, для задания скорости персонажа + настройки необходимого угла его отображения

        Vector3 pos = transform.position;
        pos.x += speed * Time.deltaTime;
        transform.position = pos;

        if (pos.x < -leftRightDistance){
            speed = Mathf.Abs(speed);
        }
        else if (pos.x > leftRightDistance){
            speed = -Mathf.Abs(speed);
        }

        if (speed >0){
            gameObject.transform.rotation = Quaternion.Euler(0, 90, 0);
        }
        else{
            gameObject.transform.rotation = Quaternion.Euler(0, 270, 0);
        }
  
    }

    //Функция для рандомного изменения направления персонажа
    private void FixedUpdate() {
        if (Random.value < chanceDirection){
            speed *= -1;
        }
        
    }


}
```
В результате выполнения данного скрипта мы получаем следующее: 
![RRMpKvwOHQ](https://user-images.githubusercontent.com/91608946/194362078-89bb0f5a-0e6c-42f5-b161-5bd7fd634b38.gif)

### 3) Написания скрипта для выпадения подарков и оформление сцены
Для начала добавим префаб подарка к префабу персонажа. Затем добавим следующие строки в скрипт, который приведен выше.
```c#
    void Start()
    {
        Invoke("DropTaddy", 2f);
    }
    
    // Функция для сбрасывания подарков
    void DropTaddy(){
        Vector3 myVector = new Vector3(0.0f,0.0f,0.0f);
        GameObject taddy = Instantiate<GameObject>(taddyPrefab);
        taddy.transform.position = transform.position + myVector;
        Invoke("DropTaddy", 2f);
    }
```

Затем импортируем ассет для оформления сцены. Для этого я выбрал ассет "Farland Skies - Cloudy Crown", в нем содержатся как текстуры неба, так и новая модель земли.
В результате всех перечисленных выше действий получаем следующее:
![jIb98pPOGF](https://user-images.githubusercontent.com/91608946/194365215-c1d4aa00-e7e8-43b6-84a2-75cab5d2f2a9.gif)

### 3) Написания скрипта для выпадения подарков и оформление сцены
Создадим скрипт, в котором пропишем настройки анимации при столкновении подарка с землей, а также настройки удаления подарков после их падения.
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Taddy : MonoBehaviour
{
    // Переменная, в котором установлена высота, при которой объект подарка будет удален
    public static float bottomY = -15f;


    void Start()
    {
        
    }

    // Настройки анимации "взрыва" объекта подарка
    private void OnTriggerEnter(Collider other) {
        ParticleSystem ps = GetComponent<ParticleSystem>();
        var em = ps.emission;
        em.enabled = true;

        Renderer rend;
        rend = GetComponent<Renderer>();
        rend.enabled = false;

    }

    // Настройки удаелния объекта подарка
    
    void Update()
    {
        if (transform.position.y <= bottomY){
            Destroy(this.gameObject);
        }
        
    }
}
```

После этого импортируем ассет с анимацией "взрыва" и настроим ParticleSystem - систему частиц, в которой можно более тонко настроить правила проигрывания анимации. Для этого я выбрал ассет "52 Special Effects Pack".
![image](https://user-images.githubusercontent.com/91608946/194367588-bf7a0787-007f-413a-add6-da65964406c6.png)

После этого создадим отдельный скрипт для генерации жизней персонажа:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TyanPicker : MonoBehaviour
{
   public GameObject heartsPrefab;

   public int numHearts = 3;

  

    void Start()
    {
        for (int i = 1; i <= numHearts; i++){
            GameObject tSpawnHearts = Instantiate<GameObject>(heartsPrefab);
            tSpawnHearts.transform.position = new Vector3 (-6.5f+i,5.5f,0);
            tSpawnHearts.transform.localScale = new Vector3(0.2f,0.2f,0.2f);
        }

        
        
    }

 
    void Update()
    {
        
    }
}
```
В результате выполнения всех действий получаем следующее:
![cwOMFkpLHD](https://user-images.githubusercontent.com/91608946/194368162-1430866d-d4f6-41ce-8b78-6dd82ac176cb.gif)

## Задание 2
### В проект, выполненный в предыдущем задании, добавить систему проверки того, что SDK подключен (доступен в режиме онлайн и отвечает на запросы);

1) В Build Settings переключем нашу игру на платформу WebGL, затем забилдим наш проект, чтобы создать файл index.html;
2) Добавляем в index.html следующие строки
```html
<head>
<script src="https://yandex.ru/games/sdk/v2"></script>

    <script>
      YaGames.init().then(ysdk => {
          ysdk.adv.showFullscreenAdv();

          const buttonElem = document.querySelector('#button');

          let commonCounter = 0;
          buttonElem.addEventListener('click', () => {
              let counter = 0;

              function getCallback(callbackName) {
                  return () => {
                      counter += 1;
                      commonCounter += 1;

                      console.log(`showFullscreenAdv; callback ${callbackName}; ${counter} call`);
                  }
              }

              ysdk.adv.showFullscreenAdv({
                  callbacks: {
                      onClose: getCallback('onClose'),
                      onOpen: getCallback('onOpen'),
                      onError: getCallback('onError'),
                      onOffline: getCallback('onOffline')
                  }
              });
          });
      });
  </script>
  </head>

  <body>
      <button id="button">Показать рекламу</button>
  </body>  
```
3) В итоге мы "показываем рекламу" с помощью Yandex SDK, однако получаем ошибку, потому что я пока понятию не имею, как его настроить. Тем не менее мы получили систему проверки Yandex SDK, которая доказывает свое существование с помощью ошибки.
![05D5chhoB4](https://user-images.githubusercontent.com/91608946/194391248-d1621b3e-48cb-417b-915a-6ee06a0aff32.gif)








## Выводы
В результате выполнения лабораторной работы №2 мы создали интерактивное приложение и изучили принципы интеграции в него игровых сервисов.


