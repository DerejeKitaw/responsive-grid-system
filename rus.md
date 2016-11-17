<article>
Одним из лучших дополнений для нестандартного web-дизайна является 
специально сделанная для него отзывчивая сетка. Вы можете настроить 
все, что вам нужно, включая количество колонок, размер колонок и отступов, 
и даже контрольные точки, в которых вы перестраиваете вашу раскладку.

К сожалению, многие люди даже не пытаются делать сетки для своих
web-сайтов, т.к. у них не хватает знаний и уверенности, что бы попробовать.

Итак, в этой статье, я хочу помочь вам зарядиться знаниями и верой в себя, которые 
вам понадобятся для создания пользовательской сетки. Надеюсь, что к концу этой статьи,
вы сможете оторваться от фреймворков и испытаете пользовательскую сетку на
вашем следующем проекте.

## Что входит в сетку? {#what-goes-into-a-grid-system}

Вам нужно знать три вещи, перед тем как делать вашу сетку

**Во-первых, вам нужно спроектировать вашу сетку**.

Вы используюете колонки одинаковой или разной ширины? Как много колонок у вас
есть? Какие размеры у ваших отступов и колонок?

Вы сможете правильно расчитать сетку только когда у вас будут ответы на вопросы выше.
Что бы помочь вам, я написал статью о [проектировании сеток][1]. Прочтите ее, если вы
хотите знать как спроектировать сетку.

**Во-вторых, вам нужно знать как ваша сетка ведет себе на разных вьюпортах.**

Будете ли вы менять размеры колонок и отступов пропорционально, когда меняется ширина
вьюпорта? Будете ли вы изменять колонки, при этом фиксируя отступы? Будете ли вы менять 
количество колонок в конкретных контрольных точках?

Вам также нужно ответить на эти вопросы. На базе этого вы поймете, как расчитать
ширину ваших колонок и отступов. Я также написал свои соображения об этом в [этой статье][2],
так что прочтите ее, если вы сомневаетесь.

**В-третьих, вам нравится писать классы сетки в вашем HTML?**

Когда дело доходит до (типографских) сеток, мир фронтенда делится на две фракции.

Одна пишет классы сетки в HTML (так делают, например,  Bootstrap и Foundation).
Я называю это **HTML-сетки**. Их HTML выглядит так: 

    <div class="container">
      <div class="row">
        <div class="col-md-9">Content</div>
        <div class="col-md-3">Sidebar</div>
      </div>
    </div>
    
Другая фракци создает сетки на CSS. Я называю это **CSS-сетки**.

*HTML для CSS-сеток проще* по сравнению с HTML для *HTML-сеток.*
Вам нужно меньше разметки для того, что создаете. Вам также не нужно
помнить какие у сетки классы:

    <div class="content-sidebar">
      <div class="content"></div>
      <div class="sidebar"></div>
    </div>
    
С другой стороны, *CSS для CSS-сеток более сложен*. 
Нужно хорошенько подумать даже для реализации простой задачи 
(если раньше вы таких сеток не создавали).
 
**Что бы я выбрал?**

Многие фронтенд-эксперты выбирают CSS-сетки. Я тоже во фракции CSS-сеток
(несмотря на то, что я не смею называть себя экспертом).

Я написал о том, почему я выбрал CSS-сетки заместо HTML-сеток
в [другой статье][3], если вам интересно это выяснить. Еще я написал [статью][4],
которая поможет вам перейти с HTML-сеток на CSS-сетки, если вы 
хотите переключиться.

(Так много статей читать... :cry:)

В любом случае, это те три вещи, которые вам нужно знать перед тем как 
вы сможете сделать вашу сетку. В кратце, вот они: 

1.  Дизайн вашей сетки
2.  Как ваша сетка ведет себя на разных вьюпортах
3.  Следует ли использовать CSS-сетки или HTML-сетки

Мы двинемся дальше, только если у нас есть эти компоненты. Вот то, что мы будем
использовать далее в статье:

1.  Сетка имеет максимальную *ширину в 1140px*, с *12 колоноками по 75px* и 
    *отступами в 20px*. (Прочтите [эту статью][2] с советами о том, 
    как получить эти числа)
