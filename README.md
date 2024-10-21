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

<h1>Product.objects.all()</h1>
<p>SELECT * FROM products;</p>

<h1>Product.objects.get(id=1)</h1>
<p>SELECT * FROM products WHERE id = 1;</p>

<h1>Product.objects.filter(id=2, name='vlad')</h1>
<p>SELECT * FROM products WHERE id = 2 AND name = 'vlad';</p>

<h1>from django.db.models import Q<br>
Product.objects.filter(Q(id=2) | Q(name='vlad'))</h1>
<p>SELECT * FROM products WHERE id = 2 OR name = 'vlad';</p>

<h1>Product.objects.filter(~Q(id=2))</h1>
<p>SELECT * FROM products WHERE NOT id = 2;</p>

<h1>Product.objects.exclude(id=2)</h1>
<p>SELECT * FROM products WHERE id != 2;</p>

<h1>Product.objects.filter(price__gt=50000)</h1>
<p>SELECT * FROM products WHERE price > 50000;</p>

<h1>Product.objects.filter(price__lt=50000)</h1>
<p>SELECT * FROM products WHERE price < 50000;</p>

<h1>Product.objects.filter(price=50000)</h1>
<p>SELECT * FROM products WHERE price = 50000;</p>

<h1>Product.objects.filter(~Q(price=50000))</h1>
<p>SELECT * FROM products WHERE NOT price = 50000;</p>

<h1>Product.objects.filter(price__gte=50000)</h1>
<p>SELECT * FROM products WHERE price >= 50000;</p>

<h1>Product.objects.filter(price__lte=50000)</h1>
<p>SELECT * FROM products WHERE price <= 50000;</p>

<h1>Product.objects.filter(category_id__in=['phones', 'notebooks'])</h1>
<p>SELECT * FROM products WHERE category_id IN ('phones', 'notebooks');</p>

<h1>Product.objects.filter(price__range=[20000, 50000])</h1>
<p>SELECT * FROM products WHERE price BETWEEN 20000 AND 50000;</p>

<h1>Product.objects.filter(name__exact='Iphone')</h1>
<p>SELECT * FROM products WHERE name LIKE 'Iphone';</p>

<h1>Product.objects.filter(name__iexact='Iphone')</h1>
<p>SELECT * FROM products WHERE name ILIKE 'Iphone';</p>

<h1>Product.objects.filter(name__startswith='Iphone')</h1>
<p>SELECT * FROM products WHERE name LIKE 'Iphone%';</p>

<h1>Product.objects.filter(name__istartswith='Iphone')</h1>
<p>SELECT * FROM products WHERE name ILIKE 'Iphone%';</p>

<h1>Product.objects.filter(name__contains='Iphone')</h1>
<p>SELECT * FROM products WHERE name LIKE '%Iphone%';</p>

<h1>Product.objects.filter(name__icontains='Iphone')</h1>
<p>SELECT * FROM products WHERE name ILIKE '%Iphone%';</p>

<h1>Product.objects.filter(name__endswith='Iphone')</h1>
<p>SELECT * FROM products WHERE name LIKE '%Iphone';</p>

<h1>Product.objects.filter(name__iendswith='Iphone')</h1>
<p>SELECT * FROM products WHERE name ILIKE '%Iphone';</p>

<h1>Product.objects.order_by('price')</h1>
<p>SELECT * FROM products ORDER BY price ASC;</p>

<h1>Product.objects.order_by('-price')</h1>
<p>SELECT * FROM products ORDER BY price DESC;</p>

<h1>Product.objects.only('name')</h1>
<p>SELECT name FROM products;</p>

<h1>Product.objects.only('name', 'price')</h1>
<p>SELECT name, price FROM products;</p>

<h1>Product.objects.defer('name', 'price')</h1>
<p>SELECT id, description, category_id FROM products;</p>

<h1>Product.objects.count()</h1>
<p>SELECT COUNT(*) FROM products;</p>

<h1>Product.objects.filter(category_id='phones').count()</h1>
<p>SELECT COUNT(*) FROM products WHERE category_id = 'phones';</p>

<h1>Product.objects.create(name='Apple Iphone 12', description='awd', price=78000, category_id='phones')</h1>
<p>INSERT INTO products (name, description, price, category_id) VALUES ('Apple Iphone 12', 'awd', 78000, 'phones');</p>

<h1>Product.objects.bulk_create([Product(...), Product(...)])</h1>
<p>INSERT INTO products (...) VALUES (...), (...);</p>

<h1>Product.objects.update(price=50000)</h1>
<p>UPDATE products SET price = 50000;</p>

<h1>Product.objects.filter(id=1).update(price=50000)</h1>
<p>UPDATE products SET price = 50000 WHERE id = 1;</p>

<h1>product = Product.objects.get(id=1)<br>product.price = 50000<br>product.save()</h1>
<p>UPDATE products SET price = 50000 WHERE id = 1;</p>

<h1>Product.objects.filter(category_id='phones').delete()</h1>
<p>DELETE FROM products WHERE category_id = 'phones';</p>

<h1>product = Product.objects.get(id=1)<br>product.delete()</h1>
<p>DELETE FROM products WHERE id = 1;</p>

<h1>from django.db.models import Avg<br>Book.objects.all().aggregate(Avg('price'))</h1>
<p>SELECT AVG(price) FROM books;</p>

<h1>from django.db.models import Max<br>Book.objects.all().aggregate(Max('price'))</h1>
<p>SELECT MAX(price) FROM books;</p>
