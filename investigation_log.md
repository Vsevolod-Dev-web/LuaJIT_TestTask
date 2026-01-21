# Подробный лог исследования проблемы

## В первую очередь, пробуем запустить билд.

Проводим стандартную сборку

```bash
make
```

Видим три сообщения, одно из них указывает на ошибку
использования необъявленной константы "INT_MAX" в функции "unbound search",
в файле lj_tab.c:

lj_tab.c: In function ‘unbound_search’:
lj_tab.c:629:21: error: ‘INT_MAX’ undeclared (first use in this function)
  629 |     if (j > (MSize)(INT_MAX-2)) {  /* overflow? */
      |                     ^~~~~~~

Так же видим два примечания(note), где, перввое, говорит, что `INT_MAX`
определена в `<limits.h>` и, кажется, не была установлена связь
с заголовочном файлом, где находиться константа. Второе примечание, говорит,
что константа в коде используется лишь раз, в строчке 629, в файле lj_tab.c.

lj_tab.c:16:1: note: ‘INT_MAX’ is defined in header ‘<limits.h>’; did you forget to ‘#include <limits.h>’?
   15 | #include "lj_tab.h"
  +++ |+#include <limits.h>
   16 | 

lj_tab.c:629:21: note: each undeclared identifier is reported only once for each function it appears in
  629 |     if (j > (MSize)(INT_MAX-2)) {  /* overflow? */
      |                     ^~~~~~~

Просмотрев логи сборки, можно заключить, что проблемма в отсутсвии
зависимости с заголовочным файлом limits.h где объевлена используемая константа.

Ошибка найдена. Ставим задачу, переходим к решению.
