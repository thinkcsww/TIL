​							      **IOS Fetch images from photo album**

------

**Concept**

Fetch images from album, you can get screenshot album, all photo, slow motion album by filter

1. Fetch collection
2. enumerate collection object
3. getAsset from collection inside **step 2**
4. Request real image from asset which fetched in **step3**

**Method**

1. Import Photos library

```
import Photos 
```

2. Run fetching collection

```
let fetchOptions:PHFetchOptions = PHFetchOptions()
        // 앨범들을 fetchedAlbums에 넣는다. ex) 모든사진, 슬로우모션, 스크린샷 앨범 등등이 있고 그중 모든 사진만 받아온다 -> subtype으로 필터링할 수 있다.
        let fetchedAlbums : PHFetchResult = PHAssetCollection.fetchAssetCollections(with: .smartAlbum, subtype: .smartAlbumUserLibrary, options: fetchOptions)
        let allPhotoCollection = fetchedAlbums[0]
        let assetsFetchResult: PHFetchResult = PHAsset.fetchAssets(in: allPhotoCollection, options: nil)
  		// Print Image counts of all photos foler
        print("assetsFetchResult.count=\(assetsFetchResult.count)")
```

3. Fetching all photos by using function

```
func getAssets(fromCollection collection: PHAssetCollection) -> PHFetchResult<PHAsset> {
        let photosOptions = PHFetchOptions()
        photosOptions.sortDescriptors = [NSSortDescriptor(key: "creationDate", ascending: false)]
        photosOptions.predicate = NSPredicate(format: "mediaType == %d", PHAssetMediaType.image.rawValue)
        
        return PHAsset.fetchAssets(in: collection, options: photosOptions)
    }
```

4. Deal with real image

```
fetchedCollections.enumerateObjects { (collection, _, _) in
            
            let result = self.getAssets(fromCollection: collection)
            print("\(String(describing: collection.localizedTitle)): \(result.count)")
            print(result.object(at: 0))
            
            for i in 0 ..< result.count {
                let asset = result.object(at: i)
                imageManager.requestImage(for: asset, targetSize: CGSize(width: 200, height: 200), contentMode: .aspectFill, options: nil) { (fetchedImage, _) in
                    // Face Detection 하려면 아래 PNG를 해줘야함
                    let imageData = UIImagePNGRepresentation(fetchedImage!)
                    let realImage = UIImage(data: imageData!)
//                    self.faceImage = VisionImage(image: finalImage!)
                    self.images.append(realImage!)
                }
            }
            self.faceImage = VisionImage(image: self.images[0])
            
        }
```

Reference**

https://stackoverflow.com/questions/50347392/how-to-fetch-photos-album-title-image-count-in-swift