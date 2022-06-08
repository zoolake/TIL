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

> **참고**
>
> [Docker (Apple Silicon/M1 Preview) MySQL "no matching manifest for linux/arm64/v8 in the manifest list entries"](https://stackoverflow.com/questions/65456814/docker-apple-silicon-m1-preview-mysql-no-matching-manifest-for-linux-arm64-v8)
