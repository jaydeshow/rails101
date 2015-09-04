# rails101

# ![Logo](https://github.com/jaydeshow/rails101/raw/master/Zircon.png)

ref: https://docs.c9.io/docs/setting-up-github-workspace

Your Repositories

1. Connected your GitHub or BitBucket account to your Cloud9 account

2. Go to your repos page (or get to it by going to your dashboard and clicking on Repositories)

3. Clone a repo!

4. 注意不能同名


 建立一個全新的專案

打開 Terminal or iTerm2

rails new first-app
建立一個新的 Rails 專案

cd first-app
進入 first-app 專案資料夾

<!--git init-->
<!--建立 git 版本控制-->

<!--git add .-->
<!--git commit -m "Commit Initial" 第一次 Commit (存檔)-->

使用鷹架( Scaffold )功能

rails g scaffold topic title:string description:text

使用鷹架建置一個叫 topic 的簡易留言板

rake db:migrate
建立資料庫

rails s
rails s -p $PORT -b $IP
開啓 server 模式

打開瀏覽器 
網址: localhost:3000/topics
https://rails101-zircon-2.c9.io/topics


即可操作簡易的留言板功能 


建立 welcome 頁面

插入一段 code
app/controllers/topics_controller.rb
class TopicsController < ApplicationController
  before_action :set_topic, only: [:show, :edit, :update, :destroy]

+ def welcome
+   #先用 render 測試!
+   render text: '<h1> render Hello World! </h1>'
+ end

設定 routes (welcome導到 topics 的 welcome method)
記得重啟 server!(routes.rb更改經測試不用重啟)

config/routes.rb
Rails.application.routes.draw do
  resources :topics  
+ get 'welcome', to: 'topics#welcome'


建立 welcome.html.erb

到 app/views/topics/ 資料夾裡建立一個檔案

app/views/topics/welcome.html.erb
<h1> Hello World! </h1>
打開瀏覽器，網址: http://localhost:3000/welcome
https://rails101-zircon-2.c9.io/welcome

設定首頁為 http://localhost:3000/topics

config/routes.rb
Rails.application.routes.draw do
  resources :topics
  get  'welcome', to: 'topics#welcome'
+ root 'topics#index'

  ...
  ...
打開瀏覽器，網址: http://localhost:3000


幫網站穿衣服：使用 Bootstrap 做前端套版
安裝 gem 'bootstrap-sass'

http://getbootstrap.com/

Bootstrap 是目前網站開發裡最好用的前端 CSS 套件
在 Rails 可以使用 ruby 函式庫 (gem) 來把 Bootstrap 裝進我們的專案裡面

gemfile
source 'https://rubygems.org'

+ gem 'bootstrap-sass'
...
...
執行安裝

bundle install
安裝 gem

將 Bootstrap 的 CSS 套件裝進專案裡面

把 app/assets/stylesheets/application.css 更名為 app/assets/stylesheets/application.css.scss

mv app/assets/stylesheets/application.css app/assets/stylesheets/application.css.scss

app/assets/stylesheets/application.css.scss
/*
 * ...(一堆註解)
 *= require_tree .
 *= require_self
 */

+ @import "bootstrap-sprockets";
+ @import "bootstrap";

記得重開 rails s

使用前



使用後


Listing Topics等字體會靠左
似乎改變不大？
那是因為我們還沒套入 Bootstrap 到 html 裡面去


幫你的專案裝上 Navbar 跟 Footbar

到 app/views 增加一個資料夾 : common

增加二個檔案

app/views/common/_navbar.html.erb
<nav class="navbar navbar-default" role="navigation">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <a class="navbar-brand" href="/">Rails 101</a>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav navbar-right">
        <li> <%= link_to("登入", '#') %> </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
app/views/common/_footer.html.erb
<footer class="container" style="margin-top: 100px;">
  <p class="text-center">Copyright ©2015 Rails101
    <br>Design by zircon</a>
  </p>
</footer>
把 bootstrap 關於下拉選單 dropdown 的程式碼掛上去

app/assets/javascripts/application.js
... (一堆註解)
//= require jquery
//= require jquery_ujs
//= require turbolinks
+//= require bootstrap/dropdown
+//= require bootstrap/alert
//= require_tree .


修改你的 app/views/layout/application.html.erb

app/views/layouts/application.html.erb
...
...
<body>

<div class="container-fluid">
+ <%= render "common/navbar" %>
  <%= yield %>
</div>
+ <%= render "common/footer" %>
  
</body>
</html>

Before



After

代入 bootstrap 的 table 套件

