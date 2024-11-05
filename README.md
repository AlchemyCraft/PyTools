# PyTools
Скрипты для работы в специализированном ПО

# pivot_table.ipynb
Скрипт для предобработки и объединения данных по скважинам.

Исходные данные: общая таблица с посуточными показателями работы скважин, несколько таблиц с помесячными давлениями по скважинам.
Исходные данные не прилагаются по причине конфиденциальности.

Как работает скрипт: в рамках предобработки данных преобразуются типы данных, уменьшается объем используемой памяти, заполняются пропущенные значения по различным показателям, объединяются таблицы с разным содержимым.

Результат: таблица с помесячными показателями работы скважин и давлениями.
Используемые библиотеки: pandas, numpy, os, datetime, typing, dotenv

# pressure_optim_calc.ipynb
Скрипт для оптимизации подбора трех параметров трубы.

Исходные данные: таблица с помесячными показателями работы скважин и давлениями.
Исходные данные не прилагаются по причине конфиденциальности.

Как работает скрипт: цель - подобрать три параметра трубы, которые позволят воспроизвести динамику фактического давления. Причем корректировка каждого из параметров оказывает разную степень влияния на изменение расчетного давления. Следовательно, целевая функция - функция минимизации разницы расчетного и фактического давления (разница рассчитывается сразу по нескольким точкам). 
Скрипт запускает метод оптимизации поиска параметров трубы, далее исходные данные передаются спец. ПО, в котором выполняются расчеты, после чего забираются результаты и сравниваются с референтными давлениями. 
В рамках тестирования были рассмотрены: метод Ньютона, метод бисекции (финальное решение), метод минимизации shgo.

Результат: подобраны три параметра трубы, которые будут использоваться для дальнейших расчетов в спец. ПО.

Используемые библиотеки: pandas, matplotlib.pyplot, re, typing, scipy, sklearn, win32com (подключение к специализированному ПО)

# pressure_adapt_with_ofp.ipynb
Скрипт для настройки давления (Рпл) по скважинам с помощью варьирования ОФП (ОФП влияют на течение флюидов в пласте).

Исходные данные: таблица с помесячными показателями работы скважин и давлениями.
Исходные данные не прилагаются по причине конфиденциальности.

Алгоритм выполнения расчета по каждой скважине:
1. Расчет начального Кпрод
2. Задание ОФП, которые будут использоваться для корректировки Кпрод
3. Выбор Рзаб на основе исходных данных. Варьируется Рпл, используется метод половинного деления. Настройка выполняется на весь период работы скважины
4. Расчет среднеквадратической ошибки фактического и расчетного Рпл
5. Запоминание лучшей таблицы ОФП и наименьшей среднеквадратической ошибки
6. Формирование итоговой статистики по лучшим ОФП по каждой скв

Результат: подобранные ОФП для каждой скважины, позволяющие наилучшим образом воспроизвести давление (Рпл).
Используемые библиотеки: pandas, numpy, matplotlib, seaborn, sklearn, warnings, tqdm, typing, os, shutil
