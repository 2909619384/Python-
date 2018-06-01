

[TOC]
####1.flask第一个程序
	#从flask这个框架中导入Flask这个类
	from flask import Flask


​	
	#初始化一个Flask对象
	#需要传递一个参数__name__
	#传递该参数的目的1.方便flask框架去寻找资源
	#2.方便flask插件比如Flask-Sqlalchemy出现错误的时候，好去寻找问题所在的位置
	app = Flask(__name__)
	
	#@app.route是一个装饰器
	#@开头并且在函数上面，说明是装饰器
	#这个装饰器的作用，是做一个url与视图函数的映射
	#127.0.0.1:5000，去请求hello_world这个函数，然后将结果返回给浏览器
	@app.route('/')
	def hello_world():
		return '我是第一个Flask程序"
	
	#如果当前这个文件是作为入口程序运行，name就执行app.run()
	if __name__ == '__main__':
		#启动一个应用服务器，来接受用户的请求
		#while True:listen()
		app.run()

####2.设置debug模式
1.在app.run（）中传入一个关键字参数debug,如app.run(debug=True),就是设置当前项目为debug模式。
2.debug模式的两大功能：
  *当程序出现问题的时候，可以在页面中看到错误信息和出错的位置
  *只要修改了项目中的python文件，程序就会自动加载，不需要手动重启服务器。

####3.URL传参数
1.参数的作用：可以在相同的url，但是指定不同的参数来加载不同的数据
2.在flask中如何使用参数
			
			@app.route('/article/<id>/')
			def article(id):
				return 'id是:%s' % id
*参数需要放在两个尖括号中
*视图函数中需要放和url中的参数同名的参数
		
####4.反转url
1.什么叫反转url:从视图函数到url的转换叫做反转url
2.反转url的用处：
 *在页面重定向的时候，会使用url反转
  *在模板中，也会使用url反转
 3.常用反转函数redirect/url_for
实例如下：
			
			@app.route('/')
			def index():
				#使用反转url获取login函数的url地址
				#然后再使用redirect进行跳转
				#这样的好处：当login的url发生改变与否，只要函数名称不改变，我们就可以找到url
				login_url = url_for('login')
				return redirect(login_url)
				return '这是首页'
			
			@app.route('/login/')
			def login():
				return '这是登录页面'
			
			@app.route('/request/<is_login>/')
			def question(is_login):
			#定义一个参数is_login用来判断登录与否
			#当登录失败，返给用户登录页面
				if is_login = '1':
					return '这是发布问题的页面'
				else:
					return direct(url_for('login'))

####5.页面跳转和重定向

1.用处：在用户访问一些需要登录的页面时，如果用户没有登录，name可以让他重定向到登录页面

2.代码实现如下：	

```
	@app.route('/request/<is_login>/')
		def question(is_login):
		#定义一个参数is_login用来判断登录与否
		#当登录失败，返给用户登录页面
			if is_login = '1':
				return '这是发布问题的页面'
			else:
				return direct(url_for('login'))
```




####6.flask渲染jinjia2模板和传参
1.如何渲染模板：
	*模板放在‘templates’文件夹下
	*从flask中导入render_template函数
	*在视图函数中，使用render_template函数渲染模板。
	注意：只需要填写模板名字，不需要填写'templates这个文件夹的路径。
2.模板传参：
	*如果只有一个或者少量参数，直接在‘render_template函数中添加关键字参数就可以了
	*如果有多个参数的时候，那么可以先把所有的参数放在字典中，然后再添加到render_template中。使用两个型号，把字典转换为关键字参数传递进去。
	实例如下：
	
		@app.route（‘/’）
		def index():
			content = {
			'username':'美女',
			'gender':'男',
			'age':18
			}
			return render_template('index.html',**content)
		
		if __name__ == '__main__':
			app.run(debug=True)

3.在模板中，如果要使用一个变量，语法是{{ params}}

4.访问模型中的属性或者是字典，可以通过{{params.property}}的形式，或者是{{params['age']}}

	@app.route（‘/’）
	def index():
		class Person(objects):
			name = '美女'
			age = 18
		
		p = Person()
		content = {
	        'username':'美女',
	        'gender':'男',
	        'age':18,
	        'person':p
	        'websites':{
	            'baidu':'www.baidu.com',
	            'google':'www.google.com'
	        }
		}
		return render_template('index.html',**content)
	
	if __name__ == '__main__':
		app.run(debug=True)
HTML中部分代码：

