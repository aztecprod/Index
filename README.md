# Индексы - Александр Шевцов
![image](https://github.com/aztecprod/Index/assets/25949605/b8de9c0a-c79f-4a76-99f8-b76320d8059d)
![image](https://github.com/aztecprod/Index/assets/25949605/8babeb59-9590-4ea7-96ff-9d4e65f1c59a)
![image](https://github.com/aztecprod/Index/assets/25949605/eece72a4-f882-4c98-82fd-b8971c73d4c4)
![image](https://github.com/aztecprod/Index/assets/25949605/d3784799-217f-488a-a8e3-ece99f74516d)
До оптимизации:
![image](https://github.com/aztecprod/Index/assets/25949605/94cc7f2c-fa2b-4ba5-87a9-983f7a22896a)

Можно убрать из Select “over (partition by c.customer_id, f.title)”, ”distinct”.

Из “from” можно удалить все, кроме Customer ,

Добавить два INNER JOIN

Добавить группировку по имени.

![image](https://github.com/aztecprod/Index/assets/25949605/7b95f29d-3c92-41b6-965f-cc6f613ee739)

После оптимизации:

![image](https://github.com/aztecprod/Index/assets/25949605/0d52b2d3-65cb-44f5-8ccc-0d49c5d30f20)

После создания индекса:

'''
> Table scan on <temporary>  (actual time=3.69..3.73 rows=391 loops=1)\n  
  -> Aggregate using temporary table  (actual time=3.69..3.69 rows=391 loops=1)\n
  -> Nested loop inner join  (cost=571 rows=634) (actual time=0.0332..2.99 rows=642 loops=1)\n 
  -> Nested loop inner join  (cost=349 rows=634) (actual time=0.0231..1.19 rows=634 loops=1)\n 
  -> Filter: ((r.rental_date >= TIMESTAMP\'2005-07-30 00:00:00\') and (r.rental_date < <cache>((\'2005-07-30\' + interval 1 day))))  (cost=127 rows=634) (actual time=0.0155..0.387 rows=634 loops=1)\n
  -> Covering index range scan on r using rental_date over (\'2005-07-30 00:00:00\' <= rental_date < \'2005-07-31 00:00:00\')  (cost=127 rows=634) (actual time=0.0138..0.274 rows=634 loops=1)\n
  -> Single-row index lookup on c using PRIMARY (customer_id=r.customer_id)  (cost=0.25 rows=1) (actual time=0.00112..0.00114 rows=1 loops=634)\n
  -> Index lookup on p using data_payment_id (payment_date=r.rental_date)  (cost=0.25 rows=1) (actual time=0.00217..0.00269 rows=1.01 loops=634)\n'

'''