app/views/topics/index.html.erb
<h1 >Listing topics</h1>

-<table>
+<table class="table">
  <thead>
...
...

Before



After

Why should not use scaffold?

在前二篇，我們體驗了用 Rails 內建的鷹架模式快速地做了一個有 『 CRUD (註) 』 功能的留言板

Scaffold 是個很方便的功能，但如果您想成為一個稱職的 Rails developer

必須要學會如何 從零做出一個 CRUD 功能

有很多很酷的功能，都是由最基本的 CRUD 設定去做延伸，
如果太依賴 Scaffold ，會讓您很難理解如何學習、創造出來 

 How to use this course for lean Rails ?

強烈建議一定要『 親自動手做 』

並請把『 遇到bug 』當成是一個非常正常的事情
debug 的過程，才是您進步的原動力

在開始真正的教程之前，
建議您先把環境設定好

Ruby on Rails 最佳開發環境建置

(以下是預設您使用 Mac)


Ruby on Rails 最佳裝機實務
Sublime Text 2 設定

下載並安裝 iTerm2, 打開 iTerm2 做 終端機設定 


我卡關了！要如何找到人求救？

歡迎您到各地 Rails Meetup 帶著你的筆電與問題找人詢問

如果您要在網路上找人詢問求救， 下面提供一篇『 發問的藝術 』
供您參考，絕對會大幅提高找到人回應您問題的機會

為什麼上網發問沒有⼈人要理你?

    不知道你的作業系統與 Ruby 版本
    不知道你的錯誤訊息
    不知道你的錯誤畫⾯面
    沒有你的原始檔案

發問格式(範例)

    我目前在「實作檔案上傳」。我在「傳檔時」遇到錯誤。
    我⽤用的是 「Ubuntu 12.04」 , ruby 是⽤用 「rvm 上的的 2.0.0」
    (貼 console 「全部訊息到 gist 」)
    (貼瀏覽器的 「全部錯誤訊息到 gist 」)
    (截瀏覽器整張圖張貼)
    把 Repo 網址公開(例如專案的 github ),讓⼈人直接看
    少⼀樣都不⾏！

特別注意

請不要直接把錯誤訊息貼在 Facebook 上，
因為 FB 的排版格式用在貼 Code 是場悲劇

除非經過當事人同意，
也請不要直接用 FB 的私訊問問題
因為大部份的人都是把 FB 用於私人時間上
一二次還好，太多次是會讓當事人想把你封鎖的

請保持應有的禮貌
沒有人有義務幫你解決問題

只要保持以上原則，相信您一定能得到別人善意的幫助！ 


   CRUD

What is CRUD?

CRUD 是一個縮寫，由

Create
Read
Update
Delete

四個單字組成，剛好也是一個網站運作最最最基本的功能

創建
讀取
更新
刪除 

 CRUD in Rails


在 Rails 的架構中，有一套規範強制要求開發者一定要照它的規則來開發 CRUD 功能
不同於其他程式語言做出來的網站，有很大的自由度隨你設定

這套規則就是 MVC 架構 與 RESTful
在初期要理解這套規則對新手來說無異是非常大的障礙

我們未來會開新篇幅解釋何謂 MVC架構 與 RESTful
對於身為新手的您只要知道一件事

先實做出來就對了

未來當您開發到一定的階段，就會理解到何為『 制約即解放 』

由於 CRUD 功能是一個網站最基本的規劃，太過自由的設定(例如命名、變數、流程)
會造成未來維護與再開發時一個非常大的困擾
=> 寫 code 只需要一次 ， but 卻會花很多次來讀 code

如何把 code 寫的簡潔、乾淨、易讀、好維護是門很深的學問
本 blog 的教程也會儘量以上述的原則來寫出 Code

而 MVC 架構 跟 RESTful 則可以幫助我們在建置 CRUD 功能時，

做出一套簡潔、乾淨、易讀、好維護的程式碼 

作業目標

本章的作業目標：

    建置一個 Rails 專案 ( 版本 4.2.0 )
    安裝gem: brakeman 跟 rails_best_practices

Brakeman is a static analysis tool which checks Ruby on Rails applications for security vulnerabilities.

http://www.slideshare.net/ihower/rails-best-practices

 建立新專案

先確認 ruby 的版本

$ ruby -v

本教材使用 ruby 2.1.2 版本

安裝 rails 4.2.0
$ gem install rails -v 4.2.0

建立一個新 Rails 專案 ( 版本 4.2.0 ) 後面的 "-T" 是指不安裝內建的 test unit
$ rails _4.2.0_ new rails101s -T


