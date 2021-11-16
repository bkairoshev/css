Telegram: @bek_ulan :fire:

Структура для CSS. По ситуации надо доработать.

# Разделы

- Общие
- Структура
- Цвета
- Шрифты
- JS
- SVG

# Общие
1) Все стили надо писать исключительно в sass/scss в resources, чтобы в public попадал только готовые бандлы. 
2) Предлагаю пока что не определять в общие классы гриды, флексы, padding, margin и всякие размеры чтобы не портить html.
3) Все размеры писать в относительных единицах, преимущественно в rem. С выходом 4k мониторов px уже утратили актуальность. 
4) При именованиях классов использовать БЭМ, между блоком и элементом использовать двойной пробел __. 
А модификатор использовать как в bootstrap типа button, card для соответствующих элементов. 
Допустим если в странице юзера есть карточка с описанием, это будет выглядеть вот так: 
```
// Это блок
.profile {

  //Это  элемент
  &__description {}
}
```
В html:
```
 <div class="profile">
   <div class="profile__description card">
     Описание
   </div> 
 </div> 
```
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
# JS
  JS файлы структурированы примерно так же как SCSS и views с одним отличием что тут нет разделения на страницы.
  Тут есть только разделы, и в каждом разделе есть index.js который импортирован в main.js и весь код пишется в index.js
  
> - assets
>    - js
>      - web
>        - _index.js
>      - layouts
>        - _index.js
>      - admin
>        - _index.js
>      - cabinet
>        - _index.js
>      - main.js
  
# SVG
   SVG файлы кидать в папку /resources/assets/icons с соответствующим рисунку названием. Если наименования повторяются через дефис указать место использования типа 
   email-header.svg. Все иконки проходят через webpack и объединяются в один спрайт в папке public/dist/images/icons.svg, и каждая иконка обзаведется id по названию файла. А         использовать его можно будет так:  <svg> <use xlink:href="/dist/images/icons.svg#название_файла"></use> </svg>
   
   ```
   <i class="nav__messages__icon">
       <svg>
          <use xlink:href="/dist/images/icons.svg#icon-email"></use>
       </svg>
   </i>
   ```
   
   Важное замечание. Держите svg в каком нибудь контейнере с классом, и обращайтесь к самому svg через этот класс. В нашем случае это будет: 
   
   ```
   .nav {
      &__messages {
        &__icon {
          svg {
            width: 2.4rem;
            height: 1.6rem;
          }
        }
      }
    }
   
   ```
   Точно так же можно поменять цвет через свойство fill или можете перевернуть через transform: rotate().
  
