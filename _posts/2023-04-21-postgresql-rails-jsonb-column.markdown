---
layout: post
title:  Postgresql how to create new field in existing jsonb column
description:
date:   2023-04-21 00:31:46.882708 -0500
author: sdemian
image:  '/images/2023-04-21-postgresql-rails-jsonb-column.png'
tags:   [rails, postgresql, jsonb, database]
tags_color: '#477690'
featured: true
---
## How to create new field in existing jsonb column using Rails migration and Active Record

Here is an example of how to add a new field called **status_number** with a value of **new_value** to a JSONB column called **data** in a table called **services**

```sql
UPDATE services
SET data = jsonb_set(data, '{status_number}', '"new value"')
WHERE id = 1;
```

> To create a new field in an existing JSONB column in <span class="code">PostgreSQL</span> use the <span class="code">jsonb_set</span> function. The jsonb_set function allows you to modify a JSONB object by specifying a path to the field you want to modify with new value

In this example, the <span class="code">jsonb_set</span> function takes three arguments:

- **JSONB object to modify**
- **path to the new field**
- **new value**


## How to create new field in existing jsonb column with the value from another jsonb field for all the records in the table

Add new field **status_number** to a JSONB column called **data** in a table called **services**, where the value for **status_number** is taken from an existing field called **account_number**

```sql
UPDATE services
SET data = jsonb_set(data, '{status_number}', data->'account_number')
WHERE id = 1;
```

To apply this update to all the records in the table, simply remove the WHERE clause. The resulting query would look like this:

```sql
UPDATE services
SET data = jsonb_set(data, '{status_number}', data->'account_number')
```

## How to remove field in existing jsonb column for all the records in the table

To remove a field from an existing JSONB column for all the records in a table use <span class="code">JSONB Operators</span> from [Postgresql Documentation](https://www.postgresql.org/docs/9.5/functions-json.html)

![Postgresql jsonb Operators]({{site.baseurl}}/images/2023-04-21-postgresql-rails-jsonb-column-operators.png)

Remove a field called **status_number** from a JSONB column called **data** in a table called **services**

```sql
UPDATE services
SET data = data - 'status_number'
WHERE id = 1;
```

## Use Rails to do database manipulations with JSONB columns

Create a Rails DB migration:

```bash
bin/rails g migration update_services_data_account_number
```

Write **up** and **down** methods for Rails database migration:

```bash
class UpdateServicesDataAccountNumber < ActiveRecord::Migration[6.1]
  def up
    sql = <<-SQL.squish
      UPDATE services
      SET data = jsonb_set(data, '{status_number}', data->'account_number')
      ;
    SQL
    execute(sql)
  end

  def down
    sql = <<-SQL.squish
      UPDATE services
      SET data = data - 'status_number'
      ;
    SQL
    execute(sql)
  end
end
```

Run Rails DB migration for `development` environment

```bash
bin/rails db:migrate
```

Run Rails DB migration for `test` environment

```bash
RAILS_ENV=test bin/rails db:migrate
```

Now new **status_number** field in JSONB column **data** is present with value from **account_number**

This is all for today.

Congratulations 🏆 on learning about <span class="code">Postgresql jsonb column</span> and use of Rails migrations.
