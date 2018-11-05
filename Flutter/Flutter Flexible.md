​									**FLutter Flexible**

------

**Concept**

Caution When Using Flexible

Flexible's usage is to have a flexible text. -> Multiple textline.

**Method**

Sequence must be Row -> Flexble ->  Column -> (Optional Container with width!)

```
Row(
	crossAxisAlignment: CrossAxisAlignment.start,
    children: <Widget>[
    Padding(
    padding: const EdgeInsets.fromLTRB(0.0, 6.0, 10.0, 0.0),
    child: Image.network(
    recentMessage.imageURL,
    width: 50.0,
    height: 50.0,
    fit: BoxFit.fill,
    ),
    ),
            Flexible(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  // 메시지 내용
                  Padding(
                    padding: const EdgeInsets.only(top: 4.0),
                    child: Padding(
                      padding: const EdgeInsets.fromLTRB(8.0, 2.0, 8.0, 2.0),
                      child: Container(
                          decoration: BoxDecoration(
                            border: Border.all(color: Colors.grey),
                            borderRadius: BorderRadius.circular(15.0),
                          ),
                          width: 200.0,
                          padding: EdgeInsets.fromLTRB(10.0, 2.0, 10.0, 2.0),
                          child: Text(
                            message.message,
                            style: TextStyle(color: Colors.grey.shade600),
                          ),
                      ),
                    ),
                  ),
                ],
              ),
            ),

          ],
        ),
```

