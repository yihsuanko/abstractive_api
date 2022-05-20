# abstractive_api

- [程式建置流程](#程式建置流程)
- [程式說明](#程式說明)
   - [FASTAPI](#FASTAPI)
        - [title](#title)
   - [postman](#postman)
   - [docker](#docker)

## 程式建置流程
- 透過FASTAPI 來製作 get/post api
- 使用postman測試post api
- 使用Jinja2來製作HTML template
- 使用transformers pipelines 來進行模型預測
- 使用docker製作映像檔

## File Outline and Explanation

### Folder 

-app : FASTAPI main folder

-models : the directory of models

    --mt5_small_zh_short : auto title model

    --mt5_small_zh_ny : auto summary model


--------
### Code File
-main.py FastAPI Demo

- code:
    ```python
        # clean punctuation
        def clean_punc(text):
            for i in punctuation_string:
                text = text.replace(i, '')
            return text

        # predict title function
        def pred_title_result(article, max_length=50, num_return_sequences=1, do_sample=False, early_stopping=True, no_repeat_ngram_size=3):
            ...
        
        # predict summary function
        def pred_summary_result(article, max_length=150, num_return_sequences=1, do_sample=False, early_stopping=True, no_repeat_ngram_size=3):
            ...
    ```

## 程式說明

### [FASTAPI](https://fastapi.tiangolo.com/)
- installation
    - pip install fastapi
    - pip install "uvicorn[standard]"
    - pip install jinja2
- Run the code
    - uvicorn app.main:app --reload
- api 用途
    - POST: to create data.
    - GET: to read data.
    - PUT: to update data.
    - DELETE: to delete data.
- api
    - `/`: (get/post) 用於自動產生標題
    - `/summary`: (get/post) 用於自動產生摘要
    - `/api/sum`: (post) 可以讀多個檔案
- 附上兩個模型
    - title: mt5_small_zh_short
    - summary: mt5_small_zh_ny

#### title
- URL: `/`
- method: `get\post`
    - Headers:
        - `Content-Type`: `text/html; charset=utf-8`
    - HTML `<form>` 使用post，使網址不會因為input改變
    - 可調整變數
        - sample: `True`:抽樣 `False`:選機率最大
        - num_return_sequences: 產生的句子數量（因為num_beams=10，如果想要產出超過10個句子，需要調整num_beams）

#### summary
- URL: `/summary`
- method: `get\post`
    - Headers:
        - `Content-Type`: `text/html; charset=utf-8`
    - HTML `<form>` 使用post，使網址不會因為input改變
    - 可調整變數
        - sample: `True`:抽樣 `False`:選機率最大
        - num_return_sequences: 產生的句子數量（因為num_beams=10，如果想要產出超過10個句子，需要調整num_beams）

#### post api
- URL: `/api/sum`
- Method: `POST`
- Headers:
    - `Content-Type`: `application/json`
    - `accept`: `application/json`
- Example Request Body:
    ```
    [
        {"id": 1,
        "content":"韓國女子天團少女時代唱紅許多洗腦神曲，而今年8月5日是她們出道滿15週年，5月1號凌晨少女時代官方IG無預警曬出全粉的預告照，引起各界猜疑少女時代是否會回歸。沒想到照片發布不到一天，竟然引來10萬人按讚，可見網友們都十分興奮，不過其實少女時代隊長太妍在之前的視訊簽售會就被問到「15週年是否會回歸」，她則透露「也許能看到」，即使不確定但粉絲還是充滿期待。",
        "do_sample":true,
        "num_return_sequences":2},
        {"id": 2,
        "content":"免疫系統的記憶力跟人的記憶力相似，它可能對有些感染記憶猶新，但也會忘記另外一些感染。例如，麻疹，通常患過一次後可獲得終身免疫。但人體的免疫系統會遺忘許多其他病毒，例如兒童會在一個冬季多次感染呼吸道合胞病毒（RSV，respiratory syncytial virus) 。而這次的新冠病毒（Sars-CoV-2,）由於出現時間不長，所以還無從得知免疫力能維持多久。但是，有6種其他人類冠狀病毒可以為人們提供一些線索。其中有4種引起普通感冒的冠狀病毒，人體對此的免疫力很短。研究表明有些病人可以在一年之內反覆感冒。好在普通感冒的症狀較輕。另外兩種冠狀病毒更厲害，一種是導致薩斯（也稱沙士或非典）的病毒；另一種則是中東呼吸綜合症（Mers)的病毒。如果感染這兩種病毒，幾年後康復者身體內仍然可以測到抗體。英國東安格利亞大學的醫學教授亨特說，問題不在於你是否有免疫力，而是它能維持多久。亨特補充說， 幾乎肯定人體不會終生免疫。亨特還表示，根據對薩斯抗體的研究，其免疫力可能只維持一到兩年。但目前尚不確定。然而，即使你完全沒有免疫力，二次感染時症狀可能不會那麼嚴重。",
        "do_sample":false,
        "num_return_sequences":1}
    ]
    ```
- Example Request:
    ```
    curl -X 'POST' \
    'http://127.0.0.1:8000/api/sum' \
    -H 'accept: application/json' \
    -H 'Content-Type: application/json' \
    -d '[
    {
        "id": 0,
        "content": "疫情期間不多打擾大家，我除了在我從小長大最愛的礁溪麗翔、自助拍婚紗為家人留念，其餘禮俗一切從簡。我年初登記，照著流程懷上水虎寶寶，好不容易它剛脫離危險期卻馬上遇到另一個考驗，實在對小孩很抱歉，雖然因為特殊身體狀況，很多藥不能吃，要靠自體免疫克服，但我會努力，也希望它是個跟媽媽一樣堅強的小孩。染疫消息曝光，我感受到滿滿的愛，各界好同事、好朋友不只關心慰問還幫忙搜羅實際的補給品，真的無比感恩！雖不一一點名，但我銘感五內一輩子會記得",
        "do_sample": false,
        "num_return_sequences": 1
    }
    ]'
    ```
- Example Succcess Response:
```
{
    "result": [
        {
            "id": 1,
            "content": "韓國女子天團少女時代唱紅許多洗腦神曲，而今年8月5日是她們出道滿15週年，5月1號凌晨少女時代官方IG無預警曬出全粉的預告照，引起各界猜疑少女時代是否會回歸。沒想到照片發布不到一天，竟然引來10萬人按讚，可見網友們都十分興奮，不過其實少女時代隊長太妍在之前的視訊簽售會就被問到「15週年是否會回歸」，她則透露「也許能看到」，即使不確定但粉絲還是充滿期待。",
            "num_return_sequences": 2,
            "do_sample": true,
            "result": [
                {
                    "summary_text": "少女時代15週年被問「是否回歸」 網友興奮"
                },
                {
                    "summary_text": "少女時代15週年被問「是否回歸」 網友興奮"
                }
            ]
        },
        {
            "id": 2,
            "content": "免疫系統的記憶力跟人的記憶力相似，它可能對有些感染記憶猶新，但也會忘記另外一些感染。例如，麻疹，通常患過一次後可獲得終身免疫。但人體的免疫系統會遺忘許多其他病毒，例如兒童會在一個冬季多次感染呼吸道合胞病毒（RSV，respiratory syncytial virus) 。而這次的新冠病毒（Sars-CoV-2,）由於出現時間不長，所以還無從得知免疫力能維持多久。但是，有6種其他人類冠狀病毒可以為人們提供一些線索。其中有4種引起普通感冒的冠狀病毒，人體對此的免疫力很短。研究表明有些病人可以在一年之內反覆感冒。好在普通感冒的症狀較輕。另外兩種冠狀病毒更厲害，一種是導致薩斯（也稱沙士或非典）的病毒；另一種則是中東呼吸綜合症（Mers)的病毒。如果感染這兩種病毒，幾年後康復者身體內仍然可以測到抗體。英國東安格利亞大學的醫學教授亨特說，問題不在於你是否有免疫力，而是它能維持多久。亨特補充說， 幾乎肯定人體不會終生免疫。亨特還表示，根據對薩斯抗體的研究，其免疫力可能只維持一到兩年。但目前尚不確定。然而，即使你完全沒有免疫力，二次感染時症狀可能不會那麼嚴重。",
            "num_return_sequences": 1,
            "do_sample": false,
            "result": [
                {
                    "summary_text": "中東呼吸綜合症可能出現時間不長,醫學教授稱你不會終生免疫"
                }
            ]
        }
    ]
```

### [postman](https://www.postman.com/)
- 由於直接輸入網址獲取資料屬於get方法，因此無法檢視post api以下有兩個辦法可以檢視post api
- FASTAPI內建的 /doc
run fast api 之後在網址上
    1. 輸入`http://127.0.0.1:8000/docs`
    2. 點選try it out 即可開始測試
- postman
    1. 下載postman
    2. 選取api的方法（get,post...）
    3. 使用post時，在body的部分輸入測試內容


### [docker](https://www.docker.com/)
- 如何使用docker
    1. 安裝 Docker
    2. 準備打包資料和requirements.txt<br>
    將所有需要的套件寫入requirements.txt
    ```
    # 舉例
    fastapi>=0.68.0,<0.69.0
    pydantic>=1.8.0,<2.0.0
    uvicorn>=0.15.0,<0.16.0
    ```
    資料放置方式示範
    ```
    .
    ├── app
    │   ├── __init__.py
    │   └── main.py
    ├── Dockerfile
    └── requirements.txt

    ```
    3. 撰寫 Dockerfile
    ```
    FROM python:3.9
    WORKDIR /code # 在docker裡增加一個叫code的資料夾
    
    # 安裝使用環境
    COPY ./requirements.txt /code/requirements.txt
    RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

    # 複製檔案、資料（複製local的app資料夾到docker的 code/app資料夾）
    COPY ./app /code/app
    
    # run program的方法
    CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]

    ```
    4. Docker build<br>
    `docker build -t name:tag .`<br>
    5. Docker run<br>
    `docker run -d --name mycontainer -p 80:80 myimage`<br>