```
<p>用户名：{{ username }} </p>

<p>性别：{{ gender}} </p>

<p>年龄：{{ age}} </p>

<hr>

<p>名字：{{ person.name}} </p>

<p>年龄：{{ person.age}} </p>

<hr>

<p>百度：{{ websites.baidu}} </p>

<p>谷歌：{{ websites.google}} </p>

或者：

<p>百度：{{ websites['baidu']}} </p>

<p>谷歌：{{ websites['google']}} </p>
```

#### 7.if判断

1.语法

```
{% if XXX %}

{% else %}

{% endif %}
```

2.使用方法和python差不多，具体使用如下：

```
@app.route('/<is_login>/')

def index(is_login):

	if is_login == '1':

		user = {

			'username':'小白'

			'age':18

			}

		return render_template('index.html', user)

	else:

		return render_template(index.html'')
```



```
{% if user %} #如果用户存在

	<a href="#">{{ user.username}}</a>

	<a href="#">注销</a>
{% else %}
	<a href="#">登录</a>

	<a href="#">注册</a>

{% endif %}

		
```

#### 8.for循环遍历列表和字典

1.字典的遍历，语法和python一样，可以使用items(),keys(),values(),iteritems(),iterkeys(),itervalues()

```
{% for k,v in user.items() %}
	<p>{{ k }}:{{ v }}</p>
{% endfor %}
```

2.列表的遍历：语法和python一样

用法一：

```
{% for website in websites %}    
	<p>{{  website }}</p>
{% endfor %}
```

用法二：

```
@app.route('/')
def hello_world():
    books = [
                {'author': '李白',
               'publish': '湖北',
    'price': '100'},
        {'author': '白居易',
         'publish': '湖南',
         'price': '120'},
        {'author': '张三丰',
         'publish': '武当',
         'price': '170'},

    ]
    
```

```
{% for book in books %}
    <tr>
        <td>{{ book.author }}</td>
    <td>{{ book.publish }}</td>
    <td>{{ book.price }}</td>

    </tr>

{% endfor %}
```

结果：

**作者    出版社  价格**

李白     湖北      100

白居易 湖南       120

张三丰   武当      170 



#### 9.过滤器

1.过滤器的作用：把原始的变量经过处理后再展示出来

2.default过滤器，语法：

```
{{  avatar|default('XXXX') }}
```

实例：如果用户传了图像，显示用户图像，否则，显示原图

```
@app.route('/photo/')
def user_photo():
    return render_template('index.html',avatar='https://avatar.cXXXX1XX9742.jpg')
```

```
<body>
<img src="{{ avatar|default('默认头像地址') }}" alt="">
</body>
```

3.length过滤器：求列表或者字符串或者字典。元祖的长度，语法：

实例：获取评论数

```
@app.route('/commentss/')
def user_comment():
    comments = [
        {'username':'小张',
         'com':'帅呆了'},
        {'username': '李白',
         'com': '李白的诗真好'},
        {'username': '李清照',
         'com': '怨妇'},
        {'username': '骆冰王',
         'com': '吃冰棒'},
    ]
    return render_template('index.html',comments=comments)
```

```
 <p>评论数:({{ comments|length }})</p>
{% for com in comments %}
    <li>
        <a href="#">作者:{{ com.username }}</a>
        <p>评论:{{ com.com }}</p>
    </li>
{% endfor %}
```

代码运行结果：

评论数:(4)

作者:小张

评论:帅呆了

作者:李白

评论:李白的诗真好

作者:李清照

评论:怨妇

作者:骆冰王

评论:吃冰棒

####10.数据库表的创建、增、删、改、

models.py中的代码：

	from flask_sqlalchemy import SQLAlchemy
		
		db = SQLAlchemy()
		
		class Student(db.Model):
			#创建学生表模型
			#s_id作为关键字，且是依次递增的整数
		    s_id = db.Column(db.Integer,primary_key=True, autoincrement=True)
		    #创建类型为string的s_name，且改名字唯一不能重复
		    s_name = db.Column(db.String(20), unique=True)
		    #创建为整形的学生年龄s_age，默认为18岁
		    s_age = db.Column(db.Integer, default=18)


			#在数据表中的表名设置为student
		    __tablename__ = 'student'

创建数据表：
					
					@stu.route('/createtable/')
					def create_db():
						db.create_all()
						return '创建成功'
####11.运算符
#####filter(模型名.字段.运算符（‘值’）),如：
	#查询姓名为火神的学生信息
	Student.query.filter(Student.s_name=='火神')

#####_lt__ 小于，用法：
	#查询年龄小于16岁的学生信息
	stus = Student.query.filter(Student.a_age.__lt__(16))

#####__le__ 小于等于
	#查询年龄小于等于16岁学生的信息
	stus = Student.query.filter(Student.a_age.__lt__(16))

