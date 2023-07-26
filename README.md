# UnityRenderStreaming package改造

## 1. 只保留工程下的com.unity.renderstreaming, 并提取至根目录

## 2. 修改webrtc依赖版本
```diff
# package.json
- "version": "3.1.0-exp.7",
+ "version": "3.1.0-exp.8",

- "com.unity.webrtc": "3.0.0-pre.5",
+ "com.unity.webrtc": "3.0.0-pre.6",
```

## 3. 修改VideoStreamSender.cs中的码率控制
```diff
-static readonly uint s_defaultMinBitrate = 0;
-static readonly uint s_defaultMaxBitrate = 1000;
+static readonly uint s_defaultMinBitrate = 1000;
+static readonly uint s_defaultMaxBitrate = 3000;
```

## 4. webrtc删除testrunneroption.json

## 5. 修改适配2021.2.9以前的版本
```cs
# Editor/SignalingManagerEditor.cs
var prop = field.GetType().GetField("m_Choices", System.Reflection.BindingFlags.NonPublic
                                                    | System.Reflection.BindingFlags.Instance);
prop.SetValue(field, availableObjects.ToList());
// field.choices = availableObjects.ToList();
```
```cs
# Editor/RenderStreamingWizard.cs
// new Entry(Scope.BuildSettings, macCameraUsageDescription, IsMacCameraUsageCorrect, FixMacCameraUsage),
// new Entry(Scope.BuildSettings, macMicrophoneUsageDescription, IsMacMicrophoneUsageCorrect,
//     FixMacMicrophoneUsage),
// new Entry(Scope.BuildSettings, iOSCameraUsageDescription, IsIOSCameraUsageCorrect, FixIOSCameraUsage),
// new Entry(Scope.BuildSettings, iOSMicrophoneUsageDescription, IsIOSMicrophoneUsageCorrect,
//     FixIOSMicrophoneUsage),
// new Entry(Scope.BuildSettings, androidMinimumAPILevel, IsAndroidMinimumAPILevelCorrect,
//     FixAndroidMinimumAPILevel),
// new Entry(Scope.BuildSettings, androidScriptBackend, IsAndroidScriptBackendCorrect,
//     FixAndroidScriptBackend),
// new Entry(Scope.BuildSettings, androidTargetArchitecture, IsAndroidTargetArchitectureCorrect,
//     FixAndroidTargetArchitecture),
// new Entry(Scope.BuildSettings, androidInternetAccess, IsAndroidInternetAccessCorrect,
//     FixAndroidInternetAccess),
```