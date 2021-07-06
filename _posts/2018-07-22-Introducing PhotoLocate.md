Date: 7/22/2018

## Introducing PhotoLocate -- Tag Your Photos, Right on Your iPhone

<center>![PhotoLocate](/public/PhotoLocate.png)</center>

Over the past few weeks, I've built another simple application for the iPhone and iPad. It's called PhotoLocate, and it is [available on the App Store right now](https://itunes.apple.com/us/app/photolocate/id1403197703?ls=1&mt=8) for free.

The point of PhotoLocate is simple: it adds a location (latitude and longitude) to photos for Apple's built-in Photos app to read.

### Why?

Photos taken on an iPhone already include this information. However, I realized while backpacking in Europe that it was useful to assign a location to photos taken on a DSLR or other camera and then imported to an iPhone or iPad.

Reasons for wanting to do this include:
* Photos taken with other cameras appear in Apple's "Places" album
* Photos taken with other cameras are included in the generated moments in the Photos app
* Starting in iOS 12, "For You" uses location to share photos with friends who attended the same events

### Technical Notes

Unlike OMKit, which was essentially a glorified calculator, PhotoLocate involved some interesting problem-solving while dealing with Apple's iOS frameworks. 

I had a few specific goals with PhotoLocate:
* Assign a location for use in the Photos app
* Maintain existing EXIF information
* Maintain original image quality

#### Take One

The first iteration of the app simply read in image data, and changed the location attribute of the [PHAsset](https://developer.apple.com/documentation/photokit/phasset) (an internal object that is used throughout PhotoKit -- Apple's current system for interfacing with the Photos app and libraries).

A limitation of PhotoKit appears to be that PHAssets aren't editable in place. Therefore, the first solution was to copy the image data into a new PHAsset, and then set the location attribute to what the user selected.

This cleared all existing EXIF data. 

#### Take Two

The second iteration, and what ultimately became the shipping version, was more complicated.

In order to read in and maintain EXIF data, the [Image I/O library](https://developer.apple.com/documentation/imageio?changes=_8) was needed. 

The user now selects photos to be tagged. This is done in [DKImagePickerController](https://github.com/zhangao0086/DKImagePickerController), a framework to select photos. This framework returns an array of PHAssets.

The user than selects a location and taps "Apply". 

This then triggers PhotoLocate to iterate through the array of PHAssets, copying each item to a temporary directory using the Image I/O library. This function preserves EXIF data, allowing PhotoLocate to then make a copy as a Dictionary object. 

PhotoLocate then creates a new PHAsset and inserts it into the Photos Library, merging the image data with the original EXIF data of the image. 

These operations are done for every object in the PHAsset array.

If the user has selected the option to delete the original image, PhotoLocate then passes the PHAsset array to PhotoKit to delete the original images.

### Design

PhotoLocate also took more time to design. OMKit is an incredibly vanilla iOS app, using stock colors, buttons, and labels for most of its UI.

Design is not my strong point. In order to present an app with a more fluid interface, I asked [designer Anna Wang](http://annawang.me) to help. She presented me with some mockups, and I worked to implement them.

The final product is close to what she proposed. Some elements -- like more responsive UI elements to show when an action is complete -- were a little beyond my immediate knowledge/skill. However, I was able to dip into @IBDesignable custom interface elements and implement more custom buttons that draw the eye.

Additionally, the horizontal lines help distinguish each function, giving more of an appearance of three distinctive steps. 

Moving forward, I want to create a vastly-improved iPad interface. This will require distint storyboards for the iPhone version and for the iPad version, which is why this isn't in the original release.

### Moving Forward

PhotoLocate represents a step forward for my iOS app development experience. While OMKit was put together to learn the process of submitting to the App Store, PhotoLocate solves certain issues that aren't well-documented -- namely, pulling EXIF data from PHAssets -- and provides a more valuable function to a slightly wider audience.

Again -- this app is free. The source code is [available on GitHub](https://github.com/jonathankkizer/PhotoLocate) (not as open source, necessarily, but mostly for anyone wanting to learn from how I've solved these problems). I now have a full-time job in a very different industry. iOS development remains, for me, an enjoyable hobby. But with each release, I learn something new and get to engineer solutions around problems. And that's all I can ask for!

I am considering implementing the solution I developed for this and extending it into a much more full-featured way to edit and view EXIF data (date, time, location, copyright, etc.). Still very early in the thought/planning phase!

With that said, feel free to reach out with questions or suggestions.