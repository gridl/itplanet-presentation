itplanet-presentation
=====================
Презентация к моему [диплому](https://github.com/Amet13/bachelor-diploma) для конкурса ["Лучший свободный диплом"](http://world-it-planet.org/projects/competition_detail.php?ID=41543)

Структура
---------
`beamerthemeSevGU.sty` — файл стиля презентации

`Makefile`

`preamble.tex` — преамбула в которой задаются настройки

`presentation.pdf` — конечный результат компиляции

`presentation.tex`— компилируемый файл, является "костяком" проекта

`report.md` — доклад к презентации

`slides.tex` — само содержимое презентации

`images/` — сюда складываются изображения, которые используются в презентации

Работа с LaTeX
--------------
Как установить LaTeX: http://blog.amet13.name/2014/06/latex.html

Обязательно должен быть установлен пакет `latex-beamer`.

В качестве основного шрифта используется PT Sans, скачать его можно [тут](http://fonts.ru/public/).

Компиляция проекта
------------------
Для этого можно воспользоваться Makefile.
Пример компиляции проекта:
```bash
git clone https://github.com/Amet13/itplanet-presentation.git
cd itplanet-presentation/
make
```

Пример очистки сборочных файлов после компиляции (кроме PDF):
```bash
make clean
```

16:9
----
Есть возможность использовать соотношение сторон не 4:3, а 16:9.
Для этого нужно в файле `presentation.tex` привести данные строки к виду:
```tex
%\documentclass[xetex,mathserif,serif,t]{beamer}
\documentclass[aspectratio=169,xetex,mathserif,serif,t]{beamer}
```

Лицензия
--------
[Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0/deed.ru)

![CC BY-SA](https://licensebuttons.net/l/by-sa/4.0/88x31.png)
