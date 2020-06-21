# OC和Swift混编

## OC项目中使用Swift类

- 创建一个 Swift 类，同时系统自动提示创建桥接文件，"项目名称-Bridging-Heade", 比如`cloudExchange-Bridging-Header`

  > 如果想更改创建的桥接文件的位置，则在 build settings中搜索 bridging，在 Objective-C Bridging Header 后面双击更改位置，如`$(SRCROOT)/cloudExchange-Bridging-Header.h`

- 在 target 的 build settings 中
  - Product Module Name 中设置一个名字，到时会生成一个叫”Product Module Name-Swift.h”的文件
  - Defines Module : YES 【?】
  - Always Embed Swift Standard Libraries : YES 【?】
  - Install Objective-C Compatibility Header : YES 【?】

- 调用Swift类，我们想要调用Swift类的方法里面引入生成的头文件：”Product Module Name-Swift.h”，比如 `#import "cloudExchange-Swift.h"`

  > 要让 OC 可用的 Swift 类，要么自己继承自 NSObject，要么它的父类继承自 NSObject
  >
  > class YourSwiftClassName: NSObject
  >
  > 要让 OC 可调用的 属性，必须在 属性声明 前面加 @objc

- 要在Swift文件中使用的OC类需要在桥接文件中引入头文件，暴露给Swift

## OC项目中使用Swift第三方库

- Podfile中添加 use_frameworks!

  > 添加这句代码是因为Apple不允许build包含swift的静态库了，而cocoapod使用了framework动态框架的方式来集成swift库

- 重新pod install

- 重新打开项目

- 如果需要的话，找到pod-->build setting->swift-language-version设置为4.0

- 编译的话，有可能报找不到.h文件的错，试着重新import一下

- 如果项目中有剔除x86_64, i386这两个架构的shell script，可能会报lipo相关的错误，改为下面改良过的脚本

  ```
  #改良过的，剔除掉x86_64, i386这两个架构的shell代码
  #!/usr/bin/env bash
  
  APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"
  
  # This script loops through the frameworks embedded in the application and
  # removes unused architectures.
  find "$APP_PATH" -name '*.framework' -type d | while read -r FRAMEWORK
  do
      FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)
      FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"
  
      if [ ! -f "${FRAMEWORK_EXECUTABLE_PATH}" ]; then
          continue
      fi
  
      if xcrun lipo -info "${FRAMEWORK_EXECUTABLE_PATH}" | grep --silent "Non-fat"; then
          echo "Framework non-fat, skipping: $FRAMEWORK_EXECUTABLE_NAME"
          continue
      fi
  
      echo "Thinning framework $FRAMEWORK_EXECUTABLE_NAME"
  
      EXTRACTED_ARCHS=()
  
      for ARCH in $ARCHS
      do
          echo "Extracting $ARCH from $FRAMEWORK_EXECUTABLE_NAME"
          xcrun lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"
          EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")
      done
  
      echo "Merging extracted architectures: ${ARCHS}"
      xcrun lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"
      rm "${EXTRACTED_ARCHS[@]}"
  
      echo "Replacing original executable with thinned version"
      rm "$FRAMEWORK_EXECUTABLE_PATH"
      mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"
  done
  ```

  