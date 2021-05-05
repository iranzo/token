# Token adder for metatamask

Check [iranzo.io/token](https://iranzo.io/token) to access the generated web interface for adding tokens to your metamask wallet.

## Test changes locally

```sh
mkdir .jekyll-cache
touch Gemfile.lock
chmod 666 Gemfile.lock
chcon -Rt svirt_sandbox_file_t -l s0:c1,c2 .

podman run -p 4000:4000 -v $(pwd):/srv/jekyll:Z jekyll/jekyll jekyll serve --watch --future
```
