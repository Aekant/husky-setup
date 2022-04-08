## Installing Husky

1. Install husky using `npm i husky --save-dev`

2. Then we need to create a `.husky` folder which can be created manually by us or by the `husky` command as `npx husky install`. This would create a `.husky` directory. This directory has a `_` directory in it, with two files; `.gitignore` and `husky.sh`. But if you do `git 
status` it won't show up in untracked or tracked files. The reason for this is the wild card in the `.gitignore` file inside `_` directory.
That wild card basically includes all files under that directory and git does not track empty directories

3. The third step would be to add `husky install` in the `prepare` script inside the `scripts` in the `package.json` file. Prepare is a
script that npm runs after `npm install` is executed. So what will happen is anybody who is cloning our project and runs `npm install` we
want them to enable git hooks. This prepare script will do that

## Adding Hooks and Commands

1. To add a new hook we use `npx husky add <file> <command_to_run>`. For example, `npx husky add .husky/pre-commit "npm run build"`. We then
need to add this hook into the git repo so that everyone can use this hook

2. If we run `npx husky add .husky/pre-commit` with a different command then it adds another command to it. Its not like it would replace the
previous one, instead it will run both commands sequentially

## Configuring Lint-Staged

1. First install `lint-staged` using `npm i lint-staged --save-dev`

2. To configure `lint-staged` we need to add an object in `package.json` file with the key `lint-staged`. This object has key-value pairs
where each key is a glob pattern and the value is the command to run on that pattern. For example,

```ts
{
  "lint-staged": {
    "*.js": "eslint --cache --fix"
  }
}
```

will run the `eslint` command on all **staged** files matching the glob pattern `*.js`. If there are multiple sequential commands we can
put them in an array

3. To run the `lint-staged` command at pre-commit add this command to the pre-commit hook `npx husky add .husky/pre-commit "npx lint-staged"`

