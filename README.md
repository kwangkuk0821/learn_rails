# ruby on rails

레일즈는 루비 언어로 작성된 웹 어플리케이션 프레임워크 입니다. 레일즈는 모든 개발자가 개발을 시작 할때 필요한 초기 준비나 가정들을 쉽게 만들수 있는 도구를 제공하여, 웹 어플리케이션 프로그래밍을 더 쉽게 만들수 있도록 설계 되어 있습니다. 레일즈는 다른 언어와 프레임웍에 비해서 더 적은 코드로 작성됩니다.

레일즈는 주장이 확실한 소프트웨어 입니다. 레일즈는 "최고"의 방법을 가정하고, 그러한 방법을 격려하도록 설계되어 있습니다. 여러분이 “레일즈의 방법(The Rails Way)” 배우면, 아마도 굉장한 생산성 향상을 발견하실 겁니다.


## 학습 목표
Ruby On Rails 를 통해서 MVC 패턴을 배우고, 웹 개발에 대해서 이해한다.  
만들어 볼 프로젝트는 **전화번호부 만들기**입니다.

###프로젝트 시작하기
- c9.io 접속
- Ruby Workspace 로 프로젝트 생성
- README.rdoc 제거
※ c9 에서는 ruby 선택시 자동으로 빈 레일즈 프로젝트를 만들어주지만, 본래 프로젝트 생성 명령어는 다음과 같습니다.
`rails new ProjectName(임의의 이름)`

###서버 구동
 - c9.io 경우 중앙 최상단의 Run Project 버튼을 누르시면 됩니다.
 - 그 후 터미널에 나오는 주소를 클릭하여 접속하시면 됩니다.(약간의 시간이 소모 될 수 있습니다.)
 ※ c9 에서는 버튼 클릭 한 번으로 서버 구동이 가능하지만, 본래 서버 구동 명령어는 다음과 같습니다.
`rails s`

###MVC 패턴(모델, 뷰, 컨트롤러)
Ruby On Rails 를 비롯한 다양한 웹 프로젝트들은 MVC 패턴을 따릅니다.  
MVC 패턴은 Model, View Controller 를 의미하며 각자의 역할은 다음과 같습니다.  
- Model(모델) : 데이타베이스와 그 데이터에 해당되는 다양한 조건을 정의
- View(뷰) : 모델에 있는 데이터를 기반으로 사용자 인터페이스의 생성을 담당
 - Html 파일이라고 생각하셔도 좋습니다.
- Controller : 모델과 뷰의 중계 역할 ➝ 클라이언트로부터 요청을 받아 모델과 상호작용 ➝ 적절한 뷰를  보여줌

### 컨트롤러 생성하기
Ruby On Rails 제대로된 작업을 시작해보도록 합니다. 먼저 MVC 패턴 중 컨트롤러를 생성하도록 하겠습니다. 명령어의 형식은 다음과 같습니다.  
`rails g controller ControllerName(임의의 이름)`

저희가 만들어볼 프로젝트는 전화번호부이기 때문에 컨트롤러의 이름을 **Contact**라고 짓겠습니다. 따라서 명령어는 다음과 같습니다.  
`rails g controller contact`

### 컨트롤러의 액션 만들기
다음과 같이 컨트롤러 파일이 생겼습니다. `app/controllers/contact_controller.rb`  
```ruby
class ContactController < ApplicationController
   def index 
   end       
end
```
위와 같이 코드를 수정합니다. contact_controller 에 index 라는 액션을 생성했습니다.  
액션은 클라이언트로부터 요청을 받고 이를 처리하는 컨트롤러의 컴포넌트 단위라고 생각하시면 됩니다.  
예를 들면 유저가 `www.mysite.com(임의의 주소)` 으로 접근했을 때 클라이언트는 해당 경로로 요청을 보내고, 루비온레일즈에서는 이 요청을 받아들이고, 특정 **액션**으로 보내 해당 요청을 처리하게 만듭니다.

