# फ़्लटर एनिमेशन्स

एनिमेशन फ़्लटर अनुप्रयोगों में जीवन को लाते हैं जो दृश्य प्रभावों को जोड़कर और उपयोगकर्ता अनुभव को सुधारते हैं। फ़्लटर एक शक्तिशाली एनिमेशन एपीआई प्रदान करता है जो ट्वीन्स, कर्व्स, संवहन, और भौतिकीय आधारित एनिमेशन्स सहित विभिन्न प्रकार के एनिमेशन्स का समर्थन करता है। डेवलपर्स फ़्लटर की एनिमेशन फ़्रेमवर्क का उपयोग करके चिकना और अंतराक्षीय एनिमेशन बना सकते हैं।

फ़्लटर की एनिमेशन क्षमताओं के साथ, डेवलपर्स यूआई तत्वों को एनिमेट कर सकते हैं, स्क्रीनों के बीच संवहन कर सकते हैं, और जटिल गति प्रभाव बना सकते हैं। फ़्लटर के घोषित एनिमेशन के लिए घोषणा करने की घोषणा से डेवलपर्स सरल और स्पष्ट API का प्रयोग करके एनिमेशन को परिभाषित कर सकते हैं, जिससे डेवलपमेंट प्रक्रिया सहज और स्थिर होती है।

# फ़्लटर एनीमेशन (अवलोकन)

एनीमेशन फ़्लटर अनुप्रयोगों के यूज़र अनुभव को बढ़ाने में महत्वपूर्ण भूमिका निभाते हैं, जिससे यूआई तत्वों में गति और अंतर्क्रियात्मकता जोड़ी जा सकती है। फ़्लटर ने अलग-अलग प्रकार की एनीमेशन बनाने के लिए विभिन्न उपकरण और एपीआई प्रदान की है, जिसमें स्थानिक एनीमेशन, निष्पक्ष एनीमेशन, और कस्टम एनीमेशन शामिल हैं।

## फ़्लटर में एनीमेशन के प्रकार

### 1. स्वाभाविक एनीमेशन

फ़्लटर में स्वाभाविक एनीमेशन वे एनीमेशन होते हैं जो फ़्लेमवर्क में शामिल होते हैं और इम्प्लीमेंट करने के लिए न्यूनतम कोड की आवश्यकता होती है। इन एनीमेशन्स को स्वचालित रूप से विजेट गुणों के परिवर्तनों को एनिमेट करते हैं, जैसे कि आकार, स्थान, पारदर्शिता, और रंग।

उदाहरण:
```
AnimatedContainer(
  duration: Duration(seconds: 1),
  width: _selected ? 200 : 100,
  height: _selected ? 200 : 100,
  color: _selected ? Colors.blue : Colors.red,
  child: FlutterLogo(size: 50),
),
```

### 2. निष्पक्ष एनीमेशन

निष्पक्ष एनीमेशन अधिक नियंत्रण देने में शामिल होते हैं और एनीमेशन प्रक्रिया को स्पष्ट रूप से परिभाषित करने की अनुमति देते हैं। फ़्लटर प्रक्षेपक, ट्वीन, और AnimatedBuilder जैसी कक्षाएँ प्रदान करता है, जो निष्पक्ष एनीमेशन बनाने के लिए उपयोगी होती हैं।

उदाहरण:
```
AnimationController _controller;
Animation<double> _animation;

@override
void initState() {
  _controller = AnimationController(
    duration: Duration(seconds: 1),
    vsync: this,
  );
  _animation = Tween<double>(begin: 0, end: 300).animate(_controller)
    ..addListener(() {
      setState(() {});
    });
  _controller.forward();
  super.initState();
}

@override
void dispose() {
  _controller.dispose();
  super.dispose();
}

@override
Widget build(BuildContext context) {
  return Center(
    child: Container(
      height: _animation.value,
      width: _animation.value,
      color: Colors.blue,
      child: FlutterLogo(size: 50),
    ),
  );
}
```

### 3. कस्टम एनीमेशन

कस्टम एनीमेशन विशिष्ट उपयोग मामलों या प्रभावों के लिए एनीमेशन बनाने का समर्थन करते हैं। फ़्लटर कस्टम एनीमेशन बनाने के लिए एनिमेशन कंट्रोलर, ट्वीन, कर्व्स, और कस्टम पेंटर ऑब्जेक्ट का संयोजन का उपयोग करता है।

उदाहरण:
```
class MyCustomWidget extends StatefulWidget {
  @override
  _MyCustomWidgetState createState() => _MyCustomWidgetState();
}

class _MyCustomWidgetState extends State<MyCustomWidget>
    with SingleTickerProviderStateMixin {
  AnimationController _controller;
  Animation<double> _animation;

  @override
  void initState() {
    _controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );
    _animation = CurvedAnimation(
      parent: _controller,
      curve: Curves.easeInOut,
    );
    _controller.repeat(reverse: true);
    super.initState();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: RotationTransition(
        turns: _animation,
        child: Icon(
          Icons.favorite,
          color: Colors.red,
          size: 50.0,
        ),
      ),
    );
  }
}
```

## निष्कर्ष

एनीमेशन फ़्लटर अनुप्रयोगों को रोचक और दिलचस्प बनाने का महत्वपूर्ण हिस्सा है। फ़्लटर द्वारा प्रदान की गई विभिन्न एनीमेशन तकनीकों का उपयोग करके, डेवलपर्स अपने ऐप्स को जीवंत और आकर्षक बना सकते हैं और उपयोगकर्ता अनुभव को आनंदमय बना सकते हैं।

