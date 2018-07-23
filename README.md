# sequelize-auto-migrations
Migration generator &amp; runner for sequelize

This package provide two tools:
* `generate-migration` - tool for create new migrations
* `run-migration` - tool for apply created by first tool migrations

## Install
`npm install @bakjs/sequelize-auto-migrations`

## Usage
* Init sequelize, with sequelize-cli, using `sequelize init`
* Create your models
* Create initial migration - run:

`./node_modules/.bin/generate-migration --name <migration name>`
* Change models and run it again, model difference will be saved to the next migration

To preview new migration, without any changes, you can run:

`./node_modules/.bin/generate-migration --preview`

`generate-migration` tool creates `_current.json` file in `migrations` dir, that is used to calculate difference to the next migration. Do not remove it!

To create and then execute migration, use:
`generate-migration --name <name> -x`

### Options

* `--preview` - Show migration preview (does not change any files)
* `--name` - Set migration name (default: "auto-generated")
* `--comment` - Set migration comment
* `--execute` - Create new migration and execute it
* `--root` - The path to the root folder
* `--migrations-path` - The path to the migrations folder, relative to root
* `--models-path` - The path to the models folder, relative to root

## Executing migrations
* There is simple command to perform all created migrations (from selected revision):

`./node_modules/.bin/run-migration`
* To select a revision, use `--rev <x>`
* If migration fails, you can continue, use `--pos <x>`
* To prevent execution next migrations, use `--one`


For more information, use `generate-migration --help`, `run-migration --help`

## TODO:
* Migration action sorting procedure need some fixes. When many foreign keys in tables, there is a bug with action order. Now, please check it manually (`--preview` option)
* Need to check (and maybe fix) field types: `BLOB`, `RANGE`, `ARRAY`, `GEOMETRY`, `GEOGRAPHY`
* Downgrade is not supported, add it
* This module tested with postgresql (I use it with my projects). Test with mysql and sqlite.