### 액션에 대응하는 뷰파일(html.erb) 생성하기
뷰(View)는 클라이언트에 보여지게 되는 웹페이지 입니다. 지금까지 배웠던 html 파일과 거의 동일하다고 생각하시면 됩니다.  
html 이 아닌 html.erb 파일라는 차이점이 있다는 것을 일단은 알아두시면 됩니다.

`app/views/contact` 폴더는 contact 컨트롤러의 뷰파일들을 관리하는 폴더입니다.  
먼저 해당 폴더에 index.html.erb 파일을 만들어주세요.  
그리고 그 후에 다음과 같이 간단한 html 코드를 입력해봅시다.

**app/views/contact/index.html.erb**
```html
<h1> contact 컨트롤러 index 액션의 뷰파일입니다.</h1>
```
`<html>, <title>, <head>, <body>` 같은 태그를 쓰지 않았습니다.  
Ruby On Rails 에서는 layout 파일이 별도로 존재하기 때문에 사용하지 않아도 됩니다.
layout 파일의 위치는 다음과 같습니다. `app/views/layout/application.html.erb`

※ 아직 자세히 설명하지는 않겠지만, `<%= yield %>` 라는 코드가 있는 곳에 `index.html.erb` 파일의 내용이 삽입되게 됩니다.

### 경로 명시해주기
컨트롤러를 만들고, index 액션을 만들었습니다. 그리고 그에 대응하는 index.html.erb 라는 뷰파일 또한 만들었습니다.  
다음으로 해야할 것은 `config/routes.rb` 파일에 경로를 명시해주는 것입니다.  
Ruby On Rails 에서 routes.rb 파일의 역할은 특정 경로를 컨트롤러의 액션에 매칭시켜서, 그 특정 경로로 클라이언트가 접속했을 때 그 요청을 매칭되어 있는 액션에서 처리하게 됩니다.  
저희 같은 경우에는 만든 index 액션에서 요청을 처리하도록 해야겠죠.

```ruby
Rails.application.routes.draw do
  get '/' => 'contact#index' 
  ...
  ...
  ...
  (생략...)
```

위와 같이 코드를 수정합니다. '/' 는 일반적으로 사이트의 접근했을 때의 경로를 의미합니다.  
(예시 :  '/' -> www.naver.com, '/abc' -> www.naver.com/abc)

