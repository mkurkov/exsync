ExSync
======

Yet another Elixir reloader.

## System Support

ExSync deps on [FileSystem](https://github.com/falood/file_system)

## Usage

1. Create a new application:

        mix new my_app

2. Add exsync to your `mix.exs` dependencies:

```elixir
def deps do
  [ {:exsync, "~> 0.2", only: :dev} ]
end
```

## Usage for umbrella project

1. Create an umbrella project

        mix new my_umbrella_app --umbrella

2. Add exsync to your `mix.exs` dependencies:

```elixir
def deps do
  [ {:exsync, "~> 0.2", only: :dev} ]
end
```

3. start your umbrella project with `exsync` task

        iex -S mix exsync

## Config

All configuration for this library is handled via the application environment.

`:addition_dirs` - Additional directories to monitor

For example, to monitor the `priv` directory, add this to your `config.exs`:

```elixir
config :exsync, addition_dirs: ["/priv"]
```

`:extensions` - List of file extensions to watch for changes. Defaults to: `[".erl", ".hrl", ".ex", ".eex"]`

`:extra_extensions` - List of additional extensions to watch for changes (cannot be used with `:extensions`)

For example, to watch `.js` and `.css` files add this to your `config.exs`:

```elixir
config :exsync, extra_extensions: [".js", ".css"]
```

`:reload_callback` - A callback [MFA](https://codereviewvideos.com/blog/what-is-mfa-in-elixir/) that is called when a set of files are done reloading. Can be used to implement your own special handling to react to file reloads.

`:reload_timeout` - Amount of time to wait in milliseconds before triggering the `:reload_callback`. Defaults to 150ms.

For example, to call `MyApp.MyModule.handle_reload()` add this to your `config.exs`:

```elixir
config :exsync,
  reload_timeout: 75,
  reload_callback: {MyApp.MyModule, :handle_reload, []}
```
