# What_I_learned_today
A  casual blog to record things I learned on internet related to programming.

Timeless sources:   
- https://github.com/Asabeneh/30-Days-Of-JavaScript   
- https://github.com/leonardomso/33-js-concepts   
- https://github.com/ossu/computer-science   
- https://github.com/bradtraversy/design-resources-for-developers
- https://cs50.harvard.edu/x/2022/
- https://cs50.harvard.edu/web/2020/

------
 22/2/2022

- In Node.js, `console.log()` is actually:
 `console.log = function (d) {
  process.stdout.write(d + '\n');
};`

source: https://nodejs.org/docs/v0.3.1/api/process.html#process.stdout

- One can use `alt+shift+I` in `VS Code` to have multiple cursors for all the selected elements.  
Usage example: for formatting all the copy-pasted list of words that are not properly formatted as list items for json.

source: https://www.youtube.com/watch?v=QcXlyriZVa8

------
24/2/2022

- one can open up a folder in the current VS Code window, which by default opens up a new window, use `-r` as in `code -r [your dir]`   

------
3/8/2022   
- `if` statement, if not followed by `else` or `else if`, must `return` something within the brackets (or its lexical scope, if we omit the brackets), in order to work. Even if a function, method or any expression would return something, in that lexical scope the `return` keyword is still needed.    
   
- to print a `function` in `console.log()` simply use the inbuilt function object method called `toString()`. `toString()` is also available for Array object.   
   
- `...args` as multiple arguments for a function's parameter requires the 3 dots `...`, whereas within the function no need to add 3 dots `...` and `args` alone is valid.   
Note: however, when passing it within a function, as an argument, to a nested function or a returned function, `...args` syntax must be preserved.
  
    
------   
9/3/2022    
- a function that does the deep clone (in contrast to shallow clone `[...x]/{...x}`):   
 ```js
const deepClone = (obj) => {
  if (typeof obj !== 'object' || obj === null) return obj;

  // create an array or object to hold the value
  const newObj = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    const value = obj[key];
    // recursive call for nested objects and arrays
    newObj[key] = deepClone(value);
  }

  return newObj;
};   
```
   
-----   
10/3/2022   
- to center an item, without using flex or grid:   
first the html template:   
```html
<div class='outer-box'>
 <div class='inner-box'></div>
</div>
```   
now the version #1 with absolute positionng, which used to be an old, popular way:   
```css
.outer-box {
<!--  styling code -->
  position: relative;
}

.inner-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
<!--  styling code -->
}
```   
Its Codepen link: https://codepen.io/matinsasan/pen/jOagyOX   

Now, using absolute positioning #2, using `inset`, plus `margin: auto`, in CSS:   

```css
<!-- same code as the previous CSS snippet -->

.inner-box {
  position: absolute;
  inset: 0;
  margin: auto;
<!--  styling code -->
}

```   
Its Codepen link: https://codepen.io/matinsasan/pen/GROVrOG   

-----   
13/3/2022   
- `for...of` loop is for `array`, whereas `for... in` loop is for `object`.   
`.entries()` method gives index and value for array:   
`for (let [index, value] of someArray.entries())`,   
whereas key-value pair for object:   
`for (const [key, value] in someObject.entries())`. 
-----  
25/3/2022   
- an often used `CSS` shorthand `background` should best be avoided, as it can interfere with, for example, `background-color` and `background-image` to work properly.      
----- 
29/3/2022   
- React updates state in batches:   
in setState method, for example, updating through `setCount = () => count+1` within a function call multiple times would fail and still use the original, previous state as a reference, while using `setCount = prev => prev+1` by passing the `previous state` as an argument we can accomplish this.
-----   
4/4/2022   
- Some web events can cause cost performance badly, like input, mousemove, etc. where there might be heavy API usage.   
With the help of `debounce` and `throttle` we can address this issue.   
Link to the gist of how to implement debounce and throttle: https://gist.github.com/MatinSasan/25e7ba3837df68c0cc1d2ebfab8a5552
-----   
9/4/2022   
- in CSS, whenever we assign `padding` with `width` to an element, we use `box-sizing:border-box` to keep the math as simple as possible.   
- to center with flexbox (will update for grid and some tricks):  
simply add to the parent element, along with `display:flex`, `justify-content:center` to horizontally center as well as `align-items:center` to vertically center.   
Note that in order to make `align-items` work, we have to add `height` to the parent element, which is usually `100vh` (vh: a percentage of the full viewport height).   
To center just one item, the parent element has `display:flex` while the child one `margin:auto`. 
-----   
14/4/20222   
- in `React` to clean up after in `useEffect` all we need is to use within that function:   
`return () => { *code to clean up* }`   
It will run first everytime `useEffect` gets called.   
-----
17/4/2022   
- Advanced Async/Await, serialized:   
```js
const getPost = async (id) => {
  return await (
    await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`)
  ).json();
};

