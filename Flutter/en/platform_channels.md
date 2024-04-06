# Platform Channels in Flutter

## Introduction

Platform channels in Flutter enable communication between Flutter code and platform-specific code written in languages like Java/Kotlin for Android or Objective-C/Swift for iOS. This bi-directional communication allows Flutter apps to access platform-specific features and services that are not directly available through Flutter's framework APIs.

## Setting up Platform Channels

### Android

For Android, you'll typically define a method channel in your Flutter code and implement its corresponding handler in Java or Kotlin code. The Flutter framework provides the `MethodChannel` class for this purpose.

### iOS

Similarly, for iOS, you'll define a method channel in your Flutter code and implement its handler in Objective-C or Swift. Flutter provides the `MethodChannel` class for iOS as well.

## Example: Accessing Platform-specific Features

Let's consider a scenario where we want to access the device's battery level, which is a platform-specific feature.

### Flutter Code

```
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

class BatteryLevelScreen extends StatefulWidget {
  @override
  _BatteryLevelScreenState createState() => _BatteryLevelScreenState();
}

class _BatteryLevelScreenState extends State<BatteryLevelScreen> {
  static const platform = MethodChannel('com.example.app/battery');

  String batteryLevel = 'Unknown';

  Future<void> _getBatteryLevel() async {
    try {
      final int result = await platform.invokeMethod('getBatteryLevel');
      setState(() {
        batteryLevel = 'Battery level is $result%';
      });
    } on PlatformException catch (e) {
      setState(() {
        batteryLevel = 'Failed to get battery level: ${e.message}';
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Battery Level'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            ElevatedButton(
              onPressed: _getBatteryLevel,
              child: Text('Get Battery Level'),
            ),
            SizedBox(height: 20),
            Text(batteryLevel),
          ],
        ),
      ),
    );
  }
}
```

### Platform-specific Code (Android)
```
package com.example.app;

import android.os.BatteryManager;
import android.content.Context;
import androidx.annotation.NonNull;
import io.flutter.embedding.engine.FlutterEngine;
import io.flutter.embedding.engine.FlutterEngineGroup;
import io.flutter.embedding.engine.plugins.shim.ShimPluginRegistry;
import io.flutter.embedding.engine.plugins.util.GeneratedPluginRegister;

public class MainActivity extends FlutterActivity {
    @Override
    public void configureFlutterEngine(@NonNull FlutterEngine flutterEngine) {
        super.configureFlutterEngine(flutterEngine);
        flutterEngine
                .getPlugins()
                .add(
                        new io.flutter.plugins.GeneratedPluginRegistrant());
        flutterEngine
                .getPlatformChannel()
                .setMethodCallHandler(
                        (call, result) -> {
                            if (call.method.equals("getBatteryLevel")) {
                                int batteryLevel = getBatteryLevel();
                                if (batteryLevel != -1) {
                                    result.success(batteryLevel);
                                } else {
                                    result.error("UNAVAILABLE", "Battery level not available.", null);
                                }
                            } else {
                                result.notImplemented();
                            }
                        }
                );
    }

    private int getBatteryLevel() {
        int batteryLevel = -1;
        BatteryManager batteryManager = (BatteryManager) getSystemService(BATTERY_SERVICE);
        if (batteryManager != null) {
            batteryLevel = batteryManager.getIntProperty(BatteryManager.BATTERY_PROPERTY_CAPACITY);
        }
        return batteryLevel;
    }
}

```

### Platform-specific Code (iOS)
```
import UIKit
import Flutter
import UIKit

@UIApplicationMain
@objc class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    GeneratedPluginRegistrant.register(with: self)
    let controller : FlutterViewController = window?.rootViewController as! FlutterViewController
    let batteryChannel = FlutterMethodChannel(name: "com.example.app/battery", binaryMessenger: controller.binaryMessenger)
    batteryChannel.setMethodCallHandler({
      [weak self] (call: FlutterMethodCall, result: FlutterResult) -> Void in
      guard call.method == "getBatteryLevel" else {
        result(FlutterMethodNotImplemented)
        return
      }
      self?.receiveBatteryLevel(result: result)
    })

    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
  
  private func receiveBatteryLevel(result: FlutterResult) {
    let device = UIDevice.current
    device.isBatteryMonitoringEnabled = true
    if device.batteryState == UIDevice.BatteryState.unknown {
      result(FlutterError(code: "UNAVAILABLE", message: "Battery info unavailable", details: nil))
    } else {
      result(Int(device.batteryLevel * 100))
    }
  }
}
```
# Conclusion
Platform channels in Flutter provide a powerful mechanism for integrating platform-specific functionality into your Flutter apps. By using platform channels, you can access native features and services seamlessly, enhancing the capabilities of your Flutter applications.

