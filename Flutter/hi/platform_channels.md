# फ्लटर में प्लेटफ़ॉर्म चैनल

## परिचय

फ्लटर में प्लेटफ़ॉर्म चैनल्स फ्लटर कोड और प्लेटफ़ॉर्म-विशिष्ट कोड (जैसे Android के लिए जावा / कोटलिन या iOS के लिए Objective-C / Swift) के बीच संचार को संभव बनाते हैं। यह द्विदिशीय संचार फ्लटर ऐप्स को प्लेटफ़ॉर्म-विशिष्ट सुविधाओं और सेवाओं तक पहुँचने की अनुमति देता है जो फ्लटर के फ़्रेमवर्क API के माध्यम से सीधे उपलब्ध नहीं हैं।

## प्लेटफ़ॉर्म चैनल सेटअप

### Android

Android के लिए, आप आमतौर पर अपने फ्लटर कोड में एक मेथड चैनल को परिभाषित करेंगे और उसके संबंधित हैंडलर को जावा या कोटलिन कोड में लागू करेंगे। फ्लटर फ़्रेमवर्क इस उद्देश्य के लिए 'MethodChannel' कक्षा प्रदान करता है।

### iOS

इसी तरह, iOS के लिए, आप अपने फ्लटर कोड में एक मेथड चैनल को परिभाषित करेंगे और उसका हैंडलर Objective-C या स्विफ्ट में लागू करेंगे। फ्लटर ने iOS के लिए भी 'MethodChannel' कक्षा प्रदान की है।

## उदाहरण: प्लेटफ़ॉर्म-विशिष्ट सुविधाओं तक पहुँच

चलो एक स्थिति को ध्यान में रखें जहाँ हमें उपकरण के बैटरी स्तर तक पहुँचना है, जो एक प्लेटफ़ॉर्म-विशिष्ट सुविधा है।

### फ्लटर कोड
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

### प्लेटफ़ॉर्म-विशिष्ट कोड (Android)
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

### प्लेटफ़ॉर्म-विशिष्ट कोड (iOS)
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
# निष्कर्ष
फ्लटर में प्लेटफ़ॉर्म चैनल्स फ्लटर ऐप्स में प्लेटफ़ॉर्म-विशिष्ट फ़ंक्शनैलिटी को एकीकृत करने के लिए एक शक्तिशाली मेकेनिज़्म प्रदान करते हैं। प्लेटफ़ॉर्म चैनल्स का उपयोग करके, आप नेटिव सुविधाओं और सेवाओं तक बिना किसी अंतर के पहुँच सकते हैं, जिससे आपके फ्लटर ऐप्स की क्षमताएँ बढ़ जाती हैं।


