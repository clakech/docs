# Supported tags and respective `Dockerfile` links

-	[`1.7`, `1.7.21`, `latest`, `1.7-jre`, `1.7.21-jre` (*1.7/jre/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/10d7ac08b7138c274a819af1bd8258d61cb55f9e/1.7/jre/Dockerfile)
-	[`1.7-jdk`, `1.7.21-jdk` (*1.7/jdk/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/10d7ac08b7138c274a819af1bd8258d61cb55f9e/1.7/jdk/Dockerfile)
-	[`1.7-onbuild`, `1.7.21-onbuild` (*1.7/onbuild/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/10d7ac08b7138c274a819af1bd8258d61cb55f9e/1.7/onbuild/Dockerfile)
-	[`9.0.0.0`, `9.0.0.0-jre` (*9000/jre/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/9d048db2e65af55daf6acfbc623f38f1979ff88a/9000/jre/Dockerfile)
-	[`9.0.0.0-jdk` (*9000/jdk/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/9d048db2e65af55daf6acfbc623f38f1979ff88a/9000/jdk/Dockerfile)
-	[`9.0.0.0-onbuild` (*9000/onbuild/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/9d048db2e65af55daf6acfbc623f38f1979ff88a/9000/onbuild/Dockerfile)

For more information about this image and its history, please see the [relevant manifest file (`library/jruby`)](https://github.com/docker-library/official-images/blob/master/library/jruby) in the [`docker-library/official-images` GitHub repo](https://github.com/docker-library/official-images).

# What is JRuby?

JRuby (http://www.jruby.org) is an implementation of Ruby (http://www.ruby-lang.org) on the JVM.

Ruby is a dynamic, reflective, object-oriented, general-purpose, open-source programming language. According to its authors, Ruby was influenced by Perl, Smalltalk, Eiffel, Ada, and Lisp. It supports multiple programming paradigms, including functional, object-oriented, and imperative. It also has a dynamic type system and automatic memory management.

> [wikipedia.org/wiki/Ruby_(programming_language)](https://en.wikipedia.org/wiki/Ruby_%28programming_language%29)

JRuby leverages the robustness and speed of the JVM while providing the same Ruby that you already know and love. With JRuby you are able to take advantage of real native threads, enhanced garbage collection, and even import and use java libraries.

![logo](https://raw.githubusercontent.com/docker-library/docs/master/jruby/logo.png)

# How to use this image

## Create a `Dockerfile` in your Ruby app project

	FROM jruby:1.7-onbuild
	CMD ["./your-daemon-or-script.rb"]

Put this file in the root of your app, next to the `Gemfile`.

This image includes multiple `ONBUILD` triggers which should be all you need to bootstrap most applications. The build will `COPY . /usr/src/app` and `RUN bundle install`.

You can then build and run the Ruby image:

	docker build -t my-ruby-app .
	docker run -it --name my-running-script my-ruby-app

### Generate a `Gemfile.lock`

The `onbuild` tag expects a `Gemfile.lock` in your app directory. This `docker run` will help you generate one. Run it in the root of your app, next to the `Gemfile`:

	docker run --rm -v "$PWD":/usr/src/app -w /usr/src/app jruby:1.7 bundle install --system

## Run a single Ruby script

For many simple, single file projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a Ruby script by using the Ruby Docker image directly:

	docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp jruby:1.7 jruby your-daemon-or-script.rb

# License

View [license information](https://github.com/jruby/jruby/blob/master/COPYING) for the software contained in this image.

# Supported Docker versions

This image is officially supported on Docker version 1.7.1.

Support for older versions (down to 1.0) is provided on a best-effort basis.

# User Feedback

## Documentation

Documentation for this image is stored in the [`jruby/` directory](https://github.com/docker-library/docs/tree/master/jruby) of the [`docker-library/docs` GitHub repo](https://github.com/docker-library/docs). Be sure to familiarize yourself with the [repository's `README.md` file](https://github.com/docker-library/docs/blob/master/README.md) before attempting a pull request.

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/cpuguy83/docker-jruby/issues).

You can also reach many of the official image maintainers via the `#docker-library` IRC channel on [Freenode](https://freenode.net).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue](https://github.com/cpuguy83/docker-jruby/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.
