### **YAML 문법**

쿠버네티스에 요청을 보낼 시에 어떤 오브젝트를 사용할지, 상세 설정을 YAML 형식으로 정의

 

#### **기본문법**

들여쓰기(indent)

- 기본적으로 2칸(추천) 또는 4칸 지원

데이터 정의(map)

- key: value 형식

배열 정의(array)

- -로 표시

주석(comment)

- \#으로 표시

참/거짓

- true, false
- yes, no

숫자 표현

- 정수 또는 실수를 따옴표(") 없이 사용하면 숫자로 인식

#### **주의사항**

띄어쓰기

- key와 value 사이에는 반드시 빈칸 필요

문자열 따옴표

- 대부분의 문자열을 따옴표 없이 사용할 수 있지만 : 가 들어간 경우는 반드시 따옴표 필요

#### **참고**

json2yaml

- JSON to YAML 변환 사이트
- [www.json2yaml.com/https://www.json2yaml.com/)



yamllimit

- YAML 문법을 체크하고 어떻게 해석하는지 결과를 알려줌
- [www.yamllint.com/](http://www.yamllint.com/)