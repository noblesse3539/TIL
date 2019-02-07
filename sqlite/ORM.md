# ORM

## [flask-sqlalchemy](http://flask-sqlalchemy.pocoo.org/2.3/)

* 파이썬에서 사용하는 orm.

### 1. 기본 설정

``` bash
$ pip install flask_sqlalchemy flask_migrate // 한번만 작성하면 되는 설치하는 과정
```


app.py

``` python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///db_flask.sqlite3'
db = SQLAlchemy(app)

migrate = Migrate(app, db)
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return f'{self.id}: {self.username}'
```


### 2. flask db 설정

   * 초기 설정(`migration` 폴더 생성)

   ``` bash
   $ flask db init
   ```

   * migration 파일 생성

   ``` bash
   $ flask db migrate
   ```

   * db 반영

   ``` bash
   $ flask db upgrade
   ```



### 3. python으로 DB 조작하기

​	CRUD(Create , Read, Update, Delete)

* Create:

```python
user = User(username='재찬', email='lee@lee') 
db.session.add(user) 
db.session.commit()
```

* Read:

``` python
# 모든 값을 가져온다.
users = User.query.all()
User.query.filter_by(username='병석').all()
# get 메소드는 primary key로 지정된 값을 통해 가져온다.
user = User.query.get(1)
# 특정 컬럼의 값을 가진 것을 가져오려면 다음과 같이 쓴다.
user = User.query.filter_by(username='이재찬').all()
user = User.query.filter_by(username='이재찬').first()
```

* Update:

``` python
u1 = User.query.get(2)
u1.username = 'opalcat'
db.session.commit()
```

* Delete:

``` python
user = User.query.get(1)
db.session.delete(user)
db.session.commit()
```





암호화 sha256

``` bash
$ pip install werkzeug
```

python

```python
from werkzeug.security import generate_password_hash, check_password_hash

a = 'hihi'
# 암호화
hash = generate_password_hash(a)
print(hash)
# 차이점 확인
check_password_hash(hash, 'hihi')
check_password_hash('hihi', hash)
```



