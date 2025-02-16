# Обработчик кадров

## Сервисы:

- Основной сервис:

Отвечает за приём потока (файл, rtsp), его нарезку на кадры, сохранение временной метки и данных о кадре, сериализацию и отправку на второй сервис. [Находится тут](https://github.com/naburnm8/rtspListener)

- Второй сервис:

Отвечает за обработку присланного кадра и сохранение информации о нем (как было сказано в ТЗ: "некоторый json, содержащий 4 дробных числа и 1 строку"). [Находится тут](https://github.com/naburnm8/frameListener)

## Краткое описание решения:

Решение состоит из двух сервисов, каждый из которых представляет собой приложение на Spring Boot. Сервисы общаются между собой посредством http, формат данных: JSON.

Основной сервис получает на вход либо url rtsp потока, либо путь до видео файла, запускает его покадровую нарезку и отправляет в отдельных посылках каждый кадр на второй сервис.

Второй сервис после получения данных, обрабатывает их и заносит "4 дробных числа и 1 строку" в базу данных, тем самым сохраняя их. Также JSON с обработанными данными отправляется назад на основной сервис.
