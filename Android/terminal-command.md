## 안드로이드 터미널 명령어 

<br>

- 의존성 충돌 분석
```
./gradlew :app:dependencies --configuration kapt
```
---

- 캐시 정리 및 재빌드
```
./gradlew clean
./gradlew --stop
./gradlew build --refresh-dependencies
```