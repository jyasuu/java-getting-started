# java-getting-started

A barebones Java app, which can easily be deployed to Heroku.

This application supports the [Getting Started with Java on Heroku](https://devcenter.heroku.com/articles/getting-started-with-java) article - check it out.

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Running Locally

Make sure you have Java and Maven installed.  Also, install the [Heroku CLI](https://cli.heroku.com/).

```sh
$ git clone https://github.com/heroku/java-getting-started.git
$ cd java-getting-started
$ mvn install
$ heroku local:start
```

Your app should now be running on [localhost:5000](http://localhost:5000/).

If you're going to use a database, ensure you have a local `.env` file that reads something like this:

```
JDBC_DATABASE_URL=jdbc:postgresql://localhost:5432/java_database_name
```

## Deploying to Heroku

```sh
$ heroku create
$ git push heroku main
$ heroku open
```

## Documentation

For more information about using Java on Heroku, see these Dev Center articles:

- [Java on Heroku](https://devcenter.heroku.com/categories/java)

By default, your app deploys on a free dyno. A dyno is a lightweight Linux container that runs the command specified in your Procfile. After deployment, ensure that you have one web dyno running the app. You can check how many dynos are running using the heroku ps command:

```sh
heroku ps
```

## Scale the App

Horizontal scaling an application on Heroku is equivalent to changing the number of running dynos.

Scale the number of web dynos to zero:

```sh
heroku ps:scale web=0
```

Access the app again by refreshing your browser or running heroku open. You get an error message because your app no longer has any web dynos available to serve requests.

Scale it up again:

```sh
heroku ps:scale web=1
```

To prevent abuse, scaling a non-free application to more than one dyno requires account verification.

The example app has spring.datasource.url set to the value in the JDBC_DATABASE_URL to establish a pool of connections to the database:

spring.datasource.url: ${JDBC_DATABASE_URL:}
The official Heroku Java buildpack that’s automatically added to your app sets this JDBC_DATABASE_URL environment variable. This variable is dynamic and doesn’t appear in your list of configuration variables when running heroku config. You can view it by running the following command:

```sh
heroku run echo \$JDBC_DATABASE_URL
```

Now that you know it works as expected locally, set this variable as a config var on your app running on Heroku. Execute the following:

```sh
heroku config:set ENERGY="20 GeV"
Setting ENERGY and restarting calm-beyond-57162... done, v9
ENERGY: 20 GeV
```

View the app’s config vars using heroku config to verify you’ve done it correctly:

```sh
heroku config
=== calm-beyond-57162 Config Vars
DATABASE_URL:         postgres://avhrhofbiyvpct:3ab23026d0fc225bde4544cedabc356904980e6a02a2418ca44d7fd19dad8e03@ec2-23-21-4-7.compute-1.amazonaws.com:5432/d8e8ojni26668k
ENERGY:               20 GeV
PAPERTRAIL_API_TOKEN: ChtIUu9fHbij1cBn7y6z
```
