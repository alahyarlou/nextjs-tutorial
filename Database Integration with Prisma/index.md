## Database Engines

in this section we're going to use `MySQL` for storing our data.\
in case you don't know, MySQL is very populer databse engine. There of course many ohter databse engines out there like:

- MySQL
- Postgres
- SQL Server
- MongoDB

If you prefer a diffrent databse engine, that's totally fine, but I would sugges you to use MySQL in this section, so you can easily follow the lessons.

so head over to:

1. [MySQL](https://www.mysql.com)
2. Go to Downloads Tab
3. bottom of the page find the link `MySQL Community(GPL) Downloads`
4. Go to MySQL Community Server
5. Download latest version for operating system.
6. install it

---

Then we also need for viewing oure databse.Now MySql gives you a tool called `MySQL Workbench` again it's free. I don't like this tool 🥲.

So I'll be using tool called `DataGrid` from (`https://www.jetbrains.com`)

## Setting Up Prisma

Now we're going to install Prisma which is a very popular ORM or object relational mapper.

We use ORMs to work with our databases. So an `ORM` is like a tool that sits between our application and a database.

We use this ORM to send queries to our database and get data back or use it to `create`, `update`, or `delete` data.

It's very simple.

Now, in this course we're just going to scratch the surface of Prisma, there's so much more about Prisma that goes beyond the scope of this course, because our focus here is on Next .js and not Prisma.

---

Next, we're going to go in the terminal, and install Prisma.

```js
npm install prisma
```

Prisma comes with a command line interface that we can work with using npx.

#### Prisma Command:

```bash
prisma [command]

init            Set up prisma for your app
generate        Generate artifacts(e.g. Prisma Client)
db              Manage your databse schema and lifecycle
migrate         Migrate your databse
studio          Browse your data with Prisma Studio
validate        Validate your Prisma schema
format          Format your Prisma schema

```

---

So set up prisma

```bash
npx prisma init
```

In our project, it creates a Prisma folder and puts a schema file in this folder.

It also creates an environment file where we store our environment variables, in this case, a database url.

by default, Prisma uses `Postgres`, but we're going to use `MySQL`, there are other database engines that are
available, so we're going to change this connection url or connection string to something that is compatible with `MySQL`.

---

we going to website prisma.io [Prisma doc](https://www.prisma.io/docs/orm/reference/connection-urls)

### Connection URL

Here's an overview of the components needed for a MySQL connection URL:

![Structure of the MySQL connection URL](https://www.prisma.io/docs/static/a3179ecce1bf20faddeb7f8c02fb2251/42cbc/mysql-connection-string.png)

```bash
DATABSE_URL="mysql://root:MyP@ssw0rd@localhost:3306/nextapp"
```

---

Now Go to `prisma/schema.prisma` and change that:

```js
generator client{
    provider="prisma-client-js"
}

datasource db{
    provider = "mysql"
    url=env("DATABSE_URL")
}
```
