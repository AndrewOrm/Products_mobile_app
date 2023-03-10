# Products_mobile_app

Проект 10 "Мобильное приложение по продаже продуктов питания" - построение воронки продаж мобильного приложения.    
Задача проекта: на основе данных использования мобильного приложения проанализировать воронку продаж, а также оценить результаты A/A/B-тестирования.    
Инструменты: A/B-тестирование, Matplotlib, Pandas, Plotly, Python, NumPy, SciPy, Seaborn, проверка статистических гипотез, продуктовые метрики, событийная аналитика.    
Ключевые навыки: А/А-тест, A/B-тест, визуализация, конверсия, воронка продаж, статистический тест.    
Статус: завершён    

Итоговый вывод и рекомендации:    

В ходе подготовки данных мы разъединили "слипшиеся" столбцы, исправили тип данных во времени события. Привели названия столбцов к хорошему стилю, поменяли их названия и добавили столбец с датой. Выяснили количество строк - 244 216, достаточно репрезентативно.

Затем проверили данные на пропуски, дубликаты, временные аномалии и задвоение девайсов в разных группах. Было выявлено 413 явных дубликатов (менее 0.2% данных), которые мы удалили. Осталось 243 713 строки.

В анализе данных сделали распределение записей по датам, мы удалили данные за июль месяц, поскольку трафики июля и августа существенно отличаются друг от друга. По всей видимости, произошли какие-то важные изменения в мобильном приложении или в рекламных кампаниях и получении трафика.

В итоге для дальнейшего исследования была создана таблица с 98.8% записей и 99.8% уникальных пользователей. В ней 240 887 записей по 7 534 пользователям за 7 дней. В среднем 32 записи на 1 пользователя (при медиане 20). Все экспериментальные группы пользователей и виды событий также присутствуют. Пользователи распределены примерно поровну между всеми трёмя группами эксперимента. Таблица репрезентативна.

Анализ воронки продаж показал следующее:   

Открытие главной страницы приложения - её открыли 7 419 пользователей из 7 534, 117 431 записей из 240 887 - почти половина всех записей.    
Открытие страницы с Предложениями - сюда дошли уже 4 593 пользователя 46 350 раза.    
Корзина - только половина пользователей добралась до Корзины.    
Успешное завершение оплаты - почти никто не передумал и 3 539 пользователя успешно оплатили приложение.    

Таким образом, успешно дошли до финиша и совершили покупку 47%. Это много! Впрочем, конверсия из Корзины в Оплату - 95%. Хорошо бы довести её хотя бы до 99%.

Только 61% пользователей приложения открывало страницу с Предложениями. И конверсия сюда с Главной страницы всего 62%. Это самое слабое звено. Почти у половины посетителей Главной страницы не возникает мотивации перейти к следующему этапу. Надо будет выяснить причину. Она может иметь технический характер (неудобное расположение кнопки, её незаметность или зависание), либо приложение может быть в целом неудобным или неинтересным пользователям (тут уже не обойтись без маркетологов).

Ещё у 11% пользователей возникли вопросы при использовании приложения и они обращались к странице "Руководство". Это плохо.

Отметим ещё несколько важных результатов анализа воронки продаж:   

Проанализировав разницу между общей частотностью посещения страниц и числом уникальных заходов, мы обнаружили, что существенная часть заходов (до 12% на Главной странице) - повторные. Важно выяснить причину этого - возможно, она технического характера.

Также нужно выборочно проверить трёх лидеров из ТОП-10 с тысячами и сотнями уникальных заходов в приложение за неделю. Действительно ли они такие фанаты мобильного приложения, или здесь кроется какой-то технический баг.

Кроме того, оказалось, что не все пользователи начинали свой путь в приложении с главной страницы. 115 из них, видимо, зашли в него по реферальным ссылкам сразу на страницу с ценовыми предложениями.

Взглянув на воронку продаж отдельно по группам эксперимента, мы выяснили, что максимальная доля пользователей, успешно осуществивших оплату - в группе 246: 48.3%, тогда как в группе 248 - 46.6%, а в группе 247 - вообще 46.1%.

Перед А/В-тестом проверили А/А-тест для проверки корректности двух контрольных групп. Чтобы проверить, если ли статистическая разница между группами 246 и 247, мы рассчитали доли пользователей в разных группах, посетивших одни и те же страницы мобильного приложения. Затем проверили нулевые гипотезы об их равенстве.

Поскольку число пользователей значительно превышает 30, а выборки независимые, использовали z-тест (z-критерий Фишера).

В условиях множественных сравнений (несколько сравнений на одних и тех же данных), когда с каждой проверкой растёт вероятность ошибки I рода (ложнопозитивного результата теста), для уменьшения FWER применили метод Бонферонни.

Результаты А/А-теста показали, что разница в доли пользователей для всех страниц статистически не значима. Следовательно, статистически значимых отличий между контрольными группами 246 и 247 нет. Разбиение на две контрольные группы работает корректно.

Перейдя к А/В-тесту, мы также сравнили доли пользователей, посетивших одинаковые страницы, в группе 248 с изменённым шрифтом и в контрольных группах: сначала сравнили группы попарно, а потом целевую группу с объединённой контрольной группой. Для проверки воспользовались снова z-тестом с поправкой Бонферонни.

Результаты А/В-теста показали, что разница в доли пользователей для всех страниц между целевой и контрольными группами также статистически не значима. Следовательно, статистически значимых отличий между группой 248 и контрольными группами 246 и 247 нет.

Таким образом, внедрение новых шрифтов не влечёт за собой статистически значимых улучшений. Следовательно, нет необходимости тратить на это ресурсы и время.
