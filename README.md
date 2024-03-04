       1.Retrieve Product Information:
    C. )
SELECT name, description
FROM products;
    D. )
SELECT name, description,
       JSON_EXTRACT(attributes, '$.color') AS color,
       JSON_EXTRACT(attributes, '$.size') AS size,
       JSON_EXTRACT(attributes, '$.price') AS price,
JSON_EXTRACT(attributes, '$.brand) AS brand
FROM products;SELECT
    o.order_id,
    o.order_date,
    o.customer_id,
    p.name AS product_name,
    od.quantity,
    od.price
FROM
    orders o JOIN
    order_details od ON o.order_id = od.order_id
JOIN products p ON od.product_id = p.product_id;

       2.Query Orders and Order Details:
    C.  )
SELECT
    o.order_id,
    o.order_date,
    o.customer_id,
    p.name AS product_name,
    od.quantity,
    od.price
FROM
    orders o JOIN
    order_details od ON o.order_id = od.order_id
JOIN products p ON od.product_id = p.product_id;

    D.  )
SELECT
    o.order_id,
    SUM(od.quantity * od.price) AS total_cost
FROM
    orders o
JOIN
    order_details od ON o.order_id = od.order_id
GROUP BY
    o.order_id;

       3.Filtering Products Based on Attributes:
    C.  )
SELECT *
FROM products
WHERE JSON_EXTRACT(attributes, '$.price') > 50;

    D.  )
SELECT name, JSON_EXTRACT(attributes, '$.price') AS price
FROM products
WHERE JSON_EXTRACT(attributes, '$.color') = 'silver'
AND JSON_EXTRACT(attributes, '$.brandName') = 'Walker LLC ';


       4.Calculating Aggregate Data:
    C.  )
SELECT 
    p.product_id,
    p.name AS product_name,
    SUM(od.quantity * od.price) AS total_revenue
FROM 
    products p
JOIN 
    order_details od ON p.product_id = od.product_id
GROUP BY 
    p.product_id, p.name;

    D.  )
SELECT 
    p.product_id,
    p.name AS product_name,
    SUM(od.quantity) AS total_quantity
FROM 
    products p
JOIN 
    order_details od ON p.product_id = od.product_id
GROUP BY 
    p.product_id, p.name;


       5.Advanced Filtering and Aggregation: 
    C.  )
SELECT
    p.product_id,
    p.name AS product_name,
    SUM(od.quantity) AS total_quantity_sold
FROM
    products p
JOIN
    order_details od ON p.product_id = od.product_id
GROUP BY
    p.product_id, p.name
ORDER BY
    total_quantity_sold DESC Limit 5;

    D.  )
SELECT
    AVG(JSON_EXTRACT(attributes, '$.price')) AS average_price,
    JSON_EXTRACT(attributes, '$.brandName') AS brand
FROM
    products
WHERE
    JSON_EXTRACT(attributes, '$.brandName') = 'Your_Brand_Name'
GROUP BY
    JSON_EXTRACT(attributes, '$.brandName');

       6.Nested JSON Queries: 
    C.  )
SELECT
    JSON_EXTRACT(attributes, '$.color') AS color,
    JSON_EXTRACT(attributes, '$.size') AS size
FROM
    products
WHERE
    product_id = 1234;

    D.  )
SELECT JSON_OBJECT(
    'product_id', product_id,
    'name', name,
    'descriSELECT * FROM `products`ption', description,
    'attributes', attributes
) AS product_info
FROM products;

       7.Data Joining Multiple Tables: 
    C.  )
SELECT 
    o.order_id,
    o.order_date,
    c.customer_id,
    p.name AS product_name,
    od.quantity
FROM 
    orders o
JOIN 
    order_details od ON o.order_id = od.order_id
JOIN 
    products p ON od.product_id = p.product_id
JOIN 
    customers c ON o.customer_id = c.customer_id;

    D.  )
SELECT
    CONCAT(c.firstname, ' ', COALESCE(c.middlename, ''), ' ', c.lastname) AS full_name,
    c.customer_id,
    SUM(od.quantity * JSON_EXTRACT(p.attributes, '$.price')) AS total_revenue
FROM
    customers c
JOIN
    orders o ON c.customer_id = o.customer_id
JOIN
    order_details od ON o.order_id = od.order_id
JOIN
    products p ON od.product_id = p.product_id
GROUP BY
    c.customer_id, full_name;

       8.Data Manipulation with JSON Functions: 
    A.  )
	1.
SELECT * FROM products WHERE product_id = 1234;

	2.
UPDATE products
SET attributes = JSON_SET(attributes, '$.price', 800.00)
WHERE product_id = 1234;

	3.
SELECT * FROM products WHERE product_id = 1234;

    B.  )
	1.
ALTER TABLE products ADD COLUMN weight VARCHAR(255) DEFAULT 'default_value';

	2.
SELECT name, description,
       JSON_EXTRACT(attributes, '$.color') AS color,
       JSON_EXTRACT(attributes, '$.size') AS size,
       JSON_EXTRACT(attributes, '$.price') AS price,
 JSON_EXTRACT(attributes, '$.brandName') AS brand,
       JSON_EXTRACT(attributes, '$.weight') AS weight
FROM products;



       9.Advanced JSON Operations: 
    A.  )
SELECT *
FROM products
WHERE JSON_EXTRACT(attributes, '$.color') = 'blue'
  AND JSON_EXTRACT(attributes, '$.size') = 'medium';

    B.  )
SELECT JSON_EXTRACT(attributes, '$.features[0]') AS first_feature
FROM products;
