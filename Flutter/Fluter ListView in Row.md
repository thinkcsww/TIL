​										**Listview in Row**

------

**Concept**

How to put ListView in Row ? 

**Method**

Flexible -> SingleChildScrollView -> StreamBuilder -> Container(Width, Height must be aligned) -> ListView...

```
return Column(
      children: <Widget>[
        Row(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: <Widget>[
            _buildCategoryHomeLeftView(context),
            _buildCategoryPosterListView(context),
          ],
        )
      ],
    );
```

```
Widget _buildCategoryPosterListView(BuildContext context) {
    return Flexible(
      child: SingleChildScrollView(
        scrollDirection: Axis.horizontal,
        child: StreamBuilder<QuerySnapshot>(
          stream: Firestore.instance
              .collection('Posters')
              .where('auth', isEqualTo: true)
              .snapshots(),
          builder: (context, snapshot) {
            if (snapshot.hasError) return Text('Error, please try again');
            if (!snapshot.hasData) return LinearProgressIndicator();
            return _buildCategoryList(context, snapshot.data.documents);
          },
        ),
      ),
    );
  }
```

```
Widget _buildCategoryList(
      BuildContext context, List<DocumentSnapshot> snapshot) {
    return Container(
      height: 350.0,
      width: 300.0,
      child: ListView(
          scrollDirection: Axis.horizontal,
          children: snapshot
              .map((data) => _buildCategoryListItem(context, data))
              .toList()),
    );
  }
```

