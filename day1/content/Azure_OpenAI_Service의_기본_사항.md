# Azure OpenAI Service의 기본 사항

## 목차
- [Azure OpenAI Service의 기본 사항](#azure-openai-service의-기본-사항)
  - [목차](#목차)
  - [소개](#소개)
    - [OpenAI AI 모델의 기능](#openai-ai-모델의-기능)
  - [생성 AI란?](#생성-ai란)
  - [Azure OpenAI 설명](#azure-openai-설명)
    - [Azure OpenAI Service 소개](#azure-openai-service-소개)
    - [Azure OpenAI 워크로드 이해](#azure-openai-워크로드-이해)
    - [Azure OpenAI와 Azure AI 서비스의 관계](#azure-openai와-azure-ai-서비스의-관계)
  - [Azure OpenAI를 사용하는 방법](#azure-openai를-사용하는-방법)
    - [Azure OpenAI Studio](#azure-openai-studio)
      - [플레이그라운드](#플레이그라운드)
  - [OpenAI의 자연어 기능 이해](#openai의-자연어-기능-이해)
    - [자연어 생성을 위한 GPT 모델 이해](#자연어-생성을-위한-gpt-모델-이해)
      - [GPT 모델의 응답은 어떻게 표시되나요?](#gpt-모델의-응답은-어떻게-표시되나요)
    - [모델이 새 사용 사례에 적용되는 방법](#모델이-새-사용-사례에-적용되는-방법)
  - [OpenAI 코드 생성 기능 이해](#openai-코드-생성-기능-이해)
    - [코드 생성의 예](#코드-생성의-예)
    - [GitHub Copilot](#github-copilot)
  - [OpenAI의 이미지 생성 기능 이해](#openai의-이미지-생성-기능-이해)
    - [DALL-E](#dall-e)
    - [이미지 세대](#이미지-세대)
    - [이미지 편집](#이미지-편집)
    - [이미지 변형](#이미지-변형)
  - [Azure OpenAI의 액세스 및 책임 있는 AI 정책 설명](#azure-openai의-액세스-및-책임-있는-ai-정책-설명)
    - [Azure OpenAI에 대한 제한된 액세스](#azure-openai에-대한-제한된-액세스)
  - [연습 - Azure OpenAI Service 살펴보기](#연습---azure-openai-service-살펴보기)
  - [TODO : 실습자료 만들기](#todo--실습자료-만들기)
  - [요약](#요약)
  - [출처](#출처)
---
## 소개

뉴스의 최신 AI(인공 지능) 혁신에 대한 팀의 이해에 도움이 되고자 한다고 가정해 보겠습니다. 동료들은 이러한 혁신이 가져다주는 기회를 검토하고 AI의 발전을 윤리적으로 유지하기 위해 무엇을 해야 하는지 이해하고자 합니다.

오늘날 안정적인 AI 모델이 정기적으로 프로덕션에 투입되어 전 세계에서 상업적으로 사용되고 있다는 것을 팀과 공유하세요. 예를 들어 Microsoft의 기존 Azure AI 서비스는 지금까지 수년 동안 비즈니스의 요구 사항을 처리해 왔습니다. 2022년, AI 연구 기업 OpenAI는 ChatGPT로 알려진 챗봇과 DALL-E라는 이미지 생성 애플리케이션을 만들었습니다. 이러한 기술은 AI 모델을 통해 구축되었으며 자연어를 입력하면 기계가 만들었지만 마치 사람과도 같은 응답을 내놓습니다.

Azure OpenAI Service를 통해 사용자가 OpenAI 모델을 사용하여 엔터프라이즈급 솔루션을 빌드할 수 있다는 것을 팀과 공유합니다. Azure OpenAI를 사용하면 텍스트를 요약하고, 코드 제안을 받고, 웹 사이트에 대한 이미지를 생성하는 등의 작업을 수행할 수 있습니다. 이 모듈에서는 이러한 기능을 자세히 설명합니다.

### OpenAI AI 모델의 기능

OpenAI의 AI 모델에는 여러 범주의 기능이 있으며 그 중 세 가지는 다음과 같습니다.

| 기능     | 예제                                                      |
|--------|---------------------------------------------------------|
| 자연어 생성 | 예: 다양한 읽기 수준에 대한 복잡한 텍스트 요약, 문장의 대체 표현 제안 등             |
| 코드 생성  | 예: 한 프로그래밍 언어에서 다른 프로그래밍 언어로 코드 변환, 코드의 버그 식별, 문제 해결 등  |
| 이미지 생성 | 예: 텍스트 설명에서 발행물에 대한 이미지 생성 등                            |


---
## 생성 AI란?

OpenAI는 개발자가 ChatGPT와 같은 강력한 소프트웨어 애플리케이션을 구축할 수 있도록 AI 모델을 제공합니다. OpenAI 사이트에는 코드에서 텍스트를 생성하는 것과 같은 실용적인 것부터 무서운 이야기를 구성하는 것과 같은 순전히 재미있는 것까지 다양한 OpenAI 다른 예의 애플리케이션이 많이 있습니다.

OpenAI 모델이 AI 환경에 적합한 위치를 식별해 보겠습니다.

 - 인공 지능은 출력할 내용에 대한 명시적 지침 없이 머신에 의존하여 작업을 학습하고 실행함으로써 인간의 행동을 모방합니다.
 - 기계 학습 알고리즘은 기상 조건과 같은 데이터를 가져오고 모델을 데이터에 맞추어 특정 날짜에 매장에서 얼마나 많은 돈을 벌 수 있는지 예측합니다.
 - 딥 러닝 모델은 인공 신경망 형태의 알고리즘 계층을 사용하여 더 복잡한 사용 사례에 대한 결과를 반환합니다. 많은 Azure AI 서비스는 딥 러닝 모델을 기반으로 합니다. 기계 학습과 딥 러닝의 차이점에 대해 자세히 알아보려면 이 문서를 참조하세요.
 - 생성 AI 모델은 입력에 설명된 내용을 기반으로 새 콘텐츠를 생성할 수 있습니다. OpenAI 모델은 언어, 코드, 이미지를 생성할 수 있는 생성 AI 모델의 컬렉션입니다.

다음으로 Azure OpenAI가 사용자에게 Azure의 엔터프라이즈급 솔루션을 OpenAI의 동일한 생성 AI 모델과 결합할 수 있는 기능을 제공하는 방법을 알아봅니다.

---
## Azure OpenAI 설명

Microsoft는 OpenAI와 협력하여 다음 세 가지 주요 목표를 달성했습니다.

 - 보안, 규정 준수, 지역 가용성을 포함한 Azure의 인프라를 활용하여 사용자가 엔터프라이즈급 애플리케이션을 빌드할 수 있도록 지원합니다.
 - Azure AI 제품을 포함하여 Microsoft 제품 전반에 걸쳐 OpenAI AI 모델 기능을 배포합니다.
 - Azure를 사용하여 OpenAI의 모든 워크로드를 구동합니다.

### Azure OpenAI Service 소개
Azure OpenAI Service는 Microsoft와 OpenAI 간의 파트너십의 결과입니다. 이 서비스는 Azure의 엔터프라이즈급 기능과 OpenAI의 생성 AI 모델 기능을 결합합니다.

Azure OpenAI는 Azure 사용자가 사용할 수 있으며 다음 네 가지 구성 요소로 구성됩니다.

 - 미리 학습된 생성 AI 모델
 - 사용자 지정 기능 - 사용자 고유의 데이터로 AI 모델을 미세 조정할 수 있는 기능
 - 사용자가 AI를 책임감 있게 구현할 수 있도록 유해한 사용 사례를 감지하고 완화하는 기본 제공 도구
 - RBAC(역할 기반 액세스 제어) 및 개인 네트워크를 사용하는 엔터프라이즈급 보안

Azure OpenAI를 사용하면 Azure의 개인 네트워킹, 지역 가용성, 책임 있는 AI 콘텐츠 필터링을 활용하면서 Azure 서비스와 OpenAI로 작업 간에 전환할 수 있습니다.

### Azure OpenAI 워크로드 이해

일반적인 AI 워크로드에는 기계 학습, 컴퓨터 비전, 자연어 처리, 대화형 AI, 변칙 검색, 지식 마이닝이 포함됩니다.

Azure OpenAI는 다음과 같은 여러 생성형 AI 작업을 지원합니다.

 - 자연어 생성
   - 텍스트 완성: 텍스트 생성 및 편집
   - 포함: 텍스트 검색, 분류, 비교
 - 코드 생성: 코드 생성, 편집, 설명
 - 이미지 생성: 이미지 생성 및 편집

### Azure OpenAI와 Azure AI 서비스의 관계
```
2023년 7월부터 Azure AI 서비스는 이전에 Cognitive Services 및 Azure Applied AI Services로 알려진 모든 것을 포함합니다.
```

Azure AI 서비스는 AI 워크로드를 해결하기 위한 도구입니다. 사용하기로 선택한 서비스는 수행해야 하는 작업에 따라 달라집니다. 특히 Azure AI 언어 서비스와 Azure OpenAI Service 사이에는 번역, 감정 분석, 키워드 추출과 같은 몇 가지 중복 기능이 있습니다.

특정 서비스를 사용해야 하는 경우에 대한 엄격한 지침은 없지만 Azure AI 언어 서비스는 최소한의 튜닝(모델 성능 최적화 프로세스)이 필요한 널리 알려진 사용 사례에 사용할 수 있습니다. Azure OpenAI Service는 고도로 사용자 지정된 생성 모델이 필요한 사용 사례나 탐색적 연구에 더 유용할 수 있습니다.

```
Azure OpenAI 및 Azure AI 언어 서비스의 가격 책정은 다릅니다. 여기를 참조하세요.
```

어떤 유형의 모델을 사용할지 비즈니스적 의사 결정을 내릴 때는 기계 학습 훈련에 시간 및 컴퓨팅 요구 사항이 어떤 영향을 미치는지 이해하는 것이 중요합니다. 효과적인 기계 학습 모델을 생성하기 위해선 상당한 양의 정제된 데이터를 통한 모델의 훈련이 필요합니다. 훈련의 ‘학습’ 부분이란 컴퓨터가 데이터에 가장 적합한 알고리즘을 식별하는 것을 말합니다. 모델이 처리해야 하는 작업의 복잡성과 희망하는 모델 성능 수준은 모두 최적의 알고리즘에 필요한 가능성 있는 솔루션을 실행하는 데 걸리는 시간에 영향을 미칩니다.

---
## Azure OpenAI를 사용하는 방법

현재 Azure OpenAI에 액세스하려면 신청을 수행해야 합니다. 액세스 권한이 부여되면 다른 Azure 서비스와 마찬가지로 Azure OpenAI 리소스를 만들어 서비스에 사용할 수 있습니다. 리소스가 만들어지면 REST APIs, Python SDK 또는 Azure OpenAI Studio의 웹 기반 인터페이스를 통해 서비스를 사용할 수 있습니다.

### Azure OpenAI Studio
![](../img/azure-openai-studio-start.png)

Azure OpenAI Studio에서 AI 모델을 빌드하고 소프트웨어 애플리케이션에서 공개 사용하도록 배포할 수 있습니다. Azure OpenAI의 기능은 몇 가지 특정 생성 AI 모델을 통해 구현됩니다. 모델별로 각기 다른 작업에 최적화되어있습니다. 일부 모델은 요약 및 일반적인 비정형 응답을 제공하는 데 특화되어있고 다른 모델은 텍스트 입력에서 코드 또는 고유한 이미지를 생성하도록 빌드되었습니다.

이 Azure OpenAI 모델은 다음을 포함합니다.

 - 자연어 및 코드에 대한 최신 생성 모델을 나타내는 GPT-4 모델.
 - 프롬프트에 따라 자연어 및 코드 응답을 생성할 수 있는 GPT-3.5 모델.
 - 분석을 위해 텍스트를 숫자 벡터로 변환하는 Embeddings 모델(예: 텍스트 원본의 유사성 비교).
 - 자연어 설명을 기반으로 이미지를 생성하는 DALL-E 모델.

Azure OpenAI의 AI 모델은 모두 미세 조정을 통해 학습되고 사용자 지정할 수 있습니다. 여기서는 사용자 지정 모델에 대해 설명하지 않지만 Azure 설명서의 [모델 미세 조정](https://learn.microsoft.com/ko-kr/azure/ai-services/openai/how-to/fine-tuning?pivots=programming-language-studio%3Fazure-portal%3Dtrue)에서 자세히 알아볼 수 있습니다.

```
생성 AI 모델은 항상 실제 값을 반영할 확률이 있습니다. 특정 작업에 대해 미세 조정된 모델과 같이 성능이 높은 모델은 실제 값을 반영하는 응답을 반환하는 데 더 효과적입니다. 생성 AI 모델의 출력을 검토하는 것이 중요합니다.
```

#### 플레이그라운드
Azure OpenAI Studio에서 플레이그라운드로 OpenAI 모델을 실험해 볼 수 있습니다. 완성 플레이그라운드에서는 별도의 코딩 없이 프롬프트를 입력하고 매개 변수를 구성하고 응답을 볼 수 있습니다.
![](../img/azure-openai-completions-playground.png)

채팅 플레이그라운드에서 도우미 설정을 통해 모델에 동작 방식을 지시할 수 있습니다. 도우미는 시스템 메시지에서 정의한 어조, 규칙, 형식에 맞춰 응답을 재현하려 할 것입니다.
![](../img/azure-openai-chat-playground.png)


---
## OpenAI의 자연어 기능 이해

Azure OpenAI의 자연어 모델은 자연어를 사용하고 응답을 생성할 수 있습니다.

자연어 학습 모델은 토큰이라고 하는 문자의 단어 또는 청크에 대해 학습됩니다. 예를 들어 “hamburger”라는 단어는 ham, bur, ger 토큰으로 나눠지지만 “pear”과 같은 짧고 일반적인 단어의 토큰은 단일 토큰입니다. 이러한 토큰은 학습에 사용할 수 있도록 기계 학습 모델의 벡터에 매핑됩니다. 학습된 자연어 모델이 사용자의 입력을 받아들이는 경우에는 입력도 토큰으로 나누게 됩니다.

### 자연어 생성을 위한 GPT 모델 이해

GPT(Generative pre-trained transformer) 모델은 자연어를 이해하고 만드는 데 탁월합니다. AI가 질문에 답하거나 프롬프트를 기반으로 단락을 작성하는 것과 관련된 최근 뉴스를 본 적이 있다면 GPT-35-Turbo 또는 GPT-4와 같은 GPT 모델에서 생성되었을 수 있습니다.

#### GPT 모델의 응답은 어떻게 표시되나요?

OpenAI 생성 AI의 주요 측면은 자연어, 시각적 개체 또는 코드 응답을 반환하기 위해서는 입력 또는 프롬프트가 필요하다는 것입니다. GPT는 프롬프트를 기반으로 사용자 질문의 컨텍스트를 유추하거나 추측하려고 합니다.

GPT 모델은 다음과 같은 몇 가지 자연어 작업을 완료하는 데 유용합니다.

| Task        | 프롬프트                           |
|-------------|--------------------------------|
| 텍스트 요약      | “이 텍스트를 짧은 안내문으로 요약”           |
| 텍스트 분류      | “이 책은 어떤 장르인가요?”               |
| 이름 또는 구 생성  | “내 꽃 회사를 위한 태그 라인 작성”          |
| Translation | “‘How are you’를 프랑스어로 번역”      |
| 질문 답변       | “Azure OpenAI는 어떤 기능을 제공하나요?”  |
| 콘텐츠 제안      | “최고의 결혼식 노래 다섯 곡을 알려주세요.”      |

요리 레시피를 요청하는 텍스트를 입력하는 프롬프트를 예로 들어보겠습니다.

```
Write a recipe based on these ingredients and instructions:

Fruit Pie

Ingredients:
Strawberries
Blueberries
Flour
Eggs
Milk
```

다음은 OpenAI API 생성 응답의 예입니다.

```
Instructions:

1. Preheat your oven to 350 degrees Fahrenheit.

2. In a medium bowl, mix together 1 cup of flour and 1 egg until it forms a dough.

3. Grease a 9-inch pie dish with butter or non-stick cooking spray.

4. Roll out the dough and place it in the pie dish.

5. In a separate bowl, mix together 1 cup of strawberries, 1 cup of blueberries, and 1 cup of milk.

6. Pour the fruit mixture into the pie dish.

7. Bake
```

맛있어! 생성된 응답이 머신에서 추측된 최고의 응답이라는 것을 이해하는 것이 중요합니다. 이 경우 생성된 텍스트는 실제 생활에서 맛 좋은 요리에 유용할 수도 있고 그렇지 않을 수도 있습니다.

### 모델이 새 사용 사례에 적용되는 방법

채팅 포털에서 프롬프트를 입력하고 자동으로 응답을 받으며 ChatGPT의 예측 기능을 사용해 보셨을 것입니다. 포털은 사용자에게 표시되는 프런트 엔드 사용자 인터페이스(UI)와 생성형 AI 모델을 포함하는 백 엔드로 구성됩니다. 프런트 엔드와 백 엔드의 조합은 챗봇으로 설명할 수 있습니다. 백엔드에서 제공되는 모델은 OpenAI API 및 Azure OpenAI API 모두에서 구성 요소로 사용할 수 있습니다. GPT-35-터보 모델을 통해 Azure OpenAI에서 ChatGPT의 기능을 활용할 수 있습니다. 다른 애플리케이션에서 생성형 AI 기능이 표시되면 개발자가 구성 요소를 가져와 사용 사례로 사용자 지정한 다음 새로운 프런트 엔드 사용자 인터페이스의 백 엔드에 빌드한 것입니다.

---
## OpenAI 코드 생성 기능 이해

GPT 모델은 자연어 또는 코드 조각을 가져와서 코드로 변환할 수 있습니다. OpenAI GPT 모델은 C#, JavaScript, Perl, PHP와 같은 12개 이상의 언어에 능숙하며 Python에서 가장 성능이 뛰어납니다.

GPT 모델은 자연어와 퍼블릭 리포지토리에서 수십억 줄의 코드에 대해 학습되었습니다. 모델은 코드 주석과 같은 자연어 명령에서 코드를 생성할 수 있으며 코드 함수를 완료하는 방법을 제안할 수 있습니다.

예를 들어 “Python에서 1에서 10까지의 for loop 계산 작성”이라는 프롬프트가 표시되면 다음과 같은 답변이 제공됩니다

```
for i in range(1,11):
    print(i)
```
GPT 모델은 개발자가 더 빠르게 코딩하고, 새 코딩 언어를 이해하고, 애플리케이션에서 더 큰 문제를 해결하는 데 집중할 수 있도록 도와줍니다. 개발자는 목표를 더 간단한 작업으로 나누고 GPT를 사용하여 알려진 패턴을 사용하여 이러한 작업을 구축할 수 있습니다.

### 코드 생성의 예

GPT-3에 대한 학습 데이터의 일부에는 프로그래밍 언어가 포함되어 있으므로 GPT 모델이 프로그래밍 질문에 대답할 수 있다는 것은 놀라운 일이 아닙니다. Codex 모델 제품군의 독특한 점은 GPT 모델보다 더 많은 언어에서 더 많은 기능을 사용할 수 있다는 것입니다.

코드 생성은 자연어 프롬프트에서 코드를 작성하는 것 이상입니다. 다음 코드가 주어지면 단위 테스트를 생성할 수 있습니다.

```
# Python 3
def mult_numbers(a, b):
  return a * b

# Unit test
def
```

GPT는 함수에 대한 단위 테스트를 빌드합니다.

```
# Python 3
def mult_numbers(a, b):
  return a * b

# Unit test
def test_mult_numbers():
  assert mult_numbers(3, 4) == 12
  assert mult_numbers(0, 10) == 0
  assert mult_numbers(4, 0) == 0

# Unit test
def test_mult_numbers_negative():
  assert mult_numbers(-1, 10) == -10
  assert mult_numbers(10, -1) == -10
```

또한 GPT는 이미 작성된 함수를 요약하고, SQL 쿼리 또는 테이블을 설명하고, 함수를 한 프로그래밍 언어에서 다른 프로그래밍 언어로 변환할 수도 있습니다.

GPT 모델과 상호 작용할 때 라이브러리 또는 언어별 태그를 지정하여 Codex에 원하는 것을 명확하게 할 수 있습니다. 
예를 들어 HTML 주석 
```
<!-- build a page titled "Let's Learn about AI" -->
```
이 프롬프트를 제공하고 다음의 결과를 얻을 수 있습니다.

```
<html>
<head>
<title>Let's Learn about AI</title>
<link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
<div class="wrapper">
<div class="header">
<h1>Let's Learn about AI</h1>
</div>
<div class="nav">
<ul>
<li><a href="index.php">Home</a></li>
<li><a href="about.php">About</a></li>
<li><a href="resources.php">Resources</a></li>
<li><a href="contact.php">Contact</a></li>
</ul>
</div>
<div class="content">
<h2>Contact</h2>
<p>
<!-- build a form to contact the site owner -->
<form action="contact.php" method="post">
<label for="name">Name:</label>
<input type="text" name="name" id="name" required>
<label for="email">Email:</label>
<input type="email" name="email" id="email" required>
<label for="subject">Subject:</label>
<input type="text" name="subject" id="subject" required>
<label for="message">Message:</label>
<textarea name="message" id="message" required></textarea>
<input type="submit" value="Send">
</form>
</p>
</div>
<div class="footer">
<p>Let's Learn about AI</p>
</div>
</div>
</body>
</html>
```
### GitHub Copilot
OpenAI는 GitHub와 협력하여 AI 쌍 프로그래머라고 하는 GitHub Copilot을 만들었습니다. GitHub Copilot은 OpenAI Codex의 기능을 Visual Studio Code와 같은 개발자 환경을 위한 플러그 인에 통합합니다.

플러그 인이 설치되고 사용하도록 설정되면 코드 작성을 시작할 수 있으며 GitHub Copilot은 코드 주석 또는 함수 이름을 기반으로 함수의 나머지 부분을 자동으로 제안하기 시작합니다. 예를 들어 파일에 함수 이름만 있고 회색 텍스트가 자동으로 제안되어 완료됩니다.

![](../img/github-copilot-newyear-function.png)

GitHub Copilot은 바로 가기 키를 사용하여 탭할 수 있는 코드 완성을 위한 여러 제안을 제공합니다. 유익한 코드 주석이 제공되면 전체 함수 코드와 함께 함수 이름을 제안할 수도 있습니다.

![](../img/github-copilot%20(1).gif)

---
## OpenAI의 이미지 생성 기능 이해

이미지 생성 모델은 프롬프트, 기본 이미지 또는 둘 다를 사용하여 새로운 것을 만들 수 있습니다. 이러한 생성 AI 모델은 실제 이미지와 꾸밈 이미지를 모두 만들고, 이미지의 레이아웃 또는 스타일을 변경하고, 제공된 이미지에 변형을 만들 수 있습니다.

### DALL-E
생성형 AI 모델은 자연어 기능 외에도 이미지를 편집하고 만들 수 있습니다. 이미지와 함께 작동하는 모델을 DALL-E라고 합니다. GPT 모델과 마찬가지로 DALL-E의 후속 버전이 DALL-E 2와 같은 이름에 추가됩니다. 이미지 기능은 일반적으로 이미지 만들기, 이미지 편집, 이미지 변형 만들기의 세 가지 범주로 나뉩니다.

### 이미지 세대
원본 이미지는 이미지를 원하는 텍스트 프롬프트를 제공하여 생성할 수 있습니다. 프롬프트가 자세할수록 모델이 원하는 결과를 제공할 가능성이 높아집니다.

DALL-E를 사용하면 “빈센트 반 고흐 스타일의 개”와 같은 특정 스타일의 이미지를 요청할 수도 있습니다. 스타일은 편집 및 변형에도 사용할 수 있습니다.

예를 들어 “맨 위에 햄버거를 들고 서 있는 코끼리 스타일 디지털 아트”라는 프롬프트가 표시되면 모델은 요구되는 내용을 정확하게 묘사하는 디지털 아트 이미지를 생성합니다.

![](../img/dall-e-elephant-burger.png)

“분홍색 여우”와 같이 좀 더 일반적인 것을 요구할 때 생성된 이미지는 요구되는 것을 충족시키면서 더 다양하고 단순합니다.

![](../img/dall-e-pink-fox.png)

그러나 “모네 스타일의 들판을 달리는 분홍색 여우”와 같이 프롬프트를 보다 구체적으로 만들면 모델은 훨씬 더 유사한 세부 이미지를 만듭니다.

![](../img/dall-e-pink-fox-monet.png)

### 이미지 편집

이미지가 제공되면 DALL-E는 스타일을 변경하거나, 항목을 추가 또는 제거하거나, 추가할 새 콘텐츠를 생성하여 요청된 대로 이미지를 편집할 수 있습니다. 편집은 원본 이미지를 업로드하고 편집할 이미지의 영역을 나타내는 투명 마스크를 지정하여 수행됩니다. 이미지 및 마스크와 함께 편집할 내용을 나타내는 프롬프트는 모델에 영역을 채우기 위한 적절한 콘텐츠를 생성하도록 지시합니다.

위의 분홍색 여우 이미지 중 하나, 여우를 덮고 있는 마스크 및 “들판에서 책을 읽는 파란색 고릴라”라는 프롬프트가 표시되면 모델은 제공된 입력을 기반으로 이미지 편집을 만듭니다.

![](../img/blue-gorilla-edit.png)

### 이미지 변형

이미지를 제공하고 원하는 이미지의 변형 수를 지정하여 이미지 변형을 만들 수 있습니다. 이미지의 일반 콘텐츠는 동일하게 유지되지만 주체의 위치 또는 보이는 위치, 배경 장면, 색이 변경될 수 있는 등의 측면이 조정됩니다.

예를 들어 햄버거를 모자로 쓰고 있는 코끼리의 이미지 중 하나를 업로드하면 동일한 주체의 변형된 이미지를 얻게 됩니다.

![](../img/dall-e-elephant-variations.png)

---
## Azure OpenAI의 액세스 및 책임 있는 AI 정책 설명

AI 시스템 작업의 윤리적 의미를 고려하는 것이 중요합니다. Azure OpenAI는 다양한 작업을 완료하고 안전하고 공정한 사용을 위해 각각의 고려 사항이 있는 여러 가지 다른 사용 사례에서 작동할 수 있는 강력한 자연어 모델을 제공합니다. AI 시스템을 개발하고 배포를 담당하는 팀 또는 개인은 피해를 식별, 측정, 완화하기 위해 노력해야 합니다.

Azure OpenAI 사용은 다음 6가지 Microsoft AI 원칙을 따라야 합니다.

 - 공정성: Al 시스템은 그룹이나 개인의 편견을 차별하거나 지지하는 결정을 내려서는 안 됩니다.
 - 신뢰성 및 안전성: Al 시스템은 새로운 상황과 잠재적 조작에 안전하게 대응해야 합니다.
 - 개인 정보 및 보안: Al 시스템은 안전해야 하며 데이터 프라이버시를 존중해야 합니다.
 - 포괄성: AI 시스템은 모든 사람에게 힘을 주고 사람들과 관계를 맺어야 합니다.
 - 책임: 사람들은 Al 시스템의 작동 방식에 대해 책임을 져야 합니다.
 - 투명성: AI 시스템은 어떻게 빌드되고 사용되는지 사용자가 이해할 수 있도록 설명이 있어야 합니다.

책임 있는 AI 원칙은 Azure OpenAI에 대한 Microsoft의 투명성 고지 및 다른 제품에 대한 설명을 안내합니다. 투명성 고지는 Microsoft의 AI 기술의 작동 방식, 시스템 소유자가 시스템 성능과 동작에 영향을 줄 수 있는 선택 사항, 기술, 사람, 환경을 포함한 전체 시스템에 대한 사고의 중요성을 이해하는 데 도움을 주기 위한 것입니다.

Azure에서 AI 시작 모듈을 완료하지 않은 경우 책임 있는 AI에서 해당 단위를 검토하는 것이 좋습니다.

### Azure OpenAI에 대한 제한된 액세스
AI를 책임감 있게 사용하기 위한 Microsoft의 노력의 일환으로 Azure OpenAI에 대한 액세스는 현재 제한되어 있습니다. Azure OpenAI를 사용하려는 고객은 초기 실험 액세스에 대한 등록 양식을 제출해야 하며 프로덕션에 대한 승인을 위해 등록 양식을 다시 제출해야 합니다.

콘텐츠 필터를 수정하거나 남용 모니터링 설정을 수정하려는 고객에게는 추가 등록이 필요합니다.

액세스를 신청하고 제한된 액세스 정책에 대해 자세히 알아보려면 Azure OpenAI 제한된 액세스 설명서를 참조하세요.

---
## 연습 - Azure OpenAI Service 살펴보기
이 연습에서는 Azure OpenAI 리소스를 프로비전하고 이를 사용하여 생성 AI 모델을 배포하고 탐색합니다.

```
이 랩을 완료하려면 Azure 구독이 필요하며 Azure OpenAI 액세스에 대한 승인을 받아야 합니다. 액세스가 필요한 경우 Azure OpenAI 제한된 액세스 페이지에서 신청하세요.
```
TODO : 실습자료 만들기
---
## 요약
이 모듈에서는 생성 AI의 개념과 Azure OpenAI Service가 생성 AI 모델에 대한 액세스를 제공하는 방법을 소개했습니다.

이 모듈에서는 다음의 방법도 알아보았습니다.

 - Azure OpenAI 워크로드 설명 및 Azure OpenAI Service 액세스 방법
 - 생성 AI 모델 이해
 - Azure OpenAI의 언어, 코드, 이미지 기능 이해
 - Azure OpenAI의 책임 있는 AI 사례 및 제한된 액세스 정책 이해

Azure OpenAI에 대해 계속 학습하고 구현할 리소스를 찾으려면 Azure OpenAI 설명서 및 Azure OpenAI 학습 경로를 사용하여 AI 솔루션 개발을 확인할 수 있습니다.

---
## 출처
[Microsoft learn Azure OpenAI Service의 기본 사항](https://learn.microsoft.com/ko-kr/training/modules/explore-azure-openai/)