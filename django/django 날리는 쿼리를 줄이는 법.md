# django 날리는 쿼리를 줄이는 법

``` python
from djnago.db.models import Prefetch

# comment_set 과 관련된 것을 for문 등을 돌려 처리하려할 때!
boards = Board.objects.all() # 비효율
boards = Board.objects.prefetch_related('comment_set').all() # 좀 더 효율적!

followings = user.followings.prefetch_related(
						Prefetch('score_set',
							query_set=Score.objects.order_by('-value'),
							to_attr='score_set_value_order'
						))
```

``` jinja2
{% for user_follow in followings %}
	<p>{{ user_follow.score_set_value_order.first.movie.title }}
{% endfor %}

근데 이것마저도 쿼리를 여러번 날리기 때문에 이것도 줄인다면

```

``` python
from djnago.db.models import Prefetch

boards = Board.objects.all() # 비효율
boards = Board.objects.prefetch_related('comment_set').all()

followings = user.followings.prefetch_related(
					Prefetch('score_set',
						query_set=Score.objects.select_related('movie').order_by('-value'),
						to_attr='score_set_value_order'
			)
```



# annotate

컬럼을 추가해서 값을 넣어놓는 것.



# prefetch_related

1:N, M:N -> N개를 미리 가져올 때(JOIN table)



# select_related

1:N -> 1개를 미리 가져올 때(JOIN)



# aggregate

오브젝트를 갖고 오는게 아니라 계산된 값만 갖고 올 때 사용함!