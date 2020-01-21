---
title: "Joy of Programming"
date: 2020-01-21T12:46:07+02:00
lastmod: 2020-01-21T12:46:07+02:00
tags: ["random"]
---

Я давно не получаю удовольствия от своей работы (какой бы она ни была). Вероятно, это характерно для любой профессиональной деятельности. Большая часть того, что я делаю — это допиливание и подхачивание уже существующих систем. Редкий проект начинается с нуля, а если и начинается, то посвящен он какой-то прагматичной области, где нет особого фана. Зато за это платят деньги, и платят хорошие деньги. 

На прошлой неделе я чот приуныл, потому что уже давно забыл когда мне было в удовольствие что-то покодить, и решил внести немного разнообразия в ежедневное ковыряние легаси джавы и ямля кубера. В голове как раз прочно села навязчивая идея сделать бота, который будет автоматически модерировать телеграм чат — в базовой вариации выдавать предупреждения за использование обсценной лексики и переводить человека в режим read-only. Воображение тут же нарисовало SaaS где за $5 администраторы чатов смогут подключить моего бота, конфигурировать блеклисты, смотреть статистику по блокировкам, кастомизировать сообщения, и использовать еще тысячу и одну функцию. Надо было делать.

Тем же вечером я приступил к работе — создал скелет сервера, нашел библиотеку для интеграции с телеграмом, сделал тестового “эхо”-бота (бот который реплицирует любое сообщение, которое ему приходит), настроил окружение и начал работу над блеклистом. В интернете был найден словарь русского мата, загнан в базу, написаны правила для выдачи предупреждений, все протестировано, задеплоено в прод и подключено к чату [моего канала](https://t.me/full_of_hatred) в silent-режиме (бот никого не блокировал и никак себя не проявлял, но делал соответствующие записи в базе данных, так что можно было проверить как он работает).

Я получил колоссальное удовольствие от этой микро-разработки. Мне нравилось пилить и хотелось сидеть и добавлять еще чего-нибудь. Причина была простой — я решал свою личную проблему (мне не нравится использование обсценной лексики, но я не сообразил установить правила в начале), продукт был виден большому количеству пользователей сразу же, и результат его работы влиял на них непосредственно.

Утром я убедился что бот не падает (код рабочий) и вывел его из беззвучного режима. Естественно, общественность (точнее небольшая ее часть) моментально возмутилась и начала тестировать бота на предмет того, какие же слова он знает. Получился такой эффект Стрейзанд :) Еще посреди разработки я понял что идея не взлетит, алгоритм определения слов я сделал слишком глупым (простое вхождение символов) — пользователи могли бы маскировать слова разделяя буквы пробелами или другими способами, но решил добить до конца. Уже через 5 минут после запуска я окончательно убедился что в базовом виде бот не работает — под раздачу попадали еще и обычные слова, где поиск находил негодные подстроки.

Стало понятно, что нужно прикручивать NLP и прочий датасаенс с машинлёрнингом, учиться определять “тон” сообщений и действовать более интеллектуально, иначе чат превратится в цирк тестировщиков бота а не в место для культурного общения.

Потратив еще пару часов я сделал другую функцию — рейтинг пользователя. Сделав ответ со строкой “+1” или “-1” можно увеличить рейтинг пользователя и потом посмотреть таблицу лидеров. Хабр в миниатюре. Функция тоже не зашла и дальнейшую разработку я прекратил.

На всё про всё я затрекал 8 часов. Непосредственная работа с пользователями, быстрый цикл обратной связи, непродолжительная борьба щита и меча принесли мне кучу удовольствия. 10 из 10 буду делать еще :)