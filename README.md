presentation-latex
==================
Шаблон презентации в LaTeX с использованием Beamer

![](https://raw.githubusercontent.com/Amet13/presentation-latex/master/images/title.png)

![](https://raw.githubusercontent.com/Amet13/presentation-latex/master/images/slide.png)

Структура
---------
`beamerthemeSevGU.sty` — файл стиля презентации

`Makefile`

`preamble.tex` — преамбула в которой задаются настройки

`presentation.pdf` — конечный результат компиляции

`presentation.tex`— компилируемый файл, является "костяком" проекта

`slides.tex` — само содержимое презентации

`images/` — сюда складываются изображения, которые будут использоваться в презентации

Работа с LaTeX
--------------
Для работы с LaTeX рекомендую использовать XeLaTeX и IDE [LaTeXila](https://wiki.gnome.org/Apps/LaTeXila) или [Atom](https://atom.io/) с плагином [language-latex](https://atom.io/packages/language-latex).

Как установить LaTeX: http://blog.amet13.name/2014/06/latex.html

Обязательно должен быть установлен пакет `latex-beamer`, не забывайте об этом.

Для пользователей GNU/Linux можно воспользоваться Makefile.
Пример компиляции проекта:
```bash
git clone https://github.com/Amet13/presentation-latex.git
cd presentation-latex/
make
```
Пример очистки ненужных файлов после компиляции:
```bash
make clean
```

16:9
----
Есть возможность использовать соотношение сторон не 4:3, а 16:9.
Для этого нужно в файле `presentation.tex` закомментировать 9ю строку и раскомментировать 10ю.
![16:9](https://raw.githubusercontent.com/Amet13/presentation-latex/master/images/16-9.png)

Лицензия
--------
[Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0/deed.ru)

![CC BY SA](https://licensebuttons.net/l/by-sa/4.0/88x31.png)
