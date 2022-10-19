### React Native
#### with `react-native-cli`

---
#### node/ watchman 확인 및 설치
```shell
node -v
watchman -v
```
---
#### ruby 확인
```shell
ruby --v
```

---
#### project create
```shell
# react-naitve with typescript
npx react-native init myLuxury --template react-native-template-typescript
```

> **IOS**
> ```shell
> cocoapods 설치
> cd > ios
> sudo arch -x86_64 gem install ffi
> arch -x86_64 pod install
> ```

> **Android**
> ```shell
> JDK 설치
> java -version (설치 후 확인)
> javac -version (컴파일러 확인: jdk가 설치되면 java 컴파일러도 같이 설치됨)
> ```

---
#### native start
```shell
# IOS - simulator
npx react-native run-ios
# AVD - emulator
npx react-native run-android
```

