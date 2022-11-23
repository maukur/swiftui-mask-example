# Mask examples

Created: November 23, 2022 3:22 PM
Tags: #linkedin, #swift, #work

# Applying a mask in SwiftUI

On one of my projects I had to use complex image masks that looked like this:

![Untitled](Mask%20examples%20c287157faca04d168e5f558951388e73/Untitled.png)

![Untitled](Mask%20examples%20c287157faca04d168e5f558951388e73/Untitled%201.png)

And there were many such templates and we were getting them from a remote server, but we didn't have the ability to process the images to the necessary there.

So I did some research on how this could be done using SwiftUI and I found an elegant solution.

We will need two Images. The first is for the image, and the second is for the mask. Then we need to wrap them in a ZStack, which should be set to .compositingGroup(), and the mask image should be set to .blendMode(.screen). This way we get our original image to be cropped by the mask.

There is a second, but the more complicated solution, which requires working with Shape. In this case, we can directly apply any Shape as a mask to the Image.

### UI example

![Untitled](Mask%20examples%20c287157faca04d168e5f558951388e73/Untitled%202.png)

### Code example with two ways

```swift
//
//  ExampleMaskView.swift
//  ExampleMask
//
//  Created by Artem Tischenko on 23/11/2022.
//

import SwiftUI

fileprivate enum Images {
    static let image = "example_image"
    static let mask = "example_mask"
}

struct ExampleMaskView: View {
    
    var body: some View {
        VStack {
            group
            mask
        }
    }
    
    fileprivate var group: some View {
        ZStack {
            Image(Images.image)
                .resizable()
                .scaledToFit()
                .cornerRadius(26)
            Image(Images.mask)
                .resizable()
                .scaledToFit()
                .blendMode(.screen)
                .cornerRadius(26)
        }
        .compositingGroup()
    }
    
    fileprivate var mask: some View {
        Image(Images.image)
            .resizable()
            .scaledToFit()
            .cornerRadius(26)
            .mask {
                Circle()
                    .frame(width: 204)
            }
        
    }
}

struct ExampleMaskView_Previews: PreviewProvider {
    static var previews: some View {
        ExampleMaskView()
    }
}
```

### My account links

[](https://www.linkedin.com/in/tim-tis/)

[maukur - Overview](http://github.com/maukur)

Thanks for reading.
