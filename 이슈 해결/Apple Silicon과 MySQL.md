# Apple Silicon과 MySQL

Docker Compose를 통해 컨테이너를 생성하는 도중, MySQL 컨테이너에 오류가 발생했다.
오류 문구는 다음과 같다.

**Docker (Apple Silicon/M1 Preview) MySQL "no matching manifest for linux/arm64/v8 in the manifest list entries"**

`docker-compose.yml` 파일에 다음과 같은 문구를 추가하여 문제를 해결하였다.

```yaml
# 수정 전
mysql:
    build: ./mysql
    restart: unless-stopped
    container_name: app_mysql
# ...생략...

# 수정 후
mysql:
    platform: linux/x86_64
    build: ./mysql
    restart: unless-stopped
    container_name: app_mysql
# ...생략...
```

### 2022.06.17 에 추가한 내용

MySQL 이미지를 다운 받으려고 시도하는 과정에서 m1 칩으로 인한 동일한 문제가 발생했으며, **플랫폼을 명시**하여 해결했다.

추가적으로 컨테이너를 실행할 때도 플랫폼을 명시한다.

```bash
# MySQL 이미지 다운로드
docker pull --platform linux/amd64 mysql
# 컨테이너 실행
docker run --platform linux/amd64 --name <컨테이너 이름> -e MYSQL_ROOT_PASSWORD=<비밀번호> -d mysql
```

> **참고**
>
> [Docker (Apple Silicon/M1 Preview) MySQL "no matching manifest for linux/arm64/v8 in the manifest list entries"](https://stackoverflow.com/questions/65456814/docker-apple-silicon-m1-preview-mysql-no-matching-manifest-for-linux-arm64-v8)
>
> [codinglog.tistory.com](https://codinglog.tistory.com/198?category=1042573)