2.  Когда вьюпорт меняет размеры, колонки должны менять размеры пропорционально,
    в то время как *отступы остаются фиксированными* с шириной 20px. 
    (Прочтие [эту статью][2], что бы понять, почему я выбрал такое поведение).
3.  Я собираюсь использовать *CSS-сетки*. (Прочтите [эту статью][3], 
    что бы понять, почему я рекомендую их).

С этими словами, давайте начнем!

## Создаем вашу сетку {#building-your-grid-system}

Есть восемь шагов для того, что сделать вашу сетку. Вкратце, вот эти шаги: 

1.  Выберите спецификацию для сетки
2.  Установите `box-sizing` в `border-box` 
3.  Создайте контейнер для сетки
4.  Расчитайте ширину колонок
5.  Определите расположение отступов
6.  Создайте сетку для отладки
7.  Внесите изменения в раскладку
8.  Сделайте вашу раскладку адаптивной

Большинство из этих шагов становятся достаточно простыми, как только
вы сделаете их хотя бы раз. Я обстоятельно объясню все, что вам нужно знать, пока
мы делаем каждый шаг.

## Шаг 1: Выберите спецификацию {#step-1-choose-a-spec}

Вы используете в вашей сетке *CSS Grid*, *Flexbox*, или старые добрые *флоаты*?
Ваши рассуждения и детали реализации будут разными для каждой спецификации.

Из всех трех спецификаций, CSS Grid на сегодняшний день является лучшим инструментов 
для создания сетки (из-за сетки :sunglasses:). К сожалению, поддержка CSS Grid 
оставляет желать лучшего, и мы не можем использовать его прямо сейчас. 
Каждый браузер прячет CSS Grid Layout под флаг, и это значит,
что мы не будет рассматривать его в статье. Я настоятельно рекомендую посмотреть
[работу Рейчел Эндрю (Rachel Andrew)][5], если вам интересен CSS Grid.

Далее, перейедм к Flexbox и флоатам. Рассуждения при использовании этих двух
спецификаций похожи, так что вы можете выбрать любую из них и читать статью дальше.
Я буду использовать флоаты, потому что их проще объяснить и они лучше
подходят для новичков.

Если вы выбрали Flexbox, имеейте ввиду, что есть несколько нюансов, которые вам 
нужно учесть.

## Шаг 2: Установите box-sizing в border-box {#step-2-set-box-sizing-to-border-box}

Свойство `box-sizing` меняет дефолтные настройки блочной CSS модели, которая
используется браузерами для расчета свойств `width` и `height`. Выставляя `box-sizing`
в `border-box`, мы сильно упрощаем расчет размеров колонок и отступов
(вы увидите это позже).

Вот картинка, которое показывает как `width` вычисляется в зависимости от значений
`box-sizing`<figure>

![Свойство Box-sizing и как оно влияет на расчет ширины][6]<figcaption>
Свойство Box-sizing и как оно влияет на расчет ширины</figcaption></figure>

Обычно я ставлю `box-sizing` в `border-box` для всех элементов на сайте, 
так что расчеты `width` и `height` остаются последовательными (и интуитивно понятными)
по всем направлениям. Вот как я делаю это:

    html {
      box-sizing: border-box;
    }
    
    *,
    *:before,
    *:after {
      box-sizing: inherit;
    }
    
Примечания: если вам нужно более детальное объяснение `box-sizing`, я рекомендую
вам [прочесть эту статью][7].


## Шаг 3: Создайте контейнер для сетки {#step-3-create-the-grid-container}

У каждой сетки есть контейнер, который определяет её максимальную ширину.
Как правило, я называю его `.l-wrap`. Префикс `.l-` означает layout, и я использую 
это соглашение по именованию с тех пор, как изучил [SMACSS][8] от 
[Джонатана Снука (Jonathan Snook)][9].

    .l-wrap {
        max-width: 1140px;
        margin-right: auto;
        margin-left: auto;
    }

Примечание: я настоятельно рекомендую использовать относительные единицы типа
`em` или `rem` заместо пикселов для доступности и отзывчивости. В этой статье
я пишу все в пикселах, потому что они проще для понимания.


## Шаг 4: Расчитайте ширину колонок {#step-4-calculate-column-width}