#####__gt__ 大于
	 #查询年龄大于16岁的学生信息
	stus = Student.query.filter(Student.a_age.__gt__(16))

##### __ge__ 大于等于
	#查询年龄大于等于16岁的学生信息
	stus = Student.query.filter(Student.a_age.__ge__(16))

#####in_ 在范围内

	#年龄在16,1,20，34,23,32
	stus = Student.query.filter(Student.s_age.in_([16,1,20,34,23,32]))

#####order_by 排序
	#按照id降序排列
	stus = Student.query.order_by('-s_id')

#####limit 截取几个信息
	 #按降序获取3个
	 stus = Student.query.order_by('-s_id').limit(3)

#####offset 跳过几个信息
	 #跳过3个数据
	 stus = Student.query.order_by('-s_age').offset(3)

#####get 获取主键对应的信息
	 #获取id等于24的学生，两种方法
	 stus = Student.query.filter(Student.s_id==24)
	 stus = Student.query.get(24)

#####and_ 并且条件
	# and_并且条件
	stus = Student.query.filter(and_(Student.s_age == 18, Student.s_name == '雅典娜'))

#####or_ 或者条件
	# or_或者条件
	stus = Student.query.filter(or_(Student.s_age == 18, Student.s_name == '火神'))

#####not_ 非
	#not_非
	Student.query.filter(not_(Student.s_age==18,Student.s_name=='火神'))


​		
​	   
####12.批量生成学生信息
	@stu.route('/createstusbyrange/')
	def create_random_stus():
	    stus_list = []  #创建一个空列表用来存储学生信息
	    for i in range(20):   #以下操作循环20次
	        stu = Student('小明%d' % random.randrange(10000),
	                      '%d' % random.randrange(30))
	        #生成小明+1到10000的随机数组成的姓名，年龄为1到30的随机数
	        stus_list.append(stu)  #将生成的学生信息追加到列表中
	    db.session.add_all(stus_list) #将所有的学生信息存储在数据库中
	    try:  #如果有错误，操作回滚，否则就执行
	        db.session.commit()
	    except:
	        db.session.rollback()
	    return '创建成功'

   将所有的学生对象存储在列表中，stus_list = [学生对象1，学生对象2,.........]。然后将所有的学生对象插入到数据库中db.session.add_all(stus_list)。以上插入信息的方式可以用在需要大量数据时的操作。只需要修改相应的参数，即可快速的获取到大量的数据。

####13.Flask-SQLAlchemy分页对象的属性
items      当前页面中的记录
query      分页的源查询
page       当前页数
prev_num    上一页的页数
next_num    下一页的页数
has_prev      是否有上页，返回True
has_next      是否有下页，返回True
pages            查询得到的总页数
total               查询返回的记录总条数


使用方法如下：
			
			总页数: {{ paginate.pages }}
			    <br>
			    一共{{ paginate.total }}条数据
			    <br>
			    当前页数：{{ paginate.page }}
			    <br>
			    {% if paginate.has_prev %}
			        <a href="/stupage/?page={{ paginate.prev_num }}">上一页</a>：{{ paginate.prev_num }}
			    {% endif %}
	
	{% if paginate.has_next %}
	    <a href="/stupage/?page={{ paginate.next_num }}">下一页</a>：{{ paginate.next_num }}
	{% endif %}
	<br>

####14. one_to_many
在one的model中定义relationship字段 
students = db.relationship('Student', backref='stu', lazy=True)

1）通过one找many，one的对象.students，结果为many的结果
2）通过many找one，many的对象.stu，结果为one的对象

####15.往数据库插入数据
	@stu.route('/stucourse/', methods=['GET','POST'])
	def stu_cou():
	    if request.method == 'GET':
	        stus = Student.query.all()
	        cous = Course.query.all()
	        return render_template('stu_cou.html', stus=stus, cous=cous)
	    else:
	
	    s_id = request.form.get('student')
	    c_id = request.form.get('course')
	    # 第一种
	    # sql = 'insert into sc(s_id, c_id) VALUES(%s %s)' % (s_id, c_id)
	    # db.session.execute(sql)
	    # db.session.commit()
	
	    #第二种
	    stu = Student.query.get(s_id)
	    cou = Course.query.get(c_id)
	
	    cou.students.append(stu)
	    db.session.add(cou)
	    db.session.commit()
	
	    return '插入成功'
####16.遇到的问题以及解决办法
![这里写图片描述](https://img-blog.csdn.net/20180523103746318?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQyMjk3NDI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
解决办法：删掉setting-project interpreter--show all中所有的原来的路径，重新选择正确的路径。保存后，等待路径加载成功再重新运行程序。



