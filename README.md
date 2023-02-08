**ARS Consulting Customer Feedback Classification Model with KoBERT and LSTM**  
KoBERT와 LSTM 기반 ARS 상담 고객 피드백 분류 모델 제안
---
2021 S사에서 주관한 [ARS 상담 고객 피드백 분류 ]에 참가하였습니다.  

OVERVIEW
---
ARS 상담시스템을 운영하는데 있어 소비자의 피드백을 유형화하여  
문제 발견 및 개선하고자 피드백 분류 모델을 이용하여 자동화된 분류 프로세스를 제안하였습니다.  
한국어 기반 데이터셋에 대하여 높은 분류 정확도를 보이는 transfer learning 중 하나인 KoBERT를 이용하였으며  
LSTM model 또한 사용하여 S사 고객 피드백 분류 모델을 만들어보았습니다.  

PROBLEMS
---
- **다양한 비문들로 구성된 데이터셋**  
'상담원연결시간이너무길고.' , '통화대기시간 이 너무길다' 등 다양한 비문들로 구성되어있는 데이터셋입니다.  
맞춤법 교정, 불용어 등을 처리하는 preprocessing 작업에 많은 시간을 투자하여 해결하고자 노력하였습니다.  

- **다양한 class의 수**  
분류해야하는 label은 대부분 3단계로 이루어져있습니다. '칭찬>고객서비스>상담원' 이렇게 이루어져있으나  
'칭찬>S사카드>XXX'의 경우 칭찬&삼성카드로 분류된 데이터셋을 대상으로  
분류해야하는 class의 수는 16개로 class의 가짓수가 많은 데이터셋입니다.  
KoBERT의 경우 분류할 수 있는 class의 개수를 16개로 설정하였을 때 오류가 발생하는 문제점을 발견하여  
가짓수가 많은 분류의 경우 LSTM model을 활용하여 분류를 진행하였습니다.  

- **복문처리**  
'A사카드는 상담사 연결시간은 짧아서 좋았습니다 반면 S사카드는 넘 기네요'와 같이 2가지 문장으로 구성된  
복문이 존재하였습니다. 복문을 1개의 문장씩으로 분리하여 S사카드와 관련된 피드백 유형만을 분리하고자 하였지만  
정확도가 높은 복문분류를 진행하지 못하여서 아쉬움이 많이 남았습니다..  

FINAL MODEL
---
<p align="center"><img src="https://user-images.githubusercontent.com/75806377/217184808-04f0c2c7-da75-45c7-aa3d-2224f899d427.png" height="600px" width="800px"></p>  

Class 수가 많은 3차 분류 모델(2), 3차 분류 모델(5)는 LSTM model을 사용하였으며  
나머지 분류의 경우 KoBERT를 활용하여 모델링을 진행하였습니다.

Limitations
---
복문처리를 미해결한 점이 아쉬웠던 프로젝트였습니다.  
preprocessing에 많은 시간을 투자하여서 적절한 균형있는 모델을 설계하지 못한 점이 아쉬웠으며  
2개 이상의 문장이 존재하는 발화를 분리하거나 혹은 sklearn의 predict_prob와 비슷하게  
어떤 class에 속할 확률이 높은지 산출하여 class만 분류하였더라도 더 좋은 결과를 얻을 수 있지 않았나 싶습니다.  
