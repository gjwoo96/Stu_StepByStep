>마크다운(markdown)이란?

___
일반 텍스트 기반의 마크업 언어로 
**'README.md'** 파일이나 <br>
온라인 문서, 혹은 일반 텍스트 편집기로 <br>
문서 양식을 편집할 때 쉽게 쓰고 읽을 수 잇으며<br> 
HTML로 변환이 가능하다
___
<br>

- Header
    - #(h1)
    - ##(h2)
    - ###(h3)
    - ####(h4)
    - #####(h5)  
    - ex) # h1헤더 ,## h2 헤더 ...

- 문단구분 
    - 마지막줄에 스페이스바 두번
    - ex) 띄워쓰기 space space  
     띄워쓰기 ok?

- 이미지 (Images)
    -  첫번째 방법  
    ```![Github log](/images/markdown_logo.jpg)```

    -   두번째 방법  
    ```
    <a href="#">
    <img src="https://github.com/gjwoo96/Stu_StepByStep/tree/main/images/dog.jpg">
    </a>
    Format: img 태그 사용 - 이미지경로는 상대경로 or 절대경로
    ```
    <a href="#">
    <img src="https://github.com/gjwoo96/Stu_StepByStep/blob/main/MarkDown/images/dog.jpg?raw=true">
    </a>
______

- 인용 상자 (Blockquotes)

    ``` '>'를 사용해서 인용상자를 생성 ```
    > This is Blockquotes

- 강조 (Emphasis)  
    ``` 
    '* , _'를 강조하려는 text앞에 사용
    * : 굵게 / _ : 기울이기
    ```
    > **안녕** _하세요_.

- 테이블 Tables
    ```
    First Header|Second Header
    |:--|:--:| -> 정렬하고 싶은 위치에 : 사용
    content cell1|content cell2
    content column 1|content column 2
    ```
First Header|Second Header
|:--|:--:|
content cell1|content cell2
content column 1|content column 2

- 이모지 사용
```
(http://emoji-cheat-sheet.com) 참조해서 사용
```

> 공부 참고 [URL]   
    (https://www.youtube.com/watch?v=dUbp9wAy178)  
(https://www.youtube.com/watch?v=kMEb_BzyUqk&t=1s)     