// serialized

const getPostsSerializedFor = async (ids) => {
  for (const id of ids) {
    const data = await getPost(id);
    console.log(data);
  }
};

// OR

const getPostsSerializedReduce = async (ids) => {
  await ids.reduce(async (acc, id) => {
    // waits for the previous item to complete
    await acc;
    // get the next item
    const post = await getPost(id);
    console.log(post)
  }, Promise.resolve()) // allows to get the first item of the result
  console.log("I'll wait on you");
}
```
-----   
26/4/2022   
- in Typescript, the error `Cannot redeclare block-scoped variable` occurs because the name variable is declared somewhere in the typings for the DOM library, so the global type definition clashes with the local variable declaration.   
To solve the problem, we need to convert the ts file to an ES module, by adding `export {}` as a module is a file that contains at least 1 import or export statement.
-----   
27/4/2022   
- in `npx` in order to force the package manager to be `npm` instead of `yarn`, use `--use-npm`.   
For example:   
`npx create-next-app my-app --use-npm`
------   
28/4/2022   
- for `jest` to have intellisense in `VS Code`:   
`npm i -D @types/jest`, then create a json file, named `jsconfig.json`, in the root directory with the following code:   
```json
{
  "typeAcquisition": {
    "include": [
      "jest"
    ]
  }
}
```
------   
30/4/2022   
- in `virtual environment` of, for example, a `django` project, `pip` might not install the packages within the venv.   
To fix this, first check the dir of `pip` with `which pip` in the terminal. If not showing the path to the venv dir, then it's incorrect.   
Delete the venv folder, and recreate it, for example `virtualenv env`. `pip` path will be correct this time.   
Now reinstall all those packages.   
- the issue above happened to me becauseo of moving venv folder to the app project.   
To start the `django` project within the same dir, there's a `.` needed at the end:   
`django-admin createproject name_of_project .`
------   
1/5/2022   
- in `VS Code` to quickly wrap a selected text/piece of code with html tags, hit `f1` or `ctrl+shift+p`, and type `wrap` which shows `Wrap with abbreviation`, hit enter, type, for example `div` and it will be wrapped so.   

- in `React` a component might double-render, for example, `console.log` ouput is given twice.   
To fix this, in `index.js` of your react app, comment out `<React.strictMode>` and `</React.strictMode>` and simply let `<App />` inside remain.   

- in `flask`, python backend framework, templates won't be updated upon modifying a html file by default.   
To force modification, add this line `app.config['TEMPLATES_AUTO_RELOAD'] = True`  after `app = Flask(__name__)` and run `flask run`.   
Note: this will NOT auto-refresh, but only auto-reload. This makes Flask unattractive for developing websites, but good and quick enough to run apis and tests on python.   
------   
3/5/2022   
### Redis In Windows
- to use `Redis` in `windows`, install WLS (Windows Subsystem for Linux): https://docs.microsoft.com/en-us/windows/wsl/install   
After that, open up a terminal in WSL (in `+` of VS Code's Terminal panel):   
1. run `sudo apt-get install redis`. If encountered `E: Unable to locate package redis` error, then update using `sudo apt-get update`.   
2. type `redis-server`, now open a new WSL terminal and start testing with `SET [key] [value]` and `GET [key` if it works.
------   
4/5/2022   
- in Python, the use of `dataclasses`:   
Let's take a look at this example below:   
```python
import random
import string

def generate_id() -> str:
    return "".join(random.choices(string.ascii_uppercase, k=12))


class Person:
    def __init__(self, name: str, address: str) -> None: # this
        self.name = name # this
        self.address = address # and this, they all will be replaced by datalass

    def __repr__(self) -> str: # this
        return f"{self.name}, {self.address}" # and this, they all will be replaced by dataclass


def main() -> None:
    person = Person(name="Joe", address="123 Main St")
    print(person)


if __name__ == "__main__":
    main()
```   
By importing `dataclasses` we can have scalability for custom classses:  
```python
...
from dataclasses import dataclass, field
...

@dataclass #used as a decorator
class Person: # no need for __init__ and __repr__ as they're generated by dataclass
    name: str # it's much shorter and cleaner to define variables and providing the type
    address: str
    active: bool = True # default value for primitive types can be provided
    email_addresses: list[str] = field(default_factory=list) # explained below about non-primitive.
    # "= []" would address every istance to the same reference to itself.
    # to solve that, dataclasses provides "default_factory" 
    id: str = field(init=False, default_factory=generate_id)
    # generate_id is a custom function, so default_factory can be any function of our choice
    # init= False : prevents outside initialization, and only dataclass can do it. A must for variables like "id"
    _search_string: str = field(init=False, , repr=False)
    # init=False, as it shouldn't be a part of arguments in class initializer
    # repr=False, as it's an internal matter and shouldn't also output what's already given in other inits. 
    # in "_search_string", "_" indicates it's private and protected, which is needed for such use case here.

    def __post_init__(self) -> None:
        self._search_string = f"{self.name}, {self.address}"
    # __post_init__ is needed for the default initialized value based on other initialiazed variables first
```   
Also:   
```python
@dataclass(frozen=True)
```
Here, `frozen=True` makes the objects of the class immutable, `constants` (not the primitive types).   
```python
@dataclass(kw_only=True)
```
Initalizing the class is only allowed with keyword arguments, with `kw_only=True`.
- bear in mind that, `@dataclass` is a regular decorator, while `@dataclass([args])` is a callable that returns a decorator.   
------
4/5/2022   
- to get a `tree directory` representation, that can be used in `readme.md`, first install `tree` on Linux or WSL:   

> sudo apt install tree   

Now you can use to get your tree dir:   
> tree -d
   
- **git**:   
1. to remove a wrong pushed commit to github, first `git log` then (`+` is to force push):   
  > git push origin +[commit_id]:main       
2. That was remote change, to locally change to, for example, the last commit:   
 > git reset HEAD~
3. now add and commit as usual :)   

- **Markdown and relative path**: click the links to learn about how to [Link in Markdown](https://stackoverflow.com/a/16426829/11330560) and [use relative path in them](https://github.community/t/link-to-a-section-in-another-readme-md-file/1130).   
-------
5/5/2022
### Docker In Windows   
1. install `WSL2` on Windows.
2. `wsl.exe -l -v` to check the version
3. run `wsl --set-version [distroname] 2` if it's not `v2`, for me `ubuntu` was my distro.   

- `Vmmem` the background process of Virtual Env for Docker will probably eat a lot of RAM by now.
1. to limit VM's Ram usage, first close `wsl.exe -t ubuntu` or `wsl --shutdown`.
2. navigate to `%UserProfile%` (paste it to the address bar of the win explorer).
3. edit/add `%UserProfile%/.wslconfig`
4. add the following lines in the file (memory=1GB, 2GB, 6GB, etc.):   
```
[wsl2]
memory=2GB
```
5. restart Docker. Enjoy preserving your sanity :)
---------   
5/5/2022
### Changing Docker Native Image Location on Windows 10   
1. access `%LOCALAPPDATA%/Docker/wsl`. There will be 2 folders:   
- data/ext4.vhdx which is consumed by docker-desktop-data
- distro/ext4.vhdx which is consumed by docker-desktop 
2. STOP Docker first, then run `wsl --shutdown` to shut down all WSL distros.
3. Export docker-desktop-data to tar file (E can be any preferred path):
```
wsl --export docker-desktop-data E:\docker-desktop\docker-desktop-data.tar
```
- be sure to create `docker-desktop` main dir to not run into path error.
4. unregister current docker-desktop-data distro:   
```
wsl --unregister docker-desktop-data
```
5. import docker-desktop-data distro from tar file:
```
wsl --import docker-desktop-data E:\docker-desktop\data E:\docker-desktop\docker-desktop-data.tar --version 2
```
- you can delete tar file now.
- in this step, we may meet the error of cannot create a specific network. Just re-run the import command.
6. Run Docker Desktop. You just saved your C drive from running out of space :)
----- 
5/5/2022
#### some useful linux commands (windows wsl included)
- `|` to pipe commands, which the second command takes as the input the output of the first command.
- `cd -` to go back the previous directory. `cd` to go to the home dir.
- `pushd [someDir]` to cache the previous dir to a stack, and `popd` to get back to that dir after navigating around.
- `ctrl+l` cleans the terminal, while `reset` completely does that.
- `ctrl+z` put a program/process to the background but freezes it, to keep it running use `bg`, and `fg` to bring it to the foregound.
- `htop` opens up a monitor showing all the processes, programs going on as well as hardware usage.
- forgot to put `sudo` while doing, e.g. `apt upgrade`? simply use `!!` in front, to avoid retyping: `sudo !!` 
- `ctrl+r` to show up previously used command, `ctrl+r` again to go one step back.
- `history` to show all recently used commands. you can `bang` to run one of those commands, like `!100` runs the 100th.
- `HISTTIMEFORMAT="%Y-%m-%d %T "` (the space at the end is important) to add date to commands in `history`, at least from now on.   
In the previous tip, it only stays with the current open session. to save it `nano ~/.bashrc` and add that line there to save globally.   
Put a space in front of a command to not let it be included in `history`.
- `ctrl+ +"` and '`ctrl+ -` to resize the terminal. `rest` to reset the size.
- to chain two commands, use `;`, e.g. `ls -l; echo "hello"`.   
While `&&` does the same, it prevents the next command to run, if the first command fails.
- `tail -f` to monitor changes in a file. It does not monitor changes in the middle of using the file.
- `truncate`: The truncate command effectively eliminates all the contents of a file. E.g. `truncate -s 0 test.txt`, size set to zero.   
It does not delete the file itelf, but leaves it as a zero-byte file on the disk.   
The file permissions and ownership will be preserved if you use the truncate command.
- `column`: e.g. `mount | column -t` to make an output look more human readable in an organized way.
   
----  
6/5/2022   
   
- **Postgres Win 10 Terminal (cmd)**:   
to fix `Console code page (437) differs from Windows code page (1252)`, add `cmd.exe /c chcp 1252 command` to `psql.bat` in `postgres\scripts`.   
In should be at the near top, the right location, shown below:
```bat
@echo off

REM Copyright (c) 2012-2014, EnterpriseDB Corporation.  All rights reserved

REM PostgreSQL server psql runner script for Windows

cmd.exe /c chcp 1252

SET server=localhost
SET /P server="Server [%server%]: "
```
- `psql`: 
`dbname=#` could change to `dbname-#` by accident, not allowing you to excute any command.   
To fix that, either hit <kbd>enter</kbd> to finish the command or press <kbd>ctrl</kbd>+<kbd>C</kbd> to terminate and start over.   
   
- `psql` default user win 10:   
`psql` uses the win's default user which is not the same as default postgres user, usually `postgres`, asking for password, which fails.
1. go to `Environment variables`, and then `System variable`.
2. add `PGUSER` as variable, and `postgres` as value.
3. now `psql` won't act stupid (this is for casual use and practicing with Postgres, otherwise one shouldn't mess with it AFAIK).
----
7/5/2022   
   
