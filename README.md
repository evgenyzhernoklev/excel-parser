Код написан на основании "идеального примера" - ```excel/brief_example_gi3.xlsx```.

### How to
* открываем файл ```dist/index.html```;
* в открывшемся окне браузера загружаем необходимый excel-файл;
* если парсинг прошел успешно, то через несколько секунд автоматически скачается готовый ```products.js```.

### Процесс парсинга
* если в строке есть такие слова: ```/Первая строка|Вторая строка|Код для заказа/```, то мы ее пропускаем;
* если в строке заполнена одна ячейка, то парсим ее как заголовок либо как условие. Заголовок идет сразу после пустой строки либо товара, условие идет после строки с текстом (заголовка);
* заголовок разбивается таким образом: первая фраза/слово до ```:``` - название таба, дальше смотрим на оставшуюся часть: если есть точка, то текст до нее записываем в ```title```, после - ```condition``` секции внутри таба, если точка не попадается - записывааем все в ```title```;
* условия разбиваются таким образом (следующая строка за заголовком, если есть):  первая фраза/слово до ```!``` отбрасывается, остальное записываем в ```condition``` текущего таба;
* при парсинге товаров текущая строка сравнивается с предыдущей: если товар один и без цветов/размеров - парсим как одиночный тотвар, иначе - как группу;
* группа определяется по совпадению ```profile code``` либо по наличию цвета/размера у единичного товара (когда до или после него есть товары с другими ```profile code```).

### Хэши табов
* необходимо расширение списка, пока как-то так:

Название таба | hash
------------- | ----
default | goods
"Макияж", "Все для макияжа" | makeup
"Ароматы" | fragrance
"Уход", "Уход за телом и лицом" | care
"Уход за лицом", "Средства по уходу за лицом" | face
"Мода и стиль" | style
"Мастера Бижутерии" | jewelery
