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
<table>
  <tr>
    <th>Without Index (Slow)  </th>
    <th>With Index (Fast)</th>
  </tr>
  <tr>
    
    <td>Database searches row-by-row.s</td>
    <td>Database uses a "Binary Search" or "B-Tree.</td>
  </tr>
  <tr>
    <td>If you have 1 million users, it checks 1 million rows.</td>
    <td>If you have 1 million users, it finds the result in about 20 steps.</td>
  </tr>
  <tr>
    <td>High CPU usage.</td>
    <td>Low CPU usage, very high speed.</td>
  </tr>
</table>
```























