Помните, мы используем флоаты для создания наших колонок и отступов. Когда мы
используем флоаты, у нас есть только пять свойств для этого 
(если вы используете Flexbox, то у вас есть еще несколько); вот эти
пять свойств:

*   width
*   margin-right
*   margin-left
*   padding-right
*   padding-left

Если вы помните, HTML для CSS-сеток выглядит примерно так:
    
    <div class="l-wrap">
      <div class="three-col-grid">
        <div class="grid-item">Grid item</div>
        <div class="grid-item">Grid item</div>
        <div class="grid-item">Grid item</div>
      </div>
    </div>
    

Мы знаем, что в этом HTML сетка имеет всего три колонки в строке. Мы также
знаем, что тут нет дополнительно `<div>` для создания отступов. Это означает:

1.  Мы создаем колонки со свойством `width`
2.  Мы создаем отступы либо со свойством `margin`, либо со свойством `padding`

Если думать о колонках и отступах одновременно, то становится сложнее,
так что давайте допустим, что сперва мы создаем сетку без отступов.

На выходе такая сетка будет похожа на что-то такое:<figure>

![Трех-колоночная сетка без отступов][10]<figcaption>Трех-колоночная 
сетка без отступов</figcaption></figure>

Это тот момент, в котором мы должны сделать немного математических вычислений.
Мы знаем, что сетка имеет максимальную ширину в 1140px, а это означает, что
каждая колонка будет 380px (`1140 ÷ 3`).

    .three-col-grid .grid-item {
      width: 380px;
      float: left;
    }
    

Пока все хорошо. Мы сделали сетку, которая работает отлично на вьюпортах больше
чем 1140px. К сожалению, все ломается, когда вьюпорт меньше, чем 1140px.<figure>

![Сетка ломается, когда вьюпорт меньше 1140px][11]<figcaption>Сетка ломается, 
когда вьюпорт меньше 1140px</figcaption></figure>

Это занчит, что мы не можем использовать пикселы в наших расчетах. Нам нужна 
единица, которая перестроится в соответствии с шириной контейнера. Лишь одна
единица может так делать - проценты (`%`). Поэтому, мы пропишем ширину в 
процентах:

    .three-col-grid .grid-item  {
      width: 33.33333%;
      float: left;
    }
    
Полученные код выше  - это простая трех-колоночная сетка без каких-либо отступов. 
Когда браузер меняет размер, эти три колонки сменят размер пропорционально.<figure>

![Три колонки без отступов][12]<figcaption>Три колонки без 
отступов</figcaption></figure>

Еще кое-что, перед тем как мы двинемся дальше. Всякий раз, когда все дочерние
элементы в контейнере имеют обтекание, высота контейнера схлопывается. Этот 
феномен называется [схлопывание флоата][13]. Это как если бы в 
контейнере не было бы никаких дочерних элементов:<figure>

![Схлопывание флоата. Изображение с CSS Tricks][14]<figcaption>Схлопывание 
флоата (изображение с CSS Tricks)</figcaption></figure>

Для того, что бы это исправить, нам нужен clearfix, который выглядит следующим
образом:

    .three-col-grid:after {
      display: table;
      clear: both;
      content: '';
    }
    

Если вы используете препроцессор типа Sass, вы можете сделать из этого 
миксину, что позволит вам использовать этот код в разных местах:

    
    // Clearfix
    @mixin clearfix {
      &:after {
        display: table;
        clear: both;
        content: '';
      }
    }
    
    // Usage
    .three-col-grid { @include clearfix; }
    
После того как мы закончили с колонками, следующим шагом создадим несколько 
отступов.

## Шаг 5: Определите расположение отступов {#step-5-determine-gutter-position}

Итак, мы знаем, что должны создать отступы либо со свойством `margin`, либо 
со свойством `padding`. Но что мы должны использовать?

Сделав несколько набросков, вы быстро поймете, что у вас есть четыре возможных
способа как сделать эти отступы.

1.  Отступы могут быть расположены *с одной стороны*, в виде *внешних отступов* 
2.  Отступы могут быть расположены *с одной стороны*, в виде *внутренних отступов* 
3.  Отступы могут быть расположены равномерно *с обоих сторон*, 
в виде *внешних отступов* 
4.  Отступы могут быть расположены равномерно *с обоих сторон*,
в виде *внутренних отступов*<figure>

