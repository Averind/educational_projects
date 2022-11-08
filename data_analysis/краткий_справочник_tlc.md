# Общие соображения (по результатам написания 4х параметрических конструкций)
* [Рамные опоры РМГ, РМТ, РМП](m2\RMX_tochinvest_v4.tlc) 
* [ОСФГ-ОГСГ светофорные опоры](m2\ОСФГ-ОГСГ светофорные опоры)
* [О-опора; М-металлическая; Г-г-образная; Ф-фланцевая; ДЗ-для дорожных знаков;](m2\ОМГФ)
* [СОД-Г светофорные опоры](m2\СОД-Г светофорные опоры)

## Когда параметризируем полностью
1. Если большой сортамент (и есть готовая таблица с данными)
2. В разных варинтах не сильно меняется схема конструкции (если в каждом подварианте отдельным образом сделана конструкция — проще сделать костыль)

## Когда лучше закостылить
* См. пример ОМГФ — где 4 варианта, которые проще было изготовить «полуиндивидуально»
* Единичные конструкции

# Как динамически моделировать конструкции
* vscode
* ![](img/2022-07-28-14-36-33.png)
  * При запуске этой «ꕯ» штуки открывается отдельное окно Visual Studio Code, tlc-файлы которого синхронизировны с Робуром: меняем значение параметра в коде — 
* 🔴 не использовать [[Ctrl + Z]] в окне Робура при использовании динамики — крэш

# Полезные инструменты
* Сниппеты [](C:\Users\user\AppData\Roaming\Code\User\snippets\clojure.json)
* Болерплэйт [](C:\Users\user\topo\YandexDisk\work\tlc\_boil.tlc)

# Конвенции
Блок геометирии — обрамлять `(defgeometry <...>)`:
* внутри if
* когда несколько построений внутри `(defun (a b c) <...>)` 

# Основные функции

## 3д-операции
### v-extrude 
* Выдавливание вдоль вектора (extrusion)
  * 1 Профиль (двухмерный)
  * 2 Трёхмерный вектор (vec x y z)
* Пример:
  * `(v-extrude (v-profile-rect a l) (vec 0 0 h))`

### v-revolve
* Тело вращения
    * 1 Профиль 2d
    * 2 Угол раскрытия
* Пример: `(v-revolve (v-profile-translate (v-profile-round D1) (vec R 0)) angle)`
* Не забываем сдвинуть профиль

## Функции построения профилей
### v-profile-rect
  * Прямоугольный профиль
    * 1 ширина
    * [2 высота]
* Пример: (v-profile-rect a b)

### v-profile-round
* Круглый профиль
  * 1 радиус
* Пример:
  * `(v-profile-round a)`

### v-profile-shape
* Создание фигуры по координатам
* Пример:
```
(v-profile-shape 
    x1 y1
    x2 y2
    .. ..
    xn yn
    x1 y1
)
```


## Функции преобразования трёхмерных фигур
### v-translate
* Перенос по трехмерной оси
  * 1 (vec x y z)
  * 2 трёхмерный объект
* Пример: 
```
(v-translate 
    (vec dx dy dz)
    (v-extrude (v-profile-rect w t) (vec 0 0 h))
)
```

### v-align
* Размещение в пространстве   
  * 1 трехмерныq вектор 
  * 2 трехмерныq вектор 
  * 3 угол
  * 4 трёхмерная фигура
* Пример: 
```
(v-align (vec 0 0 1) (vec 0 1 0) 0
    (v-revolve (v-profile-translate (v-profile-round D1) (vec R 0)) alpha)
)
```
* Пример (такая штука поворачивает разумно сдвинутое тело body на angle, относительно начала координат):
```
(v-align (vec 0 0 0) (vec 0 0 1) angle
    body
)
```

## Функции преобразования профилей
### v-profile-scale
* Регуляция масштаба
* Пример: 
  * `(v-profile-scale (v-profile-round r) mx my)`

### v-profile-translate
* Перенос фигуры
  * 1 Профиль
  * 2 Вектор 2d (vec x y)
* Пример: 
    * (v-profile-translate mus1 (vec 0 0))
* Пояснение:
    * (v-profile-translate (a-профиль) (vec x y)0

### v-profile-rotate
    * Разворот фигуры
        * 1 Профиль
        * 2 Угол (в градусах)
* Пример:
    * (v-profile-rotate a 180)
* Пояснение: 
    * (v-profile-rotate (a-профиль) (180-угол))

## Циклы
* (v-for (i (range ))
    * Создание цикла
        * 1 
        * 2
    * Пример
        * (v-for (i (range n))
        (setq x (* r (cos(/ i step))))
        (setq y (* r (sin(/ i step))))

    * Пояснение
        * (v-for (i (range n))
        (setq x (* r (cos(/ i step))))
        (setq y (* r (sin(/ i step))))

## Условный переход
```
(if (eql x "value")
    (<if true>)
    (<if false>)
)
```

# Все команды
## Вспом в Робуре
list @ robur — для скалывания координат объектов (лучше полинии в нуле)

## Общелисп
```
dotimes dolist while nconc last nreverse _nreverse assoc assq member memq listp or mapcar and append _append letrec let when if equal /= <= >= > setcdr setcar null = identity print consp not caddddddr cadddddr caddddr cadddr cdddr cddar cdadr cdaar caddr cadar caadr caaar cddr cdar cadr caar defun defmacro *version* dict-remove dict-set dict-get dict enum-reset enum-next enum-current enum-get range import dump apply symbol-name intern make-symbol gensym *gensym-counter* terpri princ prin1 2PI PI sign abs pow exp log10 log sqr sqrt tanh tan sinh cosh floor ceiling atan asin acos cos sin min max truncate / - * + mod % < eql numberp stringp length rplacd rplaca list eq atom cons cdr car false true t 
```

## Наши функции
```
defgeometry 

v-property-length-kg 
v-property-length-mm 
v-property-length-cm 
v-property-length-m 

defslots 
defslot 
setproperty 
defproperty 
defcomponent 

v-for 
v-property-typed 
v-property-string 
v-property-enum 
v-property-logic 
v-property-integer 
v-property-double 

getbounds 
getproperty 

v-slot 
v-property 

v-phong 
v-styled 

setelement 
defelement 

v-component 
v-dynamic 
v-profile-mirror 
v-profile-translate 
v-profile-scale 
v-profile-rotate 
v-profile-compound 
v-profile-shape 
v-profile-t 
v-profile-p 
v-profile-g 
v-profile-polygon 
v-profile-arc 
v-profile-round 
v-profile-rect 

v-curve-d1 
v-curve-d0 
v-curve-arc 
v-curve-straight 

v-sphere 
v-extrude 
v-revolve 
v-sweep 
v-align 
v-scale 
v-translate 
v-quality 
v-compound 

vec-sub vec-add vec-eq vec-normalize vec-lerp vec-clamp vec-max vec-min vec-reflect vec-cross vec-dot vec-len vec-z vec-y vec-x vec rot h
```


