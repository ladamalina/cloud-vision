## Эксперименты с [Google Cloud Vision API](https://cloud.google.com/vision/)

Пробуем распознать, какое блюдо на изображении.

```bash
$ base64 ./maki.jpg > maki.base64
```

Готовим json запрос

```json
{
  "requests":[
    {
      "image":{
        "content":"base64-encoded file data"
      },
      "features":[
        {
          "type":"LABEL_DETECTION",
          "maxResults":10
        }
      ]
    }
  ]
}
```

API вызов. "browser_key" заменить на свой ключ. "request_filename" – имя json файла.

```bash
$ curl -v -k -s -H "Content-Type: application/json" \
    https://vision.googleapis.com/v1/images:annotate?key=browser_key \
    --data-binary @request_filename
```

Примеры ответов:

![Суши](https://monosnap.com/file/qqwoHbGrpvEgM5gWtPURRqbm9Ox2FV.png)

```json
{
  "responses": [
    {
      "labelAnnotations": [
        {
          "mid": "/m/02wbm",
          "description": "food",
          "score": 0.814924
        },
        {
          "mid": "/m/0d1cx",
          "description": "salmonids",
          "score": 0.73476869
        },
        {
          "mid": "/m/02p2nn",
          "description": "cream cheese",
          "score": 0.68047726
        },
        {
          "mid": "/m/0ch_cf",
          "description": "fish",
          "score": 0.6627869
        },
        {
          "mid": "/m/07030",
          "description": "sushi",
          "score": 0.5962314
        }
      ]
    }
  ]
}
```

![Пицца](https://monosnap.com/file/wcBqyniPoyK8hc31ia8Rla5JOnRER4.png)

```json
{
  "responses": [
    {
      "labelAnnotations": [
        {
          "mid": "/m/02q08p0",
          "description": "dish",
          "score": 0.998695
        },
        {
          "mid": "/m/02wbm",
          "description": "food",
          "score": 0.98872179
        },
        {
          "mid": "/m/0663v",
          "description": "pizza",
          "score": 0.98456287
        },
        {
          "mid": "/m/068_x",
          "description": "pizza cheese",
          "score": 0.98280007
        },
        {
          "mid": "/m/01f79n",
          "description": "quiche",
          "score": 0.91500229
        },
        {
          "mid": "/m/09y2k2",
          "description": "italian food",
          "score": 0.85637063
        },
        {
          "mid": "/m/0krfg",
          "description": "meal",
          "score": 0.84273869
        },
        {
          "mid": "/m/018dy5",
          "description": "pepperoni",
          "score": 0.7069453
        },
        {
          "mid": "/m/03bwyyr",
          "description": "fast food restaurant",
          "score": 0.67955619
        },
        {
          "mid": "/m/018dz0",
          "description": "salami",
          "score": 0.59911573
        }
      ]
    }
  ]
}
```

![Бургер](https://monosnap.com/file/YQPk2bjjC9Z6OFmWIJzpNxHaxBKqy3.png)

```json
{
  "responses": [
    {
      "labelAnnotations": [
        {
          "mid": "/m/013q4y",
          "description": "cheeseburger",
          "score": 0.9804697
        },
        {
          "mid": "/m/02wbm",
          "description": "food",
          "score": 0.9490642
        },
        {
          "mid": "/m/0cdn1",
          "description": "hamburger",
          "score": 0.92083669
        },
        {
          "mid": "/m/02q08p0",
          "description": "dish",
          "score": 0.89894629
        },
        {
          "mid": "/m/027x8l3",
          "description": "breakfast sandwich",
          "score": 0.89111179
        },
        {
          "mid": "/m/03f476",
          "description": "veggie burger",
          "score": 0.82768649
        },
        {
          "mid": "/m/0krfg",
          "description": "meal",
          "score": 0.79202753
        },
        {
          "mid": "/m/06pcq",
          "description": "submarine sandwich",
          "score": 0.78040737
        },
        {
          "mid": "/m/01rq37",
          "description": "big mac",
          "score": 0.609646
        },
        {
          "mid": "/m/0hz4q",
          "description": "breakfast",
          "score": 0.58769476
        }
      ]
    }
  ]
}
```

[Дешево:)](https://cloud.google.com/vision/) До 1 000 API вызовов в месяц – бесплатно. Далее за услугу "Label Detection" – от $2 за тысячу обращений.
