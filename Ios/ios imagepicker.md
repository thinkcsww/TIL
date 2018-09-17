​							**IOS Image Picker**

------

**Concept**

Implement image picker

**Method**

1. Extends 

   ```
   UIImagePickerControllerDelegate, UINavigationControllerDelegate
   ```

2. Setting a imagePicker

2. ```
   let imagePicker = UIImagePickerController() <- Global variable
   
   
   Inside viewDidLoad()
   {
   imagePicker.delegate = self
   imagePicker.sourceType = UIImagePickerControllerSourceType.savedPhotosAlbum
   }
   
   ```

3. Override function

```
func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {
        if let pickedImage = info[UIImagePickerControllerOriginalImage] as? UIImage {
        	//Set a Image of button
            photoButton.setImage(pickedImage.resizedImage(newSize: CGSize(width: 82,       height: 82)), for: .normal)
        }
        // Close the ImagePickerView
        dismiss(animated: true, completion: nil)
    }
```



4. Show the image picker

```
@IBAction func photoButton(_ sender: Any) {
        
  self.present(imagePicker, animated: true, completion: nil)
 
 }
```