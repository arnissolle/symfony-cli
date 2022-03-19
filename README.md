# Run Symfony CLI through Docker.

### Build

```bash
docker build -t arnissolle/symfony-cli ./php/8.1
```

### Run

`WORKDIR` default set to `/var/www`

```bash
docker run --rm -it \
    -v $(pwd):/var/www \
    -t arnissolle/symfony-cli -V
```

### Git

By default, it will commits with: Symfony CLI \<noreply@symfony.com\>

To commit by your name, feel free to mount a volume like so:

```bash
-v $HOME/.gitconfig:/root/.gitconfig
```
