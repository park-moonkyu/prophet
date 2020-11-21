#  Prophet(Facebook)을 통한 시계열 분석 정리

![zz](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9904793B5B1BCF471B) </br></br>

아래 Facebook에서 제공하는 docs를 가시면 더욱더 자세하게 해당 내용을 익힐수 있다. </br>
<https://facebook.github.io/prophet/docs/quick_start.html>
 
# Introduction
우선 Time Series(시계열) 분석을 할때는 다양한 모델들이 쓰인다. 우선 가장많이쓰이는 뉴럴넷 기반의 LSTM 같은 Sequential 모델 뿐만 아니라, ARIMA , Prophet 등등이 있을것이다.<br>
그중 통계적 지식이 없는 실무자들도 가장 접근하기 쉬운 페이스북에서 만든 Prophet으로 다양한 데이터를 가지고 실습을 해보았다. <br>
결론부터 말하면 쓰기 엄청 쉽다  정확도가 생각보다 높으며 파라미터로 모델 수정이 용이하다.<br>
하지만, 확실히 내가 느끼는 한계를 공유하려고 한다. <br>
1. 데이터가 일단위 데이터가 있어야한다. <br>
2. 어느정도 노이즈는 괜찮지만 갑자기 너무나 다른 경향을 띄는 데이터에 대해선 오차가 심하다.<br>
첨언으로 나의 경우에는 리테일 매출 예측을 Prophet으로 돌려보았지만 코로나사태이후에 매출으로 계절성이나 트렌드가 무너지는 현상이 발생했다. <br><br><br>

# Table of content
 
1. Prophet 이란 ?
3. 레퍼지토리안에있는 코드를 통한 실제 예제 실습

# what is Prophet ?

Prophet은 페이스북에서 공개한 시계열 예측 라이브러리이다.<br>
Prophet의 주요 구성요소는 Trend, Seasonality, Holiday 이다.<br>
<br>
## y(t) = g(t) + s(t) + h(t) + ei 
### g(t) = piecewise linear or logistic growth curve for modeling non-periodic changes in time series 
### s(t) = periodic changes (즉, Weekly, yearly, seasonality)
### h(t) = effects of holidays(user provided) with irregular schedules
### ei : error term accounts for any unusual changes not accommodated by the model 

쉽게 말하면 다음과 같다.<br>
g(t) = 주기적이지 않은 트렌드를 보여준다. 선형 또는 logistic 곡선을 이룬다. <br>
s(t) = weekly, yearly 등의 주기적인 패턴을 말한다. <br>
h(t) = 휴일과 같은 불규칙한 이벤트들을 말한다 .<br>
만약 특정 기간에 값이 비정상적으로 증가 또는 감소했다면 holiday로 정의하여 모델에 반영할수 있다.<br>

마지막으로 ei는 정규분포라고 생각한 오차이다. <br>


# 그럼 레퍼지토리의 코드들로 실제 실습을 해보자.

