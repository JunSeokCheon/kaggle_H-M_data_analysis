# :womans_clothes: 캐글 H&M 쇼핑몰 데이터 분석 :womans_clothes:  
- - -
<h1>Intro</h1> 

- - -
- - -
**캐글 H&M 쇼핑몰 데이터 분석** 내용을 정리한 레포입니다.  
엘리스 AI 트랙 2차 프로젝트인 데이터 분석 웹 서비스 프로젝트에서 자유 주제로 캐글 h&m 데이터 분석을 통하여 추천 쇼핑몰 구현하는 프로젝트에서 데이터 분석 부분만 정리했습니다.

- - -

- 이번 레포는 모델링 작업이 들어가지 않고, 크게 데이터 전처리 / 데이터 준비 및 가공 / 데이터 분석으로 구성되어 있습니다.
- 캐글 h&m 데이터 분석을 통하여 추천 쇼핑몰 구현하는 프로젝트는 백엔드/프론트엔드의 홈쇼핑 구현이 메인입니다.
- 백엔드/프론트엔드에서 필요한 정보들을 데이터 전처리를 통하여 가공하고 준비해서 넘겨줍니다.
- H&M 데이터 분석을 통해서 연령대/성별을 추정하여 그에 맞는 TOP10 제품 데이터를 가공해서 넘겨줍니다.
- 연령대/성별에 맞는 TOP10 제품이 어떤 종류/유형이 있는지 시각화를 통해서 그래프를 그려서 넘겨줍니다. ( + 분기별 인기 상품 등) 
- 각 파일은 google colab 환경에서 개발을 진행했고, 파일마다 상세한 주석과 정리를 수행했습니다.


- - -

<h3>데이터 전처리</h3>

<h4>del_noimage_underwear_swimwear.ipynb</h4>
  
- 제품과 제품의 구매이력들의 정보는 있으나, 해당하는 이미지가 없는 데이터들이 존재해서 데이터 전치리 요구됩니다.
- 이미지가 없는 데이터의 article_id를 리스트에 저장 후, articles.csv/transactions.csv에 해당 상품 제거합니다.
- 이미지 중에 underwear(bra, Underwear bottom 등)와 swimwear에 해당되는 상품들은 articles.csv/transactions.csv에 상품 제거합니다.
- transactions 파일이 데이터(2천만개)가 있어서 처리하는데 곤란하여 2020-04 ~ 2020-06 데이터만 사용하기로 결정합니다.


<h4>del_young_kid_sports.ipynb</h4> 
  
- 성별을 판단할 때, 해당 제품이 어떤 유형(Ladieswear, Baby/Children, Divided, Menswear, Sport)인지 보고 구매이력에서 해당 제품을 많이 구매한 기준으로 성별을 특정합니다.
- Ladieswear와 Menswear를 제외한 유형은 성별을 판단하는데 혼동을 준다고 판단하여 제거합니다.
- 이 작업을 데이터 전처리 과정에서 실행하면 나중에 다른 유형의 분포를 볼수가 없고, 확장성이 떨어진다고 생각하여 전체 유형으로 특정하여 저장해서 필요한 정보들만 따로 저장하는 과정을 거칩니다.



<h3>데이터 준비 및 가공</h3>

<h4>category_data_extraction.ipynb</h4>
  
- 추천 상품이 아닌, 쇼핑몰의 기본 상품을 위해서 데이터를 준비하고 가공하는 작업을 진행합니다.
- 회의를 거쳐 여러 가지 상품중에서 일반적이고 데이터가 많은 셔츠(T-shirt) / 니트(Sweater) / 청바지(Trousers) / 치마(Skirt) / 신발(Sneakers) 종류 선정합니다.(확장 가능)
- transactions 파일이 데이터(2천만개)가 있어서 처리하는데 곤란하여 2020-04 ~ 2020-06 데이터만 사용하기로 결정합니다.
- articles.csv/transactions.csv에서 필요한 컬럼들을 merge/split 진행하여 각 제품의 article_id, 제품 이름, 제품 유형, 제품 색깔, 제품의 상세 설명, 가격데이터를 json 형태로 저장하고, 그에 맞는 이미지도 함께 저장하여 백/프론트로 넘겨줍니다.
- price를 원(₩)화로 변경합니다.

<h4>visualization.ipynb</h4>

**plotly 그림이 안보이는 오류가 있어서 맨 위 google colab 링크를 첨부했습니다**

- customers.csv/articles.csv/transactions.csv 각각의 컬럼들에 대하여 시각화 진행합니다.
- 연령대/성별 TOP 5~10 제품 유형 비교 시각화(필수)
- 분기/계절별 인기 상품 시각화(확장)
- 연령대 별 선호하는 색 시각화(확장)
- 계절 별 buyer 유형 시각화(확장)

<h4>age_sex_estimation_data_extraction.ipynb</h4>

- 추천 상품에 대한 데이터를 준비하고 가공하는 작업을 진행합니다.
- 셔츠(T-shirt) / 니트(Sweater) / 청바지(Trousers) / 치마(Skirt) / 신발(Sneakers) 카테 고리별로 데이터를 선정합니다.
- 위 카테고리 제품의 article_id, 제품 이름, 제품 유형, 제품 색깔, 제품의 상세 설명, 가격데이터, 해당 연령대, 남성/여성 를 json 형태로 저장하고, 그에 맞는 이미지도 함께 저장하여 백/프론트로 넘겨줍니다.
- price를 원(₩)화로 변경합니다.


<h3>데이터 분석</h3>

<h4>age_sex_estimation.ipynb</h4>
  
- 나이 분포를 확인하고, 연령대를 구분합니다. (0 - 16~19, 1 - 20-29, 2 - 30-39, 3 - 40-49, 4 - 50-59, 5 - 60-)
- transactions 정보를 확인하고 해당 손님이 어떤 유형(Ladieswear, Baby/Children, Divided, Menswear, Sport)을 많이 샀는지 파악하여 연령을 추정합니다.
- 유형별로 최대 count가 같다면 애초에 여성 데이터가 많기 때문에 여성으로 판단했습니다.
- transactions 파일이 데이터(2천만개)가 있어서 처리하는데 곤란하여 2020-04 ~ 2020-06 데이터만 사용하기로 결정합니다.
- customers.csv/articles.csv/transactions.csv에서 merge/split 진행하여 연령대/유형별 article_id 리스트 데이터 프레임을 만들었습니다.
- 연령대/유형별 TOP 10 제품의 article_id, age_id, attribute 데이터 프레임을 저장합니다.

- - -
