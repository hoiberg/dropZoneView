# DropZoneView
DropZoneView is a subclass of NSView, that will make it easier to implement a NSView as dragging destination, while keeping all the code in your NSViewController subclass. Especially if you want to accept files urls.

## How to use
In interface builder, add a custom view and set its class to DropZoneView. Add a IBOutlet of this view to your NSViewController protocols.
Here is an example on how to setup the DropZoneView:

    dropView.registerForFileExtensions(["bmp"]) // only accept .bmp files
    dropView.defaultDragOperation = .Copy
    dropView.dropDelegate = self // don’t forget to add DropZoneDelegate to your ViewController subclasses

If you don’t want to accept files, just use the default `registerForDraggedTypes()` method on the dropView.
The following delegate functions are available:

    /// Redirect of the draggingEntered function (optional)
    optional func draggingEntered(info: NSDraggingInfo) -> NSDragOperation
    
    /// Redirect of the draggingUpdated function (optional)
    optional func draggingUpdated(info: NSDraggingInfo) -> NSDragOperation
    
    /// Redirect of the draggingExited function (optional)
    optional func draggingExited(info: NSDraggingInfo)
    
    /// Redirect of the prepareForDragOperation (optional)
    optional func prepareForDragOperation(info: NSDraggingInfo) -> Bool
    
    /// Redirect of the performDragOperations (required)
    func performDragOperation(info: NSDraggingInfo) -> Bool


And the one helper function:

    class func fileUrlsFromDraggingInfo(info: NSDraggingInfo) -> [NSURL]? 
