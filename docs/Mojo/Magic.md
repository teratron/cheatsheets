**magic** - A high level package management tool by Modular for developing with Mojo and MAX.

To get started, run `magic init` in your project directory.

To see all available commands, run `magic --help` or `magic help`.

## Usage

	magic [OPTIONS] <COMMAND>

## Commands

| Команда       | Описание                                                                                                                                                      |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `init`        | Creates a new project                                                                                                                                         |
| `add`         | Adds dependencies to the project `[aliases: a]`                                                                                                               |
| `remove`      | Removes dependencies from the project `[aliases: rm]`                                                                                                         |
| `install`     | Install all dependencies `[aliases: i]`                                                                                                                       |
| `update`      | Update dependencies as recorded in the local lock file                                                                                                        |
| `run`         | Runs task in project `[aliases: r]`                                                                                                                           |
| `shell`       | Start a shell in the pixi environment of the project `[aliases: s]`                                                                                           |
| `shell-hook`  | Print the pixi environment activation script                                                                                                                  |
| `project`     | Modify the project configuration file through the command line                                                                                                |
| `task`        | Interact with tasks in the project                                                                                                                            |
| `list`        | List project's packages `[aliases: ls]`                                                                                                                       |
| `tree`        | Show a tree of project dependencies `[aliases: t]`                                                                                                            |
| `global`      | Subcommand for global package management actions `[aliases: g]`                                                                                               |
| `config`      | Configuration management                                                                                                                                      |
| `info`        | Information about the system, project and environments for the current machine                                                                                |
| `search`      | Search a conda package                                                                                                                                        |
| `self-update` | Update magic to the latest or a specific version                                                                                                              |
| `clean`       | Clean the parts of your system which are touched by pixi. Defaults to cleaning the environments and task cache. Use the `cache` subcommand to clean the cache |
| `completion`  | Generates a completion script for a shell                                                                                                                     |
| `telemetry`   | Configure how telemetry data is emitted from Modular packages                                                                                                 |
| `help`        | Print this message or the help of the given subcommand(s)                                                                                                     |

## Options

| Команда | Команда           | Описание                                                                                                         |
|---------|-------------------|------------------------------------------------------------------------------------------------------------------|
| `-v`    | `--verbose...`    | Increase logging verbosity                                                                                       |
| `-q`    | `--quiet...`      | Decrease logging verbosity                                                                                       |
|         | `--color <COLOR>` | Whether the log needs to be colored `[env: MAGIC_COLOR=] [default: auto] [possible values: always, never, auto]` |
|         | `--no-progress`   | Hide all progress bars `[env: MAGIC_NO_PROGRESS=]`                                                               |
| `-h`    | `--help`          | Print help                                                                                                       |
| `-V`    | `--version`       | Print version                                                                                                    |

## Uninstall

```shell
rm ~/.modular/bin/magic
```

## Create a Python project

```shell
magic init my-project
```

```shell
cd my-project
```

```shell
magic add "python==3.11"
```

```shell
magic run python3 --version
```

```shell
magic shell
```

```shell
python3 --version
```

Then use `exit` to deactivate the shell.
Always exit the shell before changing projects.

```shell
exit
```

```shell
magic add max
```

## Create a Mojo project

```shell
magic init my-mojo-project --format mojoproject
```

```shell
cd my-mojo-project
```

```shell
magic run mojo --version
```

```shell
magic shell
```

```shell
mojo --version
```

Then use `exit` to deactivate the shell.
Always exit the shell before changing projects.

```shell
exit
```

```shell
magic add "python==3.9"
```

## Convert a conda project to Magic

```shell
magic init --import environment.yml
```

## Manage packages

```shell
magic add max "numpy<2.0"
```

This adds the latest version of MAX and the latest version of NumPy that's less than `2.0`.
If you prefer to use PyPI for your packages, add the `--pypi` flag:

```shell
magic add --pypi "numpy<2.0"
```

However, you should avoid mixing conda and PyPi packages in the same project

## Add channels

If a package appears unavailable from conda via `magic add`, you might need to add a new conda channel. For example,
PyTorch is not available in `conda-forge`, so you must edit your `pixi.toml` or `mojoproject.toml` config file to add
the `"pytorch"` channel:

```shell
channels = ["pytorch", "conda-forge", "https://conda.modular.com/max"]
```

```shell
magic add pytorch
```

## Update a package

```shell
magic update max
```

## Define a package version

```shell
magic add "max~=24.5"
```

This ensures that the project uses MAX `24.5` but it also allows "compatible" versions such as `24.5.1`.

## Change the Python version

```shell
magic add "python==3.9"
```

```shell
magic run python3 --version
```
