# SQL_ODEV_12
--1.Query film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?
SELECT COUNT(*) FROM film
WHERE length > (
	SELECT AVG(length) FROM film
);
--2.Query film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır?
SELECT COUNT(*) FROM film
WHERE rental_rate = (
	SELECT MAX(rental_rate) FROM film
);
--3.Query film tablosunda en düşük rental_rate ve en düşük replacement_cost değerlerine sahip filmleri sıralayınız.
SELECT * FROM film
WHERE rental_rate =
(
	SELECT MIN(rental_rate) FROM film
) AND replacement_cost = 
(
	SELECT MIN(replacement_cost) FROM film
);

--4.Query payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.
SELECT customer.first_name, customer.last_name, COUNT(payment.customer_id) AS en_fazla_sayıda_alısveriş FROM payment
INNER JOIN customer ON customer.customer_id = payment.customer_id
GROUP BY payment.customer_id,customer.first_name,customer.last_name
ORDER BY en_fazla_sayıda_alısveriş DESC;
