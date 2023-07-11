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
В создании дополнительных индексов необходимости не увидел.