'/' 경로로 요청이 들어왔을 때 contact 컨트롤러 index 액션에서 이를 처리하도록 경로를 지정해주었습니다.
형식은 다음과 같습니다. `HttpType(get, post 등) '경로' => '컨트롤러명#액션명'` 
[HttpType 참고자료](http://blog.outsider.ne.kr/312)

### 확인하기
이제 서버의 URL 로 가서 확인해보면 index.html.erb 파일에 작성했던 `<h1>` 태그의 내용이 보이는 것을 알 수 있습니다.  
저희가 지금까지 했던 작업들에 대해서 정리해보도록 합니다.  
- 프로젝트 생성
 - 컨트롤러 생성(contact)
 - 액션 생성(index)
 - index 액션과 대응하는 뷰파일 생성(index.html.erb)
 - 클라이언트로부터 요청이 왔을 때 index 액션에서 요청을 처리할 수 있도록 경로를 지정(routes.rb 파일에서 작성)
위 과정들을 수정했을 때 자신이 원하는 페이지가 나타나도록 할 수 있다는 걸 알 수 있습니다.

### 모델 생성하기
기본적인 페이지를 띄우는 데에 성공했습니다. 다음은 데이터베이스를 생성해보도록 합니다.  
MVC 패턴 중 데이터베이스와 관련된 일을 하는 건 모델입니다. 모델을 생성하는 명령어는 다음과 같습니다.  
`rails g model mdoelName(임의의 이름)`

처음으로 만들 것은 전화번호부에 저장할 Contact 입니다.  
아래의 명령어로 Contact 모델과 마이그레이션 파일을 생성하도록 합니다.
※ 마이그레이션 파일에 대한 설명은 다음 스텝에서. 하도록 하겠습니다.  
`rails g model contact`

### 마이그레이션 파일과 모델 파일
Contact 모델을 만들면서 생긴 것은 모델 파일(`app/models/contact.rb` 와 마이그레이션 파일(`db/migrate/dateinfo...create_contacts.rb`) 입니다.  
모델 파일은 데이타베이스와 그 데이터에 해당되는 다양한 조건과 기능들을 정의하는 파일입니다.  
마이그레이션 파일은 데이터베이스를 설계하는 파일입니다. 주로 어떤 이름을 가질 것인지, 어떤 규칙을 부여할 지 정하는 파일입니다.  

### Contact 테이블 설계하기
설계할 Contact 테이블은 다음과 같은 요소를 가지고 있어야 합니다.  
이름(name)과 성별(gender) 그리고 전화번호(phone_numer) 입니다.  

**설계**

| 이름       | 성별       | 번호         |
| ---------- | ---------- | ------------ |
| 최○○       | 남자       | 010-○○○○-○○○○|
| 김○○       | 여자       | 010-○○○○-○○○○|
| 이○○       | 남자       | 010-○○○○-○○○○|

**db/migrate/날짜...create_people.rb**
```ruby
class CreateContacts < ActiveRecord::Migration
  def change
    create_table :contacts do |t|
      t.string :name         
      t.string :gender       
      t.string :phone_number 
      t.timestamps null: false
    end
  end
end
```
위와 같이 데이터베이스 테이블의 항목을 정의할 수 있습니다. 형식은 다음과 같습니다.  
`t.데이터타입 :항목이름` => 데이터 타입은 string(문자열), integer(숫자), text(많은 문자열) 등이 있습니다.

### 데이터베이스 생성하기
마이그레이션 파일을 작성했으면, 이제 마이그레이션 파일에 정의한 내용대로 데이터베이스를 생성할 차럐입니다.  
`rake db:migrate` 명령어를 통해서 데이터베이스를 생성할 수 있습니다.  
`rake db:drop` 명령어를 통해서 데이터베이스를 삭제할 수 있습니다.

### 컨트롤러 액션 추가, 경로 지정하기
이번 프로젝트에서 만들 기능은 크게 두 가지입니다.  
- 데이터베이스의 저장되어 있는 Contact 테이블의 정보들을 클라이언트에 보여주는 기능.
- 정해놓은 특정 Form 형식에 입력하고, 그 내용대로 Contact 테이블에 저장하는 것.

먼저 routes.rb 에 경로를 지정하도록 합니다. `resources` 라는 것을 이용해볼 것 입니다.
`resources`는 레일즈에서 지원하는 것으로서 이미 정해져 있는 경로를 생성해주는 역할을 합니다.  
`HttpType '경로' => '컨트롤명러#액션명'` 과 같은 경로들을 여러개 생성해줍니다.

**`config/
```ruby
Rails.application.routes.draw do
  get '/' => 'contact#index'
  resources :contact 
  ...
  ...
  ...
  (생략...)
```

resources 에 대해서 좀 더 쉽게 이해하기 위해서 사용하기 전과 사용한 후의 비교를 해보도록 합니다.  
`rake routes` 명령어를 통해서 경로들을 확인해볼 수 있습니다.

**resources 사용 전**
```
Prefix Verb URI Pattern Controller#Action
       GET  /           contact#index
```
**resources 사용 후**
```
       Prefix Verb   URI Pattern                 Controller#Action
              GET    /                           contact#index
contact_index GET    /contact(.:format)          contact#index
              POST   /contact(.:format)          contact#create
  new_contact GET    /contact/new(.:format)      contact#new
 edit_contact GET    /contact/:id/edit(.:format) contact#edit
      contact GET    /contact/:id(.:format)      contact#show
              PATCH  /contact/:id(.:format)      contact#update
              PUT    /contact/:id(.:format)      contact#update
              DELETE /contact/:id(.:format)      contact#destroy
```

### 기능에 맞춰서 액션 만들기
contact 에 액션을 생성할 것입니다. index 액션은 이미 있으니, new 액션과 create 액션을 새로 추가하도록 합니다.  
```ruby
class ContactController < ApplicationController
    def index
    end
    
    def new     
       @contact = Contact.new 
    end        
    
    def create 
    end        
end
```
- index 액션  : Contact 테이블의 정보를 보여줄 페이지.  
- new 액션    : Contact 데이터들을 입력할 페이지.
 - Contact.new(형식 : 모델명.new) 는 테이블의 새로운 데이터를 만들 때 사용하는 메소드입니다. name, gender, phone_number 등의 값들은 비어져 있는 상태입니다. 
- create 액션 : 새로운 Contact 데이터를 생성할 페이지.

### new page 만들기
※ new 액션의 경로는 resources 에 의해서 정의된 대로 '/contact/new' 입니다.
일단 뷰파일이 없으니 새로 만들어 주도록 합니다. (`app/views/contact/new.html.erb`)  
```erb
<h1>전화번호 추가</h1>
<%= form_for @contact, url: {action: "create"} do |f| %>
 <label>Name: </label>
 <%= f.text_field :name %><br>
 <label>Gender: </label>
 <%= f.text_field :gender %><br>
 <label>Phone Number: </label>
 <%= f.text_field :phone_number %><br>
 <%= f.submit %>
<% end %>
```
form_for 라는 rails helper 을 이용해여 만듭니다.  
위 코드는 다음과 같은 html 코드를 생성해냅니다.
```html
<form class="new_contact" id="new_contact" action="/contact" accept-charset="UTF-8" method="post">
 <input name="utf8" type="hidden" value="✓">
 <input type="hidden" name="authenticity_token" value="uD3eyX6maEHkSKf4wHeRKS0xvummBe72n2Rzfn2Jks3kd20ccvAmsxRmEmJif7ID9Mh2CtsL9SlVX6Cj4Uaqkg==">
 <label>Name: </label>
 <input type="text" name="contact[name]" id="contact_name"><br>
 <label>Gender: </label>
 <input type="text" name="contact[gender]" id="contact_gender"><br>
 <label>Phone Number: </label>
 <input type="text" name="contact[phone_number]" id="contact_phone_number"><br>
 <input type="submit" name="commit" value="Create Contact">
</form>
```
※ `authenticity_token` 은 보안에 필요한 값입니다.
### create 액션 작성하기
```ruby
class ContactController < ApplicationController
    def index
    end
    
    def new
        @contact = Contact.new
    end
    
    def create
        name = params[:contact][:name] 
        gender = params[:contact][:gender] 
        phone_number = params[:contact][:phone_number] 
        Contact.create(name: name, gender: gender, phone_number: phone_number) 
        redirect_to '/'
    end
end
```
전송된 데이터로 Contact 테이블의 데이터를 생성하고, 그 후에 '/' 경로로 보냅니다.

### index 액션에서 Contact 테이블의 모든 데이터 보여주기
```erb
<h1> contact 컨트롤러 index 액션의 뷰파일입니다.</h1>

<%= link_to '새 전화번호 등록', new_contact_path %> 

<h3>전화번호부 목록</h3> 

<% @contacts.each do |contact| %> 
name : <%= contact.name %><br> 
gender : <%= contact.gender %><br> 
phone_number : <%= contact.phone_number %><br> 
<% end %> 
```
each do 반복문을 이용해서 controller 에서 선언한 @contacts 변수를 이용하여 모든 데이터를 뿌려줍니다.

###과제

토커봇 : https://github.com/kwangkuk0821/talker - CR(Create, Read)
