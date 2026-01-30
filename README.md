<h2 align='center'> ⚡Laravel Ecommerce(TALL)</h2>


### Model, Migrations Creating & Editing :
<hr>


- 👥 Adding a new column to the user table:

```CMD
 php artisan make:migration add_phone_status_column_to_users_table --table=users
```

User.php:

```PHP
 return [
            'email_verified_at' => 'datetime',
            'password' => 'hashed',
            'is_active'=>'boolean',
        ];

```

⚠️If you leave it empty, and you rollback, those columns will stay in your database, which can lead to "Column already exists" errors if you try to migrate again.

```PHP
    public function down(): void
    {
        Schema::table('users', function (Blueprint $table) {
            // You drop the columns in the reverse order you created them
            $table->dropColumn(['phone', 'is_active']);
        });
    }

```

- 🙋🏻‍♂️ Customer :

```CMD
php artisan make:model Customer -m
```

```PlainText
$table->rememberToken(); //The Purpose: It supports the "Remember Me" checkbox on your login form.
$table->softDeletes(); //The Purpose: It allows for "Safe Deletion." Instead of permanently wiping a
                            customer from your database, Laravel sets a date in the deleted_at column.
```


- 🗺️ Address:

```CMD
php artisan make:model Address -m
```

- 🗃️ Category:
  
```CMD
php artisan make:model Category -m
```

using index in column:

```Plaintext

| Without Index (Slow)         | With Index (Fast) |
|---------------------         |------------------|
| Database searches row-by-row | Uses Binary Search / B-Tree |
| Checks 1 million rows        | Finds result in ~20 steps |
| High CPU usage               | Low CPU usage, very fast |

```

- ®️™ Brand:

```CMD
php artisan make:model Brand -m  
```
- 📦 Product

```CMD
php artisan make:model Product -m
```
- 🏷 ProductVariant

```CMD
php artisan make:model ProductVariant -m
```
- product_variants table because customers don't buy "Products," they buy "Variants."
- The products table stores the general information (the story, the brand, the category).
- The product_variants table stores the physical specifics (size, color, material).

1. Product: "Nike Air Max" (1 entry)
2. Variants: "Size 10 Red," "Size 11 Red," "Size 10 Blue" (3 entries)

- 🖼️ ProductImage:

```CMD
php artisan make:model ProductImage -m  
```
-🎟️ Coupon :

```CMD
php artisan make:model Coupon -m  
```

-🚚 Order:

```CMD
php artisan make:model Order -m 
```





## 🔗 Model Relationships

🧑 Customer & Address
- A **Customer** has many **Addresses**
- An **Address** belongs to a **Customer**

**Relationship Type:** One-to-Many

---

 🗂️ Category & Product
- A **Category** has many **Products**
- A **Product** belongs to a **Category**

**Relationship Type:** One-to-Many

---

🏷️ Brand & Product
- A **Brand** has many **Products**
- A **Product** belongs to a **Brand**

**Relationship Type:** One-to-Many
---

🏷️ Product & ProductVariant
- A **Product** has many **ProductVariants**
- A **ProductVariant** belongs to a **Product**

**Relationship Type:** One-to-Many


🏷️ Product & ProductImage
- A **Product** has many **ProductImages**
- A **ProductImage** belongs to a **Product**

**Relationship Type:** One-to-Many

🏷️ ProductVariant & ProductImage
- A **ProductVariant** has many **ProductImages**
- A **ProductImage** belongs to a **ProductVariant**

**Relationship Type:** One-to-Many

🚚 Product & Order
- A **Order** has many **Products**
- A **Product** belongs to a **Order**

**Relationship Type:** One-to-Many

🚚 Customer & Order
- A **Customer** has many **Orders**
- A **Order** belongs to a **Customer**

**Relationship Type:** One-to-Many

🚚 Coupon & Order
- A **Order** has many **Coupons**
- A **Coupon** belongs to a **Order**

**Relationship Type:** One-to-Many



  



















































