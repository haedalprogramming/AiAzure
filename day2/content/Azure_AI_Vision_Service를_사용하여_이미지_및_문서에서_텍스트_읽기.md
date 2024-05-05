# Azure AI Vision Service를 사용하여 이미지 및 문서에서 텍스트 읽기

## 목차
- [Azure AI Vision Service를 사용하여 이미지 및 문서에서 텍스트 읽기](#azure-ai-vision-service를-사용하여-이미지-및-문서에서-텍스트-읽기)
  - [목차](#목차)
  - [소개](#소개)
  - [텍스트 읽기를 위한 Azure AI 비전 옵션 살펴보기](#텍스트-읽기를-위한-azure-ai-비전-옵션-살펴보기)
  - [Read API 사용](#read-api-사용)
  - [연습 - 이미지의 텍스트 읽기](#연습---이미지의-텍스트-읽기)
  - [요약](#요약)
  - [출처](#출처)


---
## 소개

수천 가지의 이미지가 제공되고 이미지의 텍스트를 컴퓨터 데이터베이스로 전송하라는 메시지가 표시된다고 가정합니다. 스캔한 이미지에는 다양한 형식으로 구성된 텍스트가 있으며 여러 언어를 포함합니다. 적절한 시간 프레임으로 프로젝트를 완료하고 높은 정확도로 데이터를 입력할 수 있는 몇 가지 방법은 무엇일까요?

전 세계의 회사는 매일 비슷한 시나리오를 다루고 있습니다. AI 서비스가 없으면 프로젝트를 완료하는 것이 어려울 수 있습니다. 특히 규모가 변경되는 경우에는 더 어렵습니다.

AI 서비스를 사용하여 이 프로젝트를 Azure AI 비전 시나리오로 처리하고 OCR(광학 인식)을 적용할 수 있습니다. OCR을 사용하면 도로 표지판 및 제품의 사진과 같은 이미지뿐만 아니라 필기 또는 구조화되지 않은 문서와 같은 문서에서 텍스트를 추출할 수 있습니다.

자동화된 AI 솔루션을 빌드하려면 많은 사용 사례를 다루는 기계 학습 모델을 학습해야 합니다. Azure AI 비전 서비스는 이미지 처리를 위한 고급 알고리즘에 대한 액세스를 제공하고 데이터를 안전한 스토리지에 반환합니다.

이 모듈에서는 다음을 수행하는 방법을 알아봅니다.

 - Azure AI Vision 서비스를 사용하여 이미지에서 텍스트를 읽을 수 있는 방법 식별
 - SDK 및 REST API와 함께 Azure AI 비전 서비스 사용
 - 인쇄 및 필기 텍스트를 읽을 수 있는 애플리케이션 개발

---
## 텍스트 읽기를 위한 Azure AI 비전 옵션 살펴보기

Azure AI는 문서와 이미지에서 텍스트를 읽는 두 가지 기능을 제공합니다. 하나는 Azure AI Vision Service, 다른 하나는 Azure AI Document Intelligence에 있습니다. 각 서비스가 제공하는 항목은 겹치게 되지만 각 서비스는 입력 내용에 따라 결과에 최적화됩니다.

 - 이미지 분석 OCR(광학 문자 인식):
   - 이 기능은 텍스트 양이 적은 일반 구조화되지 않은 문서 또는 텍스트가 포함된 이미지에 사용합니다.
   - 결과는 단일 API 호출에서 즉시(동기식) 반환됩니다.
   - 개체 감지, 이미지 설명 또는 분류, 스마트 잘린 썸네일 생성 등을 포함하여 텍스트를 추출한 과거 이미지를 분석하는 기능이 있습니다.
   - 예를 들어 도로 표지판, 필기 노트 및 상점 표지판이 있습니다.
 - 문서 인텔리전스:
   - 이 서비스를 사용하여 이미지 및 PDF 문서에서 작은 텍스트에서 대량의 텍스트를 읽을 수 있습니다.
   - 이 서비스는 문서의 컨텍스트와 구조를 사용하여 정확도를 향상시킵니다.
   - 초기 함수 호출은 후속 호출에서 결과를 검색하는 데 사용해야 하는 비동기 작업 ID를 반환합니다.
   - 예를 들어 영수증, 문서 및 청구서가 있습니다.

REST API 또는 클라이언트 라이브러리를 통해 두 기술 모두에 액세스할 수 있습니다. 이 모듈에서는 이미지 분석의 OCR 기능에 초점을 맞춥니다. 문서 인텔리전스에 대해 자세히 알아보려면 이 모듈을 읽는 것이 좋습니다.

---
## Read API 사용

읽기 OCR 기능을 사용하려면 ImageAnalysis 함수(REST API 또는 해당 SDK 메서드)를 호출하고, 이미지 URL 또는 이진 데이터를 전달하고, 필요에 따라 성 중립적인 캡션 또는 텍스트가 작성된 언어를 지정합니다(영어의 경우 기본값은 en).

ImageAnalysis에 OCR 요청을 만들려면 시각적 기능을 .로 READ지정합니다.

C#
```c#
ImageAnalysisResult result = client.Analyze(
    <image-to-analyze>,
    VisualFeatures.Read);
```

Python
```python
result = client.analyze(
    image_url=<image_to_analyze>,
    visual_features=[VisualFeatures.READ]
)
```

REST API를 사용하는 경우 기능을 .로 read지정합니다.

```
https://<endpoint>/computervision/imageanalysis:analyze?features=read&...
```

읽기 OCR 함수의 결과는 JSON 또는 유사한 구조의 언어별 개체로 동기적으로 반환됩니다. 이러한 결과는 블록( 현재 서비스는 하나의 블록 만 사용)으로 세분화한 다음 , 줄과 단어를 사용하여 세분화됩니다. 또한 텍스트 값은 줄 및 단어 수준 모두에 포함되기 때문에 개별 단어 수준에서 텍스트를 추출할 필요가 없는 경우 전체 텍스트 줄을 더 쉽게 읽을 수 있습니다.

```json
{
    "metadata":
    {
        "width": 500,
        "height": 430
    },
    "readResult":
    {
        "blocks":
        [
            {
                "lines":
                [
                    {
                        "text": "Hello World!",
                        "boundingPolygon":
                        [
                            {"x":251,"y":265},
                            {"x":673,"y":260},
                            {"x":674,"y":308},
                            {"x":252,"y":318}
                        ],
                        "words":
                        [
                            {
                                "text":"Hello",
                                "boundingPolygon":
                                [
                                    {"x":252,"y":267},
                                    {"x":307,"y":265},
                                    {"x":307,"y":318},
                                    {"x":253,"y":318}
                                ],
                            "confidence":0.996
                            },
                            {
                                "text":"World!",
                                "boundingPolygon":
                                [
                                    {"x":318,"y":264},
                                    {"x":386,"y":263},
                                    {"x":387,"y":316},
                                    {"x":319,"y":318}
                                ],
                                "confidence":0.99
                            }
                        ]
                    },
                ]
            }
        ]
    }
}
```

---
## 연습 - 이미지의 텍스트 읽기

TODO : 실습 자료 만들기

---
## 요약

이 모듈에서 학습한 내용은 다음과 같습니다.

 - ImageAnalysis READ 기능을 사용하여 이미지에서 텍스트 읽기
 - SDK 및 REST API와 함께 Azure AI 비전 서비스 사용
 - 인쇄 및 필기 텍스트를 읽을 수 있는 애플리케이션 개발

---
## 출처
[Microsoft learn Azure AI Vision Service를 사용하여 이미지 및 문서에서 텍스트 읽기](https://learn.microsoft.com/ko-kr/training/modules/read-text-images-documents-with-computer-vision-service/)