![4 возможных способа создать колонки и отступы][15]<figcaption>4 возможных способа 
создать колонки и отступы</figcaption></figure>

Здесь начинаются сложности. Вам нужно расчитать ширину колонок по-разному,
в зависимости от метода, который вы используете.

Мы рассмотрим эти методы один за другим и посмотрим на разницу. Не торопитесь, пока
вы читаете о них.

Поехали:

### Метод 1: Односторонние оступы (внешние)

Используя этот метод, вы создаете оступы при помощи свойства `margin`. Этот
отступ будет расположен слева или справа от колонки. Вам решать какую 
сторону выбрать.

В целях этой статьи, давайте предположим, что вы задаете свои отступы справа. 
Вот что вы будете делать:

    .grid-item {
      /* Need to recalculate width property */;
      margin-right: 20px;
      float: left;
    }
    

Затем, вы пересчитываете ширину колонки как на этой картинке:<figure>

![Односторонние отступы с использованием внешних отступов][16]<figcaption>Односторонние 
отступы с использование внешних отступов</figcaption></figure>
Как вы видите на картинке выше, *1440px* равняются *трем колонкам* и *двум отступам*.

И тут у нас появилась проблема... Нам нужно, что бы колонки были описаны в процентах,
но в тоже время наши отступы зафиксированы на ширине 20px. Мы не можем делать вычисления с
двумя разными единицами измерения одновременно!

Ну, это было невозможно раньше, но возможно сейчас.

Вы можете использовать CSS-функцию `calc` для сочетания процентов с другими 
единицами. Она на лету извлекает значение процентов для вычислений.

Это значит, что вы можете задать ширину в виде функции, и браузер автоматически
расчитает для вас ее значение:

    .grid-item {
      width: calc((100% - 20px * 2) / 3);
      /* other properties */
    }
    

Это отлично.

После получения ширины колонки, вам нужно удалить последний отступ у крайнего 
правого элемента сетки. Вот как вы можете сделать это:

    .grid-item:last-child {
      margin-right: 0;
    }
    
Чаше всего, когда вы удаляете последний отступ у крайнего правого элемента, вы
также хотите задать ему обтекание по правой стороне для предотвращения ошибок
субпикселного округления, из-за которых ваша сетка переносит последний элемент 
на новую строку. Это происходит только в браузерах, которые округляют пикселы
в большую сторону.<figure>

![Ошибка субпикселного округления может сломать сетку, вытолкнув последний элемент на следующуюю строку][17]<figcaption>
Ошибка субпикселного округления может сломать сетку, вытолкнув 
последний элемент на следующуюю строку</figcaption></figure>
    
    .grid-item:last-child {
      margin-right: 0;
      float: right;
    }

Фух. Почти готово. Еще одна вещь.

Наш код хорош только в том случае, если сетка содержит только одну строку.  
Однако, он не обрезает их, если строк с элементами больше чем одна<figure>

![Наш код лажает, если строк больше чем одна][18]<figcaption>Наш код лажает,
если строк больше чем одна</figcaption></figure>

Нам нужно удалть правый внешний отступ у каждого крайнего правого
элемента в каждой строке. Лучше способо сделать это - использовать `nth-child()`:

    
    /* For a 3-column grid */
    .grid-item:nth-child(3n+3) {
      margin-right: 0;
      float: right;
    }
    

Это все, что вам нужно для создания односторонних внешних отступов.
Вот codepen, что бы вы могли поиграться с этим.

See the Pen [Single sided grid with gutters as margins][19] by Zell Liew 
([@zellwk][20]) on [CodePen][21].

Примечание: Свойство Calc не работает в IE8 и Opera mini. Вы можете посмотреть
другие методы, если вам нужно поддерживать эти два браузера.

### Метод 2: Односторонние оступы (внутренние)

Как и односторонние внешние отступы, в этот методе требуется разместить ваши
отступы на одной из сторон ваших колонок. Предположим, что вы снова выбрали правую
сторону.

    .grid-item {
      /* width property */
      padding-right: 20px;
      float: left;
    }
    
Затем, вы можете пересчитать ширину колонки как на этой 
картинке:<figure>

