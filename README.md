select * from books;

select * from customers;

select * from orders;

-- 1) Retrieve all books from the in the fiction "genre":

select * from books
where genre='Fiction';

-- 2) Find books published after the year 1950:

select title,published_year from books
where published_year>1950;

-- 3) List all customers from the canada:

select name, country from customers
where country='Canada';

--4) Show orders placed in November 2023:

select * from orders 
where order_date between '2023-11-01' and '2023-11-30';

--5) Retrieve the total stock of books available:

select * from books;

select sum(stock) from books;

-- 6) Find the details of the most expensive book:

select * from books order by price desc limit 1;

--7) Show all customers who ordered more than 1 quantity of a book:

select  c.name, o.quantity from customers c
join 
orders o on c.customer_id = o.customer_id
where quantity > 1;

--8) List all genres available in the Books table:

select distinct(genre) from books;

--9) Find the book with the lowest stock:

select title,stock from books
order by stock ASC limit 20;

--10) Calculate the total revenue generated from all orders:

select sum(total_amount) as total_revenue
from orders;

-- 11) Retrieve the total number of books sold for each genre:

select b.genre,sum(o.quantity)
from books b 
join orders o on b.book_id=o.order_id
group by b.genre;

-- 12) Find the average price of books in the "Fantasy" genre

select avg(price) from books
where genre='Fantasy';

--13) List customers who have placed at least 2 orders:

select c.name,count(o.order_id) as order_count
from customers c 
join orders o on c.customer_id=o.customer_id
group by o.customer_id,c.name 
having count(order_id)>=2;

--14) Find the most frequently ordered book:

select o.book_id,b.title,count(o.order_id) as order_count
from orders o
join books b on o.book_id=b.book_id
group by o.book_id,b.title
order by order_count desc limit 1;

-- 15) Show the top 3 most expensive books of 'Fantasy' Genre:

select title, price
from books
where genre='Fantasy'
order by price desc limit 3;

-- 16) ) Retrieve the total quantity of books sold by each author:

select b.author, sum(o.quantity) as total_quantity
from books b
join orders o on b.book_id=o.book_id
group by b.author;

-- 17) List the cities where customers who spent over $30 are located:

select distinct(c.name), c.city,o.total_amount
from customers c 
join orders o on c.customer_id=o.customer_id
where total_amount>240;

--18) Find the customer who spent the most on orders:

select c.name, sum(o.total_amount) as total_amount
from customers c 
join orders o on c.customer_id=o.customer_id
group by c.name
order by total_amount desc; 
