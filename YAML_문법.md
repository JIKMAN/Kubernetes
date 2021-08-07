### **YAML 문법**

쿠버네티스에 요청을 보낼 시에 어떤 오브젝트를 사용할지, 상세 설정을 YAML 형식으로 정의

 

### 들여쓰기 (indent)

들여쓰기는 기본적으로 **2칸** 또는 **4칸**을 지원합니다.

**2칸 들여쓰기 (추천)**

```yaml
person:
  name: Chungsub Kim
  job: Developer
  skills:
    - docker
    - kubernetes
```

**4칸 들여쓰기**

```text
person:
    name: Chungsub Kim
    job: Developer
    skills:
        - docker
        - kubernetes
```

### 데이터 정의 (map)

데이터는 `key`: `value` 형식으로 정의합니다.

- YAML
- JSON

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: echo
  labels:
    type: app
```

### 배열 정의 (array)

배열은 `-`로 표시합니다.

- YAML
- JSON

```yaml
person:
  name: Chungsub Kim
  job: Developer
  skills: 
    - docker
    - kubernetes
```

### 주석 (comment)

주석은 `#`으로 표시합니다.

**전체 라인 주석처리**

```yaml
# comment
person:
  name: Chungsub Kim
  job: Developer
  skills:
    - docker
    - kubernetes
```

**일부 주석처리**

```yaml
person:
  name: Chungsub Kim # subicura
  job: Developer
  skills:
    - docker
    - kubernetes
```

### 참/거짓, 숫자표현

참/거짓은 `true`, `false`외에 `yes`, `no`를 지원합니다.

**참/거짓**

```yaml
study_hard: yes
give_up: no
hello: True
world: TRUE
manual: false
```

**숫자**

정수 또는 실수를 따옴표(") 없이 사용하면 숫자로 인식합니다.

```yaml
# number
version: 1.2

# string
version: "1.2"
```

### 줄바꿈 (newline)

여러 줄을 표현하는 방법입니다.

**"|" 지시어는 마지막 줄바꿈이 포함**

- YAML
- JSON

```yaml
newlines_sample: |
            number one line

            second line

            last line
```

**"|-" 지시어는 마지막 줄바꿈을 제외**

- YAML
- JSON

```yaml
newlines_sample: |-
            number one line

            second line

            last line
```

**">" 지시어는 중간에 들어간 빈줄을 제외**

- YAML
- JSON

```yaml
newlines_sample: >
            number one line

            second line

            last line
```

## 주의사항

### 띄어쓰기

key와 value사이에는 반드시 빈칸이 필요합니다.

```yaml
# error (not key-value, string)
key:value

# ok
key: value
```

### 문자열 따옴표

대부분의 문자열을 따옴표 없이 사용할 수 있지만 `:`가 들어간 경우는 반드시 따옴표가 필요합니다.

```yaml
# error
windows_drive: c:

# ok
windows_drive: "c:"
windows_drive: 'c:'
```



#### **참고**

json2yaml

- JSON to YAML 변환 사이트
- [www.json2yaml.com/https://www.json2yaml.com/)



yamllimit

- YAML 문법을 체크하고 어떻게 해석하는지 결과를 알려줌
- [www.yamllint.com/](http://www.yamllint.com/)