![Односторонние отступы с использованием внутренних отступов][22]<figcaption>Односторонние 
отступы с использованием внутренних отступов</figcaption></figure>

Обратили внимание, что ширина отлчиается от предыдущего метода?
Она отличается, потому что мы переключили свойство `box-sizing` в `border-box`.
Теперь, `width` расчитывается, включая в себя `padding`.

В этом случае, две из трех колонок имеют бОльшую ширину, чем последняя, что
в конечном итоге приводит к причудливым расчетам и делает CSS код трудным для понимания.

Я предлагаю даже не пробовать этот методом. (???Оно??? станет действительно уродливым, если
вы продолжите с ним. Пробуйте на свой страх и риск.) 

### Метод 3: Разделенные отступы (внешние) {#method-3-split-gutters-margin-}

В этом методе, вы разделяете отступы на две части и размещяете по половине с 
каждой стороны ваших колонок. Код выглядит примерно так:


    .grid-item {
      /* Width property */
      margin-right: 10px;
      margin-left: 10px;
      float: left;
    }
    

Затем, вы пересчитываете ширину колонки как на этой картинке:<figure>

![Разделение внешних отступов][23]<figcaption>
Разделение внешних отступов</figcaption></figure>

Как мы узнали ранее, вам нужно расчитать ширину колонки с помощью 
функции `calc()`. В этой ситуации, вы отнимаете три отступа от 100%,
прежде чем делить ответ на три для получения ширины колонки. Другими словами,
ширина колонки будет `calc((100% - 20px * 3) / 3)`.

    .grid-item {
      width: calc((100% - 20px * 3) / 3);
      margin-right: 10px;
      margin-left: 10px;
      float: left;
    }
    

Это все! (Вам не нужно ничего дополнительно делать для сеток с несколькими строками).
Вот codepen, что бы вы могли поиграться с этим:

See the Pen [grid with split gutters as margins][24] by Zell Liew (
[@zellwk][20]) on [CodePen][21].

### Метод 4: Разделенные оступы (внутренние) {#method-4-split-gutters-padding-}

Этот метод аналогичен предыдущему. Вы делиле ваши отступы и размещаете их с каждой 
стороны ваших колонок. На этот раз, вы используете внутренние отступы:

    .grid-item {
      /* width property */
      padding-right: 10px;
      padding-left: 10px;
      float: left;
    }
    

Затем, вы расчитываете ширину вашей колонки так:<figure>

![Разделенные внутренние отступы][25]<figcaption>Разделенные внутренние 
отступы</figcaption></figure>

Обратили внимание, что в этот раз гораздо легче делать расчеты?
Все верно; это треть ширины сетки в каждой контрольной точке.

    .grid-item {
      width: 33.3333%;
      padding-right: 10px;
      padding-left: 10px;
      float: left;
    }
    

Вот codepen, что бы вы могли поиграться с этим:

See the Pen [grid with split gutters as padding][26] by Zell Liew (
[@zellwk][20]) on [CodePen][21].

Прежде чем мы двинемся дальше, я хочу сказать вам о небольшом предостережении,
если вы используете разделенные внутренние отступы. Если вы взгляните на разметку в
Codepen, то вы увидите, что я добавил дополнительный `<div>` внутри `.grid-item`. 
Этот дополнительный `<div>` важен, если ваш компонент содержит фон или границы.

Это потому что фон отображатеся на внутренних границах. Эта картинка должна
объяснить почему (я надеюсь), показав связь между `background` и другими 
свойствами.<figure>

![Фон отображатеся на внутренних границах][27]<figcaption>Фон отображатеся 
на внутренних границах</figcaption></figure>


### Что бы я использовал? {#what-would-i-use-}

Когда я начал кодить сетки два года назад, я в основном делал сетки, которые
были спроектированы по [нисходящему подходу][28] и построены на 
 [гибридной системе][29]. В таком подходе/системе, *я использовал процентные значения*
 *и для ширины, и для отступов*

В то время, я любил простоту настроек отступов с одной стороны колонки. Это было менее 
напряжно для меня, потому что я довольно плох в математике. Дополнительные 
`отступы +2` расчеты быстро вырубали меня.

