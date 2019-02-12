# C9 setting

## 1. pyenv 설정

> pyenv는 하나의 컴퓨터 내에서 여러가지 버전의 python을 활용할 수 있도록 버전관리를 도와준다.
>
> pyenv global : 전체 전역 파이썬 버전 설정
>
> pyenv local: 해당 디렉토리 파이썬 버전 설정

```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc

source ~/.bashrc
pyenv install 3.6.7
pyenv global 3.6.7
python -V
pip install --upgrade pip
pip install flask
pip install requests

```

## 2. pyenv-virtualenv

> virtualenv는 독립적인 가상환경을 제공해준다.
>
> 가장 많이 활용되는 3가지 라이브러리는 다음과 같다.
>
>  	1. pyenv-virtualenv: pyenv의 플러그인
>  	2. virtualenv
>  	3. conda : 데이터 사이언스/머신러닝/딥러닝

``` powershell
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
exec "$SHELL"
```

### 실행

``` powershell
pyenv virtualenv 3.6.7 (가상환경 이름)
pyenv local (가상환경 이름)
```



```powershell
pip install flask	(플라스크 설치할 경우)
pip install django	(장고 설치할 경우)
pip freeze > req.txt
```

라이브러리의 충돌을 방지하기 위해 설정함!

req.txt에 내가 사용하는 환경이 저장됨. 이걸 다른사람에게 전달해서 버전을 일치시키도록?





서버를 실행시키기 위해선 아래와 같이 해야하지만,

```powershell
$ flask run -h $IP -p $PORT
```

(로컬에선)

```python
$ FLASK_APP=hello.py flask run
```







python a.py를 통해 서버를 실행시키기 위해서 추가해야하는 코드

```python
if __name__ == '__main__':
    app.run(host='0.0.0.0', port='8080', debug=True)
```

c9는 포트를 8080만 사용할 수 있게 막아놓았다.



return 을 html로 하기 위해선  render_template, 요청을 받기 위해선 request

```python
from flask import render_template, request
    
@app.route('/hi/<string:name>')
def greeting(name):
    return render_template('greeting.html', html_name=name)
```



## 3. Git

> c9은 기본적으로 workspace에서 git config가 가입한 이메일로 되어 있기 떄문에, github에 커밋 기록을 제대로 남기기 위해서 설정해준다.

```powershell
git config global --user.name _______
git config global --user.email ______
```

