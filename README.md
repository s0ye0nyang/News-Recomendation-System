# Keyword Detection System based on Naver News Data
#### Big data term project
--------------------------------
뉴스에서 핵심 키워드를 추출하는 시스템
--------------------------------
- NEWS.csv  //수집한 뉴스 데이터
  ```
  pandas Dataframe
  { 제목: 기사링크, 내용: 본문 텍스트 }
  ```
>
- stopwords-ko.txt // 한국어 불용어 목록
- exceptionwords.txt // 쪼개지면 안되는 단어들 목록
- news_crawler.ipynb // 뉴스 수집
- word2vec.ipynb // 데이터 전처리 및 워드 임베딩 
  ```
  def clean_text(texts): # 한글 제외한 나머지 문자 제거
    corpus = []
    hangul = re.compile('[^ ㄱ-ㅣ가-힣]+')
    for i in range(0, len(texts)):
        result = hangul.sub('', str(texts[i]))
        corpus.append(result)
    return corpus
  
  def pos_text(texts): # 품사구분 알파벳 제거
    corpus = []
    for sent in texts:
        pos_tagged = ''
        for word in api.analyze(sent):
            for morph in word.morphs:
                if morph.tag in significant_tags:
                    pos_tagged += morph.lex + '/' + morph.tag + ' '
        corpus.append(pos_tagged.strip())
    return corpus
   
  # 동사원형을 찾는 규칙 정의
  p1 = re.compile('[가-힣A-Za-z0-9]+/NN. [가-힣A-Za-z0-9]+/XS.') # 동사
  p2 = re.compile('[가-힣A-Za-z0-9]+/NN. [가-힣A-Za-z0-9]+/XSA [가-힣A-Za-z0-9]+/VX') # 명사
  p3 = re.compile('[가-힣A-Za-z0-9]+/VV') # 형용사
  p4 = re.compile('[가-힣A-Za-z0-9]+/VX') # 부사

  def stemming_text(text): # 동사원형으로 만들어줌

  ```
  - word2vec 모델 적용
  ```
  model = Word2Vec(removed_stopword_corpus, # 리스트 형태의 데이터
                   sg=0,         # 0: CBOW, 1: Skip-gram
                   size=100,     # 벡터 크기
                   window=10,     # 고려할 앞뒤 폭(앞뒤 3단어)
                   min_count=5,  # 사용할 단어의 최소 빈도(3회 이하 단어 무시)
                   workers=2,
                   iter=100)

  model.save('word2vec.model')손 쉽게 만들 수 있는

  ```
  