Я благодарен, что я пошел этим путем. Хоть CSS и выглядит более сложным, чем
для разделенных отступов, я был вынужден изучить [свойство nth-child][30]. Я также
понял важность написания [mobile-first CSS][31]. Насколько я могу судить, 
это до сих пор является главным препятствием и для молодых, и для опытных
разработчиков.

Так или иначе, если вы попросите меня выбрать сейчас, **я выбиру разделенные отступы**
заместно односторонних, потому что CSS для них более простой. Также, 
**я рекомендую использовать внешние отступы** заместо внутренних, потому что 
разметка получается чище. (Но *внутренние отступы легче расчитать*, поэтому я продолжу 
статью с внутренними отступами).

## Шаг 6: Создайте отладочную сетку {#step-6-create-a-debug-grid}

Когда вы только начинаете, особенно полезно иметь под рукой контрольную сетку,
которая поможет вам отладить вашу разметку. Это помогает быть уверенным, что
вы все делаете правильно.

На данный момент, я знаю только кривой способ создать отладочную сетку. Нужно
создать HTML-элементы и добавить к ним немного CSS. Вот так примерно выглядит HTML:

    <div class="fixed-gutter-grid">
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
      <div class="column"></div>
    </div>
    

CSS для отладочной сетки будет следующий (я использую разделенные внешние отступы
для упрощения разметки отладочной сетки):


    .column {
      width: calc((100% - 20px * 12) / 12);
      height: 80px;
      margin-right: 10px;
      margin-left: 10px;
      background: rgba(0, 0, 255, 0.25);
      float: left;
    }
    

See the Pen [Fixed gutter debug grid][32] by Zell Liew ([@zellwk][20]) on 
[CodePen][21].

(Ультра ремарка: Сьюзан Мириам (Suzanne Miriam) and Собрал Робсон (Sobral Robson) работают
над [фоновым SVG изображением отладочной сетки для Susy v3][33]. Это мега захватывающе,
потому что вы можете использовать простую функцию для создания вашей отладочной сетки!)


## Шаг 7: Внесите изменения в раскладку {#step-7-create-layout-variations}

Следующий шаг заключается во внесении изменений в вашу раскладку на основе 
вашего контента. Это то, где CSS-сетка сияет. Вместо того, что бы создавать 
раскладку с написанием множества сеточных классов, вы можете создать для нее
разумно-звучащее имя.
 
Для примера, давайте предположим, что у вас есть сетки для раскладка, которая
используется только для гостевых статей. Для десктопа раскладка выглядит 
примерно так:<figure>

![Пример сетки для раскладки, котоорая используется только для гостевых статей][34]<figcaption>
Пример сетки для раскладки, котоорая используется только для гостевых статей</figcaption></figure>

Разметка для раскладки этой гостевой статьи может быть такой:

    div class="l-guest-article">
      <div class="l-guest"> <!-- Guest profile --></div>
      <div class="l-main"><!-- main article--></div>
      <div class="l-sidebar"><!-- sidebar widgets--></div>
    </div>
    

Хорошо, дорогуша. Итак, сейчас у нас есть 12 колонок. Ширина одной колоник 8.333% 
`(100 ÷ 12)`.

Ширина `.l-guest` равна двум колонкам. Так что, что вам нужно сделать, так это умножить
8.333% на два. Достаточно просто. Просто прополаскайте(??????) и повторите для остального.

Здесь я предлагаю использовать препроцессор типа Sass, который позволит вам расчитывать
ширину колонок проще, использую функцию `percentage`, заместо ручных расчетов:

    .l-guest-article {
      @include clearfix;
      .l-guest {
        // Ahem. More readable than 16.666% :)
        width: percentage(2/12);
        padding-left: 10px;
        padding-right: 10px;
        float: left;
      }
    
      .l-main {
        width: percentage(7/12);
        padding-right: 10px;
        padding-left: 10px;
        float: left;
      }
    
      .l-sidebar {
        width: percentage(3/12);
        padding-right: 10px;
        padding-left: 10px;
        float: left;
      }
    }
    

See the Pen [Content-sidebar-layout with fixed-gutter grid][35] by Zell Liew
([@zellwk][20]) on [CodePen][21].

