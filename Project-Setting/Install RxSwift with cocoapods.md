# Install RxSwift with Cocoapods

## ❌ Arm Architecture에서의 설치 에러
```zsh
$ Pod install

Analyzing dependencies
/Library/Ruby/Gems/2.6.0/gems/ffi-1.15.5/lib/ffi/library.rb:275: [BUG] Bus Error at 0x00000001040b4000
ruby 2.6.8p205 (2021-07-07 revision 67951) [universal.arm64e-darwin21]

-- Crash Report log information --------------------------------------------
   See Crash Report log file under the one of following:                    
     * ~/Library/Logs/DiagnosticReports                                     
     * /Library/Logs/DiagnosticReports                                      
   for more details.                                                        
Don't forget to include the above Crash Report log file in bug reports.     

Analyzing dependencies
/Library/Ruby/Gems/2.6.0/gems/ffi-1.15.5/lib/ffi/library.rb:275: [BUG] Bus Error at 0x00000001040b4000
ruby 2.6.8p205 (2021-07-07 revision 67951) [universal.arm64e-darwin21]

-- Crash Report log information --------------------------------------------
   See Crash Report log file under the one of following:                    
     * ~/Library/Logs/DiagnosticReports                                     
     * /Library/Logs/DiagnosticReports                                      
   for more details.                                                        
Don't forget to include the above Crash Report log file in bug reports.     

~~~

[NOTE]
You may have encountered a bug in the Ruby interpreter or extension libraries.
Bug reports are welcome.
For details: https://www.ruby-lang.org/bugreport.html

[IMPORTANT]
Don't forget to include the Crash Report log file under
DiagnosticReports directory in bug reports.
```

## 🛠 Solution
```zsh
$ gem install --user-install ffi -- --enable-libffi-alloc

Fetching ffi-1.15.5.gem
WARNING:  You don't have /Users/kh_lee/.gem/ruby/2.6.0/bin in your PATH,
          gem executables will not run.
Building native extensions with: '--enable-libffi-alloc'
This could take a while...
Successfully installed ffi-1.15.5
Parsing documentation for ffi-1.15.5
Installing ri documentation for ffi-1.15.5
Done installing documentation for ffi after 8 seconds
1 gem installed

$ pod install
Analyzing dependencies
Downloading dependencies
Installing RxSwift (6.5.0)
Generating Pods project
Integrating client project

[!] Please close any current Xcode sessions and use `HelloRxSwift.xcworkspace` for this project from now on.
Pod installation complete! There is 1 dependency from the Podfile and 1 total pod installed.

[!] Automatically assigning platform `iOS` with version `16.0` on target `HelloRxSwift` because no platform was specified. Please specify a platform for this target in your Podfile. See `https://guides.cocoapods.org/syntax/podfile.html#platform`.

[!] The `HelloRxSwiftUITests [Debug]` target overrides the `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES` build setting defined in `Pods/Target Support Files/Pods-HelloRxSwift-HelloRxSwiftUITests/Pods-HelloRxSwift-HelloRxSwiftUITests.debug.xcconfig'. This can lead to problems with the CocoaPods installation
    - Use the `$(inherited)` flag, or
    - Remove the build settings from the target.

[!] The `HelloRxSwiftUITests [Release]` target overrides the `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES` build setting defined in `Pods/Target Support Files/Pods-HelloRxSwift-HelloRxSwiftUITests/Pods-HelloRxSwift-HelloRxSwiftUITests.release.xcconfig'. This can lead to problems with the CocoaPods installation
    - Use the `$(inherited)` flag, or
    - Remove the build settings from the target.
```

### 🌐 Reference Site
[Macbook M1 Pro에서 부딪히는 문제 - pod install error](https://effectivecode.tistory.com/m/1583)   
[Error on M1 Mac #10287](https://github.com/CocoaPods/CocoaPods/issues/10287)   
[Error installing a pod - Bus Error at 0x00000001045b8000](https://stackoverflow.com/questions/68553842/error-installing-a-pod-bus-error-at-0x00000001045b8000)   