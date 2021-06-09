Структура для CSS. По ситуации надо доработать.

# Разделы

- Общие
- Структура
- Цвета
- Шрифты

# Общие
1) Все стили надо писать исключительно в sass/scss в resources, чтобы в public попадал только готовые бандлы. 
2) Предлагаю пока что не определять в общие классы гриды, флексы, padding, margin и всякие размеры чтобы не портить html.
3) Все размеры писать в относительных единицах, преимущественно в rem. С выходом 4k мониторов px уже утратили актуальность. 
4) При именованиях классов использовать БЭМ, между блоком и элементом использовать двойной пробел __. 
А модификатор использовать как в bootstrap типа button, card для соответствующих элементов. 
5) Используем переменные css --var, она имеет свои преимущества перед сасовскими переменными.


# Структура

Структура повторяет структуру views. Пока разделяем до уровная страниц. 

> - assets
>    - scss
>      - web
>        - page
>        - _index.scss
>      - layout
>        - page
>        - _index.scss
>      - admin
>        - page
>        - _index.scss
>      - cabinet
>        - page
>        - _index.scss
>      - _components.scss  
>      - _variables.scss
>      - _global.scss
>      - app.scss

 - Папка page это определенная страница, например tickets и внутри него будут файлы scss повторяющие названия их шаблонов во views.
 - Все отдельные файлы scss внутри page импортируется в index, а index будет уже импортирован в app.scss. 
 - В components писать модификаторы типа button, card, tooltip. 
 - Файл _global для базовых настроек.  
 
# Цвета
  - Все цвета определяем в переменные, даже #fff и #000. 
  - Именование цветов будет пока по названию конкретного цвета или оттенка типа red, light-red, blue
  - Все это будет хранится в _variables.scss. Важно не допустить повторение какого то цвета
  - В названиях переменных добавлять префикс --ct (custom), чтобы они не перебивались бутстраповскими переменными. Будет типа --ct-red
 
# Шрифты
  Размеры шрифтов предлагаю определить вот так:
  
```
:root {
    // Базовый размер шрифта
    --text-base-size: 1rem;

    // Шкала типов
    --text-scale-ratio: 1.2;
    
    // Сами переменные
    --text-xs: calc((1rem / var(--text-scale-ratio)) / var(--text-scale-ratio));
    --text-sm: calc(var(--text-xs) * var(--text-scale-ratio));
    --text-md: calc(var(--text-sm) * var(--text-scale-ratio) * var(--text-scale-ratio));
    --text-lg: calc(var(--text-md) * var(--text-scale-ratio));
    --text-xl: calc(var(--text-lg) * var(--text-scale-ratio));
    --text-xxl: calc(var(--text-xl) * var(--text-scale-ratio));
    --text-xxxl: calc(var(--text-xxl) * var(--text-scale-ratio));
}
```
Получается что с помощью  --text-base-size и --text-scale-ratio можно менять размеры всей типогрфии если понадобиться. Например в мобильных версиях.
А вот использовать можно вот так:
```
a {
  font-size: var(--text-xs);
}
```
  
  
  
  