Вы должно быть заметил, что сейчас часть кода повторяется. Мы можем сделать это
лучше, вынеся общие части в отдельный селектор типа `.grid-item`.

    .grid-item {
      padding-left: 10px;
      padding-right: 10px;
      float: left;
    }
    
    .l-guest-article {
      .l-guest { width: percentage(2/12);}
      .l-main { width: percentage(7/12);}
      .l-sidebar { width: percentage(3/12); }
    }
    

Вот так. Гораздо чище. :)

## Шаг 8: сделайте вашу раскладку адаптивной {#step-8-make-your-layouts-responsive
}

Последний шаг - это сделать вашу раскладку адаптивной.
Давайте предположим, что раскладка нашей гостевой статьи ведет себя 
следующим образом:<figure>

![Как раскладка гостевой статьи ведет себя на различных вьюпортах][36]<figcaption>
Как раскладка гостевой статьи ведет себя на различных вьюпортах</figcaption></figure>

Разметка нашей гостевой статьи не должна меняться. То, что у нас есть - это 
самая доступная раскладка, которая у нас может быть. Так что, изменения должны
быть полностью в CSS.







When writing the CSS for our responsive guest layout, I highly recommend you
write[mobile first css][37] because it makes your code simpler and neater. We
can begin by writing CSS for the mobile layout first.

Here’s the code:

    <p class="hljs-selector-class">.l-guest-article</p> {
      <p class="hljs-selector-class">.l-guest</p> {  }
      <p class="hljs-selector-class">.l-main</p> {
        <p class="hljs-attribute">margin-top</p>: <p class="hljs-number">20px</p>;
      }
      <p class="hljs-selector-class">.l-sidebar</p> {
        <p class="hljs-attribute">margin-top</p>: <p class="hljs-number">20px</p>;
      }
    }
    

There’s nothing we need to do since every component takes up the full width
by default. However, we can add some margin-top to the last two items to 
separate the elements from each other.

Next, let’s move on to the tablet layout.

For this layout, let’s say we activate the breakpoint is 700px. `.l-guest`
should be 4 of 12 columns while`.l-main` and `.l-sidebar` should be 8 of 12
columns each.

Here, we need to remove the `margin-top` property from `.l-main` because it
needs to be in line with`.l-guest`.

Also, if we set `.l-sidebar` to a width of 8 columns, it will automatically
float onto the second row because there’s not enough room on the first row. 
Since it’s on the second row, we also need to add some left margins on
`.l-sidebar` to push it into position; alternatively, we can float it to the
right. (I’ll float right since there’s no need to calculate anything
).

Finally, since we’re floating the grid items, the grid container should
include a clearfix to clear it’s own children.

    <p class="hljs-selector-class">.l-guest-article</p> {
      @<p class="hljs-keyword">include</p> clearfix;
      <p class="hljs-selector-class">.l-guest</p> {
        @<p class="hljs-keyword">media</p> (min-width: 700px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">float</p>: left;
        }
      }
      <p class="hljs-selector-class">.l-main</p> {
        <p class="hljs-attribute">margin-top</p>: <p class="hljs-number">20px</p>;
        @<p class="hljs-keyword">media</p> (min-width: 700px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">margin-top</p>: ;
          <p class="hljs-attribute">float</p>: left;
        }
      }
      <p class="hljs-selector-class">.l-sidebar</p> {
        <p class="hljs-attribute">margin-top</p>: <p class="hljs-number">20px</p>;
        @<p class="hljs-keyword">media</p> (min-width: 700px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">float</p>: right;
        }
      }
    }
    

Lastly, let’s move on to the desktop layout.

For this layout, let’s say we activate the breakpoint is 1200px. `.l-guest`
should be 2 of 12 columns,`.l-main` should be 7 of 12 columns and `.l-sidebar`
should be 3 of 12 columns.

