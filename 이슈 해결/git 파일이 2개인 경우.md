# git 파일이 2개인 경우

최상위 디렉토리에 git 파일이 존재하고 그 하위 폴더에 git 파일이 존재하는 상황이다.

이 상태에서 원격 레포지토리에 푸시를 하는 경우 하위 폴더가 정상적으로 업로드가 안되는 상황이 발생한다.

**이를 해결하기 위해 다음과 같은 순서로 진행한다.**

1. 하위 폴더에서 `.git` 파일을 삭제한다.
2. 최상위 디렉토리로 이동해서 `git rm -r --cached .` 명령어를 통해 남아있는 캐시를 삭제한다.
