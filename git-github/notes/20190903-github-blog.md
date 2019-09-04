# DevEnvironment Setup

### Visual Studio Code - Add Extensions

- Live Server
- HTML Snippets
- HTML CSS support
- Javascript (es6) code snippets
- Auto Rename Tag
- Auto Close Tag
- Material Icon Theme
- Monokai-Contrast Theme

---

### Browsers

- Chrome (required)
- Firefox (optional)

---

### Markdown Editor

- Typora

---

### Markdown Syntax

* [Basic Writing and Formatting Syntax](https://help.github.com/en/articles/basic-writing-and-formatting-syntax#lists)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

---

### VS code shortcuts

- `!` = generate html structure

- `ctrl + ~` = display terminal (set bash as default)

- `ctrl + b` = show / remove left pane

- `shift + ctrl + p` = show all commands

- `shift + ctrl + f` = find in files

- `F5` = start debugging

- `ctrl + space` = keyword lists

- `ctrl + /` = comment out

   ([see more](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf))

---

### Create Github Blog using Hexo

* Install Node.js at [nodejs.org](https://nodejs.org/en/)
* Open your shell and check Node.js version  `node -v`
* `npm i -g hexo-cli` (install global hexo client in your terminal)
* `hexo init myHexoBlog` (myHexoBlog folder created)
* `cd myHexoBlog`
* Open your code editor
* `hexo server` (run server at local)
* `hexo new myBlogPost1` (create a new post)
* `hexo new page about` (create a new page, page as type, about as page_name)
* On _config.yml in source folder (under themes/landscape), type `About: /about` inside menu
* Refresh your local server and check a new menu
* [How to use Hexo and deploy to Github pages](https://gist.github.com/btfak/18938572f5df000ebe06fbd1872e4e39)
* [Watch this tutorial](https://www.youtube.com/watch?v=Onglr1_Kgls)
* [Hexo Github page](https://gist.github.com/btfak/18938572f5df000ebe06fbd1872e4e39)
* [Hexo Documentation](https://hexo.io/docs/)
* [김 데레사 강사님 유튜브](https://www.youtube.com/user/seulbinim)

---

### Create your own theme in hexo page

* Right click "landscape" folder (under "theme" folder) and reveal in explorer
* Duplicate "landscape" and rename it as you wish
* On the bottom of "_config.yml", change theme with new folder name created above

---

### Others

- github blog용 repo 생성 후 md 파일 작성/정리
- github issue에서 이미지 관리
- 개발자 컨퍼런스 (festa, meetgo)
