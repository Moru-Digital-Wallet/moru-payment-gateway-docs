## Mobile Integration

Currently Flutter SDK is availabe for Flutter.

## Integration Steps

### Step 1: First add the following dependency in your pubspec.yaml file

```yaml
dependencies:
  moru_payment_gateway: ^0.2.6
```

### Step 2: In your main.dart

```dart

import 'package:flutter/material.dart';
import 'package:moru_payment_gateway/moru_payment_gateway.dart';

void main() {
  runApp(MyApp());
}
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Moru Payment Gateway',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}
class _MyHomePageState extends State<MyHomePage> {
  final String accessKey =
      'test_a33173ce922a4971968a6c1bf59a4aa4b88a3521c2e640feb7c3ce91e82320f8';

  @override
  void initState() {
    super.initState();
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text('Moru Payment Gateway'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(15.0),
          child: Center(
            child: Column(
              children: [
                Container(
                  height: 50,
                  color: Colors.grey[200],
                  child: Center(
                      child: Text(
                    "Total Amount: Rs.100",
                    style: TextStyle(fontWeight: FontWeight.w500, fontSize: 16),
                  )),
                ),
                SizedBox(
                  height: 20,
                ),
                MaterialButton(
                  color: Color(0xffC91F3D),
                  textColor: Colors.black,
                  minWidth: MediaQuery.of(context).size.width,
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(7),
                  ),
                  height: 48,
                  highlightColor: Colors.white30,
                  elevation: 0,
                  highlightElevation: 0,
                  onPressed: () {

                  final Widget widget =  MoruPaymentSDK.builder(accessKey: accessKey, amount: 100)
                        .withAdditionalData(
                            additionalData: {'name': 'Shubham Dhakal'})
                        .withProductIdentifier(identifier: '1')
                        .build()
                        .launch(
                            checkoutListener: (checkoutStatus, statusResponse) {
                              //listen for status and call your api to validate transaction
                          print("$checkoutStatus");
                          print(
                              "${statusResponse.accessData!.moruTxnIdentifier}");
                        });

                  Navigator.of(context).push(MaterialPageRoute(builder: (context)=>widget));
                  },
                  padding: EdgeInsets.all(12),
                  child: Text(
                    "BUY NOW",
                    style: TextStyle(
                        fontWeight: FontWeight.w800,
                        color: Colors.white,
                        fontSize: 14),
                  ),
                ),
                const SizedBox(
                  height: 20,
                ),
              ],
            ),
          ),
        ));
  }
}
```

## API

- MoruPaymentSDK

  - instantiate MoruPaymentSDK class exposing the additional methods for initiating transaction.

### Methods of MoruPaymentSDK

| Methods               | Required Params                                                                    | Usage                                                      |
| --------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| builder               | `{required String accessKey, required num amount}`                                 | takes the accessKey and amount                             |
| withAdditionalData    | `{Map<String, dynamic>? additionalData}`                                           | pass the additional data                                   |
| withProductIdentifier | `{required String identifier}`                                                     | takes the unique product identifier                        |
| build                 |                                                                                    | build the checkout modal with given data                   |
| launch                | `{required dynamic Function(CheckoutStatus, ValidatedAccessRes) checkoutListener}` | start to show the checkout modal, expect listener function |

- CheckoutStatus

`enum CheckoutStatus { COMPLETED, FAILED, UNKNOWN }`

- ValidatedAccessRes

ValidatedAccessRes has following properties:

```dart
  final AccessData? accessData;
```

accessData has following properties:

```dart
  final num? amount;
  final bool? complete;
  final DateTime? createdAt;
  final String? externalTxnIdentifier;
  final ExtraFields? extraFields;
  final int? id;
  final String? moruTxnIdentifier;
  final String? sourceType;
  final String? state;
```

> After transaction is completed in client page, you need to do the server side verification about the status of the transaction
