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
  







