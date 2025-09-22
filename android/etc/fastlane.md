## Fastlane 을 활용하여 Google Play Store 에 Android 앱 자동 배포


나의 환경 : **[MacOS Apple Silicon]**<br>

- rbenv로 Ruby 환경 구축 → fastlane 설치 → Android 프로젝트 초기화 순서로 진행.<br>
- Google Play Console, Google Clound Platform 에 추가 설정 필요.

### 1. Ruby 환경 설정 (rbenv)

```bash
*# Homebrew로 rbenv 설치*
brew install rbenv ruby-build

*# 최신 안정화 Ruby 버전 설치 (예: 3.2.0)*
rbenv install 3.2.0
rbenv global 3.2.0

*# 셸 설정 (zsh 파일에 구문 추가)
open ~/.zshrc

# 복사 붙여넣기 후 저장*
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc

# 셸 적용
source ~/.zshrc

*# 설치 확인*
ruby -v
which ruby  *# /Users/[username]/.rbenv/shims/ruby 경로 확인*
```

### 2. fastlane 설치

```bash
*# Bundler 설치 (Ruby 패키지 관리자)*
gem install bundler

*# fastlane 설치*
gem install fastlane

*# 설치 확인*
fastlane --version
```

### 3. Android 프로젝트 fastlane 초기화

```bash
*# Android 프로젝트 루트 디렉토리로 이동*
cd /path/to/your/android/project

*# fastlane 초기화 (Android용)*
fastlane init

*# 초기화 중 선택사항:
# 1. Automatically upload to Google Play? → Yes/No
# 2. Package name 입력 (예: com.yourcompany.yourapp)
# 3. Service Account JSON 파일 경로 (나중에 설정 가능)*
```

### 4. 생성된 파일 구조

```bash
📁 your-android-project/
├── 📁 fastlane/
│   ├── 📄 Appfile          # 앱 정보 설정
│   ├── 📄 Fastfile         # **배포 스크립트 구성**
│   └── 📄 Pluginfile       # 플러그인 설정
├── 📄 Gemfile              # Ruby 의존성
└── 📄 Gemfile.lock         # 의존성 버전 고정
```

### 5. 기본 설정 확인

```bash
*# 의존성 설치*
bundle install

*# fastlane 동작 확인*
bundle exec fastlane android test

*# 사용 가능한 lane 확인*
bundle exec fastlane lanes
```

---

### Google Play Console API 연동

```bash
*# 1. Google Cloud Console에서 서비스 계정 생성
# 2. JSON 키 파일 다운로드
# 3. 프로젝트 내 폴더에 저장 / (난 app/src/main/assets 에 저장함.)

# AppFile 에 아래 내용 삽입

json_key_file("app/src/main/assets/fastlane-json-key-name.json")
package_name("com.app.myapp")*
```

### 프로덕션 배포 lane 추가

```bash
# 테스트 lane
    desc "deploy to Google Play Store"
    platform :android do
        lane :deployPlayStore do
          gradle(
             task: "bundleRelease",
             print_command: true # 에러 명렁 확인 가능.
          )
    # Google Play Store에 업로드
        upload_to_play_store(
            track: 'production',
            json_key: "app/src/main/assets/*fastlane-json-key-name*.json",
            aab: lane_context[SharedValues::GRADLE_AAB_OUTPUT_PATH], # 내 aab 경로, 기본제공.
            skip_upload_apk: "true" # aab 사용 시 apk 업로드는 skip.
         )
        UI.success("🚀 앱이 Play Store 프로덕션에 성공적으로 배포되었습니다!") # 편의를 위해 성공 UI 띄움.
        end
    end
```

### gradle.properties 설정, build.gradle(app) 에 변수 정의

```kotlin
/* gradle.properties */
versionCode = 1
versionName = 1.0.0

/* build.gradle(app) */

android {
	defalutConfig{
      def versionCodeProp = project.findProperty("versionCode")
      def versionNameProp = project.findProperty("versionName")

      versionCode versionCodeProp ? versionCodeProp.toInteger() : 1
      versionName versionNameProp ?: "1.0.0"
	}
}
```

---

## ** 배포 실행 명령어**

```bash
# 실행 방법 : **fastlane [선언한 lane 이름]**
# --verbose : 상세한 로그와 디버깅 정보를 출력. 
fastlane deployPlayStore --verbose
```

## **트러블슈팅**

### Ruby 권한 문제 해결

```bash
*# sudo 없이 gem 설치하려면*
rbenv rehash
gem env home  *# 경로 확인*
```

### Ruby 환경 경로와 homebrew

[MacOS] 환경에서 Intel -> Apple 로 정보를 옮기는 과정에서
intel Mac 의 bash 환경을 그대로 가져옴.

이처럼 환경 경로가 문제되는 경우 fastlane 호출 시 에러가 발생.

```bash
*# 현재 맥 아키텍처 확인*

uname -m

*# 출력 결과:

# arm64     → Apple Silicon (M1/M2..)
# x86_64    → Intel Mac*
```

**Apple Silicon (M1/M2..)**

```bash
*# Homebrew 기본 경로*
/opt/homebrew/bin/brew

*# rbenv 설치 경로*
/opt/homebrew/bin/rbenv

*# Ruby 설치 경로*
/opt/homebrew/var/rbenv/versions/
```

**Intel Mac**

```bash
*# Homebrew 기본 경로*
/usr/local/bin/brew

*# rbenv 설치 경로*  
/usr/local/bin/rbenv

*# Ruby 설치 경로*
/usr/local/var/rbenv/versions/
```

**셸 설정 파일 수정 (아키텍처별)**

```bash
### Apple Silicon 환경
*# ~/.zshrc 설정*
echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc  
echo 'eval "$(/opt/homebrew/bin/rbenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc

### Intel 환경
*# ~/.zshrc 설정*
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(/usr/local/bin/rbenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc
```

**참고 :**

https://docs.fastlane.tools/getting-started/android/setup/