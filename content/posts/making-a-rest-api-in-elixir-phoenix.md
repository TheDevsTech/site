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
```

Now that we have phoenix framwork installed on our project let's install the dependencies like:

```sh
mix deps.get
```

