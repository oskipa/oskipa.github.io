title: One hundred Sites in Phoenix

## Possible future 
 * Fraudomatic
 * Live Texas Hold Them -live
 * Oca Game -- live and umbrella 
 * Chatboard -- channels

## Site 7: Moderated confessions

A site where you can write anonymous confessions. Yet these have to be a pproved by an adminstrator.

### What I learned

The main point on this one is to practice authentication again.

## Site 6: World Clocks

This is a site that uses LiveView and displays clocks and dates in different formats. Learning Live View along with basic use of Timex


### What I learned

The big one here is how to install and get going with something simple with LiveView.

##  There is a Tzdata library for Elixir

Talk about convenience! This library has a function that gives you all of the allowed timezones.

https://hexdocs.pm/tzdata/Tzdata.html#content

#### It is complex to set up live view
LiveView ended up being complex to set up. I wanted to set it up myself to understand how it works. 

I can see why in the contest they would have you fork one with the setup and then start working.

I enjoyed that liveview seems to be a genserver. So You are working directly with that.

#### Timex is very easy to use

I thought I was going to have to spend a lot of time here. I didn't have to. It was easy to work with. I hope they include this into the default Elixir libraries.

#### Installing the dependencies

Floki is some kind of jQuery for Elixir.

    {:phoenix_live_view, "~> 0.6.0"},
    {:floki, ">= 0.0.0", only: :test}


#### References

[How to use it](https://hexdocs.pm/phoenix_live_view/Phoenix.LiveView.html)

[Installation](https://hexdocs.pm/phoenix_live_view/installation.html#content)

## Site 5: Login to see a panda

This site let's you register and login into it. Once you log in, you will see a panda. 

### What I learned

For this one, I am working very fast through "Programming Phoenix" chapter on authentication. It is a long, but necessary chapter in the book.

I think I will have to do this one again without working through the tutorial.

#### Understanding plugs 

A module plug needs two functions `init()` and `call()`. `init()` is to setup work that we need for the connection transformation. It is called only once at startup in production. `call/2` uses output of init as the configurations.




#### Exploring Context

So an account is a meta module that keeps connected  models together. This is very cool.
 

## Site 4: Vox Populi

This a site where anyone can write a message and it appears on a page. It is like an unmoderated confession page.

### What I learned

This time I wanted to use the generator, which I haven't used for a long time. I also wanted to see what Context does.

#### I guess I need to use Timex

I didn't use it here. But I found that the native support to format dates to be pretty weak. If this is the case, timex will become another basic dependency. 

So far the ones that I collected are ecto, timex, and Decimal

#### The timestamps() fields

 `:inserted_at` and `:updated_at`.

I knew that it generated something like this. Now I know exactly what it generates.

#### Understanding routes

I initially wanted to route it like this

    get "/", PostController, :index
    get "/vox", PostController, :new
    post "/vox", PostController, :create

This didn't work. After doing some pattern comparing and troubleshooting, I got it working with this

    get "/", PostController, :index
    get "/new", PostController, :new
    post "/", PostController, :create

I asked.  I believe that it has to do with the links that are generated in the template. If they are not there, then you get an error.

#### Using the phx.gen.html generator

I usually avoid generators because the documentation for them tend to be weak. It is hard to find how you are supposed to construct the models. It is ironic because they are often described as being user friendly. 

Recently I read the documentation for Ecto SQL. This is the module that has the documentation on how the migration types work. I also had had a deeper dive into how ecto schemas work in Phoenix.

So coming back to the generator, I found it now very easy and handy. I will probably be using generators a lot more now since I know what is going on and it will save me typing.


The first thing I did once I had the generator create the supporting files was delete all of the endpoints that I don't care to support


Reference: 
[mix phx.gen.html](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Html.html#content)

#### Ecto SQL migration methods up() down() and change()

up() will add changes to the database. down() will remove it. And change() will take care of up() and down() in a simple function.

[Reference: Ecto Sql Migration](https://hexdocs.pm/ecto_sql/Ecto.Migration.html)

## Site 3: Lotto number generator

The site uses simple jQuery to generate a set of lotto numbers.

As of the writing of this post, to play [powerball](https://powerball.com) you pick 5 number between 1 and 69 and one number between 1 and 26 for the red powerball. 

### What I learned

I wanted to learn how to use or add jQuery in phoenix. I like jQuery because it is the right tool for most html page driven apps. It is also a nice way to learn how to include different javascript libraries. How to include frameworks will come later.

1. In the `assets` directory, run `npm install jquery`

2. In `assets/webpack.config`, on the top, add 

      `webpack = require('webpack')`

This is to have access to default webpack plugins.

3. In the same file, in the `plugins` section, add the following code as an entry

      new webpack.ProvidePlugin({
          '$': 'jquery',
          'jQuery': 'jquery'
      }),

This should add `$` and `jQuery` as a global value on the browser. 

ProvidePlugin loads the module automatically everywhere. The argument is a hash with an ` identifier : 'module'`, where the identifier is the variable name that you want to use in the scripts in the browser along with the module name. You can also export this way just a function. See the documenation to see how that happens.

4. Now under `assets/js/app.js` you need to add the following

      import $ from 'jquery';
      window.$ = $;
      window.jQuery = $;

And this will make it available on the site

[Reference: adding jQuery to Phoenix, SO](https://stackoverflow.com/questions/58714479/phoenix-framework-jquery-connection)

[Reference: webpack plugin provide-plugin ](https://webpack.js.org/plugins/provide-plugin/)
[gettext](http://blog.plataformatec.com.br/2016/03/using-gettext-to-internationalize-a-phoenix-application/) is the multilanguage tool.

## Site 2: Hello Word, non static

This should have been day 1. Have a controller that uses a view and displays, hello world.

##  Site 1: Hello World

Creating a static site that returns "hello, world". I don't need a database or JavaScript. Just the server.

### What I learned

You can create a new phoenix site without a number of components. To create it without a database, we can use some of the [mix phx.new](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.New.html#content)'s options. I ran

        mix phx.new hello_world --no-html --no-webpack --no-ecto

Then I created the static page under `priv/static/hello.html`.

I had to add `hello.html` to `lib/hello_world_web/endpoint.ex`'s Plug.Static `only:` config. That got html being served.

To be able to set the root route to this page I had to create a controller whose index method redirect to the static page.

      def index(conn, _params) do
          redirect(conn, to: "hello.html")
      end
     
