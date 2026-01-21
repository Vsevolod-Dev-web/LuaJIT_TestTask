# Подробный лог исследования проблемы

## В первую очередь, пробуем запустить билд.

Проводим стандартную сборку

```bash
make
```

Видим три сообщения об ошибке:

lj_tab.c: In function ‘unbound_search’:
lj_tab.c:629:21: error: ‘INT_MAX’ undeclared (first use in this function)
  629 |     if (j > (MSize)(INT_MAX-2)) {  /* overflow? */
      |                     ^~~~~~~

lj_tab.c:16:1: note: ‘INT_MAX’ is defined in header ‘<limits.h>’; did you forget to ‘#include <limits.h>’?
   15 | #include "lj_tab.h"
  +++ |+#include <limits.h>
   16 | 

lj_tab.c:629:21: note: each undeclared identifier is reported only once for each function it appears in
  629 |     if (j > (MSize)(INT_MAX-2)) {  /* overflow? */
      |                     ^~~~~~~


