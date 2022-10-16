# Install CocoaPods - Architecture Arm (M1)

## ❌ CocoaPods Error
### Command

```
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/bin/pod init
```

### Report

* What did you do?

* What did you expect to happen?

* What happened instead?


### Stack

```
   CocoaPods : 1.11.3
        Ruby : ruby 3.1.2p20 (2022-04-12 revision 4491bb740a) [arm64-darwin21]
    RubyGems : 3.3.11
        Host : macOS 12.6 (21G115)
       Xcode : 14.0.1 (14A400)
         Git : git version 2.35.1
Ruby lib dir : /opt/homebrew/Cellar/ruby/3.1.2_1/lib
Repositories : trunk - CDN - https://cdn.cocoapods.org/
```

### Plugins

```
cocoapods-deintegrate : 1.0.5
cocoapods-plugins     : 1.0.0
cocoapods-search      : 1.0.1
cocoapods-trunk       : 1.6.0
cocoapods-try         : 1.2.0
```

### Error

```
RuntimeError - [Xcodeproj] Unknown object version (56).
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/gems/xcodeproj-1.21.0/lib/xcodeproj/project.rb:228:in `initialize_from_file'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/gems/xcodeproj-1.21.0/lib/xcodeproj/project.rb:113:in `open'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/gems/cocoapods-1.11.3/lib/cocoapods/command/init.rb:41:in `validate!'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/gems/claide-1.1.0/lib/claide/command.rb:333:in `run'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/gems/cocoapods-1.11.3/lib/cocoapods/command.rb:52:in `run'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/gems/cocoapods-1.11.3/bin/pod:55:in `<top (required)>'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/bin/pod:25:in `load'
/opt/homebrew/Cellar/cocoapods/1.11.3/libexec/bin/pod:25:in `<main>'
```

――― TEMPLATE END ――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――

[!] Oh no, an error occurred.

Search for existing GitHub issues similar to yours:
https://github.com/CocoaPods/CocoaPods/search?q=%5BXcodeproj%5D+Unknown+object+version+%2856%29.&type=Issues

If none exists, create a ticket, with the template displayed above, on:
https://github.com/CocoaPods/CocoaPods/issues/new

Be sure to first read the contributing guide for details on how to properly submit a ticket:
https://github.com/CocoaPods/CocoaPods/blob/master/CONTRIBUTING.md

Don't forget to anonymize any private data!

Looking for related issues on cocoapods/cocoapods...
 - pod init after update it to XCODE 14
   https://github.com/CocoaPods/CocoaPods/issues/11546 [open] [9 comments]
   3 days ago

 - Error occurred when executing pod init
   https://github.com/CocoaPods/CocoaPods/issues/11536 [open] [12 comments]
   2 days ago

 - RuntimeError - [Xcodeproj] Unknown object version.
   https://github.com/CocoaPods/CocoaPods/issues/10099 [closed] [4 comments]
   2 weeks ago

### Resolve
```
gem update xcodeproj
sudo gem update xcodeproj
brew uninstall cocoapods
sudo gem install cocoapods
```

### 🌐 Reference Site
[pod init after update it to XCODE 14 #11546](https://github.com/CocoaPods/CocoaPods/issues/11546)   
[Error occurred when executing pod init #11536](https://github.com/CocoaPods/CocoaPods/issues/11536)   
[m1, m2 silicon mac에서 cocoapods 설치하기](https://trend21c.tistory.com/m/2253)   
[Big Sur m1 CocoaPods 설치하기(feat. 나만 안되지 또)](https://velog.io/@yoogail/Big-Sur-m1-CocoaPods-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0feat.-%EB%82%98%EB%A7%8C-%EC%95%88%EB%90%98%EC%A7%80-%EB%98%90)   