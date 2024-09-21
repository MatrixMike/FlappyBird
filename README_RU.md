# Flappy Bird, только Си, без Java/Kotlin, вес APK (armeabi-v7a + arm64-v8a) < 100 kilobytes

## История:  
  
Всё началось в 2021 году. Тогда я наткнулся на репозиторий [rawdrawandroid](https://github.com/cnlohr/rawdrawandroid). 
Появилась мотивация сделать какую-нибудь игру с максимально меньшим весом APK, но при этом, что бы игра была простой и понятной.  
В моменте появилась идея сделать клон давно забытой игры Flappy Bird. Которую уже портировали на многие языки программирования.  
Тогда, позднее в 2021 году, я нашел ещё один интересный репозиторий [Raylib](https://github.com/raysan5/raylib).  
Но, первая попытка сделать эту игру была на C++, при использовании [ImGui](https://github.com/ocornut/imgui/), потому что я уже был с ним знаком.  
А так, все трудности были представлены в Android Native Activity и сборке чистого APK из apktool без Android Studio.  
Первая попытка потерпела крах.  
Во-первых, вес APK был примерно 1 Мегабайт.  
Во-вторых, могли случаться вылеты игры.  
В-третьих, внутри APK была только библиотека для armeabi-v7a, а с 2022 года правила Google требуют наличие arm64-v8a библиотек.  
В-четвертых, структура проекта и его организация были ужасными, это создавало кашу в глазах и мешало нормально ориентироваться в проекте.  
В целом, что-то попробовал, не получилось, мысль в голове хранилась на протяжении всего этого времени, но попыток больше не предпринималось.  

## Мотивация:  
  
Примерно 14 сентября 2024 года, в дискорд-канале Raylib я увидел как один парень сделал Flappy Bird на языке C#.  
Тогда мне стало очень интересно, попробовать безумную идею, сделать эту игру на Си, для Android, весом APK меньше 100 Килобайт.
Идея казалось безумной, а также, безуспешной.  
Просто представьте, сегодня, когда вес APK достигает по 500 Мегабайт, нужно уложиться всего лишь меньше, чем 100 Килобайт.
Для чего такие рамки? Это спортивный интерес, получится ли такое? Получилось! Но было совсем не просто.
  
## Реализация:  
  
По началу я собрал себе решение которое компилировало Hello World на Си, упаковывало библиотеку в APK, всё подписывалось и отправлялось мне на устройство по USB.  
Как только всё было готово, дальше я пошел изучать ресурсы игры. Звуки сначала были в формате ogg, я их сжал, но были какие-то проблемы, я уже не помню этот момент.  
Дальше звуки всё же стали форматом mp3, сжатым по 16 (килобайт в секунду) каждый, тем самым максимально уменьшив вес, а также качество звука оставалось терпимым.  
Возникла первая трудность, если раньше для воспроизведения звука я использовал [BASS](https://www.un4seen.com/), а он тяжелый для моей цели, то пришлось изучить OpenSLES который без проблем читает формат MP3.  
Дальше из ресурсов остаются картинки, формата png. Иного вариант использования формата нет. Тогда надо было найти что-то легче, чем [stb_image](https://github.com/nothings/stb).  
Так я наткнулся на [upng](https://github.com/elanthis/upng), которая полностью решила вопрос с декодированием png файлов для дальнейшего их рендера.

В целом всё проще чем кажется.  
OpenGL ES 2 + шейдеры для отрисовки, OpenSLES для звуков, upng для декодирования png формата и конечно же Android Native Activity.  
  
## Сборка:
```
//todo
```
  
## Авторское право: 
Я не претендую на авторское право. Право на эту игру и ресурсы принадлежит **DotGEARS**.

## Вдохновление:
- [rawdrawandroid](https://github.com/cnlohr/rawdrawandroid)
- [Flapper](https://github.com/its-Lyn/Flapper)
- [Raylib](https://github.com/raysan5/raylib)
- [ImGui](https://github.com/ocornut/imgui/)