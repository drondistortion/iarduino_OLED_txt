[![](https://iarduino.ru/img/logo.svg)](https://iarduino.ru)[![](https://wiki.iarduino.ru/img/git-shop.svg?3)](https://iarduino.ru) [![](https://wiki.iarduino.ru/img/git-wiki.svg?2)](https://wiki.iarduino.ru) [![](https://wiki.iarduino.ru/img/git-lesson.svg?2)](https://lesson.iarduino.ru)[![](https://wiki.iarduino.ru/img/git-forum.svg?2)](http://forum.trema.ru)

# iarduino_OLED_txt

**This is a library for Arduino IDE. It allows to control [OLED dislay 128x64](https://iarduino.ru/shop/Displei/ekran-0-96-128x64-oled-i2c-belyy.html) Trema-module made by iArduino.ru**

**Данная библиотека для Arduino IDE позвляет управлять Trema-модулем [OLED экран 128x64](https://iarduino.ru/shop/Displei/ekran-0-96-128x64-oled-i2c-belyy.html)**

> Подробнее про установку библиотеки читайте в нашей [инструкции](https://wiki.iarduino.ru/page/Installing_librari/).

> Подробнее про подключение к [Arduino UNO](https://iarduino.ru/shop/boards/arduino-uno-r3.html)/[Piranha UNO](https://iarduino.ru/shop/boards/piranha-uno-r3.html) читайте на нашей [wiki](https://wiki.iarduino.ru/page/OLED_trema/)


| Модель | Ссылка на магазин |
|--|--|
| ![](https://wiki.iarduino.ru/img/resources/830/830.svg) | https://iarduino.ru/shop/Displei/ekran-0-96-128x64-oled-i2c-belyy.html |


## Примеры:

**Вывод текста Кириллицей с указанием разных кодировок**

```C++
#include <iarduino_OLED_txt.h>                             // Подключаем библиотеку iarduino_OLED_txt.
iarduino_OLED_txt myOLED(0x3C);                            // Объявляем объект myOLED, указывая адрес дисплея на шине I2C: 0x3C или 0x3D.
                                                           //
extern uint8_t SmallFontRus[];                             // Подключаем шрифт SmallFontRus.
                                                           //
void setup(){                                              //
    myOLED.begin();                                        // Инициируем работу с дисплеем.
    myOLED.setFont(SmallFontRus);                          // Указываем шрифт который требуется использовать для вывода цифр и текста.
}                                                          //
void loop(){                                               //
//  Вывод текста в кодировке UTF-8:                        //
    myOLED.clrScr();                                       // Чистим экран.
    myOLED.print("UTF8", 0, 0);                            // Выводим текст начиная с 0 столбца 0 строки.
    myOLED.setCoding(TXT_UTF8);                            // Меняем кодировку на UTF-8 (по умолчанию).
    myOLED.print("Ардуино iArduino", OLED_C, 4);           // Выводим текст по центру 4 строки.
    delay (5000);                                          // Ждём 5 секунд.
                                                           //
//  Вывод текста в кодировке CP866:                        //
    myOLED.clrScr();                                       // Чистим экран.
    myOLED.print("CP866", 0, 0);                           // Выводим текст начиная с 0 столбца 0 строки.
    myOLED.setCoding(TXT_CP866);                           // Меняем кодировку на CP866.
    myOLED.print("Ардуино iArduino", OLED_C, 4);           // Выводим текст по центру 4 строки.
    delay (5000);                                          // Ждём 5 секунд.
                                                           //
//  Вывод текста в кодировке WINDOWS-1251:                 //
    myOLED.clrScr();                                       // Чистим экран.
    myOLED.print("WIN1251", 0, 0);                         // Выводим текст начиная с 0 столбца 0 строки.
    myOLED.setCoding(TXT_WIN1251);                         // Меняем кодировку на WINDOWS-1251.
    myOLED.print("Ардуино iArduino", OLED_C, 4);           // Выводим текст по центру 4 строки.
    delay (5000);                                          // Ждём 5 секунд.
}                                                          //
```

**Вывод чисел**

```C++
#include <iarduino_OLED_txt.h>                             // Подключаем библиотеку iarduino_OLED_txt.
iarduino_OLED_txt myOLED(0x3C);                            // Объявляем объект myOLED, указывая адрес дисплея на шине I2C: 0x3C или 0x3D.
                                                           //
extern uint8_t SmallFontRus[];                             // Подключаем шрифт SmallFontRus.
                                                           // Если Вы не используете Кириллицу, то лучше подключить шрифт SmallFont, он займет меньше места в памяти программ.
void setup(){                                              //
    myOLED.begin();                                        // Инициируем работу с дисплеем.
    myOLED.setFont(SmallFontRus);                          // Указываем шрифт который требуется использовать для вывода цифр и текста.
                                                           //
    myOLED.print( 123456789 , 0, 0);                       // Выводим целое положительное число начиная с 0 столбца 0 строки.
    myOLED.print(-123456789 , 0, 1);                       // Выводим целое отрицательное число начиная с 0 столбца 1 строки.
    myOLED.print( 123456789 , 0, 2, HEX);                  // Выводим целое положительное число начиная с 0 столбца 2 строки, в 16-ричной системе счисления.
    myOLED.print( 123456789 , 0, 3, OCT);                  // Выводим целое положительное число начиная с 0 столбца 3 строки, в 8-ричной системе счисления.
    myOLED.print(-123.456789, 0, 4);                       // Выводим число с плавающей точкой  начиная с 0 столбца 4 строки, по умолчанию отобразится 2 знака после запятой.
    myOLED.print( 123.456789, 0, 5, 3);                    // Выводим число с плавающей точкой  начиная с 0 столбца 5 строки, указывая 3 знака после запятой.
    myOLED.print( 123       , 0, 6, BIN);                  // Выводим целое положительное число начиная с 0 столбца 6 строки, в 2-ичной системе счисления.
    myOLED.print( 123       , 0, 7, 12);                   // Выводим целое положительное число начиная с 0 столбца 7 строки, в 12-ричной системе счисления.
}                                                          //
void loop(){}                                              //
```

---
## Больше примеров на нашей [wiki](https://wiki.iarduino.ru/page/OLED_trema/#h3_6)


## Назначение функций и переменных 

**Подключаем библиотеку:**

```C++
#include <iarduino_OLED_txt.h> // Подключаем библиотеку.
iarduino_OLED_txt ОБЪЕКТ ( [ АДРЕС_I2C ] ); // Создаём объект (адрес по умолчанию 0x3C).
```

Инициализация работы с дисплеем.

```C++
ОБЪЕКТ.begin(); // Инициализация работы с дисплеем.
```

Очистка экрана дисплея (параметр - флаг разрешающий залить дисплей).

```C++
ОБЪЕКТ.clrScr( [ ЗАЛИТЬ] ); // Очистка экрана дисплея (параметр - флаг разрешающий залить дисплей).
```

Заливка дисплея (параметр - цвет. 0-чёрный, 1-белый).

```C++
ОБЪЕКТ.fillScr( [ ЦВЕТ] ); // Заливка дисплея (параметр - цвет. 0-чёрный, 1-белый).
```

Инверсия цветов экрана (параметр - флаг разрешающий инверсию).

```C++
ОБЪЕКТ.invScr( [ ФЛАГ] ); // Инверсия цветов экрана (параметр - флаг разрешающий инверсию).
```

Инверсия цветов выводимого текста(параметр - флаг разр. инверсию).

```C++
ОБЪЕКТ.invText( [ ФЛАГ ] ); // Инверсия цветов выводимого текста(параметр - флаг разр. инверсию).
```

Выбор шрифта для выводимого текста (параметр - название шрифта).

```C++
ОБЪЕКТ.setFont( ШРИФТ ); // Выбор шрифта для выводимого текста (параметр - название шрифта).
```

Получение ширины символов выбранного шрифта.

```C++
ОБЪЕКТ.getFontWidth(); // Получение ширины символов выбранного шрифта.
```

Получение высоты символов выбранного шрифта.

```C++
ОБЪЕКТ.getFontHeight(); // Получение высоты символов выбранного шрифта.
```

Указание кодировки текста в скетче.

```C++
ОБЪЕКТ.setCoding( [КОДИРОВКА]); // Указание кодировки текста в скетче.
```

Установка курсора в указанную позицию на экране.

```C++
ОБЪЕКТ.setCursor( X , Y ); // Установка курсора в указанную позицию на экране.
```

Сдвиг курсора на указанное количество пикселей.

```C++
ОБЪЕКТ.setCursorShift( X , Y ); // Сдвиг курсора на указанное количество пикселей.
```

Вывод текста в указанную позицию на экране.

```C++
ОБЪЕКТ.print( ТЕКСТ[ , X ] [ , Y ] ); // Вывод текста в указанную позицию на экране.
```

Текущую позицию курсора по оси X.

```C++
 ОБЪЕКТ.numX// Принимает и возвращает текущую позицию курсора по оси X.
```

Текущуя позиция курсора по оси Y.

```C++
Переменная ОБЪЕКТ.numY// Принимает и возвращает текущую позицию курсора по оси Y.
```

**Для вывода текстов, чисел, изображений и графики, воспользуйтесь библиотекой [iarduino&#95OLED](https://github.com/tremaru/iarduino&#95OLED)**