### Laravel setup   
- instead of using `XAMPP`, there are 2 easier ways to set up a new laravel project:   
1. using **Laravel Sail** via Docker: `curl -s https://laravel.build/example-app | bash`, `cd example-app`, then `./vendor/bin/sail up`.
2. using **Laragon**: a fast, portable, light tool.
----   
- to rename `git`'s global default brranch from `master` to `main`, simply run: `git config --global init.defaultBranch main`   
   
8/5/2022   
- to shift the behavior of `merge` in `git` from `fast-forward` to `three-way`, run (`--global` for all): `git config ff no`
----   
9/5/2022   
- **git**: `commits` are immmutable.
----
9/5/2022  
### Docker: Tag, Push
- To rename a tag, e.g. from `server` to `myname/server`:   
`docker image tag server:latest myname/server:latest` or `docker image tag d583c3ac45fd myname/server:latest`.   
`docker rmi server`, removes the older tag without removing the image itself. `:latest` can be omitted, if there's only one image's tag.
- To push to `Docker Hub`, the name of the image must be right, so `server` should be `myDockerUser/server`.
----
10/5/2022
### Ubuntu (WSL2)   
**Move WSL 2 file system to another drive**:   
1. export Ubuntu:
- `mkdir D:\backup`
- `wsl --export Ubuntu D:\backup\ubuntu.tar`
2. Unregister the same distribution to remove it from the C: drive:
- `wsl --unregister Ubuntu`
3. import Ubuntu:
- `mkdir D:\wsl`
- `wsl --import Ubuntu D:\wsl\ D:\backup\ubuntu.tar`
4. By default Ubuntu will use root as the default user, to switch back to previous user:
- `cd %userprofile%\AppData\Local\Microsoft\WindowsApps`
- `ubuntu config --default-user <username>`
- (for docker perhaps: `wsl --set-default Ubuntu-20.04 `)   
   
**Updating Ubuntu (to 20.4)**:
1. `sudo apt update`
2. `sudo apt upgrade`
3. `sudo apt dist-upgrade`
4. `sudo apt autoremove`
5. `sudo do-release-upgrade` (before that you need to reboot Ubuntu: Services.msc -> restart `LXSSMANAGER`.
