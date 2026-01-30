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
- Local Scope(Business Logic):

```PHP
 public function scopeActive(Builder $builder){
        $builder->where('is_active',true);
    }

```

## ⛔ Restriction (User can't access admin dashboard):

Filament Link: ```https://filamentphp.com/docs/5.x/users/overview```

```PHP
class User extends Authenticatable implements FilamentUser
{
    // ...

        public function canAccessPanel(Panel $panel): bool
{
    $admins = [
        'admin@example.com',
        'dev@example.com',
    ];

    return in_array($this->email, $admins);
}
}

```
CMD to make an Admin:

```CMD
php artisan make:filament-user
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
- Links physical shipping and billing locations to specific customers.

```CMD
php artisan make:model Address -m
```

- 🗃️ Category:
- Organizes products into logical groups (like Electronics) for easy navigation.
  
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
- Manages manufacturer identities to allow filtering by label (like Nike or Samsung).

```CMD
php artisan make:model Brand -m  
```
- 📦 Product:
- Acts as the central hub for general item details, descriptions, and SEO data.

```CMD
php artisan make:model Product -m
```
- 🏷 ProductVariant:
- Tracks the specific "shoppable" versions of a product, like different sizes or colors.

```CMD
php artisan make:model ProductVariant -m
```
- product_variants table because customers don't buy "Products," they buy "Variants."
- The products table stores the general information (the story, the brand, the category).
- The product_variants table stores the physical specifics (size, color, material).

1. Product: "Nike Air Max" (1 entry)
2. Variants: "Size 10 Red," "Size 11 Red," "Size 10 Blue" (3 entries)

- 🖼️ ProductImage:
- Manages the visual gallery and links specific photos to specific product variants.

```CMD
php artisan make:model ProductImage -m  
```
- 🎟️ Coupon :
- Defines the rules and values for discounts and promotional offers.

```CMD
php artisan make:model Coupon -m  
```

- 🚚 Order:
- Captures the "snapshot" of a completed transaction, including total costs and shipping data.


```CMD
php artisan make:model Order -m 
```

- 📋 OrderItem:
- Records the exact price, quantity, and name of every specific item inside an order.


```CMD
php artisan make:model OrderItem -m
```
-The "Shopping Trip" Analogy
👉 Customer: The person who went shopping.
👉 Order: The Transaction (The swipe of the credit card, the date, the store location).
👉 OrderItems: The Bag of Groceries (The milk, the bread, the eggs).

- OrderStatusHistory:
- Creates a timeline of an order’s journey from "Pending" to "Delivered."

```CMD
php artisan make:model OrderStatusHistory -m
````
- CouponUsage:
- Provides an audit trail to prevent customers from reusing codes unfairly 

```CMD
php artisan make:model CouponUsage -m
```
- Review:
- Collects social proof and star ratings to build trust with future buyers.

```CMD
php artisan make:model Review -m   
```

- Setting:
- Provides a central control panel to manage site-wide info without touching code.

```CMD
php artisan make:model Setting -m
```

## 🔗 Model Relationships

🧑 Customer & Address
- A **Customer** has many **Addresses**
- An **Address** belongs to a **Customer**

**Relationship Type:** One-to-Many



 🗂️ Category & Product
- A **Category** has many **Products**
- A **Product** belongs to a **Category**

**Relationship Type:** One-to-Many



🏷️ Brand & Product
- A **Brand** has many **Products**
- A **Product** belongs to a **Brand**

**Relationship Type:** One-to-Many


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

🚚 Customer & Order
- A **Customer** has many **Orders**
- A **Order** belongs to a **Customer**

**Relationship Type:** One-to-Many

🚚 Coupon & Order
- A **Order** has many **Coupons**
- A **Coupon** belongs to a **Order**

**Relationship Type:** One-to-Many

📋  OrderItem & Product
- A **Product** has many **OrderItems**
- A **OrderItem** belongs to a **Product**

**Relationship Type:** One-to-Many


📋  OrderItem & Order
- A **Order** has many **OrderItems**
- A **OrderItem** belongs to a **Order**

**Relationship Type:** One-to-Many


📋  OrderItem & ProductVariant
- A **ProductVariant** has many **OrderItems**
- A **OrderItem** belongs to a **ProductVariant**

**Relationship Type:** One-to-Many

- .env settings:

```Plaintext
APP_NAME='Ecommerce'
FILESYSTEM_DISK=public
```  

### Filament:
<hr>

Installing Filament 4.0
Linkd: ```https://filamentphp.com/docs/4.x/introduction/installation```

```CMD
composer require filament/filament:"^5.0"

php artisan filament:install --panels

```
- This will create and register a new Laravel service provider called app/Providers/Filament/AdminPanelProvider.php.

Link: ```https://filamentphp.com/plugins/bezhansalleh-shield```



















































