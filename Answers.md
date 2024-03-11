## 1. Explain the relationship between the "Product" and "Product_Category" entities from the above diagram

ans -> The relationship between the "Product" and "Product_Category" entities is a ``Many-to-One`` relationship. 
This means that many products can belong to one product category, but each product can belong to only one category at a time.
This relationship is crucial for organizing products into hierarchical or logical groupings,
 making it easier to manage, browse, and analyze them.

 - ``Product Entity`` :- Contains a **category_id** attribute, which is a foreign key that references the **id** of a record in the
     **Product_Category** entity. This foreign key establishes the connection between a specific product and its category.

- ``Product_Category Entity`` :- Contains an **id** attribute, which serves as a unique identifier for each category. This **id** is
   referenced by the **category_id** in the **Product** entity.

## 2. How could you ensure that each product in the "Product" table has a valid category assigned to it?

  ans -> Ensuring that each product in the **Product** table has a valid category assigned to it involves a combination of database design 
  strategies and practices focused on maintaining data integrity and enforcing relational constraints. 
  
  Here are several ways to achieve this :-

  1. ``Use Foreign Key Constraints``
      When you define the **Product** table, make sure that the **category_id** column, which references the **id** of the **Product_Category** table,
      is enforced by a foreign key constraint.

     This constraint ensures that:

      - ``Referential Integrity`` - Every **category_id** in the **Product** table must match an existing **id** in the **Product_Category** table.
           It prevents the insertion of products with a category that doesn't exist.
        ```
        Example:
        ALTER TABLE Product
        ADD CONSTRAINT fk_product_category
        FOREIGN KEY (category_id) REFERENCES Product_Category(id);
        ```
2. ``Make the category_id Column Non-Nullable``
       By making the **category_id** column in the **Product** table non-nullable, you ensure that every product inserted into the database must
       have a category assigned. This is a simple yet effective way to enforce that there are no products without a valid category.

   ```
        Example:
          CREATE TABLE Product (
              id INT PRIMARY KEY,
              name VARCHAR(255) NOT NULL,
              desc TEXT,
              SKU VARCHAR(50),
              category_id INT NOT NULL,
              inventory_id INT,
              price DECIMAL(10, 2),
              discount_id INT,
              created_at TIMESTAMP,
              modified_at TIMESTAMP,
              deleted_at TIMESTAMP,
              FOREIGN KEY (category_id) REFERENCES Product_Category(id)
          );
   ```
4. ``Implement Application Logic``
    In addition to database-level constraints, ensure that your application logic checks for the existence of the
    category before allowing the creation or update of a product.
     - This can involve:
        Validating inputs when creating or updating products.

5. ``Regular Database Maintenance``
  Data Auditing: Regularly audit your database to check for orphaned records or inconsistencies, especially if you're importing data from external sources.
