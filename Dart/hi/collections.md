# डार्ट संग्रह

डार्ट संग्रह वस्तुओं का एक समूह या सूची होते हैं। डार्ट भाषा निम्नलिखित प्रकार के संग्रहों के लिए अंतर्निहित समर्थन प्रदान करती है:

1. **सूची (List)**: एक सूची वस्तुओं का एक क्रमबद्ध समूह होती है। डार्ट में सूची डेटा प्रकार अन्य भाषाओं में अरेस के समान होती है।

    ```
    List<int> numbers = [1, 2, 3, 4, 5];
    ```

2. **सेट (Set)**: एक सेट अद्वितीय वस्तुओं का एक अक्रमबद्ध समूह होता है। यह सूची से अलग होता है क्योंकि इसमें अद्वितीय तत्व होते हैं।

    ```
    Set<String> colors = {'red', 'green', 'blue'};
    ```

3. **कतार (Queue)**: कतार वस्तुओं का एक संग्रह होता है जो अंत में डाले जाते हैं (जिसे enqueue कहा जाता है) और शुरुआत से हटाए जाते हैं (जिसे dequeue कहा जाता है)।

    ```
    Queue items = new Queue();
    items.add(10);
    items.add(20);
    ```

4. **मानचित्र (Map)**: एक मानचित्र पायथन में एक शब्दकोश या जावास्क्रिप्ट में एक ऑब्जेक्ट के समान, कुंजी-मान युग्मों का एक अक्रमबद्ध संग्रह होता है।

    ```
    Map<String, int> fruits = {
      'apples': 5,
      'bananas': 10,
      'oranges': 8
    };
    ```

इन सभी संग्रहों में प्रत्येक के पास अपने स्वयं के गुण और विधियाँ होती हैं जिनका उपयोग आवश्यकता के आधार पर किया जा सकता है।