What we do is to create a new media query within each grid item and change the
width as necessary. Take note we need to remove the margin-top property from
`',l-sidebar` as well.

    <p class="hljs-selector-class">.l-guest-article</p> {
      @<p class="hljs-keyword">include</p> clearfix;
      <p class="hljs-selector-class">.l-guest</p> {
        @<p class="hljs-keyword">media</p> (min-width: 700px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">float</p>: left;
        }
    
        @<p class="hljs-keyword">media</p> (min-width: 1200px) {
          <p class="hljs-attribute">width</p>: percentage(/);
        }
      }
      <p class="hljs-selector-class">.l-main</p> {
        <p class="hljs-attribute">margin-top</p>: <p class="hljs-number">20px</p>;
        @<p class="hljs-keyword">media</p> (min-width: 700px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">margin-top</p>: ;
          <p class="hljs-attribute">float</p>: left;
        }
        @<p class="hljs-keyword">media</p> (min-width: 1200px) {
          <p class="hljs-attribute">width</p>: percentage(/);
        }
      }
      <p class="hljs-selector-class">.l-sidebar</p> {
        <p class="hljs-attribute">margin-top</p>: <p class="hljs-number">20px</p>;
        @<p class="hljs-keyword">media</p> (min-width: 700px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">float</p>: right;
        }
        @<p class="hljs-keyword">media</p> (min-width: 1200px) {
          <p class="hljs-attribute">width</p>: percentage(/);
          <p class="hljs-attribute">margin-top</p>: ;
        }
      }
    }
    

Here’s the codepen for the final layout we’ve created:

See the Pen [guest-article layout with fixed-gutter grid (final)][38] by Zell
Liew
([@zellwk][20]) on [CodePen][21].

(Oh, by the way, you can achieve these results with Susy too. Just remember to
set the[gutter-position][39] to `inside-static`)

## Wrapping up {#wrapping-up}

Wow. This is a long article. I think I died three times writing it. (Thanks for
reading it all the way. I hope you didn’t die three times reading it though!
😛).

As you can see in this article, the steps to creating a responsive grid system
are relatively straightforward. The parts that most people get mixed up are 
steps 5 (determining gutter position) and 8 (making layouts responsive
).

Step 5 is simple when you think through all the possible methods, and we’ve
thought them through together. Step 8, on the other hand, is solvable easily 
once you have enough practice with writing[mobile first css][37]

I hope this article has given you the knowledge to build your own responsive
grid system, and I hope to see you build a custom grid for your next project.

Till then!</article>

 [1]: https://zellwk.com/blog/designing-grids
 [2]: https://zellwk.com/blog/designing-grids/
 [3]: https://zellwk.com/blog/migrating-from-bootstrap-to-susy/
 [4]: https://zellwk.com/blog/from-html-grids-to-css-grids/
 [5]: http://gridbyexample.com
 [6]: img/box-sizing.jpg
 [7]: https://zellwk.com/blog/understanding-css-box-sizing/
 [8]: https://smacss.com
 [9]: https://twitter.com/snookca
 [10]: img/columns.png
 [11]: img/grid-break.gif
 [12]: img/grid-columns.gif
 [13]: https://css-tricks.com/all-about-floats/
 [14]: img/float-collapse.png
 [15]: img/combi.png
 [16]: img/pattern-1side-margin.png
 [17]: img/subpixel.png
 [18]: img/margin-side-last-child.png
 [19]: http://codepen.io/zellwk/pen/mAYqrL/
 [20]: http://codepen.io/zellwk
 [21]: http://codepen.io
 [22]: img/pattern-1side-gutter.png
 [23]: img/pattern-split-margin.png
 [24]: http://codepen.io/zellwk/pen/BLZJza/
 [25]: img/pattern-split-padding.png
 [26]: http://codepen.io/zellwk/pen/ORYzQV/
 [27]: img/bg-relationship.jpg

 [28]: https://zellwk.com/blog/designing-grids/#how-big-should-columns-and-gutters-be-

 [29]: https://zellwk.com/blog/designing-grids/#how-the-grid-responds-to-different-viewports
 [30]: https://css-tricks.com/examples/nth-child-tester/
 [31]: https://zellwk.com/blog/how-to-write-mobile-first-css/
 [32]: http://codepen.io/zellwk/pen/ALkyAA/
 [33]: https://github.com/oddbird/susy/issues/609
 [34]: img/grid-example.png
 [35]: http://codepen.io/zellwk/pen/pEmLzY/
 [36]: img/grid-responsive.png
 [37]: https://zellwk.com/blog/mobile-first-css/
 [38]: http://codepen.io/zellwk/pen/qaGvxm/
 [39]: https://zellwk.com/blog/susy-gutter-positions/
