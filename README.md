# HelperOrm


Запускает консольный клиент для подключения к базе данных.

Интерактивная консоль Python (также интерпретатор или оболочка Python) предоставляет программистам быстрый способ
выполнить команды и протестировать код, не создавая файл

ORM django основан на querySet
querySet – это набор обьектов из БД который может использоваться для ограничения результатов(т.е SELECT – то queryset, a
 filters это условие или же лимит – WHERE)
querySet – по сути список обьектов заданной модели, он позволяет читать данные из БД фильтровать и изменять их порядок и
 тд
Мы получаем queryset используя manager и по умолчанию он называется objects, обратится к нему можно через класс модели


from applications.product.models import Product

#Product.objects.all()
#SELECT * FROM products;

#Product.objects.get(id=1)
#SELECT * FROM products WHERE id = 1;

#Product.objects.filter(условие1, условие2)
Product.objects.filter(id=2, name='vlad')
#SELECT * FROM products WHERE условие AND условие2;

from django.db.models import Q
#Product.objects.filter(Q(условие)|Q(условие2))
#SELECT * FROM products WHERE условие1 OR условие2;

#Product.objects.filter(~Q(условие))
#Product.objects.exclude(условие)
#SELECT * FROM products WHERE NOT условие;

#Product.objects.filter(price__gt=50000) #больше
#SELECT * FROM products WHERE price > 50000;

#Product.objects.filter(price__lt=50000) #меньше
#SELECT * FROM products WHERE price < 50000;

#Product.objects.filter(price=50000) #равно
#SELECT * FROM products WHERE price = 50000;

#Product.objects.filter(~Q(price=50000))
#SELECT * FROM products WHERE NOT price = 50000;

#Product.objects.filter(price__gte=50000)
#SELECT * FROM products WHERE price >= 50000;

#Product.objects.filter(price__lte=50000)
#SELECT * FROM products WHERE price <= 50000;

#Product.objects.filter(category_id__in=['phones', 'notebooks'])
#SELECT * FROM product WHERE category_id IN ('phones', 'notebooks');

#Product.objects.filter(price__range=[20000, 50000])
#SELECT * FROM products WHERE price BETWEEN 20000 AND 50000;

Product.objects.filter(name__exact='Iphone')
#SELECT * FROM products WHERE name LIKE 'Iphone';
Product.objects.filter(name__iexact='Iphone')
#SELECT * FROM products WHERE name ILIKE 'Iphone';

Product.objects.filter(name__startswith='Iphone')
#SELECT * FROM products WHERE name LIKE 'Iphone%';
Product.objects.filter(name__istartswith='Iphone')
#SELECT * FROM products WHERE name ILIKE 'Iphone%';

Product.objects.filter(name__contains='Iphone')
#SELECT * FROM products WHERE name LIKE '%Iphone%';
Product.objects.filter(name__icontains='Iphone')
#SELECT * FROM products WHERE name ILIKE '%Iphone%';

Product.objects.filter(name__endswith='Iphone')
#SELECT * FROM products WHERE name LIKE '%Iphone';
Product.objects.filter(name__iendswith='Iphone')
#SELECT * FROM products WHERE name ILIKE '%Iphone';

Product.objects.order_by('price')
#SELECT * FROM products ORDER BY price ASC;

Product.objects.order_by('-price')
#SELECT * FROM products ORDER BY price DESC;

Product.objects.only('name')
#SELECT name FROM products;

Product.objects.only('name', 'price') # запрашивает указанные поля
#SELECT name, price FROM products;

Product.objects.defer('name', 'price') # исключает указанные поля
#SELECT id, description, category_id FROM products;

Product.objects.count()
#SELECT COUNT(*) FROM products;

Product.objects.filter(...).count()
#SELECT COUNT(*) FROM products WHERE ...;

Product.objects.create(name='Apple Iphone 12',
                       description='awddwdawd',
                       price=78000,
                       category_id='phones')
#INSERT INTO products (name, description, price, category_id) VALUES \
    # ('Apple Iphone 12', 'dwadaafafaw', 78000, 'phones');

Product.objects.bulk_create([
    Product(...),
    Product(...)
]) #множественное создание

Product.objects.update(price=50000)
#UPDATE products SET price=50000;

Product.objects.filter(...).update(price=50000)
#UPDATE products SET price=50000 WHERE ...;

Product.objects.filter(id=1).update(price=50000)
#UPDATE products SET price=50000 WHERE id=1;

product = Product.objects.get(id=1)
product.price = 50000
product.save()

#Product.objects.delete()
#DELETE FROM products;

#Product.objects.filter(category_id='phones').delete()
#DELETE FROM products WHERE category_id = 'phones';

#Product.objects.filter(id=1).delete()
#DELETE FROM products WHERE id=1;

#product = Product.objects.get(id=1)
#product.delete()

#Total number of books.
>>> Book.objects.count()
2452

#Total number of books with publisher=BaloneyPress
>>> Book.objects.filter(publisher__name='BaloneyPress').count()
73

#Average price across all books.
>>> from django.db.models import Avg
>>> Book.objects.all().aggregate(Avg('price'))
{'price__avg': 34.35}

#Max price across all books.
>>> from django.db.models import Max
>>> Book.objects.all().aggregate(Max('price'))
