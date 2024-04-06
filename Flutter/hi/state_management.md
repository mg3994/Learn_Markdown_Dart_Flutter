
# फ्लटर स्टेट प्रबंधन

फ्लटर विकास में स्टेट प्रबंधन एक महत्वपूर्ण पहलू है, विशेष रूप से प्रयोजनों की स्थिति का संचालन और एप्लिकेशन के लगभग सभी विभागों में डेटा का प्रबंधन करने के लिए। फ्लटर स्टेट प्रबंधन के विभिन्न उपाय हैं, जिसमें setState(), Provider, Bloc, Redux, और MobX शामिल हैं। सही स्टेट प्रबंधन समाधान का चयन एप्लिकेशन की जटिलता और डेवलपर पसंदों पर निर्भर करता है।

# फ्लटर स्टेट प्रबंधन: एक अवलोकन

फ्लटर में स्टेट प्रबंधन, आपकी एप्लिकेशन के उपयोगकर्ता इंटरफेस की स्थिति को प्रबंधित करने के लिए महत्वपूर्ण है। यह डेटा परिवर्तनों को संभालने और उपयोगकर्ता इंटरफेस को उसके अनुसार अपडेट करने का काम करता है। फ्लटर स्टेट प्रबंधन को प्रबंधित करने के लिए विभिन्न उपाय हैं, जो विभिन्न परिदृश्यों और एप्लिकेशन आवश्यकताओं के लिए उपयुक्त हैं।

## फ्लटर में स्टेट को समझना

फ्लटर में, स्टेट वह डेटा है जो समय के साथ बदल सकता है। इसमें उपयोगकर्ता इनपुट, नेटवर्क प्रतिसाद, और आपके एप्लिकेशन में किसी भी गतिशील डेटा शामिल है। स्थिति का प्रबंधन प्रभावी रूप से सुनिश्चित करता है कि आपका यूआई अंडरलाइंग डेटा के साथ सिंक में रहता है।

## स्थिति प्रबंधन के प्रकार

फ्लटर में स्थिति प्रबंधन के कई विकल्प हैं:

### 1. StatelessWidget और StatefulWidget के साथ

इस दृष्टिकोण में, आप StatelessWidget और StatefulWidget को मिलाकर स्थिति को प्रबंधित कर सकते हैं। StatelessWidget अमर विजेट्स को प्रतिष्ठित करता है, जबकि StatefulWidget आपको परिवर्तनशील स्थिति वाले विजेट्स बनाने की अनुमति देता है।

उदाहरण:
```
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('स्थिति प्रबंधन उदाहरण'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'काउंटर:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'इंक्रीमेंट',
        child: Icon(Icons.add),
      ),
    );
  }
}
```


### 2. प्रोवाइडर पैकेज
प्रोवाइडर फ्लटर में स्थिति प्रबंधन के लिए एक लोकप्रिय पैकेज है, जो आपको अपने ऐप में स्थिति को साझा करने के लिए एक सरल और लचीले तरीके से प्रदान करता है। यह InheritedWidget का उपयोग करता है ताकि स्थिति परिवर्तनों को विजेट पेड में फैलाया जा सके।

उदाहरण:
```

class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MaterialApp(
        home: Consumer<Counter>(
          builder: (context, counter, child) {
            return Scaffold(
              appBar: AppBar(
                title: Text('स्थिति प्रबंधन उदाहरण'),
              ),
              body: Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    Text(
                      'काउंटर:',
                    ),
                    Text(
                      '${counter.count}',
                      style: Theme.of(context).textTheme.headline4,
                    ),
                  ],
                ),
              ),
              floatingActionButton: FloatingActionButton(
                onPressed: () {
                  counter.increment();
                },
                tooltip: 'इंक्रीमेंट',
                child: Icon(Icons.add),
              ),
            );
          },
        ),
      ),
    );
  }
}



```


### 3. ब्लोक पैटर्न

ब्लोक (बिजनेस लॉजिक कंपोनेंट) पैटर्न बिजनेस लॉजिक को यूआई घटकों से अलग करता है, जिससे आपका कोड ज्यादा टेस्ट किया जा सकता है और रखा जा सकता है। यह स्थिति प्रबंधन के लिए स्ट्रीम्स और सिंक्स का उपयोग करता है।

उदाहरण:
```



class CounterBloc {
  final _counterController = StreamController<int>();
  Stream<int> get counterStream => _counterController.stream;

  int _count = 0;

  void incrementCounter() {
    _count++;
    _counterController.sink.add(_count);
  }

  void dispose() {
    _counterController.close();
  }
}

class MyWidget extends StatelessWidget {
  final counterBloc = CounterBloc();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('स्थिति प्रबंधन उदाहरण'),
      ),
      body: Center(
        child: StreamBuilder<int>(
          stream: counterBloc.counterStream,
          builder: (context, snapshot) {
            return Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text(
                  'काउंटर:',
                ),
                Text(
                  '${snapshot.data ?? 0}',
                  style: Theme.of(context).textTheme.headline4,
                ),
              ],
            );
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          counterBloc.incrementCounter();
        },
        tooltip: 'इंक्रीमेंट',
        child: Icon(Icons.add),
      ),
    );
  }
}


```



## निष्कर्ष
स्टेट प्रबंधन फ्लटर एप्लिकेशन बनाने के लिए एक महत्वपूर्ण पहलू है। अपने परियोजना के लिए सही स्टेट प्रबंधन उपाय का चयन करके, आप कोड संगठन, रखरखाव, और प्रदर्शन में बेहतरी की सुनिश्चित कर सकते हैं।

