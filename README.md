# vnetod

> All the code is stored [here](https://git.pleshevski.ru/pleshevskiy/vnetod).

Dotenv state switcher

You can create many states in your `.env` and switch between them.

Rules:

- State name starts on a new line with `###` symbols (Ex. `### local`)
- State name can contain multiple comma-separated sections (Ex.
  `### local,staging`)
- Each section may specify a namespace (Ex. `### debug:on,dev:on`). If a section
  doesn't contain a namespace, it's a global namespace.
- State ends if line is empty or contains a new state name.

You can see the [full example].

[full example]: https://git.pleshevski.ru/pleshevskiy/vnetod/src/branch/main/.env.example

# Usage

Basic usage

```sh
cp .env.example .env
vnetod local        # enable local section
vnetod staging      # enable staging section
vnetod local debug  # enable local and debug sections
vnetod              # disable all sections
```

This tool uses `.env` from your current location, but you can change this
behavior with the `-f` (`--file`) flag.

```sh
cp .env.example .env.properties
vnetod .env.properties local
```

And you can also change the output file with the `-o` (`--output`) flag, if you
don't want to overwrite the input file.

```sh
vnetod -f .env.example -o .env local
```

You can also use variables from namespaces

```sh
vnetod db:staging debug:off
```

You can switch between states and overwrite from namespaces at the same time.

```sh
vnetod local db:staging debug:off
```

For more information, see the help.

```sh
vnetod --help
```

# Install

## Cargo

```sh
cargo install vnetod
```

## Docker

```sh
docker run --rm -it -v $PWD:/data pleshevskiy/vnetod --help
```

## Nix

```sh
nix run git+https://git.pleshevski.ru/pleshevskiy/vnetod -- --help
```

# License

GNU General Public License v3.0 or later

See [COPYING](./COPYING) to see the full text.

[COPYING]: https://git.pleshevski.ru/pleshevskiy/vnetod/src/branch/main/COPYING
