# Analytics e-commerce

## Описание: 
E-commerce стартап, работающий в сегменте технологий розничной торговли предоставил для независимой аналитической оценки данные своего маркетплейса, занимающегося продажей и доставкой товаров. Требуется проанализировать полученные данные и изучить пользователей маркетплейса.<br/>

**Для анализа использовался следующий стек технологий**: <br/>

![Python](https://img.shields.io/badge/-Python-0b0038?style=for-the-badge&logo=python&logoColor=3c78a9)
![Pandas](https://img.shields.io/badge/pandas-0b0038?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-0b0038?style=for-the-badge&logo=numpy&logoColor=4c74cc)
![Seaborn](https://img.shields.io/badge/seaborn-0b0038?style=for-the-badge&logo=seaborn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/matplotlib-0b0038?style=for-the-badge&logo=matplotlib&logoColor=white)
![Requests](https://img.shields.io/badge/requests-0b0038?style=for-the-badge&logo=requests&logoColor=white)

## Выполненные задачи:

1)  **Автоматизирован процесс загрузки исходных датасетов с использованиме API Яндекс.Диска** с помощью функции в  которой колонки с датами автоматически преобразуются к типу datetime64.
    ``` python 
    def load_datasets(public_URL: str) -> pd.DataFrame()
    ````
2) **Проведен разведочный анализ данных (EDA-анализ)** в ходе которой для каждого датафрейма в данных было выявлено количество уникальных значений, пропущенных значений, дубликатов и т.д. В конце на примере одного заказа продемонстирована структура данных.

3) **Выполнены следующие аналитические ad-hoc задачи c оформлением визуализаций** (предварительно дано определение и обоснование того, что считать покупкой и недоставленным заказом на основе данных):<br/>
    - Определено количество пользователей, которые совершили только одну покупку. <br/>
    - Определено среднее количество заказов в месяц, которое не доставляется по разным причинам (с детализацией по причинам). На основе получившихся результатов предложен путь по сокращению количества недоставленных заказов. <br/>
    - Определено в какой день недели каждый товар чаще всего покупается. 
    - Определено среднее количество покупок у каждого пользователя в неделю (по месяцам). Дополнительно: определена закономерность в динамике среднего количества покупок в неделю для одного из месяцев.<br/>

4) **Выполнен когортный анализ пользователей** и определена когорта с самым высоким Retantion rate на 3 месяц за рассматриваемый полный год. Признаком формирования когорты была принята дата первой покупки на маркетплейсе.

5) **Выполнен RFM-анализ** в рамках которого изучены распределения дохода и количества покупок по RFM-сегментам пользователей. На основании сочетания RF-метрик созданы категории и проведен анализ распределения пользователей по этим категориям. Сделаны выводы о клиентской базе проекта, а также об эффективности привлечения и удержания пользователей.

## Полученные результаты:
- Около 97 % пользователей маркетплейса совершили не более одной покупки;
- В среднем ежемесячно не доставляется 136 заказов, причем большая часть заказов (37,4 %) не доставляется по вине партнера по логистике. Следовательно, оптимальным вариантом снижения количества недоставленных заказов видится смена партнера по логистике на более надежного;
- Несколько лет подряд среднее количество покупок в неделю достигает максимума в феврале, что может быть связано со стартом зимних распродаж или праздничными днями (14 февраля и др.);
- Самый высокий СRR на 3-ий месяц имеет когорта с первыми покупками 2017-06 (июнь 2017). Интересно заметить, что за период наблюдений абсолютный максимум СRR пришелся на 12 месяц среди клиентов из январской когорты (возможно клиентов этой когорты на площадке привлекают новогодние предложения и они охотно возвращаются за покупками);
- Большую часть маржинальной прибыли (~58%) приносят четыре сегмента пользователей для которых характерно совершение одноразовых покупок общей стоимостью свыше 154 долларов;
- Наибольший объем продаж (около 6 % от общего) приходится на сегмент пользователей для которого характерно совершение одной покупки более 353 дней назад общей стоимостью до 46,5 долларов;
- К лояльной аудитории проекта можно отнести не более ~0,15 % клиентов (категории best customers и loyal customers). Это наиболее ценные категории, требующие особого внимания. В перспективе можно увеличить лояльную аудиторию до ~1 %, если привести клиентов категории potential loyalists к лояльным;
- Команда маркетплейса успешно справляется с привлечением новых клиентов, они приходят стабильно, но редко совершают более одной покупки, требуется активно работать над удержанием клиентов (стремиться увеличить конверсию новый покупатель -> лояльный клиент).

<!-- ## Исходные данные: 

1. **df_customers** - таблица с уникальными идентификаторами и информацией о клиентах:

    `customer_id` - позаказный идентификатор пользователя; <br/>
    `customer_unique_id` - уникальный идентификатор пользователя (аналог номера паспорта); <br/>
    `customer_zip_code_prefix` - почтовый индекс пользователя;<br/>
    `customer_city` - город доставки пользователя;<br/> 
    `customer_state` - штат доставки пользователя.

2. **df_orders** - таблица с информацией о заказах:

    `order_id` - уникальный идентификатор заказа (номер чека);<br/>
    `customer_id` - позаказный идентификатор пользователя;<br/>
    `order_status` - статус заказа;<br/>
    `order_purchase_timestamp` - время создания заказа;<br/> 
    `order_approved_at` - время подтверждения оплаты заказа;<br/> 
    `order_delivered_carrier_date` - время передачи заказа в логистическую службу;<br/>
    `order_delivered_customer_date` - время доставки заказа;<br/>
    `order_estimated_delivery_date` - обещанная дата доставки;<br/>


3. **df_order_items** - таблица с информацией о товарных позициях, входящих в заказ:

    `order_id` - уникальный идентификатор заказа (номер чека);<br/> 
    `order_item_id` - идентификатор товара внутри одного заказа;<br/> 
    `product_id` - ид товара (аналог штрихкода);<br/>
    `seller_id` - ид производителя товара;<br/>
    `shipping_limit_date` - максимальная дата доставки продавцом для передачи заказа партнеру по логистике;<br/>
    `price` - цена за единицу товара;<br/>
    `freight_value` - вес товара. -->


<!-- - Не более ~0,15 % клиентов можно отнести к лояльным, это наиболее ценные клиенты, требующие особого внимания (категории best customers и loyal customers);
- До ~1 % потенциально можно увеличить лояльную аудиторию, если привести клиентов категории potential loyalists к лояльным; -->

<!-- 
- Информация о заказах `df_orders`
- Информация о клиентах `df_customers`
- Информация о товарах в составе заказа `df_order_items` -->
<!-- <style>
ul {
    list-style-type: none; /* Убираем маркеры у ненумерованных списков */
    padding: 0; /* Убираем отступы */
}
</style>

<ul>

<details> 
    <summary>Информация о заказах `df_orders` <u>(см. подробнее)</u></summary>
    <p>

`order_id` - уникальный идентификатор заказа (номер чека)  
`customer_id` - позаказный идентификатор пользователя  
`order_status` - статус заказа  
`order_purchase_timestamp` - время создания заказа  
`order_approved_at` - время подтверждения оплаты заказа  
`order_delivered_carrier_date` - время передачи заказа в логистическую службу  
`order_delivered_customer_date` - время доставки заказа  
`order_estimated_delivery_date` - обещанная дата доставки  
</p>
</details>
</ul>

<ul>

<details> 
    <summary>Информация о заказах `df_customers` (см. подробнее)</summary>
    <p>

`customer_id` - позаказный идентификатор пользователя  
`customer_unique_id` - уникальный идентификатор пользователя (аналог номера паспорта)  
`customer_zip_code_prefix` - почтовый индекс пользователя  
`customer_city` - город доставки пользователя  
`customer_state` - штат доставки пользователя
</p>
</details>
</ul>

<ul>

<details> 
    <summary>Информация о заказах `df_order_items` (см. подробнее)</summary>
    <p>

`order_id` - уникальный идентификатор заказа (номер чека)  
`order_item_id` - идентификатор товара внутри одного заказа  
`product_id` - ид товара (аналог штрихкода)  
`seller_id` - ид производителя товара  
`shipping_limit_date` - максимальная дата доставки продавцом для передачи заказа партнеру по логистике  
`price` - цена за единицу товара  
`freight_value` - вес товара

</p>
</details>
</ul> -->

 

<!-- |  | product_id	               |    max_buy_day                  |
|- |-------------------------------------:|---------------------:|
|0 | 0066f42aeeb9f3007548bb9d3f33c38	  |  [Sunday]            |
|1 |	00088930e925c41fd95ebfe695fd2655  | [Tuesday]            |
|2 |	0009406fd7479715e4bef61dd91f2462  | [Thursday]           |
|3 |	000b8f95fcb9e0096488278317764d19  | [Friday, Wednesday]  |
|4 |	000d9be29b5207b54e86aa1b1ac54872  | [Tuesday]             |
| ... | ...                                   | ...                 | -->


<!-- |  | customer_unique_id	               |    year   | month   | count_buy_week |
|- |-------------------------------------:|-------:|--------:|---------------:|
|0 | 0000366f3b9a7992bf8c76cfdf3221e2	  |  2018  | May     | 0.2258         |
|1 |	0000b849f77a49e4a4ce2b2a4ca5be3f  | 2018   | May     | 0.2258         |
|2 |	0000f46a3911fa3c0805444483337064  | 2017   | March   | 0.2258         |
|3 |	0000f6ccb0745a6a4b88665a16c9f078  | 2017   | October | 0.2258         |
|4 |	0004aac84e0df4da2b147fca70cf8255  | 2017   | November| 0.2333         |
| ... | ...                                   | ...   | ...     |        ...     |  --> 
