### macOS Git配置

#### 配置git

```sh
git config --global user.name "xhwhis"
git config --global user.email "hi@whis.me"
git config --global pull.rebase false
```

编辑~/.gitconfig（[详见](https://github.com/xhwhis/config/blob/master/gitconfig)）

编辑~/.gitigrone_global（[详见](https://github.com/xhwhis/config/blob/master/gitigrone_global)）

#### git工具下载

```sh
brew install git-delta
brew install gitui
```

#### 配置git-commit

##### commitizen

```sh
yarn global add commitizen
```

##### commitlint、cz-conventional-changelog

```sh
yarn global add @commitlint/cli @commitlint/config-conventional
yarn global add cz-conventional-changelog
```

编辑~/.commitlintrc.js（[详见](https://github.com/xhwhis/config/blob/master/commitlintrc.js)）

```js
module.exports = { extends: ["@commitlint/config-conventional"] };
```

编辑~/.czrc（[详见](https://github.com/xhwhis/config/blob/master/czrc)）

```
{ "path": "cz-conventional-changelog" }
```

##### lint-staged

```sh
yarn global add lint-staged
```

编辑~/.lintstagedrc.json（[详见](https://github.com/xhwhis/config/blob/master/lintstagedrc.json)）

```json
{
  "*.{yml, yaml, json, xml}": "prettier --ignore-unknown --write",
  "*.md": "markdownlint-cli2 --fix"
}
```

##### husky

```sh
yarn global add husky
```
