# textlint-reviewdog-example [![Build Status](https://travis-ci.org/azu/textlint-reviewdog-example.svg?branch=master)](https://travis-ci.org/azu/textlint-reviewdog-example)

textlint project + [reviewdog](https://github.com/haya14busa/reviewdog "reviewdog") example project

reviewdog can write textlint's lint resut as GitHub review comments.

See also:

- [reviewdog — A code review dog who keeps your codebase healthy – Medium](https://medium.com/@haya14busa/reviewdog-a-code-review-dog-who-keeps-your-codebase-healthy-d957c471938b)

## How to setup?

- [ ] Write usage instructions

### 1. Setup .travis.yml

```yaml
sudo: false
language: node_js
node_js: "stable"
env:
- REVIEWDOG_VERSION=0.9.5
install:
  - mkdir -p ~/bin/ && export export PATH="~/bin/:$PATH"
  - curl -fSL https://github.com/haya14busa/reviewdog/releases/download/$REVIEWDOG_VERSION/reviewdog_linux_amd64 -o ~/bin/reviewdog && chmod +x ~/bin/reviewdog
  - npm install
script:
  - npm test
after_failure:
  - test $TRAVIS_PULL_REQUEST == "false" && $(npm bin)/textlint -f checkstyle README.md | reviewdog -f=checkstyle -name="textlint" -ci="travis"
```

See [.travis.yml](.travis.yml) for details.

### 2. Add `REVIEWDOG_GITHUB_API_TOKEN` to Travis CI Config

Get your [personal access token](https://github.com/settings/tokens/new "New personal access token").

![repo](https://monosnap.com/file/duLWpPrFoqR8uPvOZOniupuiptE1GB.png)

Set the access token to `REVIEWDOG_GITHUB_API_TOKEN`.

```shell-session
travis env set REVIEWDOG_GITHUB_API_TOKEN <YOUR_TOKEN>
```

You can check the result:

```shell-session
$ travis env list
# environment variables for azu/textlint-reviewdog-example
REVIEWDOG_GITHUB_API_TOKEN=[secure]
```

### 3. Submit PR

See Example Pull Request.

- [docs: Update README by azu · Pull Request #1 · azu/textlint-reviewdog-example](https://github.com/azu/textlint-reviewdog-example/pull/1 "docs: Update README by azu · Pull Request #1 · azu/textlint-reviewdog-example")

- [ ] Add TODO

## Running tests

Install devDependencies and Run `npm test`:

    npm i -d && npm test

## Contributing

Pull requests and stars are always welcome.

For bugs and feature requests, [please create an issue](https://github.com/azu/textlint-reviewdog-example/issues).

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## Author

- [github/azu](https://github.com/azu)
- [twitter/azu_re](https://twitter.com/azu_re)

## License

MIT © azu
