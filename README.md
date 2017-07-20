# Timber Docs

This repository is used to build the documentation pages for [Timber](http://github.com/timber/timber). The documentation is generated using the static site generator [Hugo](http://gohugo.io/).

The documentation consists of:

- **Content pages** imported from the [`docs`](https://github.com/timber/timber/tree/master/docs/) folder.
- **Reference pages** for Timber’s PHP classes, which is generated directly from the inline DocBlock documentation of the PHP class files. The relevant generator files can be found in the `generator` folder in this repository.

If you want to **contribute content** to the documentation, you would create a pull request in the [main repository](https://github.com/timber/timber/).

## Building the docs

### Requirements

If you want to work on the documentation website itself, you need to consider the following requirements:

1. This repository needs to be on the same folder level as the Timber repository.
2. You need to have [Hugo](https://gohugo.io/overview/installing/) installed. If you use Homebrew, you can run `brew install hugo`.
3. You need to have [Composer](https://getcomposer.org/) installed.

### Build the documentation

Make sure Composer has what it needs to do its magic...
```
composer install
```

The following command pulls all relevant Markdown files into the repository and builds the documentation pages:

```
bash generate-docs.sh
```

To work on the HTML and styling of the documentation site, you can start a development server with the following command:

```
hugo serve
```

The development server doesn’t build the files yet. If you want to build all HTML files, you can use the following command, which will build the documentation site into the `docs` folder:

```
hugo
```

### Publish

…

### Files and folders

Hugo comes with a set of predefined folders

- `archetypes` – Templates for new pages
- `content` – The contents of the documentation. All of the files inside this folder will be overwritten when you run `generate-docs.sh`.
- `docs` – The generated site.
- `layouts` – Contains template HTML files mixed with [Go](https://gohugo.io/templates/go-templates/) used by Hugo. 
- `static` – Contains compiled/processed assets used in the site. Never work on these files directly, because they will be overwritten when you run an NPM script.

Additionally to that, we added our own folders:

- `generator` – Contains all required files to generate the documentation. The `timber-current` folder is empty by default and will be filled with Timber’s PHP class files when you run `generate-docs.sh`.
- `static-src` – Contains SASS and JavaScript source files. When you compile assets, files from this folder will be processed into the `static` folder.

### Assets

Hugo doesn’t come with a workflow to process JavaScript and CSS files. We use [laravel-mix](https://github.com/JeffreyWay/laravel-mix/) for this. It can be configured in `webpack.mix.js`.

Before you start working on SASS and JavaScript files, you need to install all required dependencies with

```
npm install
```

If you need to change something in the build process you can follow the documentation [guide for Mix](https://laravel.com/docs/5.4/mix) or run one of the following commands:

- `npm run watch` – Watch for relevant file changes. When the development server is running, changed styles and scripts will be automatically inserted into the website.
- `npm run dev` – Build assets for development environment.
- `npm run production` - Build assets for production.
