​					**Flutter Get download URL when upload image to firebase storage**

------

**Concept**

Get Download URL when upload files to the firebase storage 

**Method**

```
Future<Null> _uploadFile(String uuid) async {
  StorageReference storageReference = storage.ref();
  final StorageReference imagesRef = storageReference.child('images/$uuid');


  StorageUploadTask uploadTask = imagesRef.putFile(_imageFile);
  //imageURL is global variable
  imageURL = await (await uploadTask.onComplete).ref.getDownloadURL();
}
```

