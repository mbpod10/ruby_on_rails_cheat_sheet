# Build New Rails API APP

```
rails new project_name --api -d postgresql --skip-git
```

# CHANGE DIRECTORIES INTO PROJECT NAME

```
cd project_name
```

# CREATE DATABASE NAMED BY YOUR PROJECT NAME

```
rails db:create
```

# CHECK THAT DB WAS CREATED (Start psql shell) Quit

```
rails dbconsole
\l
\q
```

# CREATE NEW TABLE

```
rails generate migration CreateUsers
```

-Look into db/migrate there should be a new migration.rb file
-Make necessary changes to migration to create new table schema
-MAKE SURE [6.0] IS AT THE END OF THE FIRST LINE

```
class CreateUsers < ActiveRecord::Migration[6.0]
    def change
        create_table :todos do |t|
            t.string :name
            t.boolean :member
            t.integer :age
        end
    end
end
```

# RUN MIGRATION, SCHEMA WILL APPEAR IN DB FOLDER

```
rails db:migrate
```

# CHECK DATABASE VIA PSQL SHELL (Empty database with columns should appear)

```
rails dbconsole
SELECT * FROM users;
```

# CREATE MODELS

MAKE FILE CALLED user.rb IN app/models
HAVE USER INHERIT APPLICATION RECORD IN NEW user.rb FILE

```
class User < ApplicationRecord
end
```

All this does for now is wire up our app so that we use Active Record on our User model to interface with our database.

# OPEN ACTIVE RECORD SHELL

```
rails console
rails c
```

# Query Active Record

```
User.all
User.count
```

# CREATE NEW USER VIA ACTIVE RECORD SHELL

```
User.create(name: "Hillman Mansion", member: true, age: 55)
```

-VERIFY CREATE WORKED FROM ACTIVE RECORD

```
User.all
```

-VERIFY CREATE WORKED VIA PSQL SHELL

```
SELECT * FROM users;
```

-MORE ACTIVE RECORD QUERIES (FIND)

```
User.find(1) //find by id of 1
User.where(name: "Hillman Mansion") //find by name
User.where(age: 55) //find by age
User.where(member: true) //find by member (t/f)
```

-UPDATE VIA ACTIVE RECORD QUERIES

```
User.update(1, :name => "Kcorb Reise") //find by id then change name
User.update(name: "Kcorb Reise", :age => 45) //find by name then change age
User.update(age: 45, :member => false) //find by age and update member
User.update(1, :id => 71) //find by id and change id
```

-VERIFY CHANGES VIA PSQL AND ACTIVE RECORDS

```
User.all //active records
SELECT * FROM users //psql
```
