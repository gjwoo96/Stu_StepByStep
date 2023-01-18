# 1. 로컬저장소 또는 원격저장소 연결 관련 명령어
> 깃 저장소 생성
```
git init
```
> 원격 저장소 연결
```
git remote origin(원격저장소 별칭) https://github.com/gjwoo96/Stu_StepByStep.git(원격 저장소 url)
```
> git 리모트 정보 업데이트
```
git remote update
```

> git 리모트 브랜치 최신정보로 업데이트하기
```
git remote prune origin
```

> git 리모트 정보 동기화 하여 로컬에 반영하기
```
git fetch --prune
```

# 2. 연결 후 관리 및 사용 명령어

> Staging Area에 수정한 파일 올리기
```
git add (파일명 / 수정한 파일 전부 올릴시 .(마침표) 사용)
```
- Staging Area 이란?
    - 작업 디렉토리와 Git 저장소의 변경 이력사이에 징검다리 역할  
    즉 커밋 하기 전 대기실 같은 존재
> 수정한 파일 커밋
```
git commit -m '커밋할 메시지'
```
> 원격저장소 수정파일 반영
```
git push origin(연결해둔 원격저장소 별칭) main(수정파일 반영할 브랜치)
```

> 원격 저장소 파일 레포지토리 통째로 내려받기
```
git clone https://github.com/gjwoo96/Stu_StepByStep.git
```

> 원격 저장소 프로젝트 변경사항 내려받기
```
git pull origin(연결한 원격저장소 별칭) main(내려받을 브랜치명)
```

# 3. 브랜치 관련 명령어

> 브랜치 확인
```
- 로컬 브랜치 확인
git branch
- 원격저장소 브랜치 확인
git branch -r
```
>브랜치 생성
```
1. 브랜치 생성
git branch (생성할 브랜치명)

2. 브랜치 생성후 해당 브랜치로 이동
git checkout -b (생성할 브랜치명)

3. 로컬에서 생성한 브랜치를 원격 저장소에도 생성할 경우
git push origin (생성한 브랜치명)

4. 원격저장소에 생성한 브랜치와 로컬브랜치를 연동
git branch --set-upstream-to origin/(방금생성후 원격저장소 올린 브랜치)
```
> 브랜치 삭제
```
1. 로컬브랜치 삭제
git branch -d (삭제할 브랜치명)
2. 원격 브랜치 삭제
git push origin :(삭제할 브랜치명)
```

> 브랜치 병합
```
git merge (병합 할 브랜치)

# 내가 병합을 할 브랜치로 checkout한후 병합 당할 브랜치를 merge 뒤에 명시해준다.
```