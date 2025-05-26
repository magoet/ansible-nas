---
title: "Tandoor Recipes"
---

Homepage: [https://tandoor.dev/](https://tandoor.dev/)

GitHub: [https://github.com/TandoorRecipes/recipes](https://github.com/TandoorRecipes/recipes)

Tandoor Recipe Manager is a self-hosted recipe manager that allows you to import, organize, and search your recipes, create meal plans, and build shopping lists.

## Usage

Set `tandoor_enabled: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

If you want to access Tandoor externally, set `tandoor_available_externally: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

The Tandoor web interface can be found at [http://ansible_nas_host_or_ip:9925](http://ansible_nas_host_or_ip:9925).

## Specific Configuration

For security, you should set the following variables in your `inventories/<your_inventory>/group_vars/nas.yml` file:

```yaml
tandoor_db_password: "your_secure_password_here"
tandoor_secret_key: "your_long_random_string_here"
```

On first access, you'll need to create an admin user through the web interface.
