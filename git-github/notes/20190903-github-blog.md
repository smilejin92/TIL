# 개발환경 세팅

### Visual Studion - Add Extensions

- live server
- HTML Snippets
- HTML CSS support
- javascript (es6) code snippets
- auto rename tag
- auto close tag
- material icon theme

---

### Browsers

- chrome (required)
- firefox (optional)

---

### Markdown Editor

- typora

---

### VS code shorcuts

- ! = generate html structure

- ctrl + ~ = display terminal (set bash as default)

- ctrl + b = (show / remove left pane)

- shift + ctrl + p = show all commands

- shift + ctrl + f = find in files

- F5 = start debugging

   ex) 'live server'
   
- ctrl + space = keyword lists

- ctrl + / = comment out

---

### Create Github Blog using Hexo

* Install Node.js at nodejs.org
* `npm i -g hexo-cli` (install global hexo client) in your terminal
* `hexo init myHexoBlog` (myHexoBlog folder created)
* `cd myHexoBlog`
* Run your code editor
* `hexo server` (run server at local)
* `hexo new myBlogPost1` (create a new post)
* `hexo new page about` (create a new page, page as type, about as page_name)
* on _config.yml in source folder (under themes/landscape), type `About: /about` inside menu
* refresh your local server and check a new menu

* [Watch this tutorial](https://www.youtube.com/watch?v=Onglr1_Kgls)

---

### Create your own theme in hexo page

* right click landscape folder (under theme) and reveal in exploerer
* duplicate landscape and rename the duplicated folder as you wish
* on the bottom of _config.yml, change theme with new folder created above

---

### Others

- github blog용 repo 생성 후 md 파일 작성/정리
- github issue에서 이미지 관리
- 개발자 컨퍼런스 (festa, meetgo)