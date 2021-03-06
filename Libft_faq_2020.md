# Libft FAQ (mid 2020)
В связи с тем, что в ближайшую неделю нас ожидает шквал из сдающих либу, решил собрать здесь самые популярные грабли, на которых можно завалить проект. Если перед сдачей проекта пройтись по этому чеклисту, можете сэкономить время и себе, и проверяющим.

## Дисклеймер
Всё ниже написанное - моё субъективное мнение, и может отличаться от того, что на самом деле проверяет муля на тот момент, когда вы это читаете. Как нам любят напоминать - dont trust rumors.
Если у вас есть предложения и дополнения (которые не отлавливает чекер libfttest) - пишите.

## Makefile
1. При запуске make собирается либа из основных функций. При повторном - не собирается.
2. При запуске make fclean && make bonus собирается либа из бонусных функций. При повторном - не собирается. (Для просмотра содержимого либы можно использовать команду nm libft.a). В сабджекте сказано, что в библиотеку добавляются бонусные функции, значит если либы нет, то она создаётся и в неё добавляются бонусные (а не вообще все) функции.
3. При изменении libft.h (например touch libft.h) пересобираются зависимые объектные файлы и либа.
4. При изменении любого .c файла из основной или бонусной части перекомпилируется как минимум этот файл перед сборкой либы соответствующим правилом. Если компилится только тот, который изменился - бонус вам.

## Чекеры
Из всего опробованного на linux адекватнее всего ведёт себя libfttest, рекомендую использовать его как основной. Но напоминаю, что использование чекера не заменяет проверку функций в ручном режиме, а лишь дополняет её.

## Норма
1. Не забываем, что в нормах есть пункт про то, что все включения в .h и .c файлах должны быть обоснованы. Так что будьте готовы объяснить проверяющему, чем обосновано #include "libft.h" в функции ft_toupper или ft_isdigit, если оно у вас есть.

## Константы
1. Вместо того, чтобы хардкодить константы, используйте заголовочный файл limits.h (чтобы, например, получить минимальное значение инта для текущей системы).
2. То же самое для случаев, когда ваш код рассчитывает на определённое количество символов в этих самых минимальных/максимальных значениях. В зависимости от системы они могут отличаться.

## 1 часть - Системные функции
1. ft_calloc делайте по маковскому мануалу, не по линуксовому. То есть NULL возвращаем только в случае ошибки malloc-а, но не при нулевых значениях size или nmemb.

## 2 часть
1. ft_split при пустой строке (или строке из одних разделителей) возвращает не NULL-pointer, а массив строк, в котором находится единственный элемент - NULL-pointer.
2. ft_substr возвращает пустую строку (ft_strdup("")) в случае, если индекс вне пределов строки. Да, это не логично и не понятно, это нужно просто принять и простить.
3. ft_strtrim корректно обрабатывает пустую строку.
4. Делаете вы проверки на некорректные данные или нет - для мули не важно. Важно, чтобы вы могли объяснить проверяющему, почему вы приняли такое решение.

## Бонусы
1. Если вы решили делать проверки на некорректные данные, то проверяйте не только указатели на элементы списка перед тем, как их разыменовывать, но и указатели на функции перед тем, как их использовать.

