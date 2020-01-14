---
title: "Making a REST API in Elixir Phoenix"
date: 2020-01-14T14:10:00+06:00
draft: true
authors:
- Mazhar Ahmed
tags:
- functional
- elixir
- phoenix
- rest
- api
---

Elixir is built on top of Erlang but it is quite friendly / high level than Erlang. Working with Elixir provides all the facilities of Erlang. You guys probably already know that "Elixir is a dynamic functional language which runs on Erlang BEAM virtual machine". Phoenix is a web framework for Elixir, similar with Rails (Ruby Web Framework). Today we will see how we can make a REST API in Phoenix framwork. For time limitation, today we will only see how to write LIST API (which will return a list of items) with it.

At first we need to install Elixir 1.5 or later properly. After that we can use `mix` to install packages for elixir. Let's install Phoenix Framwork from its archive and create a new project like:

```sh
mix archive.install hex phx_new 1.4.11
mix phx.new devstech
```

Now that we have phoenix framwork installed on our project named **devstech** (keep this in mind as the directory structure will be generated according to this). We could use `--no-brunch --no-html` option with `phx.new` command to remove the support of traditional HTML rendering in our app. Let's just keep it, it's not a big deal for this project. let's install the dependencies like:

```sh
mix deps.get
```

Now run `mix phx.server` and see if you can see the site in browser **http://localhost:4000**

If you see an error about plug_cowboy, add the package to mix.exs:

```ex
defp deps do 
[
  ... 
  {:cowboy, "~> 1.0"},
  {:plug_cowboy, “~> 1.0”}
]
end
```

Run mix deps.get to install the package and then start the server again. Now let's update the database configuration in `/config/dev/exs`. Phoenix now supports MySQL and PostgreSQL. Let's run migrations to make the database:

```sh
mix ecto.migrate
# or to just create the database
mix ecto.create
```

Now let's create a model named user. To generate the model, we can take help from the **phx**. Let's run:

```sh
mix phoenix.gen.model User users name:string password:string age:integer
```

*You can see this [ref](https://hexdocs.pm/phoenix/Mix.Tasks.Phoenix.Gen.Model.html) to learn more about `phx.gen.model`. This command will generate model, repository and migration for you.*

Most of our source code actually kept under `/lib` folder. We can find the repository in `/lib/devstech/user.ex`, model in `/lib/devstech_web/models/user.ex` and the migration in `/priv/repo/migrations/****_create_user.exs`. If you don't want to generate the model you can manually create those files too (just be careful about the module names).

Let's run `mix ecto.migrate` to create the newly created table on the database. Now our table is empty, let's create some data as development purpose. Let's edit the `/priv/repo/seed.exs` and add the following lines:

```ex
alias Devstech.{Repo, User}

Repo.insert! %User{
    name: "John Doe",
    password: "123456",
    age: 53
}

# you can add more entries
```

Now run `mix run priv/repo/seeds.exs` to insert the seed data. Okay, now that we have database, tables, data and everything is properly mapped to our ORM, we will create a route and controller to make a list API. Under `/lib/devstech_web/controllers` let's create a file named `user_controller.ex` with following:

```ex
defmodule DevstechWeb.UserController do
    use DevstechWeb, :controller
    alias Devstech.{Repo, Core.User}
    
    def index(conn, _params) do
        users = Repo.all(User)
        json conn, users
    end
end
```

Now let's map this controller with a URL. Let's modify the file `/lib/devstech_web/router.ex` and add `get "/user", UserController, :index` in the `/api` scope at the bottom like:

```ex
  # Other scopes may use custom stacks.
  scope "/api", DevstechWeb do
    pipe_through :api
    # this line bellow is added
    get "/user", UserController, :index
  end
```

Now let's run the server and hit **http://localhost:4000/api/user**. Surely it will show an error saying it can not convert ecto entity to json. Let's make a new file at `/lib` named `jason_encoder.ex` with following:

```ex
alias Devstech.Core.User

# lib/jason_encoder.ex
defimpl Jason.Encoder, for: User do
    def encode(%{__struct__: _} = struct, options) do
        map = struct
            |> Map.from_struct
            |> sanitize_map
        Jason.Encoder.Map.encode(map, options)
    end

    defp sanitize_map(map) do
        # remove some fields
        Map.drop(map, [:__meta__, :__struct__, :password])
    end
end

```

Now restart the server and hit the browser URL. TADA..., you will see the data from database table as JSON list.

This is a basic REST API in Phoenix. There are a lots of things to do like Authentication, JWT, Pagination etc. You can get the source used in this article from [here in GitHub](https://github.com/mazhar266/Phoenix-API).

Thank you.
