# GIT

## 생성
|명령어|설명|
|-|-|
|`$ git config --global user.name "사용자 이름"`|깃 사용자 이름 설정|
|`$ git config --global user.email "사용자 email"`|깃 사용자 이메일 설정|
|`$ git init`|.git 하위 디렉토리 생성(폴더를 만든 후, 그 안에서 명령 실행 => 새로운 git저장소 생성)|
|`$ git clone <https:.. URL>`|기존 소스 코드(저장소 url) 다운로드/복제|
|`$ git clone 로컬 저장소 경로`|로컬 저장소 복제|
|`$ git clone 사용자명@호스트:원격 저장소 경로`|원격 서버 저장소 복제|

## REMOTE
|명령어|설명|
|-|-|
|`$ git remote add origin <원격 서버 주소>`|원격저장소(remote)로 origin 이름으로 url 을 추가|
|`$ git remote remove <원격 서버 주소>`|원격 서버 주소 삭제|
|`$ git remote rm origin`|origin 이름의 원격 저장소 설정을 삭제|
|`$ git remote -v`|원격 저장소 목록|

## COMMIT
|명령어|설명|
|-|-|
|`$ git add <파일명>` `$ git add <폴더명>/`|커밋에 단일 파일의 변경 사항을 포함(staging area에 추가)|
|`$ git add -A` `$ git add *` `$ git add .`|커밋에 파일의 변경 사항을 한번에 모두 포함|
|`$ git commit -m "커밋 메시지"`|커밋 생성(실제 변경사항 확정)|
|`$ git commit -am "메세지 내용"`|스테이징과 커밋을 메세지와 함께 추가|
|`$ git commit --amend`|직전의 커밋 메세지 수정|

## LOG
|명령어|설명|
|-|-|
|`$ git status`|파일 상태 확인|
|`$ git log`|커밋 이력 확인|
|`$ git log --stat`|커밋에 관련된 파일과 함께 커밋 이력 확인|
|`$ git diff`|commit된 파일상태와 현재 수정중인 상태 비교|
|`$ git diff --staged`|commit된 파일상태와 add된 파일 상태 비교|

## BRANCH
|명령어|설명|
|-|-|
|`$ git branch`|브랜치 목록(현재 설정된 브랜치 앞에 * 가 붙음)|
|`$ git branch <브랜치이름>`|새 브랜치 생성 (local로 만듦)|
|`$ git checkout <브랜치이름>`| 해당 브랜치로 이동|
|`$ git checkout -b <브랜치이름>`|브랜치 생성 & 이동|
|`$ git branch -d <브랜치이름>`|브랜치 삭제(마스터 브랜치에서 가능)|
|`$ git push origin <브랜치이름>`|만든 브랜치를 원격 서버에 전송|
|`$ git push -u < remote > <브랜치이름>`|새 브랜치를 원격 저장소로 push|
|`$ git pull < remote > <브랜치이름>`|원격에 저장된 git 프로젝트의 현재 상태를 다운받고 + 현재 위치한 브랜치로 병합|
|`$ git merge <브랜치이름>`|현재 브랜치에 해당 브랜치 병합|
|`$ git pull`|원격 저장소의 변경 내용이 현재 디렉토리에 가져와지고(fetch) 병합(merge)됨|

## PUSH
|명령어|설명|
|-|-|
|`$ git push`|변경사항 원격 서버에 업로드|
|`$ git push origin <브랜치이름>`|커밋을 원격 서버에 업로드|
|`$ git push -u origin master`|지역 저장소의 브랜치를 원격 저장소의 마스터 브랜치와 연결 (한번만 하면됨)|

## STASH
|명령어|설명|
|-|-|
|`$ git stash`|지금 하던 작업을 임시로 저장|
|`$ git stash list`|stash 목록 확인|
|`$ git stash apply`|git stash로 저장했던 작업 가져오기|
|`$ git stash drop`|stash 제거|
|`$ git stash clear`|임시로 저장했던 stash 모두 제거|
|`$ git stash show -p \| git apply -R`|실수로 잘못 stash 한거 되돌리기|

## RESET
|명령어|설명|
|-|-|
|`$ git reset HEAD 파일이름`|스테이징 취소|
|`$ git reset HEAD^`|최신 커밋 취소|
|`$ git reset 커밋해시`|특정 커밋으로 되돌리기|
