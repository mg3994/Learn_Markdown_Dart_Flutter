# डार्ट में परीक्षण

डार्ट में परीक्षण एक महत्वपूर्ण कार्य है जो कोड की गुणवत्ता, सुरक्षा, और स्थिरता को सुनिश्चित करने में मदद करता है। परीक्षण का उपयोग विकासकों को यह सुनिश्चित करने में सहायक होता है कि उनका कोड सही तरीके से काम कर रहा है और अपेक्षित परिणाम प्रदान कर रहा है।

## डार्ट में परीक्षण क्यों महत्वपूर्ण है

- **गुणवत्ता बनाए रखना**: परीक्षण कोड की गुणवत्ता को बनाए रखने में मदद करता है। यह बग्स और त्रुटियों को पहचानने और सुधारने में सहायक होता है।

- **सुरक्षित कोड**: परीक्षण सुरक्षित कोड लिखने में मदद कर सकता है, क्योंकि यह पोटेंशियल खतरों को पहचानता है जो अपर्याप्त कोड से उत्पन्न हो सकते हैं।

- **स्थिरता सुनिश्चित करना**: परीक्षण सुनिश्चित करता है कि कोड के परिणाम विभिन्न यातायात की स्थिति में स्थिर हैं और अनुकूल हैं।

## डार्ट में परीक्षण प्रकार

- **एकीकृत परीक्षण**: एकीकृत परीक्षण विभिन्न कोड क्षेत्रों को संगठित और समूहीकृत करने में मदद करता है।

- **यूनिट टेस्टिंग**: यूनिट टेस्टिंग कोड के विभिन्न घटकों को स्वतंत्रता से परीक्षित करता है।

- **इंटीग्रेशन टेस्टिंग**: इंटीग्रेशन टेस्टिंग विभिन्न घटकों के बीच संचालनीय इंगितों को परीक्षित करने में मदद करता है।

- **कार्यक्षमता टेस्टिंग**: कार्यक्षमता टेस्टिंग कोड की गति, स्थिरता, और प्रदर्शन को मापता है।

## डार्ट में परीक्षण का उदाहरण

यहाँ एक डार्ट यूनिट टेस्टिंग का उदाहरण है:

```
import 'package:test/test.dart';

void main() {
  test('गुणवत्ता सत्यापन', () {
    var answer = 42;
    expect(answer, 42);
  });
}

```
इस उदाहरण में, हमने test() फ़ंक्शन का उपयोग करके एक साधारण यूनिट टेस्ट बनाया है जो सत्यापन करता है कि उत्तर 42 है। यह एक सरल उदाहरण है जो डार्ट में परीक्षण की महत्वपूर्णता को दर्शाता है।